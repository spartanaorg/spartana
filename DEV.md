# Development with Spartana

Checkout `spartanaorg/grafana`, then for Debian (stable) for the frontend stuff:

~~~
sudo apt-get install node-load-grunt-tasks grunt yarnpkg
yarnpkg install # - picks up local package.json
~~~

Then to build the JS:

~~~
yarnpkg run build
~~~

Not fully sure if `node-load-grunt-tasks` is needed here, though.

# Golang

For go:

~~~
make build-go
~~~
Will build the server the the `grafana-cli` (which we also don't need).

# Tessting

Testing with dashboards that are provisioned:

Add `conf/provisioning/dashboards/dashboards.yaml` with
~~~ yaml
apiVersion: 1

providers:
 - name: 'default'
   orgId: 0
   folder: ''
   folderUid: ''
   type: file
   options:
     path: /home/miek/tmp/grafana
~~~
Adjust the path to your own preference.

Then install prometheus and add a data source:

~~~
sudo apt-get install prometheus
~~~

And create a `conf/provisioning/datasources/datasources.yaml`, with
~~~ yaml
apiVersion: 1

datasources:
- name: prometheus
  orgId: 0
  type: prometheus
  access: direct
  isDefault: true
  url: http://localhost:9090
~~~

Now dashboards put in the above path should be picked up automatically.

# Testing Grafana

Use a *private* session in your browser, otherwise auth cookies from earlier tests will be picked up
and used (you can clear those of course).
