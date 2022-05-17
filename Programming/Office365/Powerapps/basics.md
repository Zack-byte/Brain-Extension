# Microsoft Power Apps

Power Apps: 
	- is a suite of apps, services, connectors and data platform that provides a rapid application development environment to build custom apps for your business needs 
	- Apps built have a responsive design, and can run seamlessly in browser or on mobile devices. 
	- Power apps also provides an extensible platform that lets pro developers programmatically interact with data and metadata, apply business logic, create custom connectors and integrate with external data. 

creating an app: go to make.powerapps.com
	- power apps studio is the app designer used for building canvas apps. 
	- App designer for model-driven apps lets you define the sitemap and add components to build a model-driven app. 
	- Power Apps portals studio is a WYSIWYG design tool to add and configure webpages, components, forms, and lists 
Types of apps: 
	- Canvas -  
	- Model-driven -
	- Portal - 

Power Apps for developers: 
	- can use code to create data and metadata, apply server-side logic using Azure functions, plug-ins, and workflow extensions, apply client side logic using JavaScript, integrate with external data using virtual entities and webhooks, build custom connectors, and embed apps into your website experiences to create integrated solutions


Power apps and Dynamics 365: 
	- use data platform (Dataverse) used by Power apps to store and secure data. 


Development with Power Platform
	- Microsoft Power Platform 
		- Power BI: MicroS business analytics solution that provides interactive data visualization BI tools to help users visualize and share data 			and insights across their organization 
		- Power Automate: is used to orchestrate activities across various services that use connectors. they can be triggered to run when specific 			events occur, such as when a record is created or scheduled to run at a specific time. 
		- Power Apps: are applications that are consumed by users through their desktop or mobile devices. These applications come in two forms: 
			- Canvas applications:  can be embedded into SharePoint, Teams, PowerBI, and Dynamics 365 applications. 
			- Model-driven applications:  are standalone, data driven applications that are built on top of Microsoft Dataverse

- Dataverse: 
	- is a composite set of capabilities that can be used to build robust business applications. these capabilities include a cloud-scale entity framework and data store, business rules, workflows, dynamically-calculated fields, and many other capabilities. 

Common Data Model: is an open-sourced standard definition of entities that represent commonly used concepts and activities. when built in conjunction with a dataverse application, a core set of entities are provided upon which application builders can add their own custom entities to support specific business scenarios. 


DATAVERSE: is the newest generation of a longstanding application platform that is built by microsoft and based on the proven Dynamics 365 customer engagement apps platform 



Canvas-app connectors for power apps: 
	- Power apps has connectors for many popular services and on-premises data sources, 
		- Sharepoint
		- SQL Server, 
		- Office 365
		- Salesforce
		- Twitter 
		- Common Data Service
		- Dynamics AX
		- Cloud Storage
		- Excel
		- Office 365 Outlook
		- Office 365 Users
		- Oracle
		- Power BI 
		- Microsoft Translator
		

	- Security Types and authentication
		- Azure AD or SQL Server Authentication, Windows Authentication
		- Open-Standard Authorization(OAUTH) 


Outlook add-ins: are integrations built by third parties into outlook by using our web-based platform. Outlook add-ins have three key aspects: 
	- the same add-in and business logic works across desktop (Outlook on Windows and MaC), 
	- Outlook add-ins consist of a manifest, which describes how the add-in integrates into Outlook (for example, a button or a task pane), and JavaScript/HTML code, which makes up the UI and business logic of the add-in. 
	- Outlook add-ins can be acquired form AppSource or side loaded by end-users or administrators

Outlook add-ins don't have any code physically installed on the user's device or outlook client. outlook reads the manifest and hooks up the specified controls in the UI, and then loads the JS and HTML. the web components all run in the context of a browser in a sandbox. 

- items that support add-ins include email messages, meeting requests, responses and cancellations, and appointments. Each Outlook add-in defines the context in which it is available, including the types of items and if the user is reading or composing an item. 



Extensions Points: are the ways that add-ins integrate with outlook
	- add-ins can declare buttons that appear in command surfaces across messages and appointments. 
	- add-ins can link off regular expression matches or detected entities in messages and appointments. 


Mailbox items available to add-ins
	- outlook add ins activate when the user is composing or reading a message or appointment, however add-ins are not activated if the current message item in a compose or raed form is one of the following 
	- protected by information rights management or encrypted in other ways for protection. a digitally signed message is an example since digital signing relies on one of these mechanisms
	- a delivery report or notification that has the message class (NDR) non-delivery report 
	- a draft
	- a .msg or .eml file which is an attachment to another message.
	- a .msg or .eml file opened from teh file system.
	- in a shared mailbox in another user's mailbox in an archive mailbox or in a public folder. 
	- using a custom form



CRM: Customer Resource Management
ERP: Enterprise resource planning

Outlook: 
	- Interactive emails: adaptive cards can increase productivity by allowing users to take quick actions from withing their inbox
	- ExtendOutlook: add-ins launch your custom app as a task panel contextual card or a simple button on the ribbon
	- Connect  to Outlook: Bring outlook -related data & features for office 365 and outlook.com users into your app using hte microsoft Graph REST Api


Outlook and Power apps: 
	- if you connect ot office 365 outlook you can show send delete and reply to email messages in addition to other tasks. You can add controls to perform these functions in your app for ex you can add text input controls to ask for the recipient the subject and the body of the email. and add a button control to send the email 