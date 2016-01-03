# README #

Conference Organization

### What is this repository for? ###

Conference Organization is a Google App Engine application written in Python that allows the user to organize conferences and sessions, using Google OAuth providers for authentication.
Once authenticated user can create conference and sessions, search and attend both.


### How do I get set up? ###

* Python (<3) is required. If you have Linux or Mac you should be good to go and you should skip to the next step, if you're on Windows get it from: http://ninite.com
* Clone the repository or simply download it as a zip file and unzip it on your pc
* Download and install Google App Engine for Python: https://cloud.google.com/appengine/downloads
* Start Google App Engine and choose File --> Add existing application
* Choose the folder where you cloned the repository
* Modify `application` in `app.yaml` to the your app ID
* Modify variables the beginning of `settings.py` according to your client IDs (set in Google Dev Console)
* Modify CLIENT_ID in `static/js/app.js` writing your Web client ID
* Start the app and open a web browser and visit: http://localhost:8090/_ah/api/explorer

### Tasks ###

Explain in a couple of paragraphs your design choices for session and speaker implementation:
To build my Session model I decided to use simple String Properties except for duration (integer), date(DateProperty) and startTime(TimeProperty).
I implemented my Sessions as children of Conference objects.
I choose this solution because it was the recommended one and also made perfect sense to me because it was clearly reproducing the relation between a Conference and its Sessions.
It also allowed me to explore the "parent" concept will be 100% useful in future.
This decision was based on the need of the simplest and fastest solution possible because my work is very demanding lately and the time I have for this course is everyday less.
Using String Properties allowed me to implement Session more or less easily without giving special care to data I was entering in any field.
This is also why my SessionForm is 100% made with StringFields and my Speaker implementation is simply adding the speaker name, as string, to the Session class.

Think about other types of queries that would be useful for this application. Describe the purpose of 2 new queries:
I prepared two very simple queries based on the model of the "getSessionsBySpeaker" one.
Those two query allows a user to find all the sessions searching for specific highlights in "getSessionByHighlight"
and to find all the sessions searching for a specific name in "getSessionByName"

The main problem to implement the requested query was that I was getting this error:
BadRequestError: Only one inequality filter per query is supported. Encountered both typeOfSession and startTime

Checking documentation I've read that Datastore doesn't permit filters on multiple fields.
That is why I decided to use an inequality filter on field typeOfSession to immediately find all sessions that have a type different from the one specified from the user.
Then I created an empty list and, with a simple python for loop I appended to the list only sessions compatible with the needed time check.
It was a quick solution that worked but I don't know if it is a good idea to use this kind of implementation in a very big database.

### Contribution guidelines ###

* If you have any idea or suggestion contact directly the Repo Owner

### Who do I talk to? ###

* ltpitt: Repo Owner
