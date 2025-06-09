Into & Theory

###### What are Microservices
- Small (2 pizza team, 2 weeks to build)
- Responsible for doing 1 thing well
- Organisationally aligned
	- Easy to implament 
	- tare down
	- talk to eachother
- Form part of the (distributed) whole
- Self-contained/Autonomus

Monolithic

- Very dificult to change
- Difficult to scale
- locked in 
	- tehnology terms
	- intellectualproperty terms 

- Benefits of microservices
	- Easier to change & deploy
	- Can be built usinng different tech stacks
	- increased Organisational ownership & alignment
	- Reslilent 
	- Scalible
	- Built to be highly replaceable and swapable
	-


The example

We will be building out a Platform  register to keep track of all the services we are building out. It will be broken into two parts

Part 1: The "Platform" Service

- Functions as an "Asset Register"
- Track all the platforms/systems in the company
- Built by the infrastructure Team
- Used by
	- Infrastructure team
	- technical support team
	- engineering team
	- Accounting
	- Procurement team

Part 2: The "Command Service"

- Function as a repository of command line arguments for given platforms
- Aid in the automation of support processes
- Built by the technical support team
- Used By:
	- Technical Support Team
	- Infrastructure Team
	- Engineering


#### The "Platform" Service
 The platform service will be a very simple service. It will be three endpoints.
 - GetAllPlatforms
 - GetPlatformBuId
 - CreatePlatform
 
 It will have the usal layers

- Controler
- Business logic
- Data access

For our Data access layer we will be making use of
- Entity frame work
- inmemory db

Step 1 define out Models and Dto

Models are what we are going to user for internal communication to and from the Database
Dto's are what we are going to use for communicating with the user. We will be using Automapper to translate between the two.

Platform Model: This will represent the basic Platform object.
It will contine a number of attributes but the important one is the Id attribute which we will lable with a atrabute [] called key. Which will indacatet that this is a primary key.

Dtos

- ReadPlatformDto
	- This will return all the information relating to the platform object
- CreatePlatformDto
	- This will return all the information needed to create a Platform. so lacking a ID


Step 2: Set up the DbContext.

We will then create the DbContext object. 

`public class AppDbContext: DbContext`
`{`
    `public AppDbContext(DbContextOptions<AppDbContext> opt): base(opt)`
    `{`
        
    `}`
`}`

The importing things here is the DbContext base class. This is what will be doing the majoriy of the work.

we then need to add the DbSet for the Platform Object 
`public DbSet<Platform> Platforms{ get; set; }`

We also will need to inject the DbContext in the Program folder 

`builder.Services.AddDbContext<AppDbContext>();`

Step 3: Seting up the PlatformRepo
The Repository file for Platform is going to contain all the code that will be calling the DB.

Since we know what functionality we want to build we can start off with a Interface to help define our scope.

We will have four Methods
- GetAllPlatforms
- GetPlatformById
- CreatePlatform
- Save

We can wirte the interface like so 
- `void save();`
- `IEnmureal Platform GetallPlatforms();`
- `Platform GetPlatformById(Id);`
- `void CreatePlatform(Platform)`

#### PlatformRepo
We can then use this interface to build out our Reposotory methods. This will give us the structure of the file but we are still missing the DbContext. Since we have already added that to our programfile as an injectable. Basic dependency injecion will allow is to create the PlatformRepo and pass in the DbContext which we will set as our global varable of _context.

And then we will go about creating out four methods.

The structure of these methods are all self explanatory but the important part will be how we are going to use EntityFramework for each one.

 - CreatePlatform
	 - We make use of the `_Context.ModelName.Add(Object)` EF method.
 - GetAllPlatforms
	 - We make use of the `_Context.ModelName.ToList()` EF method to return all the objects in a table
 - GetPlatformById
	 - We make use of the `_Context.ModelName.FirstOrDefault(x=>x.Id = model.Id)`
 - SaveChanges
	 - We make use of the `Context.SaveChanges()`

We will also need to make the IPlatformRepo injectable so we will add it to out ProjectFile

`build.services.addScoped<IPlatformRepo, PlatformRepo>`

#### PlatformControler

Now that we have our data layer completed we will need to expose it to a controler so that It can be called from out side the applaction.

our PlatformControler will inject the IPlatformRepo as well as extend the BaseControler class

`Public class PlatformController : BaseController{`
	`public PlatfromController(IPlatformRepo repo){`
		`_repo = repo`
	`}`
	
`}`

We will also need to set up the api routing for the class we can use the generic routing here

`[route("api/[controller]")]`

which will automaticly get the correct name for the API

that `[]` is a atrabute tag and we use them for all of our routing and nameing such as 

`[HttpGet]` : A Basic Http Get call

`[HttpGet("{id}"), name = GetPlatformByID]` A Http Get call that is passing in a Id to help narry down the search. We are also naming the API
`[HttpPost]` : a basic HttpPost option that we use for creating a platform.

#### In memory database
Now that we have out endpoints set up we are going to want to test them. We will eventually be using a Database that the Repo will be hitting but for now we are going to set up a InMemmory database for us to test againsed.

for now we are going to extend out builder.services.AddDbContext entry to incude the in memory db

`builder.Services.AddDbContext<AppDbContext>(opt =>
`opt.UseInMemoryDatabase("InMem"));``

this way when we pass the AppDbContext to any of our Repos the Repos will point to this "InMem" construct wich acts as our db.

PrepDB is going to be a Static class. As we are only going to want one of it. It will be responsible for creating all the test data we will be using in our in memory db.

With in PrepDB we will create a function called PrepPopulation and inject the IApplactionBuilder
This will allow us to access the inmemory db and inject into it the initial data

`builder.Services.AddAutoMapper(AppDomain.CurrentDomain.GetAssemblies());`

We can than add records into out db

context.Platforms.AddRange(
    new Platform() { Name = "Dot Net", Id = 1, Publisher = "Microsoft", Cost="Free"},
    new Platform() { Name = "SQL Server Express", Id = 2, Publisher = "Microsoft", Cost = "Free" },
    new Platform() { Name = "Dot Kuberneties", Id = 3, Publisher = "Cloud Native Computing Foundation", Cost = "Free" }
);

context.SaveChanges();

#### Auto mapper

When a user sends us a request be it to view or create we need to make sure that we are only sending back the information we want them to see. Depending on the project it might not be advisable to just returen back an entire Record from the DB to a user. So we are going to want to create models that we use only for Data transfer that we can strongly define. 

We call these methods Dto Objects. But it is time consuming to fill out every Dto object, to save time on this we use AutoMapper. Automapper is a libary that smartly review the naming convention of our models and match them up. We can also use anotations to insure that we send the correct information to the correct attrabute 

To use Automapper we will need to generate a Profile.

public class PlatformsProfile : Profile
{
    public PlatformsProfile()
    {
        // Source -> Target
        CreateMap<Platform, PlatformReadDto>();
        CreateMap<PlatformCreateDto, Platform>();

    }
}

Here we are creating a map from Platform to PlatformReadDto and from Platform CreateDto to our platform model. This represents the information we will be returning to the user when they request a platform as well as the Object we will be inserting into the DB based on the information submitted by the user.

To make use of the platforms we use the folowing methods in the controler class.

For our GetAllPlatforms we would use 
`Ok(_mapper.Map<IEnumerable<PlatformReadDto>>(results));`
Here we are passing our list of Platform objects into the mapper which will be converting them into a IEnumerable list of PlatformReadDto.

For out CreatePlatform api we will use
`var platformModel = _mapper.Map<Platform>(request);`
Which will be taking in a Dto and converting it into the Platfrom object

#### Docker
Now that we have our service coded out we are going to want to host it but to save us the time and money of hosting it up in the cloud we are going to simulate a network on out machien by user Docker.

Docker is a Containerization managment tool that will allow us to create applaction Images, create Containers that will hold those Images, run those containters and even allow us to scaile the number of containters up and down as we see fit. 

Each container will have its own set of ports and ipaddresses that we will be able to use.

first thing we need to do is set up our applaction so that it has the instructions that docker will user to create a image of the app. We call this a DockerFile and it looks like this.

`FROM mcr.microsoft.com/dotnet/sdk:9.0@sha256:3fcf6f1e809c0553f9feb222369f58749af314af6f063f389cbd2f913b4ad556 AS build`
`WORKDIR /App`

#`Copy everything`
`COPY . ./`
#`Restore as distinct layers`
`RUN dotnet restore`
#`Build and publish a release`
`RUN dotnet publish -o out`

#`Build runtime image`
`FROM mcr.microsoft.com/dotnet/aspnet:9.0@sha256:b4bea3a52a0a77317fa93c5bbdb076623f81e3e2f201078d89914da71318b5d8`
`ENV ASPNETCORE_HTTP_PORTS=80`
`EXPOSE 80`
`WORKDIR /App`
`COPY --from=build /App/out .`
`ENTRYPOINT ["dotnet", "PlatformService.dll"]`

in this file we are saying what SDK of .net we want to use, what Asp.net version we want to use and what ports we want the app to be listening to.

as well as pointing docker to run the aplaction from the "PlatformService.dll" file.

We will then build the applaction and push it to our docker hub.

docker build -t timothyryandublin/platformservice .

then to run the applaction 

docker run -p 5001:5001 -d timothyryandublin/platformservice

#### Commands service

Now we are going to set up a secondary serice called Commands service.
This service will work the same way as platformservice, using the same packages, having a docker file but pointing to another port.

We will even create a Platforms controller but its rout will be `api/c/platforms` and for now contain one endpoint TestInboudConnection.

#### Messaging
There are two ways of handeling messageing between services.
- Synchronously
	- http
	- grcp
- Asynchronusly 
	- message busses

There are upsides and down sides but its safe to say that when working with in Microservices we will be using Asynchronios communacation.

but there are still instances where you might want to handle a synchronuious call such as the following example

#### http client 

We are going to set up a communacation between the Platform and Commands services. We will be doing this via a http call. First we need to create a http client that will create a request object to be set from PlatformService to CommandsService

We will create a folder called SyncDataServices and create a sub folder called Http
With in this folder we will create a Interface called ICommandDataClient what will have one method called sendPlatformToCommand. It will return a Task and take in a PlatformDto.

we will then create a class called HttpCommandDataClient and implament the interface.

Its importent here to inject the mechanisems for how we will be doing the http call as well as where we will be getting the endpoint. we do this by injecting httpclient as well as Iconfigureation.

Next step is to build the request content. the content is going to comprise of three parts
1. the seralized platform object
2. the encoding we will be using 
3. and the headder to indacate what format the object will be taking

 `var httpContent = new StringContent(`
    `JsonSerializer.Serialize(plat),`
    `Encoding.UTF8,`
    `"application/json"`
     `);`

then we need to build the address we will be sending the request to. To do that we will make use if the configuration file. With in appsettings.json we will create a new file called appsettings.production.json 

and with in that we will add line "CommandService": "http://localhost:80",

we with in the class we will then use string interpalation to construct the address

`$"{_configuration["CommandService"]}/api/c/platforms"`

we can then pass that into the httpclient post Async method followed by the content we created before

var responce = await _httpClient.PostAsync($"{_configuration["CommandService"]}/api/c/platforms", httpContent);

After we have added this http client to our program file `builder.Services.AddHttpClient<ICommandDataClient, HttpCommandDataClient>();`
we are then able to inject this into our platformsControler and call it in any of our endpoints. in this instance we will add it to our create method.

Since we are now calling a method from out side of this service lets wrap it up in a try catch block so that we can handle things when they go wrong.

`try
`{`
`    await _commandDataClient.sendPlatformToCommand(platformReadDto);`
`}`
`catch (Exception ex) { Console.WriteLine($"Could not send syncronously {ex.Message}"); }``

We also need to add to our appsettings.json a configuration for the location of the command services 

`"CommandService": "http://localhost:80",`
#### Docker CommandService

Just as before we want to host the service as a docker container. Create a new Docker file

`FROM mcr.microsoft.com/dotnet/sdk:9.0@sha256:3fcf6f1e809c0553f9feb222369f58749af314af6f063f389cbd2f913b4ad556 AS build`
`WORKDIR /App`

`# `Copy everything`
`COPY . ./`
`# `Restore as distinct layers`
`RUN dotnet restore`
`# `Build and publish a release`
`RUN dotnet publish -o out`

`# `Build runtime image`
`FROM mcr.microsoft.com/dotnet/aspnet:9.0@sha256:b4bea3a52a0a77317fa93c5bbdb076623f81e3e2f201078d89914da71318b5d8`
`ENV ASPNETCORE_HTTP_PORTS=80`
`EXPOSE 80`
`WORKDIR /App`
`COPY --from=build /App/out .`
`ENTRYPOINT ["dotnet", "CommandsService.dll"]`


Then we can build the the container 
`docker build -t timothyryandublin/commandservice .`
`docker push timothyryandublin/commandservice` 

#### Kubernetes 
Kubernetes is a Container conducter. It allows for the easy managment and configuration and scaling of containers. It allows us to create an enviorment where Containers can easly exist and communacat with each other in isolation. 
It allows us to manage containers by:
- Easily hosting containers
- Easily configurating containers (size, addresses, etc) 
- Easily scale the number of containers (Setting a replica limit)
- Easily and automatically restart services should they fall over

The arcetucture of Kuberneties can be broken down into diffrent layers
1. Hardware (PC)
2. Operating system 
3. Container runtime (Docker)
4. Kuberneties (Docker desktop)
5. Cluster
6. Node
7. Pod
8. Container

k8s is short hand for kuberneties.

We need to create a folder with in our solution called k8s to hold all out configuration files.
Here we will create two files
- commands-depl.yaml
- platforms-depl.yaml


In each of these files we will be adding the following code.

`apiVersion: apps/v1
`kind: Deployment
`metadata: 
  ``  name: commands-depl
`spec:
  ``  replicas: 1 // the number of copies of servers we want running
    `selector:
        `matchLabels:
            `app: commandservice
    `template:
    `    metadata: 
        `    labels:
              `  app: commandservice
      `  spec:
          ``   containers:
            ``    - name: commandservice
            ``      image: timothyryandublin/commandservice:latest` // container location

We then need to build and run the services 

`kubectl apply -f platforms-depl.yaml
`kubectl apply -f commands-depl.yaml`

Once a kuberneties contain is up and running we can restart it with 
`kubectl rollout restart deployment platform-depl`

##### Node Port
At this point we should be able to see k8s containers spinning up in our docker desktop but we have a problem. How do we access these containers. To allow us access to the Platform service we are going to need to set up a NodePort that will handle the routing from the outside into the k8s container. 

Create a new .yaml file in the k8s folder called platform-np-srv.yaml
It will contain the following code

`apiVersion: v1`
`kind: Service`
`metadata:`
    `name: platformnpservice-srv`
`spec:`
    `type: NodePort`
    `selector:`
        `app: platformservice`
    `ports:`
        `- name: platformservice`
          `protocol: TCP`
          `port: 80`
          `targetPort: 80`

This will allow us to access the platform service container listening on port 80.
`kubectl apply -f platform-np-srv.yaml

#### Async vs Syncronous messaging
At this point we now have two services that can communicate to each other as a Web API. We have Platform service that when it creates a new Platform will send a Http request to the Command service and enter into the command services through its controllers. 

But this relationship is Synchronous, it is a tightly coupled relationship between the two services. Should one service not be available it would cause the systems to brake. As well we need to manually configure the services to know of each others locations.

The problems with Synchronous messaging are:
- Tight Coupling (Reduced Autonomy)
	- If one service goes down or becomes slow, it can cascade failures or performance degradation throughout the chain of synchronous calls. This defeats one of the core benefits of microservices: independent deployability and fault isolation.
- Reduced Scalability
	- Threads
	- Resourses
	- Bottlenecks
- Lower Resilience and Fault Tolerance
- Complexity in Distributed Transactions

Ways of doing Synchronous messaging
- Http
- gRPC

#### Asynchronous messaging

- No Request/Responce cycle
- Request dose not wait for a response
- Event model, eg Publish/Subscribe
- Typically used between services
- Event bus is often used

The type of Asynchronous messaging we will be using will be **RabbitMQ**
What is RabbitMQ
- A message broker that accepts and forwards messages 
- Messages are sent by producers (or publishers)
- Messages are recieved by Consumers (or subscribers)
- Messages are stored in the Queue (The broker acts as a buffer)
- Exchanges can be used to add "Routing" functionality
- Uses advansed message query protocols (AMQP)

RabbitMQ gives 4 types of Exchanges

1. Direct Exchange
2. Fanout Exchange
3. Topic Exchange
4. Header Exchange

#### ClusterIp
Cluster IPs will allow us to group services together and not hard code addresses and ports.

To create cluster ips for our Kuberneties set up we need to add extra lines to our k8s files for both of our services.

for command we add 

apiVersion: v1
kind: Service
metadata: 
    name: commands-clusterip-srv
spec:
    type: ClusterIP
    selector: 
        app: commandservice
    ports: 
    - name: commandservice
      protocol: TCP
      port: 80
      targetPort: 80

This will allow us to instead of giving the specific addresses of a command service we can pass in the name of rbmq-clusterip-srv

An example of this can be seen in our appsettins.Production file where we insteand of targeting Localhost or an ip we are targeting "CommandService": "http://commands-clusterip-srv:80",

now that both our command and Platform service had generic addresses we can no set up our rabbitMQ broker to point to them.

Create a new rabbitmq-depl.yamal file and add the following code

Running nessesry set up commands first 

`apiVersion: apps/v1`
`kind: Deployment`
`metadata:`
  `name: rabbitmq-depl`
`spec:`
  `replicas: 1`
  `selector:`
    `matchLabels:`
      `app: rabbitmq`
  `template:`
    `metadata:`
      `labels:`
        `app: rabbitmq`
    `spec:`
      `containers:`
        `- name: rabbitmq`
          `image: rabbitmq:3-management`
          `ports:`
            `- containerPort: 15672`
              `name: rbmq-mgmt-port`
            `- containerPort: 5672`
              `name: rbmq-msg-port`
---
`apiVersion: v1`
`kind: Service`
`metadata:` 
    `name: rbmq-clusterip-srv`
`spec:`
    `type: ClusterIP`
    `selector:` 
        `app: rabbitmq`
    `ports:` 
    `- name: rbmq-mgmt-port`
      `protocol: TCP`
      `port: 15672`
      `targetPort: 15672`
    `- name: rbmq-msg-port`
      `protocol: TCP`
      `port: 5672`
      `targetPort: 5672`
---
`apiVersion: v1`
`kind: Service`
`metadata:` 
    `name: rbmq-loadbalancer`
`spec:`
    `type: LoadBalancer`
    `selector:` 
        `app: rabbitmq`
    `ports:` 
    `- name: rbmq-mgmt-port`
      `protocol: TCP`
      `port: 15672`
      `targetPort: 15672`
    `- name: rbmq-msg-port`
      `protocol: TCP`
      `port: 5672`
      `targetPort: 5672`



A few things to point our here. This Deployment fill will kick off two new services.

rbmq-clusterip-srv: The generic address for accessing the Loadbalancer

rbmq-loadbalancer: The load balancer which will insure that 

rbmq-msg: the message buss
rbmq-mgmt: the managment console for viewing the incoming messages

#### Ingress
The last thing we need to set up to allow external access to the kuberneties server is to set up a gateway to allow for the calling of APIs. We will be using Ingressnginx. as before we need to insure we runn the nessessory set up commands and then create a new ingress-srv.yaml file with in our k8s folder.

`apiVersion: networking.k8s.io/v1`
`kind: Ingress`
`metadata:`
  `name: ingress-srv`
  `annotations:`
    `kubernetes.io/ingress.class: nginx`
    `nginx.ingress.kubernetes.io/use-regex: 'true'`
`spec:`
  `rules:`
    `- host: acme.com`
      `http:`
        `paths:`
          `- path: /api/platforms`
            `pathType: Prefix`
            `backend:`
              `service:`
                `name: platforms-clusterip-srv`
                `port:`
                  `number: 80`
          `- path: /api/c/platforms`
            `pathType: Prefix`
            `backend:`
              `service:`
                `name: commands-clusterip-srv`
                `port:`
                  `number: 80`

Things to note, we are opening spesfic ports for the Platform and Commands services indacating the ports they are to be accessed with but we are creating a releashion between the two and the "acme.com" Url. this will mean that when trying access a API 

