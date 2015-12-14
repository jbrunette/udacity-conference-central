Conference Central
=====================================
The Conference Central app allows you to create and manage conferences.  Users can
register to attend conferences and view conference information, all with their Google account.

Usage
===========================================================
1. Clone the following Github repository to your local machine: https://github.com/jbrunette/udacity-conference-central
2. Update the value of application in app.yaml to the app ID you have registered in the App Engine admin console and would like to use to host your instance of this sample.
3. Update the values at the top of settings.py to reflect the respective client IDs you have registered in the Developer Console.
4. Update the value of CLIENT_ID in static/js/app.js to the Web client ID
5. Run the app with the devserver using dev_appserver.py DIR, and ensure it's running by visiting your local server's address (by default localhost:8080.)
6. Deploy your application.
7. Access the front end application by visiting https://<your app engine app id>.appspot.com/
7. Access the backend API explorer to test API methods by accessing https://<your app engine app id>.appspot.com/_ah/api/explorer

Task 1 - Sessions and Speakers
===========================================================

Sessions
=================================================
Sessions are implemented very much like conferences.  A new Session model was created to store the Session
data, including conference its associated with, name, type, etc.

Sessions are linked to the conference they're associated with by conference name and by the conference's
key within the Session itself.  When accessed, the conference's web safe key is provided to make it easy to
request the conference the session was created for.

The following properties and datatypes were used in the creation of the Session model:

    conferenceName  = ndb.StringProperty(required=True)
    name            = ndb.StringProperty(required=True)
    highlights      = ndb.StringProperty()
    speaker         = ndb.StringProperty()
    duration        = ndb.IntegerProperty()
    typeOfSession   = ndb.StringProperty()
    date            = ndb.DateProperty()
    startTime       = ndb.IntegerProperty()
    websafeConferenceKey = ndb.StringProperty()

conferenceName, name, highlights, speaker, typeOfSession and websafeConferenceKey are StringProperties as their values are typically
plain text, not requiring any filtering like greater than, less than, etc.

duration is an IntegerProperty, as it represents the number of minutes the session will last, making it easy to
filter sessions of various lengths.

date is a DateProperty, making it easy to filter based on the session's date.

Speakers
==================================================
Speakers are simple a string property of the Session model.  When a session is created, the session's "speaker"
is stored as a freeform string within the Session record, and when requested is returned as a string.

Task 2 - Session Wishlist
===========================================================
The session wishlist is stored as a part of the user's profile, as multi-item property of the Profile model.
It stores the keys of the sessions the user is interested in.

Task 3 - Additional Queries
===========================================================
getSessionWishlistUsers(websafeSessionKey) - Returns user Profiles that have the provided session in their
wishlist

getUsersAttendingConference(websafeConferenceKey) - Returns user Profiles for those who have registered
for provided conference

Task 3 - Query Problem
===========================================================
Because queries cannot include inequality comparisions on more than one property, a single query itself will
not be enable to satisfy this need.

One solution would be to perform a query, filtering by startTime to limit the results to those that are before 7pm.
Then, loop over the resulting record list in python, checking for those sessions that are not workshops.  Store
the ones that aren't workships in a list and return them in a SessionForms message.

