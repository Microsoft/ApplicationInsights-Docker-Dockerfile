This repo is [not currently maintained or supported](https://docs.microsoft.com/en-us/azure/azure-monitor/app/docker) by Microsoft. Check out our official documentation for the latest investments in [container monitoring](https://docs.microsoft.com/en-us/azure/azure-monitor/insights/container-insights-overview).

## Overview

Visual Studio [Application Insights][appinsights-overview] for Docker helps you monitor your containerized applications by collecting telemetry about the performance and activity of your Docker host, Docker containers and the applications running within them.
The Application Insights container talks to the Docker agent and sends telemetry data back to [Application Insights][appinsights-home], providing you with diagnostics and data analysis tools.

## What data will I get for my containerized apps?

#### For applications that are not instrumented with an Application Insights SDK:
* Performance counters with Docker context (Docker host, image and container). In the Application Insights portal, you’ll be able to filter and group the counters by context.
* Container events such as start, stop, kill.
* Container error information.

#### For applications that are instrumented with the [Application Insights SDK for Java][appinsights-java-sdk]:
* All the data mentioned above.
* The Docker context (Docker host, image and container) is added to all telemetry data types collected by the Application Insights SDK (exceptions, http requests, events). This allows you to filter and segment your data by context.

## Supported tags
* [`0.9.2`, _(0.9)_, _(latest)_](https://github.com/kbeaugrand/ApplicationInsights-Docker/tree/0.9.2/Dockerfile)
* [`0.9.1`](https://github.com/kbeaugrand/ApplicationInsights-Docker/tree/0.9.1/Dockerfile)
* [`0.9.0`](https://github.com/kbeaugrand/ApplicationInsights-Docker/tree/0.9.0/Dockerfile)

## Supported platforms
* linux/amd64
* linux/arm64
* linux/386
* linux/arm/v7

## How to use this Image

1.	Obtain the instrumentation key of your Application Insights resource. (Look in the Essentials drop-down.) If you don’t have a resource, [create a new one][appinsights-create-resource].
2.	Run the following command, replacing %app_ikey% with your instrumentation key:
docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=%app_ikey%
3.	If your application is instrumented with the Application Insights SDK for Java, add the following line into the ApplicationInsights.xml file in your project, under the <TelemetryInitializers> element:
<Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/>

Note: Only a single container is required per Docker host. If your application is deployed on multiple Docker hosts, then create an instance of this image on every host.

## How to see Docker data
To get full Docker experience in [Application Insights portal][azure-portal], please read [Monitor Docker applications in Application Insights][appinsights-docker-article]

[appinsights-home]: https://azure.microsoft.com/en-us/services/application-insights/
[appinsights-overview]: https://azure.microsoft.com/en-us/documentation/articles/app-insights-overview/
[appinsights-java-sdk]: https://azure.microsoft.com/en-us/documentation/articles/app-insights-java-get-started/
[appinsights-create-resource]: https://azure.microsoft.com/documentation/articles/app-insights-create-new-resource/
[azure-portal]: https://portal.azure.com/
[appinsights-docker-article]: https://azure.microsoft.com/en-us/documentation/articles/app-insights-docker/
