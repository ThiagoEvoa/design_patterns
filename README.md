# Factory Method

## Define a interface for creating an object, but let subclasses decide wich class to instantiate. Factory method lets a class defer instantiation to subclasses.

### Entrypoint
```java
void main() {
  SQLDBHelper helper = SQLDBHelper();
  helper.connectDB();
}
```

### SQLDBHelper
```java
class SQLDBHelper extends DBHelper{
  connectDB(){
    this.connect(SQLConnect());
  }
}
```

### MongoDBHelper
```java
class MongoDBHelper extends DBHelper{
  connectDB(){
    this.connect(MongoConnect());
  }
}
```

### DBHelper
```java
abstract class DBHelper{
  connect(IConnect interface){
    interface.connect();
  }
}
```

### IConnect
```java
interface IConnect{
  connect();
}
```

### SQLConnect
```java
class SQLConnect implements IConnect{
  connect(){
    print('SQLConnect');
  }
}
```

### MongoConnect
```java
class MongoConnect implements IConnect{
  connect(){
    print('MongoConnect');
  }
}
```
