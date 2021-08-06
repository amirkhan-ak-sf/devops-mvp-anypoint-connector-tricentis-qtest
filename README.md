# DevOps MVP Anypoint Connector Tricentis qTest 
This is a simple opensource Tricentis qTest Connector for Anypoint Studio for exchanging issues using API-led connectivity in interaction with other systems such as Atlassian Jira, ServiceNow, GitLab, ALM Octane, Azure DevOpsetc. 
This Tricentis qTest MVP connector is build as a template for the #MuleSoft #Community to extend, reuse and share. 

Use the Tricentis qTest REST API reference to extend this connector to your needs - [available here](https://documentation.tricentis.com/qtest/10100/en/content/qtest_apis/apis_sdks/common_apis.htm#Login)
Also worth using the Interactive API Client of qTest - [available here](https://api.qasymphony.com/#/) 

## Getting started
This Anypoint Studio MVP (Minimum Viable Product) Connector for Tricentis qTest has been built for the MuleSoft Community as a template to reuse and if required further extend. 
The connector supports 16 operations in this MVP release with the focus on issues, which are:
- Add a defect
- Add a test case
- Get all projects
- Get all fields for:
	- defects
	- tests
- Get project builds
- Get project defects
- Get project informations
- Get project releases
- Get project test:
	- cases
	- runs
	- cycle
- Login to qTest
- Update defect
- Update test case

## Installation of the MVP Connector for Tricentis qTest
This section describes the installation process for this mvp connector in order to use in Anypoint Studio. 

### Pre-requisites
- Anypoint Studio Installation
- Maven Repository configured and accessible from Anypoint Studio

### Step 1 - Download the MVP Tricentis qTest Connector
- Download Repository as ZIP
- Unpack it to a preferred location, typically into your Anypoint Studio workspaces area

### Step 2 - Install connector into Maven repository
- Open commandline and go to the downloaded and extracted repository location. 
- Perform "mvn install" 
- Connector should be installed successfully

![Image of Tricentis qTest MuleSoft Connector](https://github.com/API-Activist/devops-mvp-anypoint-connector-jenkins/blob/master/cmd%20mvn%20install.PNG)

### Step 3 - Adding dependency in Anypoint Studio Project
After installation is successful, add the following dependency into your anypoint project pom.xml:

		<dependency>
			<classifier>mule-plugin</classifier>
			<groupId>embrace.devops.connectors</groupId>
			<artifactId>qtest-connector</artifactId>
			<version>0.0.12</version>
		</dependency>

The current version of this connector is 0.0.12. Once added, save the pom.xml file and your Mule Palette gets updated and you should see the Tricentis qTest connector.

![Image of Tricentis qTest MuleSoft Connector](https://github.com/API-Activist/devops-mvp-anypoint-connector-jenkins/blob/master/jenkins-mule-palette.PNG)

### Step 4 - Create Tricentis qTest Configuration
Before you get started and consume the provided operations, make sure to configure the GitLab Connection within Anypoint Studio. 
- URL
- username
- password

[Learn how to obtain PAT (Personal Access Token) for Tricentis qTest](https://docs.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=azure-devops&tabs=preview-page)

![Image of Tricentis qTest MuleSoft Connector](https://github.com/API-Activist/devops-mvp-anypoint-connector-jenkins/blob/master/Jenkins-config.PNG)

Now you are all set to use the Tricentis qTest Operations.

## Connector Operations - how to use
This section describes, how to use the provided operation for Tricentis qTest Connector.

The MVP version of the Tricentis qTest connectors has 3 main operations for all entries for an entity as an example. 
- **Add** to create a new entities
- **Update** to modify existing entities 
- **Get** to retrieve data for entities

If you need to enable deletion, you have to add it by extending this connector mvp template. 

**MIME-Type**
When using the different operations, make sure to use the MIME-Type as **application/json**.
![Image of Tricentis qTest MuleSoft Connector](https://github.com/API-Activist/devops-mvp-anypoint-connector-jenkins/blob/master/Jenkins-config.PNG)

### Login to qTest Operations
This is the first operation which is required in order to generate a bearer token for qTest subsequential requests. 

### Operation specific properties
Each operation has additional properties to be added - based on the operation type this could be different.

Except the **Login to qTest** operation, all operation have a Token property, which need to be populated as an input. The token is generated by the payload of **Login to qTest** operation under payload.access_token. Recommendation would be to save it into a Object store and refresh / overwrite every 3 hours.

Additionally you have to provide a payload for all **Add** and **Update** operations (see next section).

![Image of Tricentis qTest MuleSoft Connector](https://github.com/API-Activist/devops-mvp-anypoint-connector-jenkins/blob/master/Jenkins-config.PNG)

### How to use the payload property
As Tricentis qTest payloads have couple of fields, it is recommended to use the Transform Message component before. 

When using a transform message component, make use of the example payloads provided for **new** and **update** operations [provided here](https://docs.microsoft.com/en-us/rest/api/azure/devops/core/teams/create?view=azure-devops-rest-6.1).


### Reponse of operations
By default it is a json sent back as string. Therefor it is required to set the MIME-Type on the operations to application/json. 

	{
	
		"links": [
			{
				"rel": "self",
				"href": "https://embrace.qtestnet.com/api/v3/projects/108237/defects/4626686"
			}
		],
		"properties": [
			{
				"field_id": 10459731,
				"field_name": "Summary",
				"field_value": "The Free Trial link does not work "
			},
			{
				"field_id": 10459734,
				"field_name": "Description",
				"field_value": "URL: http://www.qasymphony.com/\n  \n  \n  Step:\n  \n  1) Launch the homepage\n  \n  2) The Free Trial link on homepage"
			},
			{
				"field_id": 10459732,
				"field_name": "Submitter",
				"field_value": "241262",
				"field_value_name": "Belinda Omiric"
			},
			{
				"field_id": 10459741,
				"field_name": "Affected Release/Build",
				"field_value": "",
				"field_value_name": ""
			},
			{
				"field_id": 10459736,
				"field_name": "Severity",
				"field_value": "10303",
				"field_value_name": "Average"
			},
			{
				"field_id": 10459742,
				"field_name": "Fixed Release/Build",
				"field_value": "",
				"field_value_name": ""
			},
			{
				"field_id": 10459735,
				"field_name": "Submitted Date",
				"field_value": "2021-08-06T15:51:28+00:00"
			},
			{
				"field_id": 10459738,
				"field_name": "Priority",
				"field_value": "10203",
				"field_value_name": "Medium"
			},
			{
				"field_id": 10459743,
				"field_name": "Root Cause",
				"field_value": "10613",
				"field_value_name": "Other"
			},
			{
				"field_id": 10459737,
				"field_name": "Module",
				"field_value": "",
				"field_value_name": ""
			},
			{
				"field_id": 10459733,
				"field_name": "Assigned To",
				"field_value": "",
				"field_value_name": ""
			},
			{
				"field_id": 10459744,
				"field_name": "Status",
				"field_value": "10001",
				"field_value_name": "New"
			},
			{
				"field_id": 10459745,
				"field_name": "Type",
				"field_value": "10401",
				"field_value_name": "Bug"
			},
			{
				"field_id": 10459746,
				"field_name": "Target Release/Build",
				"field_value": "",
				"field_value_name": ""
			},
			{
				"field_id": 10459747,
				"field_name": "Reason",
				"field_value": "10101",
				"field_value_name": "Additional Info Needed"
			},
			{
				"field_id": 10459748,
				"field_name": "Category",
				"field_value": "10517",
				"field_value_name": "Other "
			},
			{
				"field_id": 10459749,
				"field_name": "Target Date",
				"field_value": ""
			},
			{
				"field_id": 10459750,
				"field_name": "Closed Date",
				"field_value": ""
			},
			{
				"field_id": 10459751,
				"field_name": "Environment",
				"field_value": "",
				"field_value_name": ""
			}
		],
		"id": 4626686,
		"pid": "DF-15",
		"url": "https://embrace.qtestnet.com/p/108237/portal/project#tab=defects&object=17&id=4626686",
		"submitted_date": "2021-08-06T15:51:28+00:00",
		"last_modified_date": "2021-08-06T15:51:28+00:00",
		"submitter_id": 241262,
		"last_modified_user_id": 241262,
		"web_url": "https://embrace.qtestnet.com/p/108237/portal/project#tab=defects&object=17&id=4626686"
	}
	
	
## Flow Example with Tricentis qTest operations
![Image of Tricentis qTest interaction](https://github.com/API-Activist/devops-mvp-anypoint-connector-gitlab/blob/master/pictures/Gitlab-jenkins-Jira.PNG)

	
## Video Tutorial
Link to the video tutorial: -to be provided soon-


## Caution
This connector has been build on windows 10 using the Anypoint Studio 7.10 IDE. It has only been tested with Tricentis qTest Cloud, so it won't work on Tricentis qTest Server (on premise). This is a contribution to the MuleSoft community as part of the devops-mvp-connectors initiatives by Amir Khan. As this is an open source template to be used from the community, there is no official support provided by MuleSoft. Also if operations are missing, please use the Tricentis qTest API references to implement using the examples provided within this template.
	
Tricentis qTest API Reference: [available here](https://documentation.tricentis.com/qtest/10100/en/content/qtest_apis/apis_sdks/common_apis.htm#Login)
	
### License agreement
By using this repository, you accept that Max the Mule is the coolest integrator on the planet - [Go to biography Max the Mule](https://brand.salesforce.com/content/characters-overview__3?tab=BogXMx2m)