# alpaca-postman
Postman collections for Alpaca's APIs can be found in a public workspace located [here](https://www.postman.com/alpacamarkets).

## Alpaca Postman Collections
There are Postman collections for the [Data]([https://alpaca.markets/docs/api-documentation/api-v2/market-data/](https://docs.alpaca.markets/docs/about-market-data-api), [Trader]([https://alpaca.markets/docs/api-documentation/api-v2/](https://docs.alpaca.markets/docs/trading-api), and [Broker](https://docs.alpaca.markets/docs/about-broker-api) APIs. 

## Getting Started
To demonstrate how to get started, let's walk through the Broker API collection.

The first step is forking the collection. 

<img width="350" src="https://user-images.githubusercontent.com/24945583/134990354-3d645c18-2ce1-4bcd-8195-503605bf2bb5.png">

Go ahead and enter the name for your fork and select the workspace where you'll be working from.

<img width="350" alt="Screen Shot 2021-09-27 at 5 53 38 PM" src="https://user-images.githubusercontent.com/24945583/134990643-7d42b729-c1e0-4f78-bc85-40fb214d4a28.png">

You can fork the example environment as well. Name your fork and select the same workspace you forked the collection to.

<img width="350" src="https://user-images.githubusercontent.com/24945583/134991391-02b2fe26-c62e-43af-8743-97847c788476.png">

Get your API keys from [here](https://broker-app.alpaca.markets/sign-up). Upon creating an account you will be prompted to generate your keys. Be sure to store your api_key and api_secret somewhere private. Once you have your keys, head to the workspace where you forked your collection and environment. Keep in mind, this sample environment already has the host value for a sandbox account. If you would like to work in a production environment you will need to change the host URL and obtain the correct api keys for a production account. To continue with the sandbox environment, simply enter your api_key and api_secret in their respective place. Once you enter your keys, select this environment in the upper right corner as pictured below. 

<img width="902" src="https://user-images.githubusercontent.com/24945583/134991535-0c946383-fbe9-4f4c-97c3-c1511813df2d.png">

Once your environment is configured you’re ready to make your first call! The Clock or Calendar resources are a great place to start to make sure your environment is configured correctly. Head to the GET Clock request and press Send. You should receive a similar response to the one pictured below.

<img width="1202" alt="Screen Shot 2021-09-27 at 6 07 16 PM" src="https://user-images.githubusercontent.com/24945583/134991935-c9e06650-8094-4f7c-bdf7-e7ab1f5991a0.png">

## Issues
As an API-first product company, we are committed to providing the best developer experience. If you notice any bugs or just have a recommendation for how we can improve the collections please don't hesitate to file an [issue](https://github.com/alpacahq/alpaca-postman/issues).
