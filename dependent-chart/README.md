# dependent-chart

An example helm chart which fully depends on a library

To test it first update the dependency
```
helm dependency update
```

Then you can test template it (`ingress.host` is a required value so you need to provide it else you get an according error message)
```
helm install dependenttest --set  ingress.host=local-example.com . --dry-run --debug
```

If everything looks good you can install it:
```
helm install dependenttest --set  ingress.host=local-example.com .
```

Then the application will be reachable per default under your provided ingress domain under the subpath of the chart name `/dependent-chart`

In the example it would be `http://local-example.com/dependent-chart`