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
Lambda required a different folder structure so I changed it. Added node modules and .gitignore file. Spent most of the time debugging, not done yet. 

**Learnings:**
I wanted to debug the work I did so far so I opened the test simulator. I asked for a fact and it just returned the fact but not in audio, like I had specified in code. I was a bit confused so I checked the logs and nothing was there. Turns out the test simulator opened the skill that is live and returned version 1. I have to change the invocation name to test what I am doing right now. I changed it to meditation buster but somehow it still answered with the live skill. That is interesting to know because it means, that even if someone forgets a word they still call my skill. Okay changing the invocation name to Regina Philangee just to be sure. 

*New error 1*
Got this new error: 
npm WARN meditation-myth-buster-2.0@1.0.0 No repository field

Fixed it as follows: 
My solution (do this first, as the StackOverflow solution did not work on its own): 
1. Make sure that a git repository was initiated to begin with, if not run $ git init
2. make sure that the node modules you were looking for are installed in the first place, if not run $ npm install package name —save
3. if the repo exists check the status $ git status 
4. add all the things that are new $ git add .


Solution from StackOverflow: 
insert the following in the package.json file

"repository": {
    "type": "git",
    "url": "git://github.com/AlexaforMuggles/Meditation-Myth-Buster-2.0.git"
}

*New error 2*
GetNewFactHandler is not defined 

Solution: 
make sure that it is consistent both in the canHandler and the exports.handler 

*Not yet resolved error*
Error message: requestAttributes.t is not a function

"errorMessage":"requestAttributes.t is not a function","errorType":"TypeError","stackTrace"

Solution steps:  
The intent names in the developer console did not match the names in the index.js file --> fixed that, error went away briefly (maybe because of other errors) but is back. 

**Thoughts:** 
Debugging slows things down considerably but it also teaches you a lot. Nice that I feel that I have a shot at solving some of the issues. 

**Link to work:** [Meditation Myth Buster 2.0](https://github.com/AlexaforMuggles/Meditation-Myth-Buster-2.0)

### R1D6
**Today's Progress:** 
Another debugging day. Issue: requestAttributes.t is not a function

    1. removed the Question handler —> did not work, so this issue is not in the question handler
    2. removed the Launch handler —> did not work, so this issue is not in the launch handler
    3. inserted ask-sdk-core instead of just ask-sdk —> did not work
    4. bring all handlers back and insert this in each handler: console.log("THIS.EVENT = " + JSON.stringify(this.event)); —> still did not tell me where the issue was
    5. inserted line numbers in the console.log message: line 7 is the issue
    6. compared the launch request handlers with the sample code, no difference except my console.log statements and the file names
    7. on line 35 in the NewFactHandler there is a LaunchRequest bit that may cause confusion —> did not work either
    8. finally posed the question in the forum, let’s see if something useful comes back

**Learnings:**
Learned about logging, which I think will be very practical in the future. 
Insert this in every handler: 
console.log("THIS.EVENT = " + JSON.stringify(this.event));
If you don’t place this in the proper place it will just come back as undefined. 

If that doesn’t work, write out comments for each step that tells you exactly what the system was doing. For example: 
console.log("MAKING THE HTTPS CALL.");

console.log("SLOT VALUE IS XX" + slotValue + "XX");


**Thoughts:** 
Actually I should include good logging statements as a default in every skill. 
Also it's cool that I am not very emotional about trying again and again and still not resolving the issue. 

**Link to work:** [Meditation Myth Buster 2.0](https://github.com/AlexaforMuggles/Meditation-Myth-Buster-2.0)

### R1D8
**Today's Progress:** 

**Learnings:**

**Thoughts:** 

**Link to work:** [Meditation Myth Buster 2.0](https://github.com/AlexaforMuggles/Meditation-Myth-Buster-2.0)


### R1D9
**Today's Progress:** 

**Learnings:**

**Thoughts:** 

**Link to work:** [Meditation Myth Buster 2.0](https://github.com/AlexaforMuggles/Meditation-Myth-Buster-2.0)

