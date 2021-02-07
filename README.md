# GasPrice

Small CLI script that calculates what a standard ETH transaction would cost at the moment. It can send a [Prowl](https://www.prowlapp.com) push notification if the price is below a certain threshold, intended to run as a cronjob for example.

It uses the [ETH Gas Station](https://www.ethgasstation.info) API for the average gas price and the [Cryptonator](https://www.cryptonator.com) API to convert the gas price to fiat.
