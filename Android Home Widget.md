
# Android (Home screen) Widgets
Home screen widgets are broadcast receivers which provide interactive components. They are primarily used on the Android home screen. They typically display some kind of data and allow the user to perform actions with them.

Widget use RemoteViews to create their user interface. A RemoteView can be executed by another process with the same permissions as the original application. This way the widget runs with the permissions of its defining application.

The user interface for a Widget is defined by a broadcast receiver. This receiver inflates its layout into an object of type RemoteViews. This object is delivered to Android, which hands it over the home screen application.

