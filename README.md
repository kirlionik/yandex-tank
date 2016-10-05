# Yandex-tank docker container
This repository only for docker container with yandex-tank.

## Container has next applications:

* Yandex.Tank version is 1.7.32
* Oracle-jdk8
* Jmeter 
* Module yatank-online
* SSH server

## Usage

You should have already install [Docker](https://www.docker.com/).

Execute:

If you need in online monitoring:
```sh
	$ docker run -it -v $(pwd):/var/loadtest -v $HOME/.ssh:/root/.ssh kirlionik/yandex-tank:latest
```

If you do not need in online monitoring:

```sh
	$ docker run -it -v $(pwd):/var/loadtest kirlionik/yandex-tank:latest
```

All test artifacts you will find at your directory with tank configs.
