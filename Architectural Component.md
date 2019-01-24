**Entity:** Is an annotated class that describes a database table.

**SQLite database:** On the device, data is stored in an SQLite database.

**DAO:** Data access object. A mapping of SQL queries to functions.When you use a DAO, you call the methods, and Room takes care of the rest.

**Room database:** Database layer on top of SQLite database that takes care of uninterested tasks that you used to handle with an `SQLiteOpenHelper`. The Room database uses the DAO to issue queries to the SQLite database.

**Repository:** A class that you are using for managing multiple data sources.

**View Model:** Provides data to the UI. Acts as a communication center between the Repository and the UI.

**LiveData:** A data holder class that can be [observed](https://en.wikipedia.org/wiki/Observer_pattern). Always holds/caches latest version of data. Notifies its observers when the data has changed. `LiveData` is lifecycle aware.

The data for this app is words, and each word is an Entity. Create a class called Word that describes a word Entity


    import android.arch.persistence.room.ColumnInfo;  
    import android.arch.persistence.room.Entity;  
    import android.arch.persistence.room.PrimaryKey;  
    import android.support.annotation.NonNull;  
      
    @Entity(tableName = "word_table")  
    public class Word {        
      @PrimaryKey  
      @NonNull
      @ColumnInfo(name = "word")  
      private String mWord; 
      
      public Word(String mWord) {  
            this.mWord = mWord;  
      }        
      
      public String getMWord() {  
            return mWord;  
      }  
      
    }
 
 -   `@Entity(tableName =` **`"word_table"`**`)`  
    Each  `@Entity`  class represents an entity in a table. Annotate your class declaration to indicate that it's an entity. Specify the name of the table if you want it to be different from the name of the class.
-   `@PrimaryKey`  
    Every entity needs a primary key. To keep things simple, each word acts as its own primary key.
-   `@NonNull`  
    Denotes that a parameter, field, or method return value can never be null.
-   `@ColumnInfo(name =` **`"word"`**`)`  
    Specify the name of the column in the table if you want it to be different from the name of the member variable.
-   Every field that's stored in the database needs to be either public or have a "getter" method. This sample provides a  `getWord()`  method.
    
