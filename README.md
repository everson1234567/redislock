# Redis Lock for Lambdas 🗝️

![GitHub release](https://img.shields.io/github/v/release/everson1234567/redislock?color=blue&label=Latest%20Release)

Redis Lock for Lambdas is a pure Python library that provides a distributed locking mechanism using the Redis Protocol. This library is ideal for scenarios where multiple concurrent AWS Lambda executions need to ensure that certain tasks are performed exclusively by a single instance. It supports configurable TTL, backoff strategies, customizable timeouts, time zone settings, and includes a built-in Redis client.

## Table of Contents

1. [Features](#features)
2. [Installation](#installation)
3. [Usage](#usage)
4. [Configuration](#configuration)
5. [Examples](#examples)
6. [Contributing](#contributing)
7. [License](#license)
8. [Releases](#releases)
9. [Topics](#topics)

## Features

- **Distributed Locking**: Ensures that only one Lambda function instance can execute a specific task at a time.
- **Configurable TTL**: Set the time-to-live for locks to manage how long a lock should be held.
- **Backoff Strategies**: Automatically manage retries with backoff intervals to avoid contention.
- **Customizable Timeouts**: Adjust the timeout settings to fit your needs.
- **Time Zone Support**: Manage locks across different time zones.
- **Built-in Redis Client**: Simplifies connection and interaction with Redis.

## Installation

To install Redis Lock for Lambdas, you can use pip. Run the following command:

```bash
pip install redislock
```

Ensure that you have Python and pip installed on your machine. If you do not have Redis set up, follow the official Redis documentation to install it.

## Usage

Here’s a basic example of how to use Redis Lock for Lambdas in your Python code:

```python
from redislock import RedisLock

def my_lambda_function(event, context):
    lock = RedisLock('my_lock_key')

    if lock.acquire():
        try:
            # Your task logic here
            print("Task is being executed exclusively.")
        finally:
            lock.release()
    else:
        print("Could not acquire lock, task is skipped.")
```

In this example, the `my_lambda_function` attempts to acquire a lock before executing its task. If it cannot acquire the lock, it will skip the task.

## Configuration

You can configure the Redis Lock settings to fit your requirements. Here are some common configurations:

```python
lock = RedisLock(
    key='my_lock_key',
    ttl=60,  # Time-to-live in seconds
    backoff=2,  # Backoff strategy in seconds
    timeout=10,  # Timeout for lock acquisition in seconds
    tz='UTC'  # Time zone
)
```

### Key Parameters

- **key**: The unique key for the lock.
- **ttl**: Time-to-live for the lock.
- **backoff**: The time to wait before retrying to acquire the lock.
- **timeout**: The maximum time to wait for the lock.
- **tz**: The time zone to use for the lock.

## Examples

### Basic Example

Here’s a simple example demonstrating the basic functionality:

```python
from redislock import RedisLock

def my_task():
    lock = RedisLock('my_task_lock')

    if lock.acquire():
        try:
            print("Executing task...")
            # Perform your task here
        finally:
            lock.release()
    else:
        print("Task is already running.")
```

### Advanced Example with Custom Configuration

In this example, we configure the lock with custom settings:

```python
from redislock import RedisLock

def my_advanced_task():
    lock = RedisLock(key='advanced_task_lock', ttl=120, backoff=5, timeout=15)

    if lock.acquire():
        try:
            print("Executing advanced task...")
            # Perform your advanced task here
        finally:
            lock.release()
    else:
        print("Could not acquire lock for advanced task.")
```

## Contributing

Contributions are welcome! If you want to contribute to this project, please follow these steps:

1. Fork the repository.
2. Create a new branch (`git checkout -b feature-branch`).
3. Make your changes.
4. Commit your changes (`git commit -m 'Add new feature'`).
5. Push to the branch (`git push origin feature-branch`).
6. Open a pull request.

Please ensure that your code follows the project's coding standards and includes appropriate tests.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Releases

For the latest releases, please visit the [Releases](https://github.com/everson1234567/redislock/releases) section. Here you can find the latest version of the library and download it.

## Topics

This repository covers the following topics:

- AWS
- ElastiCache
- ElastiCache Cluster
- ElastiCache Redis
- Lambda
- MemoryDB
- MemoryDB Cluster
- Redis
- Redis Cluster
- Redis Server

For more information about these topics, feel free to explore the documentation or visit the [Releases](https://github.com/everson1234567/redislock/releases) section for updates.

## Conclusion

Redis Lock for Lambdas provides a reliable way to manage distributed locks in AWS Lambda environments. By using this library, you can ensure that critical tasks are executed without conflicts, improving the reliability of your serverless applications.