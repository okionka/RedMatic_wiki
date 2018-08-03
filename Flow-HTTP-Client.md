# JSON Daten von Webservice abfragen und in Systemvariable schreiben

Für dieses Beispiel wird der ein Webservice verwendet der den aktuellen Wechselkurs des Bitcoin zurückgibt. Er eignet sich gut als Beispiel da er keinen API Key verlangt und das zurückgegebene JSON recht übersichtlich ist:

`https://api.coindesk.com/v1/bpi/currentprice.json`

```Javascript
{
	"time": {
		"updated": "Aug 3, 2018 20:09:00 UTC",
		"updatedISO": "2018-08-03T20:09:00+00:00",
		"updateduk": "Aug 3, 2018 at 21:09 BST"
	},
	"disclaimer": "This data was produced from the CoinDesk Bitcoin Price Index (USD). Non-USD currency data converted using hourly conversion rate from openexchangerates.org",
	"chartName": "Bitcoin",
	"bpi": {
		"USD": {
			"code": "USD",
			"symbol": "&#36;",
			"rate": "7,388.6163",
			"description": "United States Dollar",
			"rate_float": 7388.6163
		},
		"GBP": {
			"code": "GBP",
			"symbol": "&pound;",
			"rate": "5,683.2867",
			"description": "British Pound Sterling",
			"rate_float": 5683.2867
		},
		"EUR": {
			"code": "EUR",
			"symbol": "&euro;",
			"rate": "6,384.5550",
			"description": "Euro",
			"rate_float": 6384.555
		}
	}
}
```

