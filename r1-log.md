# #100DaysOfCode Log - Round 1 - Kristen

The log of my #100DaysOfCode challenge. Started on [January 1, 2019].

## Log

### R1D1 
**Today's Progress:**
Started Meditation Myth Buster 2.0. Wrote all the handlers and except the question one all others are done. Created the package file and did the initial Github commit. 

**Thoughts:** 
Manually writing out the code let's you notice patterns that you otherwise don't pick up on if you just clone the sample code. 
Didn't quite remember how to create a repo and push it to Github initially. Good to practice that. 
Overall repetition is important for me. In the quest to push yourself it's easy to forget what was done two days or a week ago if I don't repeat certain tasks. I don't have to do brand new things every day of the challenge. Getting routine in the most common tasks is important too. 

**Learnings:**

Launch Requests are only added to intents which the user actively uses. All technical handlers only have Intent requests. 

CanHandlers define the request and return request types (intent or launch) as well as the intent name
const request = handlerInput.requestEnvelope.request;

handle() contain defined variables, error messages if applicable and response Builders
Response builders contain speak, reprompt or withSimpleCard and get response. If it's only one of them then it's chained at the end like this: return handlerInput.responseBuilder.getResponse(); 

In the response you can either give a fixed message in the paranthesis or refer to a message which is somewhere else. That is usually cleaner because you can just change the language instead of having to change the outputSpeech every time. 

I thought that i18next was a module to handle the translations but it turns out that the randomness generator is also in there. 

**Link to work:** [Meditation Myth Buster 2.0](https://github.com/AlexaforMuggles/Meditation-Myth-Buster-2.0)

### R1D2
**Today's Progress:** 
Added how-to-handlers and modified them. Inserted the various messages. Hooked up the data file with the index file. 

**Learnings:**
I learned what localization is to make an informed decision to remove it. Also by simply renaming some of the sample code intents it forces you to look closely at what depends on what. Had to go back and look at how files are connected to each other. 

**Thoughts:** 
Merging two kinds of skills really forces you to look at how each line of code works. Tomorrow we'll see what I have missed and what still needs to be debugged.

**Link to work:** [Meditation Myth Buster 2.0](https://github.com/AlexaforMuggles/Meditation-Myth-Buster-2.0)

### R1D3
**Today's Progress:** 
Added the audio content to the data file. Created the questions file and started the JSON model.

**Learnings:**
Data entry can seem dull and unproductive but actually it keeps the mind slightly busy while still focusing on the task at hand. It occurred to me that the way I wanted to do the additional feature would simply be too complicated. I have to think more about the questions someone would ask and start from their feelings such as fear, doubt, impatience, etc. 

**Thoughts:** 
Quite proud that I did my hour today as I trapped a nerve in the back and sitting was initially quite painful. 

**Link to work:** [Meditation Myth Buster 2.0](https://github.com/AlexaforMuggles/Meditation-Myth-Buster-2.0)

### R1D4
**Today's Progress:** 
Added slots and finished the JSON model

**Learnings:**
It seems that an array will not take slots. I tried to convert it to an object but that didn't work either. I will have to ask in the forum whether slots cannot be assigned to audio files. 

**Thoughts:** 
I continued on the question intent although it seems it may not be possible to do what I want just yet. However I think it's better to have the work done than to assume that it won't work out. 

**Link to work:** [Meditation Myth Buster 2.0](https://github.com/AlexaforMuggles/Meditation-Myth-Buster-2.0)


### R1D5
**Today's Progress:** 

**Learnings:**


**Thoughts:** 


**Link to work:** [Meditation Myth Buster 2.0](https://github.com/AlexaforMuggles/Meditation-Myth-Buster-2.0)

### R1D6
**Today's Progress:** 

**Learnings:**


**Thoughts:** 


**Link to work:** [Meditation Myth Buster 2.0](https://github.com/AlexaforMuggles/Meditation-Myth-Buster-2.0)