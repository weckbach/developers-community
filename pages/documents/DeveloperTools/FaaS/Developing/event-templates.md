---
pagename: "Events & Templates"
keywords:
sitesection: Documents
categoryname: "Developer Tools"
documentname: LivePerson Functions
subfoldername: Developing with FaaS
permalink: liveperson-functions-development-events-templates.html
indicator: both
redirect_from:
  - function-as-a-service-developing-with-faas-events-templates.html
---

### Events

LivePerson Functions' `lambdas` can be connected to LiveEngage events at the time of [creation](function-as-a-service-getting-started.html#step-1-choose-a-template). Once those `lambdas` are deployed, they will be executed whenever these events are triggered. Each event comes with a set of connected templates that can be used as an initial scaffolding for the developing the `lambda`.

{: .notice}
The amount of lambdas connected to a specific event is restricted and can be seen in the table below.

Currently the following events are supported:

|Event Name|Event Description|Lambda Limit|
|--- |--- |--- |
|Chat Post Survey E-Mail Transcript|Triggered after a chat conversation is finished and CSAT survey has been submitted.|10|
|Conversational Command|Use this event to implement a Conversational Command that can be invoked from within the agent workspace in LiveEngage by typing "/".|30|
|Messaging Conversation End|Triggered when the conversation is closed by agent/consumer.|1|
|Messaging Conversation Idle|Triggered when agent/consumer is not responsive or the conversation is in queue for over X secs/mins. Where Time X is configurable inside the LiveEngage UI, via the auto-messages feature.|1|
|Messaging Conversation Routing|Triggered when the conversation is transferred to a different skill.|1|
|Messaging Line in Off-Hours|Triggered when a consumer writes a message to a conversation that started in working hours, but is now in off-hours.|1|
|Messaging New Conversation|Triggered for every new messaging conversation.|1|
|Messaging Participants Change|Triggered on every participant change (joins/leaves) of a messaging conversation.|1|
|Messaging Survey Ended|Triggered when a messaging post survey ended.|1|
|Messaging Survey Started|Triggered when a messaging post survey started.|1|
|Messaging TTR|Triggered when the consumer marks a response as an urgent response, unmarks a response as urgent, or the agent manually updates the response time|1|
|No Event|Used for lambdas which only can be invoked externally||
|Third-Party Bots Custom Integration|Triggered when a bot, which is using the Third-Party Bots' Custom Integration receives a message|15|
|Third-Party Bots Post Hook|Triggered when a bot, which is using the Third-Party Bots' Post Hooks receives a message. The function will be invoked after the vendor responded|15|
|Third-Party Bots Pre Hook|Triggered when a bot, which is using the Third-Party Bots' Post Hooks receives a message. The function will be invoked before the vendor receives the payload|15|
|Third-Party Bots Error Hook|Triggered when a bot, which is using the Third-Party Bots' Error Hooks is having an issue|15|


Each of these events also has an event specific input (payload) associated with it, that the triggering system will provide at runtime. When using the [Invoke](function-as-a-service-deploying-functions.html#testing-your-function) screen, this payload is shown on the left-hand side. During development, the event payload of the `lambda` is visible on the right-hand side at the sidebar-tab. See the [Payload](function-as-a-service-developing-with-faas-overview.html#editor-sidebar) section for more information.

### Templates

Additionally, Functions offers a number of templates. They can be used as a sample to kick-start the development of custom scenarios. Some of them are connected to events which the template list below is grouped by. Templates which have the same name as the related event are to be considered the default template for an event.

|Event|Template Name|Template Description|
|--- |--- |--- |
|Chat Post Survey E-Mail Transcript|Chat Post Survey E-Mail Transcript|A template displaying some basic ways how the "Chat Post Survey E-Mail Transcript"-Event can be used.|
|Conversational Command|Conversational Command|A template displaying some basic ways how the "Conversational Command"-Event can be used.|
|Messaging Conversation End|Keyword Scanner|A template displaying how to use the Conversation Util to get a conversation and scan it for keywords.|
||Messaging Conversation End|A template displaying some basic ways how the "Messaging Conversation End"-Event can be used.|
||Replace Files for Conversation|A template displaying how to use the GDPR Util to replace all files of a conversation.|
|Messaging Conversation Idle|Messaging Conversation Idle|A template displaying some basic ways how the "Messaging Conversation Idle"-Event can be used.|
|Messaging Conversation Routing|Messaging Conversation Routing|A template displaying some basic ways how the "Messaging Conversation Routing"-Event can be used.|
|Messaging Line in Off-Hours|Messaging Line in Off-Hours|A template displaying some basic ways how the "Messaging Line in Off-Hours"-Event can be used.|
|Messaging New Conversation|Messaging New Conversation|A template displaying some basic ways how the "Messaging New Conversation"-Event can be used.|
||Read&Update-SDEs|A template demonstrating how to read and update SDEs on a new conversation.|
|Messaging Participants Change|Messaging Participants Change|A template displaying some basic ways how the "Messaging Participants Change"-Event can be used.|
|Messaging Survey Ended|Messaging Survey Ended|A template displaying some basic ways how the "Messaging Survey Ended"-Event can be used.|
|Messaging Survey Started|Messaging Survey Started|A template displaying some basic ways how the "Messaging Survey Started"-Event can be used.|
|Messaging TTR|Messaging TTR|A template displaying some basic ways how the "Messaging TTR"-Event can be used.|
|No Event|Greeting Template|A simple "Hello World" example|
||HTTP Template|An example of how to execute a HTTP request.|
||Logging Template|An example of how to write logs during lambda execution.|
||Salesforce Template|An example of how to connect to Saleforce.|
||Secret Storage Template|An example of how to use the Secret Storage.|
|Third-Party Bots Custom Integration|Default Template|A template displaying some basic ways how the "Third-Party Bots Custom Integration"-Event can be used.|


Each of these events also has an event specific input (payload) associated with it, that the triggering system will provide at runtime. When using the [Invoke](function-as-a-service-deploying-functions.html#testing-your-function) screen, this payload is shown on the left-hand side. During development, the event payload of the `lambda` is visible on the right-hand side at the sidebar-tab. See the [Payload](function-as-a-service-developing-with-faas-overview.html#editor-sidebar) section for more information.
