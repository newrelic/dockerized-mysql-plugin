[![Archived header](https://github.com/newrelic/open-source-office/raw/master/examples/categories/images/Archived.png)](https://github.com/newrelic/open-source-office/blob/master/examples/categories/index.md#archived)

# The New Relic MySQL Plugin

This is the New Relic Plugin for monitoring MySQL databases. It is the same one that can be found in [Plugin Central](https://rpm.newrelic.com/plugins) and on GitHub as [newrelic-platform/newrelic_mysql_java_plugin](https://github.com/newrelic-platform/newrelic_mysql_java_plugin), but packaged as a Docker container image for ease of use!

In order to use the MySQL Plugin, you will need an active New Relic account
and a New Relic license key.

## How to use this image

The MySQL Plugin image is configured by environment variables. These are mandatory:

* `NEW_RELIC_LICENSE_KEY`
* `AGENT_HOST`
* `AGENT_USER`
* `AGENT_PASSWD`

Optionally, you can also set:

* `NEW_RELIC_LOG_LEVEL` (default is `info`)
* `AGENT_NAME` (to change what name the Plugin reports as)
* `AGENT_METRICS` (see [metric.category.json](https://github.com/newrelic-platform/newrelic_mysql_java_plugin/blob/master/config/metric.category.json) for details)

### Example

```shell
$ docker run -d \
  -e NEW_RELIC_LICENSE_KEY=foobarbaz \
  -e AGENT_HOST=your-db-host \
  -e AGENT_USER=newrelic \
  -e AGENT_PASSWD=SuPeRsEcUrE \
  newrelic/mysql-plugin
```

## Additional Configuration

### HTTP Proxy

If you are running your plugin from a machine that runs outbound traffic through a proxy, you can use the following optional configurations:

* `PROXY_HOST` - The proxy host (e.g. webcache.example.com)
* `PROXY_PORT` - The proxy port (e.g. 8080). Defaults to 80 if a proxy_host is set
* `PROXY_USERNAME` - The proxy username
* `PROXY_PASSWORD` - The proxy password

### Monitoring MySQL Replication

To monitor stats like Replication Lag and Relay Log Volume are disabled by default. To monitor MySQL Replication the plugin needs to be told to check those additional metric sets by changing the `AGENT_METRICS` variable. The default is `newrelic,status`.

On your MySQL replicas:
`AGENT_METRICS="newrelic,status,slave"`

On your MySQL master:
`AGENT_METRICS="newrelic,status,master"`


## Getting logs and troubleshooting

To prevent filling up the container filesystem, no logs are written locally inside the container. Instead they are sent to Docker's logging system. By default, the logging level is `info`, however when troubleshooting it may be useful to set `NEW_RELIC_LOG_LEVEL=debug`.

If the plugin is failing to report data, we recommend trying to run it attached to the terminal with `docker run -t` instead of in daemon mode `-d`.

```shell
docker run -t \
  -e NEW_RELIC_LOG_LEVEL=debug \
  -e NEW_RELIC_LICENSE_KEY=foobarbaz \
  -e AGENT_HOST=your-db-host-but-with-a-typo \
  -e AGENT_USER=newrelic \
  -e AGENT_PASSWD=SuPeRsEcUrE \
  newrelic/mysql-plugin
```

## Contributing

You are welcome to send pull requests to us - however, by doing so you agree that you are granting New Relic a non-exclusive, non-revokable, no-cost license to use the code, algorithms, patents, and ideas in that code in our products if we so choose. You also agree the code is provided as-is and you provide no warranties as to its fitness or correctness for any purpose.
