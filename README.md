# Factory Method

## Definition
### Define a interface for creating an object, but let subclasses decide wich class to instantiate. Factory method lets a class defer instantiation to subclasses.

## Aplicability
### 1) Use the Factory Method when you don't know beforehand the exact types and dependecies of the objects your code should work with.
### 2) Use the Factory Method when you want to provide users of your library or framework with a way to extends its internal components.


### Entrypoint
```dart
void main() {
  DBHelper _helper;
  bool _isMysql = true;
  
  if(_isMysql){
    _helper = MysqlDB();
  }else{
    _helper = MongoDB();
  }
  
  _helper.connect();
}
```

### IDBHelper
```dart
abstract class IDBHelper{
  connect();
}
```

### MysqlDBHelper
```dart
class MysqlDBHelper implements IDBHelper{
  connect(){
    print('Connect to Msql');
  }
}
```

### MongoDBHelper
```dart
class MongoDBHelper implements IDBHelper{
  connect(){
    print('Connect to Mongo');
  }
}
```

### IConnect
```dart
abstract class IConnect{
  connect();
}
```

### Helper
```dart
abstract class DBHelper{
  connect(){
    IDBHelper iDBHelper = connectDatabase();
    iDBHelper.connect();
  }
  
  IDBHelper connectDatabase();
}
```

### MysqlDB
```dart
class MysqlDB extends DBHelper{
  IDBHelper connectDatabase(){
    return MysqlDBHelper();
  }
}
```

### MongoDB
```dart
class MongoDB extends DBHelper{
  IDBHelper connectDatabase(){
    return MongoDBHelper();
  }
}
```
