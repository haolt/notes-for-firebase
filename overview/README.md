# Overview

🔗 *<u>[Notes for Firebase](../README.md)</u>/<u>[Overview](#)</u>*

## ■ Info.
A backend platform for building Web, Android and IOS applications:
- `Real-time Database` − Firebase supports JSON data and all users connected to it receive live updates after every change.
- `Authentication` − We can use anonymous, password or different social authentications.
- `Hosting` − The applications can be deployed over secured connection to Firebase servers.

&nbsp;
## ■ Firebase Limitations
Firebase free plan is limited to 50 Connections and 100 MB of storage.

&nbsp;
## ■ Environment Setup	
`NodeJS`, `npm`.

&nbsp;
## ■ Firebase database  	
Firebase database represents `JSON objects`.

**Notes:**
*Firebase does not support Arrays directly, but it creates a list of objects with integers as key names.*

*The reason for not using arrays is because Firebase acts as a real time database and if a couple of users were to manipulate arrays at the same time, the result could be problematic since array indexes are constantly changing.*
