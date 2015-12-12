Conference Central
=====================================
The Conference Central app allows you to create and manage conferences.  Users can
register to attend conferences and view conference information, all with their Google account.

Usage
=====================================
1. View the Github repository for the project at https://github.com/jbrunette/udacity-conference-central
2. Access the app's API Explorer by going to https://udacity-conference-app-jb.appspot.com/_ah/api/explorer

Task 1 - Sessions and Speakers
======================================
Sessions are implemented very much like conferences.  A new Session model was created to store the Session
data, including conference its associated with, name, type, etc.

Speakers are simple a string property of the Session model.

Task 2 - Session Wishlist
======================================
The session wishlist is stored as a part of the user's profile, as multi-item property of the Profile model.
It stores the keys of the sessions the user is interested in.

Task 3 - Additional Queries
=======================================
getSessionWishlistUsers(websafeSessionKey) - Returns user Profiles that have the provided session in their
wishlist

getUsersAttendingConference(websafeConferenceKey) - Returns user Profiles for those who have registered
for provided conference

Task 3 - Query Problem
=======================================
The query would filter Sessions based on the startTime property and the typeOfSession property, ensuring
that startTime is less than 7pm and typeOfSession is not "workshop".

