<div style="text-align: right">
<a href="https://rkaruvath.github.io/WorkSamples/index.html">Home</a><br><a href="https://rkaruvath.github.io/WorkSamples/RestAPIDocumentationSample.html">REST API documentation sample</a><br><a href="https://rkaruvath.github.io/WorkSamples/InfographicSample.html">Infographics sample</a><br><a href="https://rkaruvath.github.io/WorkSamples/VideoSample.html">Video sample</a>
</div>
 
# Writing sample
This page contains my writing sample.

## Configuring Agentic chat in BMC Helix ITSM

As an administrator, configure Agentic chat in BMC Helix ITSM. Agentic chat uses the advanced AI capabilities of BMC HelixGPT to augment the global search, which is based on full-text search, with an AI-powered, chat-based search.

While working on incidents, service desk agents can use Agentic chat for a conversational, AI-driven experience to search for information from knowledge articles that helps them resolve the incidents. Instead of manually searching for information, service desk agents can ask specific questions in Agentic chat and get relevant, summarized answers leading to faster incident analysis and resolution.

### Before you begin
Perform the following tasks before enabling Agentic chat:

|No.|Task|Description|Reference|
|---|---|---|---|
|1|Ingest knowledge articles from the following knowledge providers into BMC HelixGPT: <br><br> - BMC Helix ITSM: Knowledge Management<br><br> - BMC Helix Knowledge Management by ComAround|BMC HelixGPT uses the published knowledge articles from these knowledge providers as an information source to generate the responses.|<*Cross-reference to the topic that contains the information*>|
|2|Associate a model with the skill that is configured to generate the responses.|The **Agent in Global Context** skill is provided out of the box to generate an answer when a service desk agent submits a question in Agentic chat. By default, this skill uses the Microsoft Azure OpenAI GPT-4o (Omni) model.<br><br>To use a different model, associate the desired model with this out-of-the-box skill.<br><br>If you have configured a custom skill and want to use it instead of the **Agent in Global Context** skill, associate the desired model with the custom skill.|<*Cross-reference to the topic that contains the information*>|

### To enable Agentic chat for BMC Helix ITSM
1. In Mid Tier, open the **AR System Configuration Generic UI** form.
2. Set the **enableHelixGPTGlobalChat** parameter to **true**.

### To set the default search mode to Agentic chat or global search 
After you enable Agentic chat, you can set the default search mode to Agentic chat or global search.

1. In Mid Tier, open the **AR System Configuration Generic UI** form.
2. Set the **helixgptGlobalSearchDefaultMode** parameter to one of the following options:
   * **search**: To set the default search mode to global search. The default value is **search**.
   * **chat**: To set the default search mode to Agentic chat.

### FAQ
<details>
  <summary>> Agentic chat does not generate any response even after you perform the required configurations.</summary>
<p>
  Possible reasons:</p>
<p>
  * A relevant published knowledge article does not exist in the knowledge repository referenced by BMC HelixGPT.</p>
<p>
  *	A relevant published knowledge article exists, but the logged-in user is not entitled to view the knowledge article.</p>
</details>
<p></p>
<details>
  <summary>> Agentic chat generates a blank response when using the Microsoft Azure GPT-4 (Omni) model.</summary>
 <p>
 The token per minute (TPM) rate limit configured for the Microsoft Azure GPT-4 (Omni) model might be reached.</p>
</details>
<p></p>
<details>
  <summary>> Agentic chat shows incorrect or varied responses when searching for information from knowledge articles.</summary>
<p>  
  Possible reasons:</p>
<p>
  * Response generation depends on many factors such as accuracy of the knowledge articles, model, and prompt configuration. Therefore, the generated responses might vary.</p>
<p>
  * BMC HelixGPT does not use information present in the attached documents of the knowledge articles for generating responses. Therefore, if the information is present in an attached document of a knowledge article, the generated response does not contain the information.</p>
</details>