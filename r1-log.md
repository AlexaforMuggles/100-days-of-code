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

### R1D7
**Today's Progress:** 
Added the localizationInterceptor as that was creating the error "Error message: requestAttributes.t is not a function". 
Installed the additional node modules and worked on more debugging. 

**Error 1 requestAttributes.t is not a function**
Solution can be found here: 
https://forums.developer.amazon.com/questions/196277/requestattributest-is-not-a-functionerrortypetypee.html


**Error 2 languageStrings is not defined (RESOLVED)**

Solution: added this
const {languageStrings} = require('./Data/data.js'); 

**Error 3 "errorMessage": "localizationClient.t is not a function"**
Posted this in the Alexa dev forum. 
https://forums.developer.amazon.com/questions/196345/localizationclientt-is-not-a-function-type-error.html


**Learnings:**
localizationInterceptors are needed even if you are not using other languages. 
When you give reputation points in the Dev forum you are giving away points from your own reputation. I should stop doing that. Very strange mechanism. 

**Thoughts:** 
I am very grateful for the people who answer issues on the developer forum. I did some of that as well yesterday. 

**Link to work:** [Meditation Myth Buster 2.0](https://github.com/AlexaforMuggles/Meditation-Myth-Buster-2.0)


### R1D8
**Today's Progress:** 
Back after a prolonged bout of sickness. Debugged localization issue and separated facts from language. Unfortunately still have a bug. 
New issue: it only reads WELCOME_MESSAGE instead of reading the actual message. This is an issue with the whole require mechanism. Something is not being exported correctly. 

**Learnings:**
Previous bug could be solved because of help from the Alexa Dev forum: 
https://forums.developer.amazon.com/questions/196345/localizationclientt-is-not-a-function-type-error.html

He also provided more resources which I should eventually consult: 
More about arguments: 
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments#Rest_default_and_destructured_parameters

More about localization: 
https://developer.amazon.com/blogs/alexa/post/285a6778-0ed0-4467-a602-d9893eae34d7/how-to-localize-your-alexa-skills


**Thoughts:** 
Glad I woke up early without an alarm to take this back up. I am wondering whether it would make sense to read up on everything and do something else tomorrow. This debugging business is very slow. Necessary but a win for a change would be nice. Maybe take a crack at the Decision Tree tomorrow. 

**Link to work:** [Meditation Myth Buster 2.0](https://github.com/AlexaforMuggles/Meditation-Myth-Buster-2.0)

### R1D9
**Today's Progress:** 
Taking a break from Meditation Myth Buster to take a stab at an issue I have been having with a decision tree skill. Downloaded the sample code, tested the model and then made substitutions only to run up against the same issue I have been having for a long time now. 

**Learnings:**
I stumbled over a best practice to-do: create a customizations.md file and detail exactly what has been substituted / removed or added from the sample code. 

**Thoughts:** 
I need to understand logging better so that I can figure out exactly where and why the problem occurs. Tried researching generic logging in Node yesterday but that's not helpful. I need to more Alexa-specific information. 

**Link to work:** Haven't put this on Github just yet. 

### R1D10
**Today's Progress:** 
Generated new slot mappings hoping it would solve the *TypeError - Cannot read property 'name' of undefined* but it did not. Also inserted more logging and while I got slightly more insight from that the crucial part of the puzzle is still missing. I also just tried if the autogenerated code by itself can create a functioning skill but there were a multitude of errors. To summarize, yet another session that was almost exclusively debugging. 

**Learnings:**
It doesn't make sense to go through the whole work of including the activity descriptions before I get the code to work properly. 
Also I came across the module initialization error and the fix is fairly simple: when you remove a handler/intent but you forget to remove that from the exports.Handler function then it creates this error. 
The following logs were helpful: 

handle(handlerInput) {
    const filledSlots = handlerInput.requestEnvelope.request.intent.slots;

    const slotValues = getSlotValues(filledSlots);

    const key = `${slotValues.energy.resolved}-${slotValues.valence.resolved}-${slotValues.time.resolved}-${slotValues.focus.resolved}`;
    const activity = options[slotsToOptionsMap[key]];
    console.log('slotsToOptionsMap starting up.'); 

function getSlotValues(filledSlots) {
  const slotValues = {};
  console.log('Helper function getSlotValues started.'); 

I still have open questions around finding the specific item that is undefined.   

**Thoughts:** 
It occurred to me that slot resolutions and mappings might be a good topic for Alexa office hours. By myself I am going in circles, considering that I had this issue months ago already.

**Link to work:** Haven't put this on Github just yet because I want to eventually save everything with a different name. 

### R1D11
**Today's Progress:** 
Did a code deep dive today because I need to learn how to implement certain features from SDK2 before I can continue with the tasks on my todo-list. 
Tomorrow I can finish up by comparing what I have with this: 
https://github.com/alexa/alexa-guided-walkthrough-using-node-sdk/blob/master/part-2/index.js

**Learnings:**
I am starting to understand how attributes work but I need to study this more closely to be able to just come up with my own score and leaderboards.

**Thoughts:** 
Not many. 

**Link to work:** Haven't put this on Github, not sure I will. 

### R1D11
**Today's Progress:** 
Finally debugged the decision tree skill. It turns out that the sequence of the slot mappings in the key was incorrect and it couldn't actually access the slot mappings. Furthermore replacing the CompletedRecommendationIntent handle section solved the *** Cannot read property 'name' of undefined *** issue. Not quite finished with the slot mappings yet but I am happy since this means that I may have a shot at publishing the elevate me skill this weekend the way I wanted to for months. 

**Learnings:**
Just taking the time to look at the code after a break was helpful. 

**Thoughts:** 
Mostly feel relief. I was starting to think whether I have bitten off more than I could chew and whether I should involve a code-mentor. That may still be a valid idea but for now this gives me quite a bit of motivation. 

**Link to work:** Not on Github as I wanted to create a functioning skill but create the repo under another name. 

### R1D12
**Today's Progress:** 
Finished the mappings on the decision tree skill. Added the ability to write the descriptions. Everything works perfectly. Tomorrow I will create the whole skill under the name "Elevate Me" and submit it for certification. I have to remember to create a slightly altered policy to make sure that nobody uses it as a substitute for therapy. 

**Learnings:**
Having a separate file with the slot mappings makes sense. That way if something goes wrong the index.js file is still okay.

**Thoughts:** 
I feel very relieved that everything works the way I envisioned it. 

**Link to work:** 
Will link up everything to the final repo name but I think I will keep it private.

### R1D12
**Today's Progress:** 


**Learnings:**


**Thoughts:** 


**Link to work:** 

### R1D12
**Today's Progress:** 


**Learnings:**


**Thoughts:** 


**Link to work:** 

### R1D12
**Today's Progress:** 


**Learnings:**


**Thoughts:** 


**Link to work:** 

### R1D12
**Today's Progress:** 


**Learnings:**


**Thoughts:** 


**Link to work:** 

### R1D12
**Today's Progress:** 


**Learnings:**


**Thoughts:** 


**Link to work:** 

### R1D12
**Today's Progress:** 


**Learnings:**


**Thoughts:** 


**Link to work:** 


### R1D12
**Today's Progress:** 


**Learnings:**


**Thoughts:** 


**Link to work:** 