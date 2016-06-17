# The New Relic MySQL Plugin

This is the New Relic Plugin for monitoring MySQL databases. It is the same one that can be found in [Plugin Central](https://rpm.newrelic.com/plugins).

# How to use this image

In order to function, the plugin needs a few environment variables set:

* `NEW_RELIC_LICENSE_KEY`
* `AGENT_HOST`
* `AGENT_USER`
* `AGENT_PASSWD`

Optionally, you can also set:

* `NEW_RELIC_LOG_LEVEL`
* `AGENT_NAME`
* `AGENT_METRICS` (see [metric.category.json](https://github.com/newrelic-platform/newrelic_mysql_java_plugin/blob/master/config/metric.category.json) for details)

## Example

```shell
$ docker run -d \
  -e NEW_RELIC_LICENSE_KEY=foobarbaz \
  -e AGENT_HOST=your-db-host \
  -e AGENT_USER=newrelic \
  -e AGENT_PASSWD=SuPeRsEcUrE \
  newrelic/mysql-plugin
```
