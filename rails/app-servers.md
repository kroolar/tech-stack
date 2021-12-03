# Application Servers

### 1. What is Web Server
The server is responsible for handling requests between the website. In the case of a standard static website, all its resources, i.e. html, CSS, JS files and pictures, do not change, so the client sends a request for a resource and always receives it back in the same state.

### 2. What is App Server
The web application is more complex. The user can not only select data but also influence it by adding, deleting or modifying it. The application server acts as an intermediary between the client that sends the request and the business logic (code) that performs the request, and then returns the response to the client. The application server can run without a web server, but most often its located in front of it dealing with the management of requests and their forwarding to the application server.

### 3. Concepts

#### Clustering
Cluster is a group of machines (computer or servers) dedicated to one purpose. The process of grouping servers is called clustering. In this case, it can be several servers with the same application installed. This term refers to the use of software that allows you to manage these servers (cluster), thanks to which you can better distribute the traffic, which will result in faster responses and a system more resistant to errors.

#### Multhithreaded
Multithreading is a function thanks to which the CPU is able to start and operate more than one thread, use the same resources in parallel.

#### Slow client buffering
Buffering is a functionality that allows you to pre-laod parts of your data before it is used.

#### Zero Downtime Deploy
This concept means that the application will never be disabled or unstable during the deployment process. To achieve this, the server has to wait until the process is finished serving the new version.

#### ActionCable
It is a module that allows you to integrate Rails applications with WebSockets.

### 4. Serwer Railsowe
The most used servers in rails applications are:

- Puma
- Unicorn
- Passenger

#### Puma
https://github.com/puma/puma

Puma is a light and fast server. It is the default server for a rails application and perfect for getting started with rails right away. It is indicated for use both in production and development.

#### Unicorn
https://github.com/defunkt/unicorn

#### Passenger
https://www.phusionpassenger.com/

Compared to the rest, it has a more complex configuration, which allows for better management of the server, especially in the production environment.


### Comparison

```
                         | UNICORN | PUMA | PASSENGER |
-------------------------|---------|------|-----------|
Clustering               |   ✅    |  ✅  |    ✅     |
-------------------------|---------|------|-----------|
Multhithreaded           |   ❌    |  ✅  |    ✅     |
-------------------------|---------|------|-----------|
Slow client buffering    |   ❌    |  ✅  |    ✅     |
-------------------------|---------|------|-----------|
ActionCable              |   ✅    |  ✅  |    ✅     |
-------------------------|---------|------|-----------|
Zero-Downtime Deploys    |   ✅    |  ✅  |    ✅     |
-------------------------|---------|------|------------
```

### There are also some less common alternatives that are used with rails
- Mongrel (https://mongrel2.org/)
- Thin (https://github.com/macournoyer/thin)
