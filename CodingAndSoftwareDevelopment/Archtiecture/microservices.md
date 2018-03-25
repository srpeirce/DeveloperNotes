# Microservices

Microservices is an architectural pattern that addresses some of the problems with a [monolith](monolith.md).

## What are microservices

...

## Benefits of microservices

### Performance

- Microservices can be scaled out independently, so no longer do you have to scale everything but just the bits that need to be scaled out.
- You could theoretically scale out infinitely to meet any demand
- There are a number of ways to configure auto-scaling

### More

...

## The drawbacks/complexity of microservices

Complexiy managing multiple services, service discovery, more moving peices and infrastrucutre to support, etc. etc...

## Useful references

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