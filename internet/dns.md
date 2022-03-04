# DNS
DNS lets users connect to websites using domain names instead of IP addresses.

### DNS Infrastructure Servers
#### DNS Recursor
Responsible for receiving requests from the client and returning the ip address. For this purpose, it must communicate with other servers.

#### Root Nameserver
One of the 13 root domain name servers. Most often it returns the address of the corresponding top-level domain(TLD) nameserver address IP.

#### TLD Nameserver
The server with domains related to the higher-level domain (.com, .org...)

#### Authoritative Nameserver
If it succeeds in connecting to the server, it returns its IP address to the recursor. It may also be responsible for redirects to subdomains.

### DNS Lookup
![image](https://user-images.githubusercontent.com/48235197/156720746-b0bb9ee3-33c3-475f-8fdd-60b2c7cbbf8f.png)

1. A user types ‘example.com’ into a web browser and the query travels into the Internet and is received by a DNS recursive resolver.
2. The resolver then queries a DNS root nameserver (.).
3. The root server then responds to the resolver with the address of a Top Level Domain (TLD) DNS server (such as .com or .net), which stores the information for its domains. When searching for example.com, our request is pointed toward the .com TLD.
4. The resolver then makes a request to the .com TLD.
5. The TLD server then responds with the IP address of the domain’s nameserver, example.com.
6. Lastly, the recursive resolver sends a query to the domain’s nameserver.
7. The IP address for example.com is then returned to the resolver from the nameserver.
8. The DNS resolver then responds to the web browser with the IP address of the domain requested initially.
Once the 8 steps of the DNS lookup have returned the IP address for example.com, the browser is able to make the request for the web page:

9. The browser makes a HTTP request to the IP address.
10. The server at that IP returns the webpage to be rendered in the browser (step 10).

_Source: https://www.cloudflare.com/en-gb/learning/dns/what-is-dns/_
