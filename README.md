# ComponentSummary
This CA PC app displays a trend view with the metric summary across all relevant components.
The metric is configurable. The app can run in a device context or dashboard view.

## Use Case
Metrics with average rollup condition should be displayed as summary trend on a device. For example,
the total number of connected users across all wireless access points.

## Example
![Component Summary App View Image]
https://github.com/CA-PM/ComponentSummary/images/appview.png

## Approach
CA PC app with following characteristics
* Metric family, metric name and metric label are configurable
* uses odata query to retrieve aggregated metric
* Uses nvd3 graphics library
* Can live on device or dashboard context
* uses as-polled data resolution for time ranges below 7days, and hourly resolution above

## Installation
The ZIP archive and can be installed through CA PM 3.2+ App Deployment function.
1. Store CompSummary.zip on your workstation
2. Under CA PC Administration -> App Deployment, select the zip archive and install it.
3. Navigate e.g. to a device context page.
4. Add a context tab, name it e.g. Connection Summary
5. In page editor, select single column layout and create an App View (under External Links)
and select "Component Summary" in the app drop down.
6. Configure the view and adapt the metric family/metric name and label to match your requirements

## App View Parameters
### Default:
URL=/pc/apps/user/CompSummary/compSummary.html?id={ItemIdDA}&ItemType={ItemType}&startTi
me={TimeStartUTC}&endTime={TimeEndUTC}&maxRows=1000&metricFamily=mobilewlanapmfs&metric
Name=im_UsersConnectedPerAP&metricLabel=Users Connected
which consists of
* id={ItemIdDA} page context (device OR group item ID DA)
* ItemType={ItemType} page context type
* startTime={TimeStartUTC} page context (start time)
* endTime={TimeEndUTC} page context (end time)
* maxRows=1000 query limit: the number of rows retrieved
* metricFamily=mobilewlanapmfs metric family name (odata format)
* metricName=im_UsersConnectedPerAP metric name (odata format)
* metricLabel=Users Connected metric label
Height: 400

### Other example: How to show the summary trend for Bits Per Second Metric
The URL will look as follows:
URL=/pc/apps/user/CompSummary/compSummary.html?id={ItemIdDA}&ItemType={ItemType}&startTi
me={TimeStartUTC}&endTime={TimeEndUTC}&maxRows=1000&metricFamily=portmfs&metricName=im
_BitsPerSecond&metricLabel=Bits Per Second

## Notes
* The app is provided as an example and no warranties are provided or made
* The app uses nvd3 lineChart and is derived from simpleTrend sample app
* To verify syntax of metric family and metric name, use the OpenAPI query builder:
http://DA-HOST:8581/odataquery/index.html
