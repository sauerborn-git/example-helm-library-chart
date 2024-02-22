# example library chart

An example helm library chart containing a couple of named templated to cover the functionality for the three provided application charts.

- The `_helpers.tpl` template is providing some generic template like one grouping together label assignments. It is used in the application chart in the folder `examplechartusingthelibrary`
- The `UI` and `API` folders are providing example named templates to template almost the whole chart for UI and API microservices. It is used in the application chart in the folder `dependent-chart`
- On `_util.yaml` it provides a named template to merge two yaml template specifications. And `overwriteable` folder contains a templated configmap which can be overwritten. It is used in the application chart in the folder `overwrite-dependent-chart`