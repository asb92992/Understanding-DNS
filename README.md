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

# A-Record Excercise 

![A-Records part 1](https://user-images.githubusercontent.com/58159183/210929360-3768c04f-1bf2-4137-978a-cb7caf5ccfe2.gif)

- I login in to remote desktop using the Public IP address of DC-1 and Client-1 and login in to both as jessica_admin and       with the password use for her. 

