# deployment-manifest
The Deployment Manifest is a declarative description of how a collection of software products should be deployed into an environment. Among other logic, it contains information about the order in which products need to be deployed. An example Deployment Manifest can be found at [manifest.yaml](manifest.yaml).

## Instructions
In a technology of your choosing:
* Create an app that reads [manifest.yaml](manifest.yaml) (or [manifest.json](manifest.json) if you prefer) and prints out an ordered list of product ids
* The order that the products should be printed should adhere to the following rules:
  * If a product contains a depends_on array, products that it depends on should appear before it in the list
  * Otherwise the order can be arbitrary
* If there is a circular dependency, the app should report an appropriate error message

NB: Feel free to represent the data in `manifest.yaml` as a code object if you wish, it is more important to have a functional algorithm than to be able to parse YAML)

### Example 1
Manifest.yaml:
```yaml
products:
  - id: 'A'
    depends_on:
      - 'B'
  - id: 'B'
```
Output:
```
Deploy Product: B
Deploy Product: A
```

### Example 2
Manifest.yaml:
```yaml
products:
  - id: 'A'
    depends_on:
      - 'B'
  - id: 'B'
    depends_on:
      - 'A'
```
The above manifest contains a circular dependency (A depends on B and B depends on A). The app should report an appropriate error.
