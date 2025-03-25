## Creating a Basic Search Agent in TotalAgility ##
For the accompanying tutorial videos, see:
[Creating a Basic AI Agent in TotalAgility](https://www.tungstendemocenter.com/items/creating-a-basic-ai-agent-in-totalagility)

1. Create the web service for Bing search
    ```https://api.bing.microsoft.com/v7.0/search?q=```

    ```Custom header: Ocp-Apim-Subscription-Key``` + the Azure Bing key

2. Create an LLM for gpt-4o-mini (if not already present)

3. Create a new Custom LLM: Web Search Agent (or similar)
    Select Create New Process

4. Edit the new process
    Add a local json data model using the Bing search example json

    Add the following new variables:
        prompt_search_optimiser
        prompt_search_query
        search_results (using the data model above)
        prompt_search_results_formatter

    Add steps:
        Gen AI ==> gpt-4o-mini
            prompt_search_optimiser + Input Prompt

            GET
            JSON

            Map the response to the search_results variable
        
        Azure Bing Search ==> web service for bing

        Format the response ==> gpt-4o-mini
            Prompt is  
                prompt_search_results_formatter
                search_results

            Map response to the Output variable

5. Create a form to test the service
        Add Advanced ==> Generative AI Control
        Configure the control to use Web Search Agent
        Test

## Example Package:
An example package is provided (note there are minor differences to the variable names used in the tutorial), however in the 8.0 TotalAgility release Generative AI providers cannot be imported or exported, so when the package imports you'll need to create new Generative AI providers for the LLM used in the process (and map these to steps 1 & 3), and create a new "Custom LLM" or "Agent" provider and map this to the imported process. Once you have mapped the "Custom LLM" to the process, the Form "Example Search RAG Agent" will need to be updated to use the new custom LLM provider.

Also note that different to the steps in the tutorial video, the Bing Search API Key is set to use a variable in the process ```BING_SEARCH_KEY``` which will need to be updated to use your API key. 
