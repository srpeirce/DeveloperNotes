# Microservices

Microservices is an architectural pattern that addresses some of the problems with a traditional monolithic application.

I will detail what I think a monolith is and some of the problems. I will then detail microservices, how they help address the issue, and the drawbacks/complexity that they bring.

## The Monolith

This is a single application, often split into multiple layers which may include:

- UI
- Infrastructure
- Services
- Domain
- Data Access

This may be the correct approach when there is:

- A small team
- A simple application

However, most of us have experienced the pain caused by a single application growing into a large, complex beast, with a growing team trying to manage it.

Here are some of the issues that I have experienced:

### Performance

Monoliths can be difficult to scale out (add more instances), and will often be scaled up (add more resources)

- Often the applications are large and slow to start
- There will likely be different parts of the application that needs to scale at different levels…
  - e.g. Image preparation could be a bottleneck, you are unable to scale out this individual piece in a monolith
  - You might need 100x instances to cope with images…but it would be too costly to scale the entire application 100x
- Usually use 1 shared database, that can get bogged down causing system wide performance issues

### Contamination across domains/bounded contexts

Over time it's easy for a monolithic applications to become a big ball of mud filled with spaghetti code…this often happens when the business is demanding new features/tweaks all the time and not allowing developers to keep their house in order. Eventually you reach the point where the code is so complex and difficult to understand, new features are very slow and difficult to add. It then becomes very difficult to refactor and re-architect code to be more maintainable.

- It's easy to re-use code that "sounds the same" but will actually be used for a different purpose
- This can cause bugs due to unexpected behaviours
- This can lead to classes being used for multiple purposes across bounded contexts…a couple extra properties here, a couple extra methods thee, leading to difficult to maintain, error prone code.
  - Using a method that already exists for a different bounded context might sound good, but then if the original creators of the method change the functionality it will now break your code.
    - DRY (Don't Repeat Yourself) can be overused - if 2 teams manage their own Customer class then they can evolve at their own rate. If it is shared between 2 teams then all of a sudden they might need to liaise for every change that is made or risk breaking each others code.
    - Shared Kernel is the place for shared code…you know that if it's there and you need to make changes, you will need to talk to some other teams.
- A large application often has a single shared database, this means it's easy for parts of the system to pull data that perhaps it shouldn't be using or not necessarily understand.

### Slow to deliver value

- If there is a change in the system, it may be difficult to understand any impact/side-effects resulting in large regression cycles
- Multiple teams will likely be working on the application simultaneously, leading to
  - merge conflicts
  - Complexity understanding what is in a release
  - Complexity with release branches
  - Tests breaking - it's not always clear who or what team is responsible
  - A case of too many chefs in the kitchen

## What are microservices

...

## Benefits of microservices

...

## The drawbacks/complexity of microservices

...

## Experience

### Purplebricks

...

### AIG

...

### ITG

Another Uber that needed splitting up.
Started making waves into a SOA world by pulling out image processing service.
Basically they had media of all different types (images, PDFs, videos) and very large sizes (single image could be upto 8GB - this is because they are created for print).

We previously had mutliple versions of imageprocessor - for different re-writes/customisations for different clients. I unified this with a single imageprocessor service to be maintained.

Used RabbitMQ for pub/sub.

Used (can't remember what it's called) to manage high-priority and low-priority workloads.
We basically had bulk imports of images that were low priority, and single image uploads that were high priority.

Configurable batch sizes.

### TIF

...

### LV=

Working in SOA at LV=.
Receive an API call for a quote, have to return a quote within a ~second? (Can't remember the exact time).

- The reason being some aggregators will show the results as they come in, or user could choose not to wait.

Within the time, we had to call multiple services

- Check customer is eligible for insurance
- Experian for partial credit check (Does not affect credit score)
- Multi policy proposition - bsically run the persons details against a huge database that has everything we know about customers
  - E.g. do they have any other policies with us
  - Have they ever missed a payment
  - Does anyone else in the property have any policies
    - Call rating engine to get a price

GI was LV=s bread and butter at the time.

Message Queues / Service Buses