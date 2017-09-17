# Grafana Dashboards for croit
Grafana dashboards to monitor Ceph clusters deployed with croit.
These dashboards use the automatically deployed croit Graphite instance and monitoring scripts.

## Setting up Grafana
The easiest way to install Grafana is using Docker.
Use the following command when deploying on the same server as the croit application:

```
sudo docker run --net=host -d --name=grafana -e "GF_SECURITY_ADMIN_PASSWORD=<set-grafana-password-here>" grafana/grafana
```
Replace the password for the initial Grafana admin user. See [Grafana documentation](http://docs.grafana.org/installation/docker/) for further options.


You can also use your existing Grafana instance, these dashboards require Grafana 4.5 or later and access to port 23647 of the croit management server.

## Adding a data source
Add a data source with the following options:

* Name: croit
* Type: graphite
* URL: http://localhost:23647 (adjust when not running on the same node)
* Access: Proxy
* Auth: Basic Auth, With Credentials
* User: graphite
* Password: your croit installation's graphite password

You can also add a Graphite user to the file `/config/.htpasswd-graphite` in the croit Docker container.

## Import the Dashboards
Select Dashboards -> Import from the Grafana main menu.

## Configure Alerts
Add a notification channel to Grafana, see [Grafana Documentation](http://docs.grafana.org/alerting/notifications/) for details.

You can now edit Graphs in the dashboards and add alerts.
Our dashboard comes with preconfigured alerts on the OSD state and operation latency, adjust them to fit your needs.

