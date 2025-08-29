# ServiceNow Integration with
AppXConnect CTI Adapter
for Genesys Cloud
this is the telephony soltion developed by AppxConnect to connect to Genesis Cloud

# Introduction
ServiceNow (often abbreviated as SNOW) requires a custom app to be created inside your production instance. This guide outlines the steps needed to set up the application, highlighting important prerequisites and setup instructions.

# Prerequisites
Before beginning this exercise, please ensure the following:

1. CTI Softphone Plugin Installed

2. Log in to your ServiceNow Instance.

3. Navigate to the 'All Applications' page after a successful login.

4. Use the search bar to search for "CTI Softphone" and click the 'Install' button if the plugin is not already installed.
Refer to the image below for guidance.


Ensure the user performing this activity has the necessary permissions and access rights.

Before beginning, please confirm the user performing this activity meets all required permissions and setup criteria.


Which screenshots or UI steps would best illustrate installing the CTI Softphone plugin
How might I explain role and permission requirements for the user performing this task
What troubleshooting tips should I add if the CTI Softphone install button is missing

4. Now navigate to 'App Engine Studio' by searching for the term, 'App Engine Studio' from
within the 'Filter Navigation' on the top left as shown below:
Creating an Application
5. Now, we will create our custom application, for this, we will click on the 'Create app' button
on the top right of the page.
6. In the New App Creation dialogue that opens up, put the name as AppxConnectCTI, enter
description and click on Continue.

Note: Please make a note of the Scope field value at this point and do not change it. If you
do have to change it, just remember to use it accordingly in the oncoming steps.

7. In the next screen, create a role 'appx_cti_user' which will be assigned to users who will
be using the CTI. This role will allow the user to execute client scripts created under the
application scope.

8. In the next screen, click on 'Go to your Dashboard'.

9.After app is created, go to left nava nd type- My Company Applications. opne recently created application by clicking on 'Edit in Studio'
10.At this point, you would be back to Application Manager page. If not, navigate to it manually and there you should be able to see your newly created app
<img width="967" height="312" alt="image" src="https://github.com/user-attachments/assets/30b227fb-cf95-4be8-a014-c3e4ec7422a4" />

If you're still unable to see you newly created app in the Application Manager, refresh
the Browser page or try clearing the cache.


# Customizing the Newly Created App
After your shiny new application has been created, it is time to customize it so that it becomes
production ready. Follow the steps as below:

**Script Includes**
1. Click on the Edit in Studio button right next to your newly created application. This will
take you to the Application Studio.
2. When the Application Studio Opens, click on Create Application File > Script
Include > Create.
3. In the New Script Include page that opens up, type the Name as 'AppxGlideData' and
click anywhere outside the Name field. You will find that some additional fields such as 'API
Name', 'Application' have been prefilled.
Also, ensure that the Client Callable and Active flags are ticked and the correct application
is set under the Application field.
4. At this point, if you're already a customer, you would've received a couple of files from us.
One of those files is a AppxGlideData.txt file. Simply copy / paste the contents of the
AppXConnect provided text file into the Script Content area within the ServiceNow page so
that it looks like below:
<img width="1055" height="475" alt="image" src="https://github.com/user-attachments/assets/6a69a16b-a8f4-4632-b493-b1ebfde05131" />

5. Repeat the above process and create a new Script Include named ‘SNAppxInteractionData’. You might find that at this point, ServiceNow might prompt you to choose a User Role for this Client Callable Script for Access Control purposes. Best practice dictates the a specific role for the Agents who would be using the CTI is created and filled in here. For the purpose of this guide, we will be using the admin user role.
<img width="969" height="443" alt="image" src="https://github.com/user-attachments/assets/66c6aad4-745b-493b-8b30-35bef83901cd" />


**UI Scripts**
1. As in the case of a Script Include, this time we would be creating some UI Scripts. For this,
follow the same process as before by navigating to Create Application File > UI Script >
Create.
2. Name this new UI Script as 'servicenow_adapter'. As before, click anywhere outside the
Name field and you will find that some additional fields such as 'API Name', 'Application' have
been prefilled.
Ensure that the Active flag is Ticked.  At this point, hold off copying anything into the Script
Content area.
3. Now we will verify the Application Scope value and note it down again. For this, go to File
(top left of the page) > Settings.
The value in the above screenshot may or may not be the same as in your environment.
Please copy and keep this value safely before proceeding from this point.
<img width="970" height="536" alt="image" src="https://github.com/user-attachments/assets/bcafca0b-06cb-449f-b6b1-29bd148ed448" />

<img width="950" height="537" alt="image" src="https://github.com/user-attachments/assets/37bafaad-607d-408c-a9d8-20d65afa0e89" />

5. Open the servicenow_adapter.txt file in your favourite text editor and replace all
occurrences of ‘x_546779_appxcti’ with the application scope that you just copied in the
previous step.
Now you can copy the content of the servicenow_adapter.txt file into script content area.
6. Repeat the above process and create a new UI Script named 'appxconnect_adapter'
 <img width="975" height="545" alt="image" src="https://github.com/user-attachments/assets/744049a3-60e9-492c-ae02-d8096c2cec0a" />


**UI Page**
1. Create a new UI page named 'Appxconnect_CTI' by following the same processes as the
previous steps.
2. Open the 'Appxconnect_CTI.txt' file and replace all occurrences for the currently defined scope
with the one that we had earlier copied and then paste in the Script Content area. Also, copy
the endpoint value shown in the UI page form and note it down.
<img width="975" height="550" alt="image" src="https://github.com/user-attachments/assets/e0df56aa-1faf-4ec5-b325-ecbdc4f7d3b9" />


**Adding Global Properties**
1. Now go back to the Service Management page and navigate to system properties by
entering sys_properties.list in filter navigator and pressing **Enter** (⏎). The System
Properties page will open up. Click on New.
2. Add 'glide.script.block.client.globals' property (make sure that you are adding the property
in the appxconnect application scope that was created earlier. This property ised to access
document since we will be using messaging framework to communicate with iframe
  -> Set the type of property to true | false.
  -> Set the value to false.
  -> Save the property.
   <img width="983" height="461" alt="image" src="https://github.com/user-attachments/assets/beb464fa-c031-4f7f-99ec-e13f2296c2c9" />


**Openframe configuration in ServiceNow**
1. Navigate to openframe servicenow module by searching for 'Openframe' in the filter view
and then clicking on the CTI row as shown below:
<img width="1672" height="485" alt="image" src="https://github.com/user-attachments/assets/88151803-563a-4adf-b807-ce7d155f93df" />

3. Do the following:
Ensure Active is Ticked.
Width is set to 350
Height is set to 625
Select the user groups for which the AppXConnectCTI App should be enabled
and move them into selected group as shown in screenshot.
<img width="1675" height="914" alt="image" src="https://github.com/user-attachments/assets/76aa50c1-f15f-48ce-a5e1-0363ab50624b" />

4. Set url field to ”/” + the value shown in the endpoint field of the UI page and prepend it
with the keywork '?sysparm_nostack=true'. For this guide, the URL looks like below:
5. After updating openframe configuration, paste the CTIID shared with you in Configuration
text box.
4. After updating openframe configuration, assign the 'sn_openframe_user' role along with
the role that was created with the app to the ServiceNow agents to whom the CTI should be
enabled.
5. Once the agent has logged in, the call button will be visible in the relevant place (top right,
bottom left etc.) of the servicenow platform interface screen depending on the module in use.
