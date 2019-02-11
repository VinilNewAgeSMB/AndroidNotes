### Room

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
    


**What is the DAO?**
In the DAO (data access object), you specify SQL queries and associate them with method calls.
The DAO must be an interface or abstract class.
1.  Create a new Interface and call it  `WordDao`.
2. Annotate the class with  `@Dao`  to identify it as a DAO class for Room.
3. Declare a method to insert one word:  `void insert(Word word);`
4. Annotate the method with  `@Insert`. You don't have to provide any SQL! (There are also  `@Delete`  and  `@Update`  annotations for deleting and updating a row, but you are not using them in this app.)
5. Declare a method to delete all the words:  `void deleteAll();`.
6. There is no convenience annotation for deleting multiple entities, so annotate the method with the generic  `@Query`.
7. Create a method to get all the words:  `getAllWords();`.  
    Have the method return a  `List`  of  `Words`.  
    **`List<Word> getAllWords();`**




        import android.arch.persistence.room.Dao;  
        import android.arch.persistence.room.Insert;  
        import android.arch.persistence.room.Query;  
          
        import java.util.ArrayList;  
          
        @Dao  
        public interface WordDao {  
          
            @Insert  
          void insert(Word word);  
          
          @Query("DELETE FROM word_table")  
            void deleteAll();  
          
          @Query("SELECT * FROM word_table order by word ASC")  
            ArrayList<Word> getAllWords();  
        }
