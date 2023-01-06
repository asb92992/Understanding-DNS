# Building Intuition for DNS

- In this lab we will use Client-1 andDC-1 to do a few excercises for the sake of understanding DNS a bit better
- example: www.google.com converts to 216.58.199.288

# Overview
- Inspect DNS A-Records on the server (hostname to IP address mappings)
- Create some of our own A-Records on the server and observe them from the client
- Delete records from server and inspect/clear the client DNS cache to gain understanding
- Touch on "CNAME" records (mapping one name to another name)

# Defintions
- A-Records: maps a domain name to the IP address of the computer hosting the domain. An A record uses a domain name to find the IP address of a computer connected to the internet. The A in record stands for address. 
- Root Hints: Operators who manage a DNS recursive resolver typically need to configure a "root hints file". This file contains the names and IP addresses of the authoritative name servers for the root zone, so the software can bootstrap the DNS resolution process. For many pieces of software, this list comes built into the software.
- Forward Lookup Zones: allow the DNS Server to resolve queries where the client sends a name to the DNS Server to request the IP address of the requested host. 
- Reverse Lookup Zones: authoritative DNS zone that is used primarily to resolve IP addresses to network resource names.

# A-Record Excercise 

![A-Records part 1](https://user-images.githubusercontent.com/58159183/210929360-3768c04f-1bf2-4137-978a-cb7caf5ccfe2.gif)

- I login in to remote desktop using the Public IP address of DC-1 and Client-1 and login in to both as jessica_admin and       with the password use for her. 


![A-Records part 2](https://user-images.githubusercontent.com/58159183/210931278-45ac3181-1fb3-474d-8a14-cfcae9399f6f.gif)


Client-1 "Tries to Ping "mainframe"
1) Check cache (no result)
2) Check host file (no result)
3) Check DNS (no result)
-Note: Client-1 tried to ping mainframe. What happens is client-1 first check the local dns cache and if it doesn't find anything in the cache it will then check it's local host file. Every window computer has a local host file. Once it can't find anything in the host file. It then moves on to check the DNS server that is assign to the network interface and when nothing there it will essentially fail. Hence the error message of mainframe. 


![A-Records part 3](https://user-images.githubusercontent.com/58159183/210932877-d3d2f7b9-14ff-441f-b5b6-1c2d1c1bf3f3.gif)


- Creating a A-record for mainframe
- Assigning mainframe IP address to DC-1 IP address
- Going back to Client-1 VM to Ping mainframe 
- DC-1 IP address return mainframe IP address


# Local DNS Cache Exercise

![A-Records part 4](https://user-images.githubusercontent.com/58159183/210933627-47e29999-3a7c-48f9-b092-0d2bcc968d23.gif)

- dc-1.mydomain.com so next time we ping the DNS server its going to use the local cache
- mainframe.mydomain.com is map to 10.0.0.4


![A-Records part 5](https://user-images.githubusercontent.com/58159183/210935438-b8a04f7b-2373-49cc-a96a-d3cc0db52581.gif)


- Go back to DC-1 and change mainframe’s record address from 10.0.0.4 to 8.8.8.8
- Go back to Client-1 and ping “mainframe” again. Observe that it still pings the old address
- Its pinging the old IP address because 10.0.0.4 still exist in the local DNS cache on Client-1 computer
- Note: A troubleshooting step is to open CMD as a adminstrator and type ipconfig /flushdns to wipe out the cache 
- Flush the DNS cache (ipconfig /flushdns). Observe that the cache is empty
- Attempt to ping “mainframe” again. Observe the address of the new record is showing up
- Now mainframe pings 8.8.8.8

# CNAME Record Exercise

![A-Records part 6](https://user-images.githubusercontent.com/58159183/210937859-b9b2893d-2b85-4efd-92d1-7458a0d1b499.gif)


- Go back to DC-1 and create a CNAME record that points the host “search” to “www.google.com”
- Go back to Client-1 and attempt to ping “search”, observe the results of the CNAME record
- On Client-1, nslookup “search”, observe the results of the CNAME record

