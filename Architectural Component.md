**Entity:** Is an annotated class that describes a database table.

**SQLite database:** On the device, data is stored in an SQLite database.

**DAO:** Data access object. A mapping of SQL queries to functions.When you use a DAO, you call the methods, and Room takes care of the rest.

**Room database:** Database layer on top of SQLite database that takes care of uninterested tasks that you used to handle with an `SQLiteOpenHelper`. The Room database uses the DAO to issue queries to the SQLite database.

**Repository:** A class that you are using for managing multiple data sources.

**View Model:** Provides data to the UI. Acts as a communication center between the Repository and the UI.

**LiveData:** A data holder class that can be [observed](https://en.wikipedia.org/wiki/Observer_pattern). Always holds/caches latest version of data. Notifies its observers when the data has changed. `LiveData` is lifecycle aware.
