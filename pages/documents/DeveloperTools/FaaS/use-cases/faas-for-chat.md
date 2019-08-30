---
pagename: Chat Conversations
keywords:
sitesection: Documents
categoryname: "Client Side Configuration"
documentname: LivePerson Functions
subfoldername: Use Cases
permalink: liveperson-functions-use-cases-chat-conversations.html
indicator: both
---

This guide explains how to enable LivePerson Functions for chat.

With **Functions for chat** you are able to invoke `lambdas` from standard chat events. For example, a chat in-queue event could be chosen as the trigger to invoke a pre-created function.

Along with the invocation, the function is sent a payload containing metadata related to the conversation which invoked the function. This payload can then be used in the function for further processing and referencing.

### Chat events for Function Invocation

LiveEngage chat uses a series of events which get fired when specific actions or events occur within the conversation. You are able to use theses events to trigger functions within Functions.

The following "Conversation State Change Events" can be used to trigger functions:

#### Chat In-Queue

This event is fired when a consumer initiates a new conversation and it is waiting in-queue for an agent to be assigned.

<table>
<thead><tr><th>1. level</th><th>2. level</th><th>3. level</th><th>description</th><th>type</th><th>example</th></tr></thead><tbody>
 <tr><td>campaignId</td><td></td><td>&nbsp;</td><td>ID of the campaign</td><td>STRING</td><td>3599735210</td></tr>
 <tr><td>chatSessionKey</td><td></td><td>&nbsp;</td><td>Chat id that can be used to query Server Chat API</td><td>STRING</td><td>H6846170109402085448-9905386f84524a008e929342b052819cK8389409</td></tr>
 <tr><td>chatStartPageURL</td><td></td><td>&nbsp;</td><td>URL where the chat started</td><td>STRING</td><td>http://example.de</td></tr>
 <tr><td>engagementId</td><td></td><td>&nbsp;</td><td>ID of the engagement</td><td>STRING</td><td>3599735310</td></tr>
 <tr><td>ipAddress</td><td></td><td>&nbsp;</td><td>IP address of the consumer</td><td>STRING</td><td>212.65.14.245</td></tr>
 <tr><td>preChatSurveyStructure</td><td>header</td><td>&nbsp;</td><td>.</td><td>STRING</td><td>1528463744663</td></tr>
 <tr><td>ttr</td><td>newTtr</td><td>value</td><td>value of ttr of the new state (after change for example to URGENT)</td><td>NUMBER</td><td>300</td></tr>
</tbody></table>


#### Chat Start

This event is fired when the conversation is assigned to an agent the first time (TODO: is this really fired once?).

#### Chat End

This event is fired when the conversation is closed by the agent or consumer.

### Step-by-Step implementation guide

#### Step 1 - Create function

Create a new function using one of the chat templates.

Currently, only one function per template type can be created. If there are multiple types of functionality needed that stem from the same event invocation, these should be coded into the same `lambda`.

#### Step 2 - Edit the Function

Adjust the coding from the template according to your needs by modifying the function. On the right side you can see an example of the payload (in the sidebar, which you might need to open):

Chat events do not support to send back commands, yet. Thus chat `lambdas` can only perform API calls such as creating cases in a CRM system, or leveraging the [Server Chat API (TODO: does this really work)](server-chat-api-overview.html).

#### Step 4 - Deploy the function

Just like any other function, this function must be deployed before it can be used. [Please see this document](function-as-a-service-deploying-functions.html) for more information on how to deploy your function. At this point, you can also test your function.

<div class="important">Try to deploy functions with a runtime of less than one second. If the runtime is longer, you may get a bad user experience because of race conditions within the server. For example, if you create a function based on the <b> Participants Change</b> event and an agent joins the conversation, the consumer may see the resulting `systemMessage` <b>after the agent already responded to the consumer themselves</b>.</div>