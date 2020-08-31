###Install docker on ubuntu : 
https://phoenixnap.com/kb/how-to-install-docker-on-ubuntu-18-04
```
$ mkdir ft_userdata
$ cd ft_userdata/
```

### Download the docker-compose file from the repository
```
curl https://raw.githubusercontent.com/freqtrade/freqtrade/develop/docker-compose.yml -o docker-compose.yml
```

### Pull the freqtrade image
```
docker-compose pull
```

If the above command fails, follow the steps :
```
sudo groupadd docker
sudo usermod -aG docker $USER
```
Log out and log back in so that your group membership is re-evaluated.

If this does not work, then:

Install docker using snap
On Ubuntu Core 18, after installing the docker snap from store,
you need to connect the home interface as it's not auto-connected by default.
    ```
    sudo snap connect docker:home :home
    ```

```
$ cd freqtrade
```

Download data:
```
$ docker-compose run --rm freqtrade download-data --pairs LTC/BTC ATOM/BTC BAT/BTC NXS/BTC ETH/BTC EOS/BTC BCH/BTC XMR/BTC NEO/BTC XRP/BTC ALGO/BTC BRD/BTC IOTA/BTC XTZ/BTC LINK/BTC --exchange binance --days 90 -t 1m
```

Backtest:
```
$ docker-compose run --rm freqtrade backtesting --config user_data/config.json --strategy SampleStrategy --timerange 20200601-20200824 -i 1m
```

HyperOpts:
```
$ docker-compose run --rm freqtrade hyperopt --spaces all --config user_data/config.json --hyperopt-loss SharpeHyperOptLossDaily --strategy SampleStrategy --hyperopt SampleHyperOpt -e 100
```

Run:
```
docker-compose up
```