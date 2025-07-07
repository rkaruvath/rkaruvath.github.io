# Configuring Agentic chat for BMC Helix ITSM

As an administrator, configure Agentic Chat in BMC Helix ITSM to provide service desk agents with a conversational, AI-driven search experience. Agentic Chat uses the advanced AI capabilities of BMC HelixGPT to augment the Full Text Search (FTS)-based global search with a chat-based search.

Instead of manually searching for knowledge articles, service desk agents can enter specific questions in Agentic Chat and get relevant, summarized answers.

For example, instead of manually searching for a knowledge article that contains an asset replacement policy, a service desk agent can type in specific question and get summarized policy information.

To generate the responses, Agentic Chat uses the Service Collaborator AI agent, which is a large language model (LLM)-based AI agent of BMC HelixGPT. Service Collaborator processes natural language inputs, autonomously learns and adapts to user interactions, makes context-aware decisions, and generates intelligent responses.

## Supported knowledge providers
BMC HelixGPT uses published knowledge articles from the following knowledge providers to generate responses for knowledge article-related questions:
* BMC Helix ITSM: Knowledge Management
* BMC Helix Knowledge Management by ComAround 

### Before you begin
Perform the following tasks before enabling Agentic chat:

|No.|Task|Reference|
|---|---|---|
|1|Ingest data from the BMC Helix ITSM: Knowledge Management and BMC Helix Knowledge Management by ComAround into BMC HelixGPT.|Cross-reference to the topic.|
|2|The **Agent in Global Context** skill is provided out of the box for Agentic chat to generate an answer when a user submits a question in Agentic chat.<br>By default, this skill uses the Azure OpenAI GPT-4o (Omni) model.<br>To use a different model, associate the desired model with this out-of-the-box skill in the BMC HelixGPT Manager administrator UI.<br>If you have created a custom skill and want to use it instead of the Agent in Global Context skill, associate the desired model with the custom skill.|Cross-reference to the topic.|

## To enable Agentic chat for BMC Helix ITSM
1. In Mid Tier, open the **AR System Configuration Generic UI** form.
2. Set the **enableHelixGPTGlobalChat** CCS parameter to true.

## To set the default mode to global search or Agentic chat
After you enable Agentic chat, you can set the default search mode to Agentic chat or global search.

1. In Mid Tier, open the **AR System Configuration Generic UI** form.
2. Set the **helixgptGlobalSearchDefaultMode** CCS parameter to one of the following options:
   * **search**: To set the default mode to global search.
   * **chat**: To set the default mode to Agentic chat.

## FAQ
<details>
  <summary>Agentic chat does not generate any response even after I have performed the required configurations</summary>
  
  Possible reasons:
  * A relevant published knowledge article does not exist in the knowledge repository referenced by BMC HelixGPT.
  *	A relevant published knowledge article exists, but the logged-in user is not entitled to view the knowledge article.
</details>


<details>
  <summary>Agentic chat generates a blank response when using the MS Azure GPT-4 (Omni) model</summary>
  The token per minute (TPM) rate limit configured for the MS Azure GPT-4 (Omni) model might be reached.
</details>


<details>
  <summary>Agentic chat shows incorrect or varied responses when searching for information from knowledge articles</summary>
  
  Possible reasons:
  * Response generation depends on many factors such as accuracy of the knowledge articles, model, and prompt configuration. Therefore, the generated responses might vary.
  * BMC HelixGPT does not use information present in the attached documents of the knowledge articles for generating responses. Hence, if the information is present in an attached document of a knowledge article, the generated response does not contain the information.
</details>