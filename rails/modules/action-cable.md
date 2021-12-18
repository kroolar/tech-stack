# Action Cable

The Action Cable module allows you to integrate WebSockets with a Rails application on both the client and server side.

### WebSockets

It is a protocol that provides two-way data communiaction as opposed to the HTTP protocol, which works in the request-response cycle.

### Connection
The basis of the client-server relationship. One Action Cable server can have multiple connections. A single user can have many connections if he uses different tabs or devices.

### Consumer
WebSocket connection client. It is allocated on the frontend side of Rails.

### Channel
Each consumer can subscribe to multiple channels. Each channel is one logical unit similar to controllers.

### Subscriber
If a user is connected to a channel, we call him then the subscriber of that channel.

### Pub/Sub
Publisher - person sending the information
Subscriber - person receiving the information

### Sources
- https://edgeguides.rubyonrails.org/action_cable_overview.html
- https://api.rubyonrails.org/files/actioncable/README_md.html
