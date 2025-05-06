The internet works primarily though the use of the HTTP protocol 

Http (Hyper Text Transport Protocol) is a protocol we use for the sending and receiving of data packits from web server to client. These packets have lots of uses such as building out websigts on a clients browser.

For example lets say a user wants to load your simple websight displaying an img

Firstly the user needs to form the Packet, a packit consists of three parts: The sourse, the Header, the body.

Source: indicates the type of http request ie. what it is trying to do such as the **Get** request which simply requests data from a server. The type of requests are Get, Post, Put & Delete

it also includes the target of the request google.com for instance  as well as the version of the HTTP protocol that is being used.

Header: The server can be configured to need more information than just the request source, that information is filled out in the headers. For instance for security reasosn the user might need to submit a Auth Token, proving that they have access rights to the servers contents. A other example might be the USer-agent headder which is used to send information about the user and their browser to better allow the server to serve up spesfic content that will be compatable wiht the uses browser or device 

Body: In our Get example this is normaly left empty as a get normaly dose not submit information, but for a Post or Put the user would be adding the information that want to add to the server or update on the server.

The server will recieve this packet and then respond with with a responce packet of its own. Quite like the requesit packet it will contain the same three parts: Sourse, header, body. But the informatin will be organized differently

The Srouse: will not return the request type ie Get, post. Insteand it will first respond with the HTTP vershion, then a http status code, 100, 200, 404, 500, followed by the status message File not found.

It will then also have its own set of headers that the browser will then use to build the content on the users browsers such as "ContentType = img"

and then the body will contain the content being sent such as the img its self.

But this covers only from a transcation point of view as to how the internet works, what the out comes are the quiston we then have to ask is how is the infmormation passed through the net work we call the internet.

Networks are just a connection of computers. As the amount of computers increases so to must the network, you cant string three computers to gether as a 1:1 connecton doesn't make sense and as such we need to make use of Routers, Routers make sure that the packet is able to find the correct server and that the server can communacate back to the client. 

But computers dont use human lanugage to coomunacate, you cant just use Computer A and Computer B and expect to be unique, computers use numerical or hexadecamel identifiers to itendify and find eachother we call this IP addresses. And its through the Internet Protocols Addresses that we allow for the transfer of information. But humans dont normaly search for servers with the use of an IP address we use fully formed URL, and its with the use of DNS that we allow for this trans lation.

DNS stands for Domain name server and it acts as a look up to help translate google to 127.1.1.0. When a request is made to a router, before the router can send on the request it must first send a look up request to the DNS to find the correct address. On a simple Lan network this DNS is normaly simple to set up, a router would be able to automacaly do this for you but when we start using the internet we need to have some form of orgnizational structuer to figer out where in the globe we need send out request. which is where TLD enter the space. TLD and CCTLD are normaly found at the end of your url, these are our .com .net .IEs and they act as the main authority for doing the look up in a zone. Companies and individuals will reserve their URL's by submitting amapping of their Domains and their IP's but even then this is at a high level. While Google.ie ipaddress  might be stored on the .ie Zone's database it wont have google.com or even google.com/images. But by using the diffrent routers on the rout we can hop from one to one collecting further infomation about the IP we are looking for so that we can eventually build the IP we are looking for.

IP addresses for example are notmaly in this format 123.45.678.90 each of those segemnts represent further identifaction of the spesfic server you are looking for. For example the 123 could represnt a Collage, the 45 could be the campus, the 678 could be the building and the 90 could be the spesfic server. Its important to know that all of this can be virtural as well existing in the cloud.

Once we have found spesfic server we are looking for the request will then be recieved by the server and if the server is happy with the request, that it is correctly formed, as the correct auth, has not been identifed as mallishious then it will build a responce to be sent back. 

Its at this point by the way that we can have modern convionunces to promote better performance. For instance insteand of having a singular server must modern systems would insteand have cluster of servers all running in tandem allow for the processing of more requests and users, this cluster could even be elastic and live in the cloud. With this being the case the end point of the address wouldnt be a server but a load balancer or gate way that would take the incomming requests and pass them out to avalabile servers or even request that new ones be spun up to handle the incoming work load.

Once the responce object has been formed we wouild then send it back to the user. The packet would then be taken up by the browers, interpratated and then rended in a way that the user would be able to under stand.





