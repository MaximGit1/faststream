# Dynamic Subscription

## What is a Dynamic Subscription?

A dynamic subscription is a subscription that is created and registered during the application's runtime. Unlike standard subscribers, which are configured during the application's initialization, dynamic subscribers allow for flexible adaptation to current tasks by adding or removing message handlers on the fly.

This functionality is especially useful for handling temporary queues or events that cannot be predetermined.


**Dynamic subscriptions offer several key benefits:**


1. Flexibility
    Add subscribers dynamically while the application is running, without requiring a restart.
2. Manageability
    Easily enable or disable subscribers, for example, to handle temporary events or perform testing.
3. Wide Compatibility
    Works seamlessly with popular brokers, including AIOKafka, RabbitMQ, Redis, NATS, and more.
4. Efficient Resource Usage
    Subscribers are only active when needed, helping to avoid unnecessary load on the system.


## Create a Dynamic Subscriber

To create a dynamic subscriber, you must specify a queue and a handler.

```python
async def handler(msg: str) -> None:
    ...


subscriber = broker.subscriber("dynamic")
subscriber(handler)
```

And register the subscriber with the broker:

```python
broker.setup_subscriber(subscriber)
```

## Start and close the Subscriber

Start the subscriber to begin processing messages from the queue:

```python
await subscriber.start()
```

When the subscriber is no longer needed, you can gracefully shut it down using the close method:

```python
await subscriber.close()
```