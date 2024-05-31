# Task Queues

Elixir has Broadway

Python has Celery to process jobs, but you still need a message broker/connector (differences [here)](https://medium.com/@saurabhrayakwar/kafka-vs-rabbitmq-vs-sqs-7c8b7838aec6) and [here](https://docs.celeryq.dev/en/stable/getting-started/first-steps-with-celery.html#id3)

## Task Queues

![Messege-broker-comparison-table](https://www.aspecto.io/wp-content/uploads/2021/05/Messege-broker-comparison-table-1-1024x878.png)

- Kafka
  - Seems like most complex with messages pulled in batch
  - offsets saved in brokers? for easy restarting
  - Allows rate of 100k+/sec and focus on throughput
  - Apache Opensource
- Rabbitmq
  - seems paid
  - can subscribe to topics
  - allows blocking/socket connections to request tasks
  - VMWare opensource
- SQS
  - Simplest to spin up in AWS with free tier offering 1M free messages
  - Does long polling 
  - Offers high throughput Standard "at least-once-delievery" which requeues a message if it was consumed from the queue and a visibility timeout passes
  - Can also do up to 3k message/sec when order important with  SQS FIFO "exactly once delivery"
  - Base rate of 20k+/sec with more expensive options to request
  - Messages must be less than 256KiB in size, but can turn it into S3 object
- SNS 
  - AWS similar but broadcasts messages instead of being consumed by single consumer



