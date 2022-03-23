# Domain Name
In order to establish a connection between the browser and the website, we need to enter the server's IP address. In fact, this approach is not used very often as IP addresses are not human readable. Therefore, we use plain text in the browser. This is what we call a domain name, i.e. a specific name associated with a specific IP address.

### How it works

After entering the domain name, the browser sends a query to DNS. This one is to find the IP address assigned to the given domain, and then return it to our browser. This process is called DNS lookup.

### Domain structure
A domain usually consists of two or three members.

`developer.mozilla.org`

#### Top-Level Domain(TLD)
The first from the right is the so-called **top-level domain** and it defines the main purpose of the website, e.g. _.gov(government website)_ or _.edu(education website)_. It can also stand for a specific language or its server location, e.g. _.pl_ or _.en_.

#### Second-Level Domain(2LD)
The second part of the address is usually your domain name.

`mozilla.com`

#### Third-Level Domain(3LD)
Sometimes, however, both the operation of the website and its location are used, in which case your domain name will be in the third position from the right.

`mozilla.co.uk`
 
#### Subdomain
Sometimes, in addition to the root domain, you also need to create subdomains. In this case, the names of these subdomains will be the main name of your domain.

`dev.mozilla.co.uk`
 
### How to buy a domain?
You can't actually buy a domain. In fact, you can buy the right to use the domain for a specific period of time. Of course, if the period is over, you have the right to re-buy it first, but if you don't, someone else will be able to use your domain.
 
### Registrar
It is a company that deals with the reservation of domains and the assignment of IP addresses for these domain names. 

### How to check a domain
Using the command line, it is very easy to see who the domain currently belongs to.
```
whois google.com
```
 
### Who is managing domains?
ICANN a non-profit organization that helps coordinate the Domain Name System
 
### DNS refreshing
DNS databases are stored on servers around the world. Therefore, each creation of a new domain or updating their value must be entered in each database. Therefore, it takes a while for the DNS server to refresh the current information.
  
#### More
- https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_domain_name
- https://www.cloudflare.com/en-gb/learning/dns/glossary/what-is-a-domain-name/
- https://www.cloudflare.com/learning/dns/glossary/what-is-a-domain-name-registrar/
