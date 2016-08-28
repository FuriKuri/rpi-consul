# Consul Agent in Docker

For more information see [Consul](http://www.consul.io/).

* `0.6.4 (latest)`
* `0.6.4-alpine`
* `0.7.0-rc1`
* `0.7.0-rc1-alpine`

## Getting the container

	$ docker pull furikuri/rpi-consul

## How to run

	$ docker run -p 8400:8400 -p 8500:8500 -p 8600:53/udp -h node1 furikuri/rpi-consul


The [Web UI](http://www.consul.io/intro/getting-started/ui.html) is enabled by default and can be accessed over:

	http://<docker-host-ip>:8500/ui

Node can be requested by:

	$ curl <docker-host-ip>:8500/v1/catalog/nodes

## Configuration
The following configuration will be loaded per default:

	{
		"data_dir": "/data",
		"ui_dir": "/ui",
		"client_addr": "0.0.0.0",
		"ports": {
			"dns": 53
		},
		"recursor": "8.8.8.8",
		"disable_update_check": true,
	    "bootstrap": true,
	    "server": true,
	    "leave_on_terminate": true,
	    "dns_config": {
	        "allow_stale": true,
	        "max_stale": "1s"
	    }
	}

If you want to use your own flag, just override them:

	$ docker run -p 8400:8400 -p 8500:8500 -p 8600:53/udp -h node1 furikuri/rpi-consul -server -bootstrap -bind 172.17.0.2

## License

MIT
