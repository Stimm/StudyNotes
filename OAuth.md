
# OAuth and OpenID are protocols

## Introduction
### What is Oauth

*Oauth* Is a way for securely communication between two or more applications with out sharing a users pass word.

### UseCases

#### Third party applications
Before OAuth, if you wanted your Yelp account to have access to you Gmail contact list you would have to share your Gmail password with Yelp

#### First-party/ trusted clients
If you have a Mobile application and you want it to access your API's you will need to allow your App to send some form of login to your API

#### More than one place login
If your website is made of many domains you would need to require your users to make multiple logins at multiple places. 

#### Risks
- Handing out your pass word to 3rd parties is a risk, you do not control there infrastructure or their security
- Every time you want to use an API you would need to pass on your login details
- The user is getting trained to give there access information to pages that may have varied interfaces increasing the chance that they may be attacked.
- Each login form represents another vector for attack 
- Makes it difficult or sometimes impossible to allow for 2FA (get good example)

#### Examples of good Aoth
	Gmail dose not ask you to give them your Gmail password, instead it sends you to googles authentication application to handle the login for you.

### What is the differance between OAuth and OpenID Connect 

In OAuth you:
- Access a Authorization server
- Request a token
- Get an Access Token
- Use that Access Token to get access to a resource else where 
	- The resource dose not need to know about you the user, only the access Token than you are using

In OIDC(OpenIdConnect) you are actually seeking User information (ID, Name, Email, ect)
OIDC is built off of OAuth but adds a extra concept called an ID Token

##### Audiences
For a Access token from OAuth: Resource server or API
For a ID Token from OIDC: Client applications

### What is the difference between Public and Confidential Clients?

##### Confidential Clients
- Applications running on a server
- Has the ability to keep strings secret since code is running in a trusted environment

##### Public Clients
- The application can't keep strings secret
- JavaScript/Single-Page apps: "View Source" Native apps: decompile and extract strings

Client_id: Identifies the application
Client_secret: The application's password


### What is the job of the OAuth client?
Firstly what are the roles
##### Roles in Oauth
- The User: Resource Owner
- Device: User Agent
- The Application: Client
- OAuth Server: Authorization server aka the token factory
- API Resource server

In some instances you may have one piece of software acting as multiple of these roles. Example:
	Git hub acts as both the OAuth Server and the API 
	
**Main role of OAuth client**
- To get access token
- Use the Access token to make or modify data 

We use the access token by adding it to a HTTP request as a **Header**


### How do we get access to a OAuth token

To get access we use one of the **Access Flows** 

**Access Flows** 
- Authorization code 
- Most common and used in most environments 
	- Web
	- Mobile
	- SPA
	- CLI
- Device Flow
- For when the app is running on a device with out a browser
	- CLI
	- Browserless devices
- Client Credentials
- When there is no user invloved in the flow
	- Server
	- Server
- Implesit Flow
	- Not recommended
- Password Flow
	- Not recommended 

### How is the Front Channel like sending a letter in the mail?

##### The Front Channel
The Front Channel is when we send information between to pieces of software between the users address bar. (Hands the info the browser to handle.)

The user, or malicious software, can modify the requests and responses

Its like sending a letter in the mail and hoping it gets to where it needs to go with out anyone tampering with it.

You don't know if the message was received, if it was copied or if it was stolen
Recieving the mail cant garentie it is legitament.

###### Front Channel Benefits
- The user being involved enables them to give consent
- Enables easier two-factor authorization integration
- Doesn't require the receiver to have a publicly routable IP (e.g. Can work on a phone)

##### The Back Channel 
Is sending the information through a HTTP request. (Secure)

HTTPS requests from client to server so requests cannot be tampered with

Its like walking up to someone and handing them a letter.

###### Back Channel Benefits
- The application knows it's talking to the right server
- Connection from app to server can't be tampered with (encryption)
- Response from the server can be trusted because it came back in the same connection

#### Implicit flow
1. User: Makes a request to the app for access
2. App: Sends the User to the Authorization server to grant access to the App
3. User: Asks the OAuth Server if it can log into the Applaction
4. OAuth Server: Sends to the User the Access token via the browser
5. User sends the Access token to the App
6. App then accesses the user's data

Risks
- OAuth Server dose not know if the Token has been received by the user or if it was stolen
- App dose not know if the Token came from the OAuth Server

The implicit flow exists because of legasy systems.

#### Authorization code (PKCE)

PKCE is an extension to the Authorization code flow and is a pretty well recommended flow

1. User: Makes a request to the app for access
2. App: Generates a new secret and hash's it (Has is a one way process to generate a key)
3. App: Sends the User to the OAuth server and gives the user the Hash it generated
4. User: Makes a request to the OAuth Server to access the App and gives the Server the Hash
5. OAuth Server: Takes in the Users login info and the Hash and generates a temporary code and sends it back to the user. Code or Token is short lived and valid for only one use
6. User: makes a request to the user passing in the Token it received from the OAuth Server
7. App: Makes a request to the OAuth Server with the Token as well as the Hash it generated in the beginning 
8. OAuth Server: Confirms that the Hash and Token are valid
9. App: Then can access the users detail.

### How can we use Refresh Tokens to get a better user experience?

Depending on the devices and systems having tokens that expire could have detrimental effects the users experience. Browsers would have an easer time because you could just navagate back to the previous url but for Applactions this could cause the user to return to the start of the applaction.

Refresh Tokes: Are tokens who's entire role is to get new Access Tokens.

### Where is the best place for a SPA to store Tokens

 - LocalStorage
	 - More or less permanent
 - SessionStorage
	 - Only active when the current session is open
 - Cookies
	 - Old way of doing it which is just awkword?

All three are venerable to XSS: Cross-Site Scripting attacks.

One potion is to use a Service Worker
If you make your Service worker a OAuth server then JS can directly access your token. 

Another option is to use your Backend for you Frontend. The SPA makes a request to a OAuth server but the server sends the data to a App Server not to the SPA. The App server then serves up information to the SPA but never shares the access tokens.

### How does the client learn who logged in?
