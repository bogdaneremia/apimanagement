# Layered security, best practices behind firewall, API security

### Login to API Platform

- Now login to API Platform
  - < apip url !!>/apiplatform/apis
  - Please note that the username is different than the one used by OIC (same password)
- Here is my API:

![](images/apip/image010.png)



- Note: a Plan has also been created. APIs are made available to developers through
  Plans.



### Change API Request Policy

- Click on **API**, then click on **API Implementation** than on **API Request Policy** and then **Edit**

![](images/apip/image020.png)



- Under **API Request URL** enter *OrganizationNN*

![](images/apip/image030.png)



### Deploy the API to a Gateway

- Now we will deploy the API to a Gateway
  - These can run anywhere – on-premise, in the Oracle cloud, in any other cloud
- Click on **Settings**

![](images/apip/image040.png)



- Click **Deploy API** and click **Deploy**

![](images/apip/image050.png)

- Select **Development Gateway**


![](images/apip/image060.png)



- The API will get *Active* on **Development Gateway** :

![](images/apip/image070.png)



### Activate API Plan

- Click on **Plans**, then click on particular API and then *three dots* on top left corner
  and than **activate**

![](images/apip/image080.png)



### Test the API in Postman

- Now let’s test the API – again in Postman - !!!

![](images/apip/image090.png)



- How did I know that I had to add the */createOrg* suffix? Let’s look at the API definition:

![](images/apip/image100.png)



Our proxy – API Request is /organization

Our backend Service is https://OIC-gse00014400.integration.ocp.oraclecloud.com:443/ic/api/integration/v1/flows/rest/CREATESERVICEORG_01/1.0

Remember the Endpoint for the OIC integration was:

![](images/apip/image105.png)



### Add a Policy

- Add the Traffic Policy by selecting *API Rate Limiting* from *Traffic Management* Policies:

![](images/apip/image110.png)



- Setup:
  - **API Rate Limit**: *4*
  - **Time Interval**: *Minute*
- Click **Apply**:

![](images/apip/image120.png)



- The *API Rate Limiting* should appear in *Request* pipeline:

![](images/apip/image130.png)



- Re-deploy to the Gateway
- Test in Postman
  - The 5th request will elicit the following response:

![](images/apip/image140.png)



### Publish to the Developer Portal

- Before we publish, let’s look at the Plan:

![](images/apip/image150.png)



- The API is listed in the plan, but needs to be published to make it active

![](images/apip/image160.png)



- It gets marked as *Published*:

![](images/apip/image170.png)



- Now we can publish the plan to the developer portal:

![](images/apip/image180.png)



- Choose a plan URL containing the **NN** suffix:

![](images/apip/image190.png)



- Once Published, you can unpublish, republish etc.

![](images/apip/image200.png)



- Let’s now deploy the API to the Developer Portal

![](images/apip/image210.png)



- Choose an API URL containing the NN suffix:

![](images/apip/image220.png)



- Click **Publish to Portal**

![](images/apip/image230.png)



### Check out the API in the Developer Portal

- !! Login URL is https://aapiad2-gse00014400.apiplatform.ocp.oraclecloud.com/developers
- Here is the API

![](images/apip/image240.png)



- Click on it:

![](images/apip/image250.png)



- Note the embedded documentation from Apiary.
- Click on **Select Plan**:

![](images/apip/image260.png)



Click on **Subscribe**:

![](images/apip/image270.png)



APIs are used in the context of an Application, e.g. a mobile app the developer is working on.

- Click Create New Application
  - Enter your app name etc.

![](images/apip/image280.png)



- Note the **Application Key** (copy this for later use)
- Click **Subscribe**

![](images/apip/image290.png)



- !! XXXX

![](images/apip/image300.png)



### Apply a Security Policy

- Back in the API Platform Management Console:

![](images/apip/image310.png)



- Select **Key Validation** from **Security Policies** List
- Configure as follows:
  - **Key Delivery Approach**: *Header*
  - **Key Header**: *app-key*
- Click **Apply**:

![](images/apip/image320.png)



- Re-deploy the API to the Gateway
- Test in Postman

![](images/apip/image330.png)



- Now add the key to the request
- !! XX