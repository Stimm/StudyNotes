
What is OAuth:
OAuth is a open standard for handling the creation and controling of permissions (Access delagation) on the web with out giving out sensative user information like passwords. 

OAuth allows for a safe way for users to give third party applactions controle over their data stored in another application.

OAuth dose this by allowing the user to request from an Authorization server a access token which can be shared with a Third party, the tokens will have limited scope of actions as well as an expiery timer preventing permanent and complete access to a users account.


OAuth workflow:
1. Authorization request
	1. The Third party Applaction requests to the user access to some Resource or Action from another Target application
2. User Consent
	1. The User is navagated to a Authorization portal hosted by the Target Application
	2. The User enters their UserName and password and confirms access for the third part applaction
3. The Authorization portal sends back to the Third Party Application an Authorization code
4. The Third Party connects with an Authorization Server and exchanges the Authorization code for an Authorization Token
5. The Third Party Applaction then attempts to access the Target Applaction's resours passing in the Token as an access key


OAuth implamentation.
JWT(JSON Web Token) Bearer Authentication is a common implementation of AOuth

		eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWUsImlhdCI6MTUxNjIzOTAyMn0.KMUFsIDTnFmyG3nMiGM6H9FNFUROf3wh7SmqJp-QV30

The Token string is split up into three . seperated parts that represent the:

- **JOSE Header**
	- Containing Meta data about the token such as what algorithem was used to make the token
- **JWS payload**
	- The security settings of the Token. Identity of the user as well as the Scope of the Token
- **JWS signature**
	- Used to valadate the vladity of the token and make sure it has not been tamperd with.



Setting up the project 
Create a new .net API project
As this project is going to be about having users with data and giving acess to that data we are going to want to be able to registere users. We will be storing the users in a db with the use of Entity framework

- Create a Controler "AuthControler"
- Create a Entity called User
	- Name
	- PasswordHash
- Create a DTO called UserDto
	- Name
	- Password
#### Register
With in our AuthControler create a Endpoint called Registered that returns the type Action Result<>user and takes in a UserDto

The prepose of this API is to return a User object containing a hashed version of the Password the user had just sent.

To hash the password we will use Microsoft's Identity service, sumply use the **PasswordHasher** class. HashPassword.

When we want to register a new user we need to save the users password but it is bad to keep the password as is so we will instead generate a hash of the pass word. 

We will then store this Hash and the User for access later (at the start we just create a static object called User but later on we will be storing it in a db)

#### login

Next we create a login method. the Login method for now will return a ActionResult string but will once again take in the UserName and Password, the string we will be returning will be a JWT Security token. More from that to come.

This time how ever we will be checking to see if the passed in user password is the same as the one we have stored in has from.

To do this we must hash the incoming password and compare the results to that which we have on file.

To do that we can once again use the Mirosoft identie's PasswordHasher<>User() but this time use the **VerifyPasswordHash**(model, storedPasswordHash, incoming Password);  If false, return an error if true return a new token for the user. We will create a private method called Create token.

#### Create Token and JWT Security tokens. 

###### JWT Security tokens.
Jwt is a secure, compact way of sharing information between parties in the form of a encrypted Json object. This standard way of creating secure objects can be secured by a number of encryption algorithems such as RSA, HMAC or ECDSA, we will be looking at how JWT can sign its tokens with Public/Private Key pairs.

The Structure of a JWT Security Token. 
In its token form a Security token looks like this 

eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWUsImlhdCI6MTUxNjIzOTAyMn0.KMUFsIDTnFmyG3nMiGM6H9FNFUROf3wh7SmqJp-QV30

This contains three distant '.' seprated sections that represent differnt parts of the token. 

- The Header
	- Type: In this case its JWT
	- Alg: The algorithem used to encrypt the Token. RSA/SHA256/etc..
- The Body/Payload 
	- The Payload contains the clames of the Token which represnts data about the token such as Entities, access scopes and expiry information. There are 3 types of clames
		- Registered Claims: A set of predefined Claims that are not nessesory
			- **iss**: Issuer
			- **aud**: audience
			- **sub**: Subject 
			- others: https://tools.ietf.org/html/rfc7519#section-4.1
		- Public Claims: These Claims can be defined at will but to avoid collisions they should be defined in the IANA Json web Token Regisry https://tools.ietf.org/html/rfc7519#section-4.1
		- Private Claims: Curtom Claims used by private parties that agree on there format and are nether registered or public claims.
- The Signature 
	- A signature is used to insure that the Token is valid and has not been tampred with a Signature is constructed of Four Parts
		- The Encoded header
		- The encoded payload
		- A Secret
		- The Algorithm selected in the header 


###### Create Token

To create the token we are going to use the **JwtSecurityTokenHandler.WriteToken()** method.

As stated above a Jwt token needs Three parts, The header, the Payload and the Signiture.

The Payload as stated above will contain the Claims.

In this instance the only Claims we are looking to capture are the Claim Type, The Audience and the issuer as well as an expiry date.

We start off the with the The Claims. Firstly we create a Claim object adding the Claim type of Name and the user Name. This will link the claim to the user. Then we add the "audience" and the "issuer", the values of which we will be hardcoding into the AppConfig data for now.

Then we will be adding "expires" which will be set to DateTime.Now.AddDays(1)

We will then start to build the Signing information which we will make by taking in a salt key and then using a encoding algorythem to generate the credential. 

Finally we will create a TokenDescripter which will be fed into the above described Write function for the JwtSecurityTokenHandler class.

		var claims = new List<Claim>
	{
    new Claim(ClaimTypes.Name, user.Name)
	};

	var key = new SymmetricSecurityKey(
	    Encoding.UTF8.GetBytes(configuration.GetValue<string>("AppSettings:Token")!));

	var creds = new SigningCredentials(key, SecurityAlgorithms.HmacSha512);

	var tokenDescripter = new JwtSecurityToken(
    issuer: configuration.GetValue<String>("AppSettings:Issuer"), // who is issuing the token
    audience: configuration.GetValue<String>("AppSettings:Audience"),// users using the token
    claims: claims,
    expires: DateTime.Now.AddDays(1),
    signingCredentials: creds);


#### Set up Entity framework
Now that we have everything set up to return a JWT security token lets set up Entity framework so that we can store user information such as their Name and Hashed Password.

In your project folder create a Data folder and an AppDBContext Class with in that.

the class will take in the EntityFramework class DbContextOptions as well as pass the options into its base class of DBContext
![[Pasted image 20250512112006.png]]
We will be using this to auto generate our SQL Schema. But first we need to get SQL running on the machien. To do this we will be downloading and installing SQL Express and SQL managment studio.

Install Microsoft.entityFramework.Tools
install Microsoft.EntityFrameworkCore.SqlServer

We now need to registered our db in the program.cs file 

![[Pasted image 20250512115000.png]]
and create a new connection string pointing to our empty DB

![[Pasted image 20250512115042.png]]
In the connection string we are defining a Database name as well as setting th eTrustedServerCertificate = true

Next we need to do is auto create a new User Table based on out User Model. To do this first we must create a Primary key. We can do this by creating a new Properity with in the model called ID we will set it as type Guid to insure that it is unque.

Then we run two commands in the devloper console of VS
**Add-Migration Initial**: This will generate a script that will be used to populate the DB with the new DB configrations and tables.
**Update-Database**: This will push the changes to the Database.

#### Refactor the Auth Controler to uses the new DB

Before we can hook the db and the controler up we should first refactor the project to use a clean coding arcetucture, taking the logic and db calls out of the Controle and adding them to other classes.

We will create a service to handle the Auth controlers functionality. 

We can easly set this up by creating a Interface first with two methods 

A RegesterAsync method which returns a Task with type User and takes in a UserDto
A LoginAsync method with returns Task with type String

Then we can start striping out the logic we had added to the controler and move it into the service.

###### RegisterAsync
This method should be made async as it will be calling our new db.

First thing we need to do is check to make sure that now user in the DB already exists with the same name.

**context.Users.AnyAsync(n => n.Name == request.name)** then return null

Then we can build out User object like we did in the controler but this time we will then add the new User object to the DB

**context.User.Add(user)**: will stage the new user object to be added to the db but first we must commit the change.

**context.SaveChangesAsync();** will commit the change and add the record to the db

We then need to change the Controler method to be async and to return the Task containing the original return type. replace the code to get the user = await service.registerAsync(request)

Till will trigger the adding of the user to the DB

###### LoginAsync
As above we need to move the logic into the service. Remembering to update the Controler to be of type Async and returning the Task<> type. We also move the CreateToken logic into the serves.

The functionality for this endpoint will remain the same as it will send back the jwt token
 
#### Test the Authorization
Now that we are able to create users and create for them a unique Authorization token lets test to see if we can lock endpoints behind this Authorization.

asp.net gives is the [Authorize] attribute for our controllers but first we need to define what our authorization scheam is.

With in our Project.cs file we need to add another service.

	builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme).AddJwtBearer(options =>
{
    options.TokenValidationParameters = new Microsoft.IdentityModel.Tokens.TokenValidationParameters
    {
        ValidateIssuer = true, //We will valadate the issuer
        ValidIssuer = builder.Configuration["AppSettings:Issuer"], // location of the issuer value
        ValidateAudience = true, // we will valadate the audience
        ValidAudience = builder.Configuration["AppSettings:Audience"], // location of the audience
        ValidateLifetime = true, // that there will be a life time and that we will valadate it 
        IssuerSigningKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(builder.Configuration["AppSettings:Token"]!)), // that we will be valadating the signing key
        ValidateIssuerSigningKey = true
    };
});


Once this is done we can create a simple end point and add the [Authorize] attrabute above it. When we are calling the endpoint in Scalar we need to insure we add the header **Authorization** and set it to be **Bearer** [The returned Jwt token we got from the login endpoint.]


#### Roles
We can now lock down endpoints. But what if we wanted to lock down endpoints by roles. 

To do this we need to extend the User context and add in a new attrabute called Roles. In the User model add in the new attrabute.

We then need to extend the Claims object in the Auth service to include a Claim of Claim type Roles that will take in the User.Role attrabute.

#### Refresh tokens
Last thing for us to do is add the refresh tokens. 

Refresh tokens generated secure tokens that allow for a user to automatically refresh their Access Token which out loging in. The Refresh token acts as a promise that is longer lived than the Access token which is created at the same time as the Access token and is stored with in the Access tokwn as a claim. As such it will not require the same level of security and implamentation as the access token. 

So lets set this up now. With in out Auth service we are going to create a new method that will return a string. GenerateAndSaveRefreshToken.

###### GenerateAndSaveRefreshToken

Unlike the previous token we do not need to be as secure with how we generate the OAuth token as this Refresh token will simply be added to the Access Token. To generate the token we are going to simply use a RandomNumber generator to generate the token as well as define a longer lived Expiry date in comparason to the Access token. 

![[Pasted image 20250514102632.png]]
	In this example we will be storing the RereshToken information into the User Table in the db, to do this we must expand the table to include a RefreshToken and RefreshTokenExpiryTime Attrabute. 

##### Extending the return type

We can add the new GenerateTokenAndSaveRefreshToken method to our Register method so that when a user creates an account we automaticly create one but the important thing is to extend the LogInMethod to now not only return the AccessToken but also the RefreshToken. To do this we will need to create a new model. The TokenResponseDto object will contain two strings, the AccessToken and the RefreshToken. this is what will be returned back to the user when they log in.

Now that this is complete we need to creatr a new end point refresh-Token. Which will see us passing in the Guid and the Refresh token. Here we will call the GenerateTokenand SaveRefreshToken method. 








