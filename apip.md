# Layered security, best practices behind firewall, API security

### Login to API Platform

- Now login to API Platform - Management Portal
- Here is my API (look for CreateServiceOrg-*NN* unique API):

![](images/apip/image010.png)



- Note: a Plan has also been created. APIs are made available to developers through Plans.



### Change API Request Policy

- Click on **API**, then click on **API Implementation** than on **API Request Policy** and then **Edit**

![](images/apip/image020.png)



- Under **API Endpoint URL** enter *organizationNN*; this is the unique suffix that the API will have when deployed to a Gateway

![](images/apip/image030.png)



### Deploy the API to a Gateway

- Now we will deploy the API to a Gateway
  - These can run anywhere – on-premise, in the Oracle cloud, in any other cloud
- Click on **Settings**

![](images/apip/image040.png)



- Click **Deploy API** and click **Deploy**

![](images/apip/image050.png)

- Select **Development Gateway** and **Deploy**


![](images/apip/image060.png)



- The API will get *Active* in a while on **Development Gateway** :

![](images/apip/image070.png)



- Take note of the *Load Balancer URL* information! It should contain the full URL of the Gateway and the unique suffix (relative path) given to the API:

![](images/apip/image071.png)



### Activate API Plan

- Click on **Plans**, then click on particular API and then *three dots* on top left corner and than **Activate**

![](images/apip/image080.png)



### Test the API in Postman

- Now let’s test the API – again in Postman

![](images/apip/image090.png)



- How did I know that I had to add the */organization* suffix? Let’s look at the API definition:

![](images/apip/image100.png)



Our proxy – API Request is /organization**NN**

Our backend Service is https://JAMOIC-oractdemeabdmnative.integration.ocp.oraclecloud.com:443/ic/api/integration/v1/flows/rest/CREATESERVICEORG_**NN**/1.0

Remember the Endpoint for the OIC integration was:

![](images/apip/image105.png)

When we configured the REST-Trigger of the *CreateServiceOrg* orchestration, we defined the *Endpoint's relative resource URI* as */organization*



### Add a Policy

- Add the Traffic Policy by selecting *API Rate Limiting* from *Traffic Management* Policies; Click **Apply**

![](images/apip/image110.png)



- Setup in second page of configuration:
  - **API Rate Limit**: *4*
  - **Time Interval**: *Minute*
- Click **Apply**:

![](images/apip/image120.png)



- The *API Rate Limiting* should appear in *Request* pipeline:

![](images/apip/image130.png)



- **Save**
- Re-deploy to the Gateway
- Test in Postman
  - The 5th request will elicit the following response:

![](images/apip/image140.png)



### Publish to the Developer Portal

- Before we publish, let’s look at the Plan:

![](images/apip/image150.png)



- The API is listed in the plan, but needs to be published to make it active; Click **Publish**

![](images/apip/image160.png)



- It gets marked as *Published*:

![](images/apip/image170.png)



- Now we can publish the plan to the developer portal; Click *Publication* left menu icon:

![](images/apip/image180.png)



- Choose a plan URL containing the **NN** suffix, for example *CreateServiceOrg-NN-Plan*; Click **Save**

![](images/apip/image190.png)



- Click **Publish to Portal**:

![](images/apip/image195.png)



- Once Published, you can unpublish and then republish etc.

![](images/apip/image200.png)



- Let’s now deploy the API to the Developer Portal

![](images/apip/image210.png)



- Choose an API URL containing the NN suffix; Click **Save**

![](images/apip/image220.png)



- Click **Publish to Portal**

![](images/apip/image230.png)



### Check out the API in the Developer Portal

- Login to API Platform - Developer Portal
- Here is the API

![](images/apip/image240.png)



- Click on it:

![](images/apip/image250.png)



- Note the embedded documentation from Apiary; Click **Subscribe** (upper left corner)
- Click on **Continue** to select default plan:

![](images/apip/image260.png)



- Now you should select an application before being able to subscribe:


![](images/apip/image270.png)



APIs are used in the context of an Application, e.g. a mobile app the developer is working on.

- Click *Register Application* Link
  - Enter an **Application Name** using *NN* suffix, for example MobileApplication-*NN*
  - Choose an **Application Type**

![](images/apip/image280.png)



- Click **Save**
- Your application should get pre-selected;
- Note the *Application Key* (copy this for later use)
- Now you can click **Subscribe**:

![](images/apip/image285.png)



- Click **Subscribe**

![](images/apip/image290.png)



- Now the Mobile Application is subscribed to the API:

![](images/apip/image300.png)



### Apply a Security Policy

- Back in the API Platform Management Console:

![](images/apip/image310.png)



- Select **Key Validation** from **Security Policies** List (by clicking **Apply**)
- Configure as follows in the second screen:
  - **Key Delivery Approach**: *Header*
  - **Key Header**: *app-key*
- Click **Apply**:

![](images/apip/image320.png)



- Click **Save**
- Re-deploy the API to the Gateway
- Test in Postman

![](images/apip/image330.png)



- Now add the key to the request (as *app-key* header) and test again:

![](images/apip/image340.png)



- Success!