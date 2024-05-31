# Simple Queue Service

**See Deployment/Task_Queues for comparing between services, this is just a stub**

- Simplest to spin up in AWS with free tier offering 1M free messages
- The service must be long **polled** for messages
- Offers high throughput Standard "at least-once-delievery" which requeues a message if it was consumed from the queue and a visibility timeout passes
- Can also do up to 3k message/sec when order important with  SQS FIFO "exactly once delivery"
- Base rate of 20k+/sec with more expensive options to request
- Messages must be less than 256KiB in size, but can turn it into S3 object



