# Invoke-RackAPI

This is a powershell tool built to automate large portions of working with the RACK API leaving you to focus on the objects you want to work with. It works by checking your Powershell Session for an Auth Token and Service Catalog. If it can't find either, it will prompt you for api credentials which it will use to generate a Token that gets stored in your Powershell session. If it does find a token, it will automatically validate your token and prompt you if your token is expired or going to expire in the next 5 minutes.

Usage is fairly simple is flexible enough to allow you to work with most parts of the Rackspace API:

```Powershell
Invoke-RackAPI -cloudRegion ORD -cloudService cloudServersOpenStack -filter /servers/detail
```

After prompting you for API Credentials, it will return something like:
>servers
>-------
>{@{status=ACTIVE;...

So let's go over the parameters this function will accept:

- cloudRegion = ("DFW","ORD","SYD","IAD","HKG") - This defines the region you're working in. This parameter is a Validate Set meaning it will check input and match it against the predefined list.
- cloudService = ("cloudFilesCDN","cloudFiles","cloudBlockStorage","cloudImages","cloudQueues","cloudBigData","cloudOrchestration","cloudServersOpenStack","autoscale","cloudDatabases","cloudBackup","cloudNetworks","cloudMetrics","cloudLoadBalancers","cloudFeeds","cloudMonitoring","cloudDNS","rackCDN")
	Another Validate Set parameter that defines the Rackspace API space, or product you are working with. 
- filter = This paramter is a partial URL of the service you're working with; the rest of the URL is built with the paramters provided above. You can search through the [Rackspace Docs](https://docs.rackspace.com), and please note where the docs show /v1 or /v2 or they request the account ID, those portions are already handled by the module itself. So under the list volumes API, it says you'll need "/v1/{tenant_id}/volumes" but with this module you can leave off the /v1/{tenant_id} and just use /volumes.
- requestType = ("Get","Post","Put","Delete") - This is set to Get by default, but ultimately you'll use it to indicate what type of API call you're making, GET to retrieve information, POST to create something, PUT to update, and DELETE to delete.
- body = This parameter is not required in most GET requests, however if you are making say a new load balancer, you'll need it. It accepts a hashtable which you can build inline, or create a separate variable and pass that variable in to the function call.

##Installing the module

So installing this module is pretty simple. Download the psm1 file from here, and create a folder called Invoke-RackAPI in one of your PSModules path, and drop the psm1 in that folder. If you don't know where your PSModules path is, run $env:PSModulePath from Powershell and use one of the paths it spits out.

That's all for now, feel free to create issues for feedback, bugs, or feature requests.