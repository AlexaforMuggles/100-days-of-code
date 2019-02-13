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

### R1D13
**Today's Progress:** 
Ironed out the last few details, did some additional testing, added the fallback intent for graceful error handling and submitted the Elevate Me skill for certification. 

**Learnings:**
I was so focused on getting Alexa skills to work that I didn't take the time to understand the capabilities of the code editor. A simple step like installing a linter can really help me learn more about coding in general. Moral of the story: take 30 min to an hour to understand the tools you are working with. It will pay off later. 

The test simulator pulled up an older version of Elevate Me. Had to delete it to make everything work. Important to remember that this can be the case. 

**Thoughts:** 
It's always nice to submit a skill to the store. Feels like I accomplished something, especially after having tried to get this skill to work since August. 

**Link to work:** 
Elevate Me https://github.com/AlexaforMuggles/elevate-me

### R1D14
**Today's Progress:** 
Elevate Me got accepted into the Alexa skill store, yay. Didn't work on it today though. 
Today I continued with my NodeJS course, specifically finishing up the MongoDB portion and starting with the Socket.IO section. 

**Learnings:**
I may or may not have found a solution to one of my bugs relating to paths. 

**Thoughts:** 
I am glad to be done with MongoDB because it wasn't fun and I didn't see the applicability to Alexa. I find it a very convoluted way of working on a database and although I am sure it's got its fans and good use cases I am glad that DynamoDB just makes more sense to me overall. 

**Link to work:** 
Chat Bot App: https://github.com/AlexaforMuggles/node-chat-app

### R1D15
**Today's Progress:** 
Continued with Socket.IO in the NodeJS course. Forgot to commit in the morning.

**Learnings:**
Not quite sure just yet how applicable this will be to other things.

**Thoughts:** 
This may deepen my understanding of emit and listening functions in Alexa. Not sure yet though. 

**Link to work:** 
Chat Bot App: https://github.com/AlexaforMuggles/node-chat-app

### R1D16
**Today's Progress:** 
Continued with the Node course. 

**Learnings:**
Event emitting and listening as well as broadcasting. 

**Thoughts:** 
Another break due to illness, hope I am done now with that and the rest of the 100 day challenge can continue with more consistency. 

**Link to work:** 
Chat Bot App: https://github.com/AlexaforMuggles/node-chat-app

### R1D17
**Today's Progress:** 
Went through the first 170 lines of code in the foodie skill and described what every bit of it does. Still have about 770 lines of code to go. 

**Learnings:**
Found some great and very detailed documentation about the ASK SDK2 that allows me to look up what every piece of code actually is and what it does and what it's connected to.  
Furthermore this skill has some good logging examples that I can use in other skills I build. 

**Thoughts:** 
It's great to have found such a detailed resource and it allows me to do code deep-dives in complex Alexa skills I would otherwise have no shot at understanding in detail. 
Curious to see whether I understand the more complex functions that come further down the line. 
Initially I just wanted to build Alexa skills in these 100 days but I noticed quickly that I was plateauing, fighting with some of the same errors I had issues with for months. By a) progressing with my NodeJS course and b) doing new things such as this code deep dive I can move forward and then return to issues armed with new knowledge and tools. 

**Link to work:** 
Code Deep Dives: https://github.com/AlexaforMuggles/deep-dives

### R1D18
**Today's Progress:** 
Continued with the code deep dive from lines 170 to 438. 

**Learnings:**
Even if you use MomentJS you still need to add quite a bit of code to capture dates in the location of the user. 

**Thoughts:** 
It's getting easier and making much more sense than it used to. 

**Link to work:** 
Code Deep Dives: https://github.com/AlexaforMuggles/deep-dives

### R1D19
**Today's Progress:** 
Finished the code deep dive. Also read the majority of the debugging chapter in the Node Cookbook. 

**Learnings:**
 Open questions: 


defines whether the slots are required to fulfill the intent or not. Not sure why this needs to be hard-coded here, as it's already defined in the console. 
not sure why the object called responseBuilder is set equal to the handler output 
 .addElicitSlotDirective("deliveryOption") // not sure why it doesn't include all the slots that are being elicited but only the deliveryOption
What's the difference between an error message and an error stack? 
What is the difference between a response and a request interceptor? 
What does the process keyword/method do? 
How does the saveNewlyFilledSlotsToSessionAttributes interceptor interact with other aspects of persistence? 
if (currentIntentSlots[key].value && !currentIntent.slots[key].value) { // don't know what this does exactly
currentIntent.slots[key] = currentIntentSlots[key]; // don't know what this does exactly
getSlotValues is a function I don't understand at all how it works. I see the lines but I dont' understand what it means. 



Learnings: 
What is in the request envelope? Contains the incoming Request and other context.
What does the SIPRecommendationIntentHandler do exactly? It figures out if all the required slots are filled thanks to the disambiguate helper functions.   
it's super obvious but if I want to know exactly what aspects are in the sessionAttributes or in the requestEnvelope or wherever I can just log those things
seems a bit generic, shouldn't it be addressIntent or some specified name? --> no. This allows this code to be re-usable in different intents.
what is currentIntent is needed for? When we're collecting slots the program needs to know where we are. In case there is an interruption slots from the currentIntent get transferred to the profile where they can later by found again. 
Is interceptor just a fancy name for helper function? No, there are a bunch of helper functions which mainly initialize stuff or provide messages. Interceptors are more complex and cover quite a bit of logic. Helper functions are used within interceptors. 
How are interceptors related to each other? They can be linked but don't have to be, as they are perfectly capable of standing alone. Linked interceptors might perform sequential tasks whereas some interceptors share an activity such as initializing a process. 
how does this address interceptor relate to other address functions above? My guess is that the handlers just query address details whereas the interceptors actually add them to the profile. 
What is disambiguation? I think it means that not all slots have been filled and some kind of reprompt is necessary to fill all required slots. 
not sure what the difference is between the getNewSlots function and the gotSlotsValues function --> 
        // intentHasNewlyFilledSlots given a previous and current intent and a set of 
        // slots, this function will compare the previous intent's slots with current 
        // intent's slots to determine what's new. The results are filtered by the 
        // provided array of "slots". For example if you wanted to determine if there's
        // a new value for the "state" and "city" slot you would pass the previous and
        // current intent and an array containing both strings. If previous is undefined,
        // all filled slots are treated as newly filled. 
        // Returns: 
        // {
        //   found: (true | false)
        //   slots: object of slots returned from getSlots
        // }

**Thoughts:** 
Interceptors and helper functions are more complex than the rest of the code. This may have to do with familiarity as they're part of the new SDK2 and also not necessarily part of simple skill architecture. 

**Link to work:** 
Code Deep Dives: https://github.com/AlexaforMuggles/deep-dives

### R1D20
**Today's Progress:** 
Late with the logging, but I did do my coding in the last two days nevertheless. Emitting and listening to events. 
Then I read a big chunk of the Debugging chapter in the Node Cookbook. 

**Learnings:**
I have seen Browser based developer tools but I never understood anything about how they worked. Now I know at least a tiny bit more. 

**Thoughts:** 
Some things about coding and developers are still deeply mystifying to me. For example they acknowledge that some error messages are completely unreadable and incomprehensible so somebody develops a module that supposedly solves that. Only then you look at the results and almost all the information has disappeared. And I am like "gee yes it's more nicely formatted but instead not being able to comprehend it now the info has just disappeared. How the f**k is that better???

**Link to work:** 
Node Chat app: https://github.com/AlexaforMuggles/node-chat-app

### R1D21
**Today's Progress:** 
NodeJS class: finished the broadcasting events lecture and moved on to message generator tests. Got stuck with a bug so after not being able to solve it for a while I spent the rest of my hour finishing the Debugging chapter in the Node Cookbook. 

**Learnings:**
Hovering is a good idea in developer tools. Furthermore breakpoints are set according to in which functions you suspect the bug to be. 

**Thoughts:** 
The debugging process still makes very little sense to me. Instead of going all cryptic why doesn't the system just say "Line 35 this and this is broken." Instead loggers produce all these useless lines. But maybe I have to humbly accept that maybe some of that is not rubbish, a bit like when genetists thought we were full of "junk DNA" but they just didn't understand yet the whole point. 

**Link to work:** 
Did not want to commit the bug to Github. 

### R1D22
**Today's Progress:** 
Spent the hour 50-50 doing two completely different things. First half was trying to debug an issue I had in the NodeJS class. My test keeps failing although I have exactly the same code as the instructor. After trying to track it down for a while I finally posted the question in the forum. Let's see what comes back. 
For the second part I returned to the Meditation Myth Buster 2.0 skill that I had temporarily abandoned due to not being able to solve the bugs. 

**Learnings:**
Activated a linter a few days ago that I hadn't used on the Meditation Myth Buster code. Got Alexa to successfully access the Welcome Message after fixing some of the issues and changing up the language.js and the language variable, something that hadn't worked last time I worked on this skill. However now it seems to have issues accessing the actual data. 

**Thoughts:** 
There is a possibility that something in the linked files is wrong. I should check that next time I work on the chat bot. 
Yes debugged at least parts of the problem that I spent days trying to debug before taking a detour with other projects. I do feel that my other activities taught me things that are helpful now and should help me move forward with this skill. I feel prepared and somewhat ready to try to move forward with this skill. 

**Link to work:** 
I didn't do any new commits since I didn't want to have wrong code in my chat bot. 
Meditation Myth Buster 2.0: https://github.com/AlexaforMuggles/Meditation-Myth-Buster-2.0

### R1D23
**Today's Progress:** 
Tried to debug Meditation Myth Buster but made no progress at all. 

**Learnings:**
I tried out different ways to log things and checked the outcome in CloudWatch. Some of the suggestions that I had written down created actual code errors. I captured what lines of logging code led to what kind of log. 

**Thoughts:** 
I truly do not understand fully enough how data is accessed across different files and why it sometimes just reads the message title or the content and sometimes the expected message. 

**Link to work:** 
No commits since I didn't debug anything that didn't already work yesterday. 

### R1D24
**Today's Progress:** 
Went through the new features tutorial to understand newly released Alexa SDK features. 

**Learnings:**
* When you click on certification it will tell you info such as when a skill was certified as well as the certification history. 
* In the certification box there is a country availability details drop-down
* In test tab you can test either the development version or the live version
* It’s not possible to swap invocation names of published skills
* It is possible to withdraw a skill from submission if you find a bug after submitting
* Alexa-hosted skills can be done within the developer console (it creates a hello world skill). You can change the code in the code tab. The code is not hosted on your own account and you are not paying  for it, Amazon is. It has a default region that cannot be changed.
* Click on interfaces and activate Auto Delegation —> this means you don’t have to code dialog delegation into your index.js anymore. You still have to make the slots required for this to work.
* If you click on an intent there is a new button called utterance profiler. You can insert something there and then it will give you info such as what intent was chosen, what slots were used, which slots are filled or not and etc. What is nice is that you can test what is possible and what doesn’t work without having to go through the testing tool and playing the whole thing over and over again

**Thoughts:** 
Most excited about the Auto Delegation feature. It will be much simpler not having to code that feature into every handler. 

**Link to work:** 
Nada

### R1D25
**Today's Progress:** 
Played around with the sample code of the reminder API. 

**Learnings:**
Test console does not work for reminder app
If you use your own device use a unique invocation name, otherwise it will just read your real reminders
The permissions tab is a great way to introduce simple advanced features without needing to add additional code. 
Granting the permission was not very intuitive. Initially I thought it was not possible in my locale but I eventually managed to set the reminder permission.  
Error 401 is an authorization error. 

**Thoughts:** 
It doesn't seem like the user has the power to actually create a reminder. Rather they pick one that is offered. Not sure yet if that's just a feature of the demo version or if that is actually the case. 

**Link to work:** 
Reminders folder in Deep Dives: https://github.com/AlexaforMuggles/deep-dives/tree/master/Reminder

### R1D26
**Today's Progress:** 
50-50 day: continued with the Node course, specifically event acknowledgements and debugging. Then I worked on a new Alexa skill that is based on Our World in Data.

**Learnings:**
My bug was due to something I did ten days ago. It's weird that lots of results still turned out as expected but that it came to bite me so much later. Also it was a fairly simple mistake but I didn't look in the right file: arguments were missing in my function in the message.js file. 

**Thoughts:** 
Created a references.md file and am dumping all the answers as well as the references there. Better safe than sorry. 
Also it occurred to me that I could do a code deep dive and focus on the NodeJS features that are used on each line. I am very hazy on the details and it would help thinking about what functions, methods, libraries etc. are being used. 

**Link to work:** 
Will publish once the skill is certified. 

### R1D27
**Today's Progress:** 


**Learnings:**


**Thoughts:** 


**Link to work:** 

### R1D28
**Today's Progress:** 


**Learnings:**


**Thoughts:** 


**Link to work:** 

### R1D29
**Today's Progress:** 


**Learnings:**


**Thoughts:** 


**Link to work:** 