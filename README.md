# Sentiment Analysis Application

## Overview

This project is a sentiment analysis application that leverages Twitter news streams, Kafka messaging, and NLP techniques to analyze the sentiment of messages in real-time. The application is built using Spring Boot and integrates with Stanford CoreNLP for sentiment analysis.

## Features

- **Start News Stream**: Starts a filtered news stream based on a keyword.
- **Stop News Stream**: Stops the current news stream.
- **Grouped Messages**: Groups messages received from Kafka within a specified time window.
- **Sentiment Analysis**: Analyzes the sentiment of messages received from Kafka and provides an average sentiment score.

## Project Structure

- **com.handson.sentiment.controller.AppController**: Main controller handling HTTP requests and coordinating the application's functionality.
- **com.handson.sentiment.kafka.AppKafkaSender**: Handles sending messages to Kafka topics.
- **com.handson.sentiment.nlp.SentimentAnalyzer**: Provides sentiment analysis functionality using Stanford CoreNLP.
- **com.handson.sentiment.twitter.AppNewsStream**: Handles streaming of news from Twitter.

## Endpoints

### 1. Start News Stream
- **URL**: `/startNews`
- **Method**: GET
- **Description**: Starts the news stream filtered by the provided text.
- **Parameters**: 
  - `text` (String): The keyword to filter news.

### 2. Stop News Stream
- **URL**: `/stopNews`
- **Method**: GET
- **Description**: Stops the currently running news stream.

### 3. Grouped Messages
- **URL**: `/grouped`
- **Method**: GET
- **Description**: Retrieves and groups messages from Kafka within a specified time window.
- **Parameters**: 
  - `text` (String, default: "israel"): The keyword to filter news.
  - `timeWindowSec` (Integer, default: 3): The time window in seconds to group messages.

### 4. Sentiment Analysis
- **URL**: `/sentiment`
- **Method**: GET
- **Description**: Analyzes the sentiment of messages within a specified time window.
- **Parameters**: 
  - `text` (String, default: "obama"): The keyword to filter news.
  - `timeWindowSec` (Integer, default: 3): The time window in seconds to analyze messages.

## Setup

### Prerequisites

- Java 11 or higher
- Maven
- Kafka

### Installation

1. Clone the repository:
    ```sh
    git clone <repository-url>
    cd <repository-directory>
    ```

2. Update the `application.properties` file with your Kafka credentials.

3. Build the project using Maven:
    ```sh
    mvn clean install
    ```

4. Run the application:
    ```sh
    mvn spring-boot:run
    ```

## Usage

Once the application is running, you can interact with it using the provided endpoints. Use a tool like Postman or `curl` to make HTTP requests to the application's endpoints.

## Sentiment Analysis

The sentiment analysis is performed using the Stanford CoreNLP library. The sentiments are categorized and mapped to numerical values as follows:

- Very negative: 1
- Negative: 2
- Neutral: 3
- Positive: 4
- Very positive: 5

The average sentiment score is calculated based on the messages within the specified time window.

## Contributing

Contributions are welcome! Please open an issue or submit a pull request for any changes or improvements.
