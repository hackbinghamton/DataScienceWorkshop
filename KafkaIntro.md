## What is Kafka?

Kafka is a **big data streaming service** that allows multiple sources to upload and download data, such as log files or bug reports. Kafka organizes data and ensures that it is kept in order, and that all data goes where it needs to. Kafka was originally created by LinkedIn, but is now maintained by Apache.

# Messages

Kafka transmits data in the form of **messages**, which are small files containing any type of data. Messages are created and transmitted in real-time, and some examples of messages include:
- program crash logs
- customer support chat records
- forms received through a webpage

These messages are given to Kafka via API calls. Once a message is given to Kafka, the data is queued and stored in servers until users access the messages

# Producers and Consumers

Programs or users that create and send data are called **producers**, and programs or users that read data are called **consumers**. There are separate APIs for [producers](https://kafka-python.readthedocs.io/en/master/apidoc/KafkaProducer.html) and [consumers](https://kafka-python.readthedocs.io/en/master/apidoc/KafkaConsumer.html), and you can find examples of how to use them [here](https://kafka-python.readthedocs.io/en/master/usage.html).


# Kafka Topics

Producers and consumers subscribe to Kafka topics, which are the structure Kafka uses for **data organization**. A topic is a group of related data that is separated into its own sub-stream. Organizations can pick and choose who has access to which topics, which allows companies to keep data secure by limiting the number of people who have access to it.

# Kafka Clusters



# Data Queueing

# Data Partitioning
