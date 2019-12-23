# RoomApp  

<p float="left">
  <img src="https://www.techotopia.com/images/0/04/Room_architecture_diagram.png" height="340" width="400" />
  <img src="https://coderain.ir/wp-content/uploads/1_xK4WW-i__up51vXdXsCudA.png"  height="340" width="400" /> 
</p>


The **[Room](https://developer.android.com/training/data-storage/room)** persistence library provides an abstraction layer over SQLite to allow for more robust database access while harnessing the full power of SQLite.  
The library helps you create a cache of your app's data on a device that's running your app. This cache, which serves as your app's single source of truth, allows users to view a consistent copy of key information within your app, regardless of whether users have an internet connection.  

**Adding Dependencies**  
Inside app level build.gradle file add the following dependencies.  

```gradle
   //room
    implementation "android.arch.persistence.room:runtime:$room_version"
    annotationProcessor "android.arch.persistence.room:compiler:$room_version"
    testImplementation "android.arch.persistence.room:testing:$room_version"
```

**Components of Room**  

We have 3 components of room.  
- **Entity**: Instead of creating the SQLite table, we will create the Entity. Entity is nothing but a model class annotated with `@Entity`. The variables of this class is our columns, and the class is our table.  

```java
@Entity
public class User {
    @PrimaryKey
    public int uid;

    @ColumnInfo(name = "first_name")
    public String firstName;

    @ColumnInfo(name = "last_name")
    public String lastName;
}
```

- **Database**: It is an abstract class where we define all our entities.  
```java
@Database(entities = {Task.class}, version = 1)
public abstract class AppDatabase extends RoomDatabase {
    public abstract TaskDao taskDao();
}
```

- **DAO**: Stands for Data Access Object. It is an interface that defines all the operations that we need to perform in our database.    
```java
@Dao
public interface TaskDao {
 
    @Query("SELECT * FROM task")
    List<Task> getAll();
 
    @Insert
    void insert(Task task);
 
    @Delete
    void delete(Task task);
 
    @Update
    void update(Task task);
}
```


