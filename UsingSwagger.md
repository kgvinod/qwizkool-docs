## Using swagger-api.yaml

The swagger api yaml file contains the Qwizkool REST API specification. 
This is a 'live' specification, which means it can be updated, tested and can be used to auto-generate API code.

To use the yaml spec:

1. Point the browser to http://swagger.qwizkool.com/
2. The swagger editor will open with 2 vertical panes : the left side shows the yaml code.
3. Paste (replace) the contents of the left pane with contents of [swagger-api.yaml](swagger-api.yaml)
4. The API documentation should now show on the right pane.

You can now view the documentation, and also invoke the methods and test each API and parameter from the documentation pane.

The 'host' attribute and the 'basePath' attribute in swagger-api.yaml specifies the root of the REST endpoint.
For e.g. the default value in swagger-api.yaml is host: vinod.qwizkool.com and basePath: /slim_api. This will set the base path 
to http://vinod.qwizkool.com/slim_api