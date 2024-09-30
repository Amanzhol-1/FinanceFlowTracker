# FinanceFlowTracker

## Description
FinanceFlowTracker is a microservice developed using Spring Boot, designed for managing financial transactions and monitoring monthly spending limits. The service allows for recording transactions in different currencies, automatically converting amounts into USD using current exchange rates, setting individual limits by spending categories, and generating reports for transactions that exceed the established limits.

## Technologies
- **Spring Boot** — framework for creating and managing RESTful APIs.
- **Hibernate/JPA** — for working with a relational database.
- **Lombok** — a library for reducing boilerplate code.
- **RestTemplate/WebClient** — for interacting with external APIs (currency exchange rates).
- **Docker** — for containerizing the application.
- **Docker Compose** — tool for managing multi-container Docker applications.
- **JUnit 5** — for unit testing and writing test cases.

## Features
- **Transaction recording**: records and saves information on expense transactions in various currencies (e.g., KZT, RUB).
- **Monthly spending limit**: stores monthly spending limits in USD for "goods" and "services" categories.
- **Currency exchange rates**: daily updates of KZT/USD and RUB/USD currency pairs with storage in the database. If current data is unavailable, the rate from the previous day is used.
- **Limit exceeded flag**: automatically flags transactions that exceed the monthly limit with a limit_exceeded flag.
- **Setting a new limit**: allows setting a new spending limit with the current date. The new limit does not affect past transactions.
- **Exceeded limit report**: provides a list of transactions that exceeded the limit, including the limit amount, currency (USD), and the date the limit was set.

## API Endpoints

### 1. Transaction Handling API
| Method | HTTP Request | Description |
|-------|-------------|----------|
| POST  | `/api/transactions/create` | Creates a new transaction |
| GET   | `/api/transactions/all` | Retrieves a list of all transactions |
| GET   | `/api/transactions/exceeding-limit?limit={limit}` | Retrieves transactions that exceeded the specified limit |
| GET   | `/api/transactions/by-category-and-month` | Retrieves transactions by category and month |
| GET   | `/api/transactions/limit-exceeded-report` | Retrieves a report of transactions that exceeded the limit |

### 2. Client API for Limit Management
| Method | HTTP Request | Description |
|-------|-------------|----------|
| POST  | `/api/limits/set` | Sets a new spending limit |
| GET   | `/api/limits/all` | Retrieves a list of all set limits |
| GET   | `/api/limits/by-category/{category}` | Retrieves limits for the specified spending category |

### 3. API for Updating Currency Rates
| Method | HTTP Request | Description |
|-------|-------------|----------|
| GET   | `/update-currency-rates` | Manual update of currency exchange rates |

## Additional Information
- **Default Currency**: All limits are set in USD.
- **Currency Rates**: Currency rates are fetched from an external API and cached in the database to optimize requests.
- **Handling rates on weekends and holidays**: If exchange rates are unavailable on the current date, the last available rate is used.



----


# Documentation on launching the FinanceFlowTracker project
## 1. Repository cloning

Clone the project repository to your local computer:

```bash
git clone https://github.com/Amanzhol-1/FinanceFlowTracker.git
```

## 2. Configuring API key to get currency rates

### Setting up API key to get currency rates:
Sign up for the service [Twelve Data](https://www.twelvedata.com/) 

### Specify the API key in the project:
 Open the file `CurrencyService.java`, en route:
   ```bash
   src/main/java/work/financeflowtracker/service/CurrencyService.java
   ```

 Find the line:
   ```java
   String apiKey = "YOUR API KEY";
   ```

3. Replace `"YOUR API KEY"` with your actual API key.

## 3. Configuring environment variables

In the file `docker-compose.yml`, you need to add your database details etc

## 4. Starting the application

Open the terminal and navigate to the root directory of the FinanceFlowTracker project:

```bash
cd FinanceFlowTracker
```

```bash
docker-compose up --build
```
