# Android (Home screen) Widgets
Home screen widgets are broadcast receivers which provide interactive components. They are primarily used on the Android home screen. They typically display some kind of data and allow the user to perform actions with them.

Widget use RemoteViews to create their user interface. A RemoteView can be executed by another process with the same permissions as the original application. This way the widget runs with the permissions of its defining application.

The user interface for a Widget is defined by a broadcast receiver. This receiver inflates its layout into an object of type RemoteViews. This object is delivered to Android, which hands it over the home screen application.

## Steps to create a Widget
Widget creation need the following steps:
- Define a layout file
- Create an XML file (AppWidgetProviderInfo) which describes the properties of the widget, e.g. size or the fixed update frequency.
- Create a BroadcastReceiver which is used to build the user interface of the widget.
- Enter the Widget configuration in the AndroidManifest.xml file.
- Optional you can specify a configuration activity which is called once a new instance of the widget is added to the widget host.

## Widget size
Before Android 3.1 a widget always took a fixed amount of cells on the home screen. A cell is usually used to display the icon of one application. As a calculation rule you should define the size of the widget with the formula: ((Number of columns / rows) * 74) - 2. These are device independent pixels and the -2 is used to avoid rounding errors.

As of Android 3.1 a widget can be flexible in size, e.g., the user can make it larger or smaller. To enable this for widget, you can use the android:resizeMode="horizontal|vertical" attribute in the XML configuration file for the widget.

## Creating the Broadcast receiver for the widget
To register a widget, you create a broadcast receiver with an intent filter for the android.appwidget.action.APPWIDGET_UPDATE action.
```xml
<receiver
       android:icon="@drawable/icon"
       android:label="Example Widget"
       android:name="MyWidgetProvider" >
       <intent-filter >
            <action android:name="android.appwidget.action.APPWIDGET_UPDATE" />
       </intent-filter>

       <meta-data
          android:name="android.appwidget.provider"
          android:resource="@xml/widget_info" />
</receiver>
```
