<h1 align="center">
  <br />
  <img src="https://user-images.githubusercontent.com/168240/41822669-34e92094-77a8-11e8-831e-67d38e686c21.png" alt="go-coinmarketcap" width="600" />
  <br />
  <br />
  <br />
</h1>

> The latest and most up-to-date [CoinMarketCap](https://coinmarketcap.com/) API client for [Go](https://golang.org/).

[![License](http://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/miguelmota/go-coinmarketcap/master/LICENSE.md) [![Build Status](https://travis-ci.org/miguelmota/go-coinmarketcap.svg?branch=master)](https://travis-ci.org/miguelmota/go-coinmarketcap) [![Go Report Card](https://goreportcard.com/badge/github.com/miguelmota/go-coinmarketcap?)](https://goreportcard.com/report/github.com/miguelmota/go-coinmarketcap) [![GoDoc](https://godoc.org/github.com/miguelmota/go-coinmarketcap?status.svg)](https://godoc.org/github.com/miguelmota/go-coinmarketcap)

Supports the CoinMarketCap API [Pro Version](https://pro.coinmarketcap.com/api/v1), [V2](https://coinmarketcap.com/api) and V1 Public API

## Documentation

[https://godoc.org/github.com/miguelmota/go-coinmarketcap](https://godoc.org/github.com/miguelmota/go-coinmarketcap)

## Install

```bash
go get -u github.com/miguelmota/go-coinmarketcap
```

## Pro V1 (latest)

| Type           | Endpoint                               | Implemented? |
|----------------|----------------------------------------|--------------|
| Cryptocurrency | /v1/cryptocurrency/info                | Yes          |
| Cryptocurrency | /v1/cryptocurrency/map                 | -      |
| Cryptocurrency | /v1/cryptocurrency/listings/latest     | Yes          |
| Cryptocurrency | /v1/cryptocurrency/market-pairs/latest | -      |
| Cryptocurrency | /v1/cryptocurrency/ohlcv/historical    | -      |
| Cryptocurrency | /v1/cryptocurrency/quotes/latest       | -      |
| Cryptocurrency | /v1/cryptocurrency/quotes/historical   | -      |
| Exchange       | /v1/exchange/info                      | -      |
| Exchange       | /v1/exchange/map                       | -      |
| Exchange       | /v1/exchange/listings/latest           | -      |
| Exchange       | /v1/exchange/market-pairs/latest       | -      |
| Exchange       | /v1/exchange/quotes/latest             | -      |
| Exchange       | /v1/exchange/quotes/historical         | -      |
| Global Metrics | /v1/global-metrics/quotes/latest       | -      |
| Global Metrics | /v1/global-metrics/quotes/historical   | -      |
| Tools          | /v1/tools/price-conversion             | -      |

### Getting started

```go
package main

import (
	"fmt"
	"log"

	cmc "github.com/miguelmota/go-coinmarketcap/pro/v1"
)

func main() {
	client := cmc.NewClient(&cmc.Config{
		ProAPIKey: "01585d6d-123-456-789-3146576cbc70",
	})

	listings, err := client.CryptocurrencyListingsLatest(&cmc.CryptocurrencyListingsLatestOptions{
		Limit: 1,
	})
	if err != nil {
		log.Fatal(err)
	}

	for _, listing := range listings {
		fmt.Println(listing.Name)               // "Bitcoin"
		fmt.Println(listing.Quote["USD"].Price) // 6316.75736886
	}
}
```

### Examples

For more examples, check out the [`./pro/v1/example`](./pro/v1/example) directory and [documentation](https://godoc.org/github.com/miguelmota/go-coinmarketcap/pro/v1)

---

## V2

NOTE: CoinMarketCap will deprecated this API on December 2018

### Getting started

```go
package main

import (
	"fmt"
	"log"

	cmc "github.com/miguelmota/go-coinmarketcap"
)

func main() {
	tickers, err := cmc.Tickers(&cmc.TickersOptions{
		Start:   0,
		Limit:   100,
		Convert: "USD",
	})
	if err != nil {
		log.Fatal(err)
	}

	for _, ticker := range tickers {
		fmt.Println(ticker.Symbol, ticker.Quotes["USD"].Price)
	}
}
```

### Examples

For more examples, check out the [`./v2/example`](./v2/example) directory and [documentation](https://godoc.org/github.com/miguelmota/go-coinmarketcap/v2)

---

## V1

NOTE: CoinMarketCap will deprecated this API on November 2018

### Getting started

```go
package main

import (
	"fmt"
	"log"

	cmc "github.com/miguelmota/go-coinmarketcap"
)

func main() {
	tickers, err := cmc.Tickers(&cmc.TickersOptions{
		Start:   0,
		Limit:   100,
		Convert: "USD",
	})
	if err != nil {
		log.Fatal(err)
	}

	for _, ticker := range tickers {
		fmt.Println(ticker.Symbol, ticker.Quotes["USD"].Price)
	}
}
```

### Examples

For more examples, check out the [`./v1/example`](./v1/example) directory and [documentation](https://godoc.org/github.com/miguelmota/go-coinmarketcap/v1)

## License

MIT
