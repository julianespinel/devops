# Nodes

We will monitor the resource consumption of a node (machine) by using:

1. Collectd
1. InfluxDB
1. Grafana

To ease the deployment process we will use docker to deploy InfluxDB and Grafana.

## Installation

In order to configure the tools needed to monitor a node please follow these steps:

1. Install collectd in the node you want to monitor: `sudo apt-get install collectd`
1. Configure collectd to send monitor data to InfluxDB.<br>
   In the collectd config file: `/etc/collectd/collectd.conf`<br>
   1. Remove the `#` at the start of the line: `LoadPlugin network`<br>
   1. Add the following lines:
      ```
      <Plugin network>
        Server "127.0.0.1" "25826"
      </Plugin>
      ```
1. Restart collectd after you have configured it: `sudo service collecd restart`
1. Start InfluxDB and Grafana with docker: `docker-compose up -d`

**Check the installation was successful:**

1. InfluxDB web interface: http://localhost:8083/
1. Grafana: http://localhost:3000/.

You should be able to login to Grafana with user: `admin` and password: `admin`

## Next steps

After the installation is complete please perform the following steps:

### Grafana

1. Change the `admin` default password in Grafana.
1. Add InfluxDB as data source to Grafana.<br>
   See: http://docs.grafana.org/datasources/influxdb/
   1. The URL should be: `http://localhost:8086/`
   1. The database name should be: `collectddb`
1. Create a new dashboard with the graphs and metrics you need.<br>
   See: http://docs.grafana.org/guides/getting_started/
1. You could also download community dashboards from the Grafana website and import them into your Grafana instance: https://grafana.net/dashboards?dataSource=influxdb&collector=collectd

### Collectd

1. Configure additional collectd plugins you may want to use.<br>
   See: https://collectd.org/wiki/index.php/First_steps#Configuration
1. Do not forget to restart collectd after changing its Configuration:<br>
   `sudo service collecd restart`

### InfluxDB

Check what measurements is collecd storing in InfluxDB:

1. Go to the InfluxDB web interface: http://localhost:8083/
1. On the top right, select the database named `collectddb`
1. Type `SHOW MEASUREMENTS` in the Query bar and hit enter.
