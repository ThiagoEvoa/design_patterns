# Decorator

## Definition.
### Decorator is a Conceptual pattern that allows adding new behaviors to objects dynamically by placing them inside special wrapper objects.

## Aplicability
### Using decorators you can wrap objects countless number of times since both target objects and decorators follow the same interface. The resulting object will get a stacking behavior of all wrappers.

### Entrypoint
```dart
void main() {
  String anything = 'blá';
  
  DataSourceDecorator dataSourceDecorator = DataSourceDecorator(EncryptionDecorator(FileDataSource('.txt')));
  dataSourceDecorator.writeData(anything);

  IDataSource iDataSource = FileDataSource('.txt');
 
  print(iDataSource.readData());
  print(dataSourceDecorator.readData());
}
```

### IDataSource
```dart
abstract class IDataSource{
  writeData(String data);
  String readData();
}
```

### FileDataSource
```dart
class FileDataSource implements IDataSource{
  String _name;
  
  FileDataSource(String name){
    this._name = name;
  }
  
  writeData(String data){
    print('FileDataSource writeData');
  }
  
  String readData(){
    return 'FileDataSource readData';
  }
}
```

### DataSourceDecorator
```dart
class DataSourceDecorator implements IDataSource{
  IDataSource _iDataSource;
  
  DataSourceDecorator(IDataSource iDataSource){
    this._iDataSource = iDataSource;
  }
  
  writeData(String data){
    _iDataSource.writeData(data);
  }
  
  String readData(){
    return _iDataSource.readData();
  }
}
```

### EncryptionDecorator
```dart
class EncryptionDecorator extends DataSourceDecorator{
  EncryptionDecorator(IDataSource iDataSource) : super(iDataSource);
  
  writeData(String data){
    super.writeData(data);
  }
  
  String readData(){
    return decode(super.readData());
  }
  
  String encode(String data){
    return data;
  }
  
  String decode(String data){
    return data;
  }
}
```

### CompressionDecorator
```dart
class CompressionDecorator extends DataSourceDecorator{
  int _compressLevel = 6;
  
  CompressionDecorator(IDataSource iDataSource): super(iDataSource);
  
  getCompressLevel(){
    return _compressLevel;
  }
  
  setCompressLevel(int compressLevel){
    this._compressLevel = compressLevel;
  }
  
  writeData(String data){
    super.writeData(compress(data));
  }
  
  String readData(){
    return decompress(super.readData());
  }
  
  String compress(String data){
    return data;
  }
  
  String decompress(String data){
    return data;
  }
}
```
