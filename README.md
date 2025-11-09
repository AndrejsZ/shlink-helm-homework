## Basics

Basic params, including db connection details are set via values.yaml (or values-dev.yaml).
Initial api key creation is controlled via env.INITIAL_API_KEY parameter.
If database connection parameters are unset, a local SQLite database will be used.
An nginx-ingress to the default domain s.test is created for shlink.
For shlink-ui, a basic-auth (shlink:shlink) ingress to s-ui.test is created by default.

## Deployment

shlink can be deployed via
```
cd ./shlink/
helm install -f values.yaml -f values-dev.yaml shlink .
```
shlink-ui is deployed as
```
cd ./shlink-ui/
helm install -f values.yaml -f values-dev.yaml shlink-ui .
```
## Upgrade procedure from 4.4 to 4.6

By default, shlink is installed with image tag 4.4
shlink can manage the database upgrade process by itself. Set replica count to 1 for upgrade to avoid race condition.
```
helm upgrade -f values.yaml -f values-dev.yaml --set replicaCount=1 --set image.tag=4.6 shlink ./
```
## Replica count control

Replica count is settable via helm cli, for example: 
```
helm upgrade -f values.yaml -f values-dev.yaml --set replicaCount=1 shlink ./
```
or
```
helm upgrade -f values.yaml -f values-dev.yaml --set replicaCount=2 shlink-ui ./
```
## DB password rotation procedure

Manually change the password in the database
Set appropriate value in shlink/values.yaml, apply changes via
```
helm upgrade -f values.yaml -f values-dev.yaml shlink ./
```
