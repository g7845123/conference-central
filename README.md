# Overview

This is a project for [Full Stack Web Developer Nanodegree](https://www.udacity.com/course/nd004) provided by [Udacity](https://www.udacity.com). 

In this project, I developed a cloud-based API server to support a provided conference organization application that exists on the web. The API supports the following functionality found within the app: user authentication, user profiles, conference information and various manners in which to query the data.

# Live demo

App ID: cogent-tree-94912

Live demo is available [here](https://cogent-tree-94912.appspot.com/)

All APIs can be tested via Google APIs Explorer [here](https://cogent-tree-94912.appspot.com/_ah/api/explorer) 

# Responses required by Udacity

> Explain in a couple of paragraphs your design choices for session and speaker implementation.

I implement session as a child of the conference, considering the fact that one conference can have multiple sessions while a session can only belong to a specific conference. 

In Session object, I use `duration` to specify the session duration in minutes, thus IntegerProperty is the proper choice. I also use KeyProperty `speakerKey` to store the speaker key. It's natural to use DateProperty and TimeProperty for `date` and `startTime`, respectively. Other Session properties, including name, highlights and typeOfSession are string, thus I choose StringProperty.

I implement speaker as a full fledged entity instead of a string for two reasons. First, this kind of design makes the speaker entity extendable: speaker properties such as title, institution, field of expert, can all be implemented with just a few lines of code change. Second, the speaker is reusable: one speaker can give lectures in multiple sessions and conferences. 

In Speaker object, both of the two properties: name and title, are string. Thus I use StringProperty for them. 

> Think about other types of queries that would be useful for this application. Describe the purpose of 2 new queries and write the code that would perform them.

* querySessionByTimeInterval(lowerBond, upperBond) - Query sessions that start within the given time interval. Both lowerBond and upperBond are of the form `HH:MM` specifying time interval. 
* querySessionByDuration(lowerBond, upperBond) - Query sessions that lasts in the given interval. Both lowerBond and upperBond are integer specifying the duration. 

> Let’s say that you don't like workshops and you don't like sessions after 7 pm. How would you handle a query for all non-workshop sessions before 7 pm? What is the problem for implementing this query? What ways to solve it did you think of?

If this query is implement directly, there would be an error because inequality filters can not be applied on multiple properties. I solve this problem by first filter the result using startTime condition, then filter the typeOfSession using list comprehension in Python. However, this method use Python code to filter the result, which may encounter efficiency issue. 

# Setup Instructions

1. Update the value of `application` in `app.yaml` to the app ID you have registered in the App Engine admin console and would like to use to host your instance of this sample.
1. Update the values at the top of `settings.py` to reflect the respective client IDs you have registered in the [Developer Console](https://console.developers.google.com/).
1. Update the value of CLIENT_ID in `static/js/app.js` to the Web client ID
1. (Optional) Mark the configuration files as unchanged as follows:
   `$ git update-index --assume-unchanged app.yaml settings.py static/js/app.js`
1. Run the app with the devserver using `dev_appserver.py DIR`, and ensure it's running by visiting your local server's address (by default [localhost:8080](https://localhost:8080/).)
1. (Optional) Generate your client library(ies) with [the endpoints tool](https://developers.google.com/appengine/docs/python/endpoints/endpoints_tool).
1. Deploy your application.

# References

All Web sites, books, forums, blog posts, github repositories etc. that I referred to or used are listed in `references.txt`. 
