# overwrite dependent chart

An example helm chart containing two things:
- A Deployment which includes a named template from a helm library chart.
- A ConfigMap it includes form the library chart and overwrites some values into it

To test it first update the dependency
```
helm dependency update
```

Then you can test template it (`ingress.host` is a required value so you need to provide it else you get an according error message)
```
helm install overwrite-test .  --set ingress.host=local-example.com --dry-run --debug
```

If everything looks good you can install it:
```
helm install overwrite-test . --set ingress.host=local-example.com
```
Then the application will be reachable per default under your provided ingress domain under the subpath of the chart name `/overwrite-dependent-chart`

In the example it would be `http://local-example.com/overwrite-dependent-chart`

And you can also check the ConfigMap, describing it will show the overwritten annotation:
```
kubectl describe  configmap overwrite-dependent-chart-cm
Name:         overwrite-dependent-chart-cm
Namespace:    default
Labels:       app.kubernetes.io/managed-by=Helm
Annotations:  meta.helm.sh/release-name: overwrite-test
              meta.helm.sh/release-namespace: default
              overwritten: true

Data
====
index.html:
----
<!DOCTYPE html>
<html>
<head>
<title>Welcome to Default ConfigMap nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to Default ConfigMap nginx!</h1>
</body>
</html>

BinaryData
====
```
