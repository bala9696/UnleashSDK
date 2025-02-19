# unleashSDK

## Overview

The `unleashSDK` Python package simplifies interaction with comprehensive NFT and blockchain analytics APIs. This package allows developers to fetch, process, and analyze data with ease, offering extensive features such as market metrics, whale and shark analytics, transaction trends, and wash trade evaluations.

## Features

- Fetch data on NFT collections, traders, transactions, and market activity.
- Access whale and shark metrics for detailed insights.
- Analyze wash trading activities with advanced indexes.
- Retrieve market state scores and trends.
- Support for various time ranges: 24h, 7d, 30d, 90d, or custom ranges.
- Handles edge cases like unavailable data, infinity values, and precision rounding.

## Installation

Install the package via pip:

```bash
pip install unleashSDK
```

## Usage

### Initialization

Start by importing the package and initializing the client with your API key:

```python
from unleashSDK import UnleashNftApi

# Initialize client
client = UnleashNftApi()
client.set_api_key_token("your_api_key")
```

### Examples

#### Fetch Market Analytics

Retrieve market metrics for a specific NFT collection:

```python
response = client.market_analytics_report(blockchain="ethereum", time_range="7d")
print(response)
```

#### Analyze Wallet Trades

Fetch wallet trade data for a given blockchain:

```python
response = client.wallet_traders(blockchain="ethereum", time_range="30d")
print(response)
```

#### Gaming Metrics

Analyze gamming metrics activities:

```python
response = client.gaming_metrics()
print(response)
```

### Error Handling

The package gracefully handles API errors and missing data. For example:

```python
try:
    response = client.get_market_metrics(collection_id="invalid_id")
except unleashSDK.exceptions.APIError as e:
    print(f"An error occurred: {e}")
```

## API Endpoints

### Currencies
- **Description**: All currency values are string-serialized to prevent rounding issues.
- **Format**: Monetary values are returned in the requested currency and, if applicable, the original currency.

### Percentages
- Percentages are returned as ratios (e.g., 0.394 for 39.4%).

### Missing/Unavailable Data
- Missing data points are returned as `"NA"`.

### Infinity Values
- Positive infinity: `"INF_POS"`
- Negative infinity: `"INF_NEG"`

### Date/Datetime
- All date and datetime values are formatted in ISO 8601.

## Metrics

The following metrics are available through the APIs:

| Metric                    | Description                                                                 |
|---------------------------|-----------------------------------------------------------------------------|
| `assets`                  | Number of assets in a collection.                                          |
| `holders`                 | Number of traders currently holding NFTs.                                 |
| `marketcap`               | Total market value of the NFT collection.                                 |
| `price_avg`               | Average price at which NFTs are sold.                                     |
| `sales`                   | Number of NFTs sold.                                                      |
| `transactions`            | Number of transactions.                                                   |
| `washtrade_volume`        | Total trade value suspected of wash trading.                              |
| `traders_ratio`           | Percentage of active traders compared to total traders.                   |

## Trend Time Ranges and Periods

| Time Range  | Parameter | Period of One Data Point | Number of Data Points |
|-------------|-----------|--------------------------|-----------------------|
| 24 hours    | `24h`     | 1 hour                   | 24                    |
| 7 days      | `7d`      | 4 hours                  | 42                    |
| 30 days     | `30d`     | 1 day                    | 30                    |
| 90 days     | `90d`     | 1 day                    | 90                    |
| Custom Range| `range`   | 1 day                    | Based on range        |

## Contributing

Contributions are welcome! Please fork the repository and submit a pull request.

## License

This project is licensed under the MIT License. See the LICENSE file for details.
