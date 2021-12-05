# Redis Database Usage with Minikube

We are building a coupon service which is essentially like a streaming service for some requests. We will use Redis Streams for Queuing. We will then make the image of the service and deploy the redis instance and image to a minikube kubernetes cluster. The essential commands will be in this Readme.

## Working of the Coupon Service

We have 4 major regions (APAC, NA, SA, EU) with running service who want coupons to distribute to their local users. They constantly demand coupon codes from our server. As merchants add the coupons, they become available for redemption.

## What we are Building?
We are making a microservice that has a coupon code distribution instance. This can be demanded from different consumers. The coupons are stored in our database categorized based on merchants. The merchants add their codes to our database using REST API. For each merchant we have a Redis list. After every coupon addition, messages are added to redis stream based on the coupons in the list. These streams are subscibed by consumers who then get code based on requests. We also purge all the older requests every 24 hours if they have not been fulfilled.

## Redis Database

Redis is an open source database that can be treated as a key-value store that we can use for Database purposes(NoSQL), Caching and for Message brokering.