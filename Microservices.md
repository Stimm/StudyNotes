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



