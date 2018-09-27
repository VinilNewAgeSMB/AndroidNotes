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
The receiver can get a label and icon assigned. These are used in the list of available widgets in the Android launcher.

You also specify the meta-data for the widget via the ```android:name="android.appwidget.provider"``` attribute. 
```xml
<?xml version="1.0" encoding="utf-8"?>
<appwidget-provider xmlns:android="http://schemas.android.com/apk/res/android"
    android:initialLayout="@layout/widget_layout"
    android:minHeight="72dp"
    android:minWidth="146dp"
    android:updatePeriodMillis="1800000" >
</appwidget-provider>
```
The configuration file referred by this metadata contains the configuration settings for the widget. It contains, for example, the update interface, the size and the initial layout of the widget.

# Available views and layouts
Below Android 3.0 you can use the FrameLayout, LinearLayout and RelativeLayout classes. As views you can use AnalogClock, Button, Chromometer, ImageButton, ImageView, ProgressBar and TextView.

As of Android 3.0 more views are available: GridView, ListView, StackView, ViewFlipper and AdapterViewFlipper. These adapter views require that you define a collection view widget

The only interaction that is possible with the views of a widget is via an OnClickListener event. This OnClickListener can be registered on a widget and is triggered by the user.

## AppWidgetProvider
Your BroadcastReceiver implementation typically extends the ```AppWidgetProvider``` class.

The ```AppWidgetProvider``` class implements the ```onReceive()``` method, extracts the required information and calls the following widget life cycle methods.

As you can add several instances of a widget to the home screen, you have life cycle methods ```onEnabled()``` and ```onDisabled()``` which are called only for the first instance added and removed to the home screen and others which are called for every instance of your widget.

|Method   |Description   |
| ------------ | ------------ |
| onEnabled()  | Called the first time an instance of your widget is added to the home screen.  |
| onDisabled()  | Called once the last instance of your widget is removed from the home screen. |
| onUpdate()  | Called for every update of the widget. Contains the ids of appWidgetIds for which an update is needed. Note that this may be all of the AppWidget instances for this provider, or just a subset of them, as stated in the method’s JavaDoc. For example, if more than one widget is added to the home screen, only the last one changes (until reinstall).  |
| onDeleted() | Widget instance is removed from the home screen. |
