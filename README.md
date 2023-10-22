# LLM RASA Experiments

This repo contains implementations of different [Custom Graph Components](https://rasa.com/docs/rasa/custom-graph-components/)
for [Rasa](https://rasa.com/) that utilize Large Lanuguage Models (LLMs). The components have been created as experiments
while working on my Master Thesis. 

In my experiments I had very promising results with the main advantages being that you don't need to create training data
and you don't have to train an NLU model locally. 
However, this also leads to the main disadvantage of using LLMs like GPT3.5-turbo. 
The significantly larger respone time compared to using e.g. 
the DIET component for Intent and Entity extraction. It usually takes a few seconds until the OpenAPI returns a response.

All components rely on the OpenAI API and require an "OPENAI_API_KEY" as environment variable or in a .env file to work.

The following components have been created.

## Intent Classification

The so-called IntentClassifier component implements as the name suggest a Custom Graph Component that 
can use OpenAI's LLMs to classify intents from the user input.

### Usage

To use the DualIntentAndEntityLLM you add the component to the pipeline in Rasa's config.yaml file.
You then specify the intents and the entities as shown below. To provide a description is optional, 
but it can be very useful for finetuning to get the desired behavior.

```yaml
- name: intents.IntentClassifier
   intents:
   - greeting "Greetings from the user. Don't extract entities."e
   - provide_number "Intent that contains a numeric input. Entities (number)"
   - provide_address "Intent that contains the users address. Entities (city, street, number)
   - goodbye
```

## Entity Extraction

The so-called EntityExtractor component implements as the name suggest a Custom Graph Component that 
can use OpenAI API's LLMs to extract entities from the user input.

### Usage

To use the DualIntentAndEntityLLM you add the component to the pipeline in Rasa's config.yaml file.
You then specify the intents and the entities as shown below. To provide a description is optional, 
but it can be very useful for finetuning to get the desired behavior.

```yaml
- name: entities.EntityExtractor
   entities:
   - city
   - street
   - number
```

## Intent Classification and Entity Extraction

The so-called DualIntentAndEntityLLM component implements as the name suggest a Custom Graph Component that 
can use OpenAI's LLMs to classify intents and extract entities from the user input. Its name has
been inspired by Rasa's DIET (Dual Intent and Entity Transformer) component.

### Usage

To use the DualIntentAndEntityLLM you add the component to the pipeline in Rasa's config.yaml file.
You then specify the intents and the entities as shown below. To provide a description is optional, 
but it can be very useful for finetuning to get the desired behavior.

```yaml
- name: intents_and_entities.DualIntentAndEntityLLM
   intents:
   - greeting "Greetings from the user. Don't extract entities."e
   - provide_number "Intent that contains a numeric input. Entities (number)"
   - provide_address "Intent that contains the users address. Entities (city, street, number)
   - goodbye
   entities:
   - city
   - street
   - number
```