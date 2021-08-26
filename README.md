# My Driving Team APIs

The DevOps open hack event is designed to foster learning via implementing DevOps practices with a series of challenges.

## Architecture

The application used for this event is a heavily modified and recreated version of the original [My Driving application](https://github.com/Azure-Samples/MyDriving).

The team environment consists of the following:

* Azure App Service for Linux which has four APIs deployed:

  * POI (Trip Points of Interest) - CRUD API written in .Net Core 3.1 for points of interest on trips
  * Trips - CRUD open API written in golang 1.11 for trips connected to the client application
  * UserProfile - CRUD open API written in Node.JS for the users of the client application
    > Note:PATCH/POST operations not functional
  * User-Java - API written in Java with POST and PATCH routes plus swagger docs routes for the users of the client application.
* Mobile Apps - for iOS and Android which will display driving trip data

## Getting Started

To understand each of the components above in more detail, please visit the readme files inside the root folder of each corresponding part of the application.

### Prerequisites

It is useful but not required to have a basic knowledge of the following topics:

* Azure App Services
* Azure Container Registry and Docker
* GitHub, Azure DevOps (formally VSTS) or Jenkins

## Resources

The provisioning of this environment for proctors can be found in the [DevOps Openhack Proctor](https://github.com/Azure-Samples/openhack-devops-proctor) Github repository.
> **Note**: During the Dry Run relevant code can be found in the **openhack_refresh** branch. Post Dry Run these changes will be committed to master.


## Useful tips
 * Setting up the Azure Credential for the GitHub action can be done with the following command and the output stored as a repository secret:
   ```
   az ad sp create-for-rbac --name "GHActionSP" --role contributor \
                            --scopes /subscriptions/69ed429c-d95f-44f7-9c92-3d4209b3d042/resourceGroups/openhack4nl2avg0rg \
                            --sdk-auth
   ```       
   
 * Web Applications in Azure support a health check URL.   Each API has a health check endpoint.   Specifying the health check allows deployment slot swaps to occur only when the    staging slot is healthy.
   ```
   az webapp config set -g <groupName> -n <web name>  --generic-configurations '{"healthCheckPath": "/api/health/"}'
   ```
