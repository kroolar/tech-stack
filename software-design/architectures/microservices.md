# Microservices

Microservices is an application composed of several smaller websites, most often each of them has its own process, database and communicate with each other via API. They are often divided according to business goals.

### Pros
- Flexibility in the selection of technology, each website can be built in a different technology
- Each website can be implemented independently of the others
- An error in one service does not affect the entire application
- It's easier to add new functionalities
- Easier to understand and manage (you only need to know one context)
- Better scalability
- Easier to test individual modules

### Cons
- It's harder to test the entire application
- Communication between modules is slower than in the case of the monolith
- Reliability less
- Less security
- More configurations (databases, API, login, cache)

### When to use
- If your application starts to grow 
- If you have knowledge and experience in microservices
