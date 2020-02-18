# Factory Method

## Define a interface for creating an object, but let subclasses decide wich class to instantiate. Factory method lets a class defer instantiation to subclasses.

### Entrypoint
```dart
void main() {
  SQLDBHelper helper = SQLDBHelper();
  helper.connectDB();
}
```

### SQLDBHelper
```dart
class SQLDBHelper extends DBHelper{
  connectDB(){
    this.connect(SQLConnect());
  }
}
```

### MongoDBHelper
```dart
class MongoDBHelper extends DBHelper{
  connectDB(){
    this.connect(MongoConnect());
  }
}
```

### DBHelper
```dart
abstract class DBHelper{
  connect(IConnect interface){
    interface.connect();
  }
}
```

### IConnect
```dart
abstract class IConnect{
  connect();
}
```

### SQLConnect
```dart
class SQLConnect implements IConnect{
  connect(){
    print('SQLConnect');
  }
}
```

### MongoConnect
```dart
class MongoConnect implements IConnect{
  connect(){
    print('MongoConnect');
  }
}
```
