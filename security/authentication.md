# Authentication


- [Basic Auth](#basic)

### <a name="basic">Basic Auth</a>
It is a simple authentication scheme built into the HTTP protocol. The client sends HTTP requests with the Authorization header that contains the word Basic, followed by a space and a base64-encoded username and password _(username:password)_.

```rb
username = admin
password = admin123

encoded_credentials = Base64.strict_encode64("#{username}:#{password}") # => "YWRtaW46YWRtaW4xMjM="

# This is how the header should look like
# Authorization: Basic YWRtaW46YWRtaW4xMjM=
headers = { Authorization: "Basic #{encoded_credentials}" }

HTTParty.get("https://example.com", headers: headers)
```

It is easy to decrypt credentials, so it is recommended to use the HTTPS protocol so that no one can see the transmission.
```rb
Base64.strict_decode64('YWRtaW46YWRtaW4xMjM') # => "admin:admin123"
```


Pros:
- Simple implementation
- Only one call to the server, making it fast

Cons
- Credentials are sent with every request which increases the risk
- It is easy to decode credentails due to lack of encryption


Encoding encyption hashing
