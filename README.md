# GasPrice

GasPrice is a collection of two little scripts to quickly show what a standard ETH transaction would cost at the moment, similar to what can be found on [Etherscan](https://etherscan.io/gastracker): a Python command line script and [Scriptable](https://scriptable.app/) script to be used as iOS widget.

They use the [ETH Gas Station](https://www.ethgasstation.info) API for the average gas price and the [Cryptonator](https://www.cryptonator.com) API to convert the gas price to fiat.

# Scriptable Widget

The widget version of the script, to run as a Scriptable script and used as iOS widget or Siri answer. Change the “parameter” in Scriptable to `USD` to change the fiat currency, it will convert to `EUR` by default.

## Usage

Copy the [gasprice.scriptable](gasprice.scriptable) JavaScript code to a new script in the Scriptable iOS app. Now add the widget to the Home Screen.

## Example

![Scriptable iOS widget](widget.png)

# CLI Script

The Python version, to run on the command line. This script can also send a [Prowl](https://www.prowlapp.com) push notification if the price is below a certain threshold, intended to run as a cronjob, for example.

## Usage

```
usage: gasprice [-h] [--currency {USD,EUR}] [--only-if-below ONLY_IF_BELOW] [--prowl-key PROWL_KEY]

Gets the average Etherium gas price from the ETH Gas Station API and calculates
what a standard transaction would cost in fiat using Cryptonator’s API.

optional arguments:
  -h, --help            show this help message and exit
  --currency {USD,EUR}  fiat currency to convert to
  --only-if-below ONLY_IF_BELOW
                        only trigger if gas price is below set value (in gwei)
  --prowl-key PROWL_KEY
                        sends a push notification if a Prowl API key is given
```

Don’t forget to mark the script as executable. By default, the script will print to STDOUT but you can redirect it to Prowl by providing a Prowl API key. Nothing will be shown if the gas price is larger than the target value when the `--only-if-below` argument is used.

## Examples

Simple.

```
$ ./gasprice
Average gas price is 277 gwei (~ 7.58 EUR)
```

In USD.

```
$ ./gasprice --currency=USD
Average gas price is 274 gwei (~ 9.01 USD)
```

Only if gas price is < 100 gwei (no output since the current gas price is 274 gwei).

```
$ ./gasprice --only-if-below=100
```

With Prowl (no output since the output is redirected to Prowl).

```
$ ./gasprice --only-if-below=500 --prowl-key=ABC123
```
