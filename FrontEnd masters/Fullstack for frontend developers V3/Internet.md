**computer -> network card -> router -> ISP -> Datacenter -> server cluster -> load balancer -> server**

- computer
	- network card
		- router 
		- router makes sure that computer have IP address
			- ISP
			- person you pay to get access
				- Tier 1 ISP
				- backbone of the internet
				- They usually talk to other ISPs
					- Datacenter
						- Server cluster
							- Load balancer
							- to prevent overloading the server
								- Server


## Network tools exercise
- `ping google.com`
	- check status of network host
- `traceroute google.com`
	- follow path of your request 
	- tells you the hops it takes you to get from your computer to target destination
- `netstat -lt | less`
	- tell you about all the processes happening on local computer and all the processes running on local ports

## Terminology
- **TCP** 
	- Transmission control Protocol
	- **TCP handshake**
		- Syn, Sycn aknowledged, aknowledged
- **UDP**
	- user datagram protocol
	- udp does not care, just sends you one way
	- useful for streaming a video, where it does not matter if you lose some packets
- **ICMP**
	- internet control message protocol
- **packet**
	- unit of data transferred over a network

## DNS & URL
- **DNS**
	- domain name system
	- nameserver holds DNS records to translate domain names into IP addresses
	- browser talks to name server
	- **A record**
		- maps name to IP address
	- **CNAME**
		- maps name to name
	- `nslookup google.com`
		- looksup the ip of the goodle in the DNS
	- `dig google.com`
		- same but more verbose
- **URL** - uniform resource locator
	- blog.youromain.com/en/fullstack?test=true
		- blog.yourdomain.com = subdomain
		- yourdomain.com = domain
		- /en/fullstack = path
		- ?test=true = query parameter

## Buying a domain
- www.namescheap.com probably
- on Digital Ocean add two A records with your IP address
	- @
	- www

## First actions to take on a servere
- update software
- restart your server
- create new user
- make that user a superuser
- enable login for new user
- disable root login