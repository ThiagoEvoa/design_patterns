# Facade

## Definition
### Facade is a structural design pattern that provides a simplified (but limited) interface to a complex system of classes, library or framework.

## Aplicability
### While Facade decreases the overall complexity of the application, it also helps to move unwanted dependencies to one place.

### Entrypoint
```dart
void main() {
 VideoConversionFacade conversionFacade = VideoConversionFacade();
  conversionFacade.convertVideo('test.mp4');
}

class VideoFile{
  String _name;
  String _codecType;
  
  VideoFile(String videoName){
    _name = videoName;
    _codecType = _name.substring(_name.indexOf('.') + 1);
  }
  
  getName(){
    return _name;
  }
  
  getCodecType(){
    return _codecType;
  }
}
```

### ICodec
```dart
abstract class ICodec{
  
}
```

### MPEG4CompressionCodec
```dart
class MPEG4CompressionCodec implements ICodec{
  String type = 'mp4';
}
```

### OggCompressionCodec
```dart
class OggCompressionCodec implements ICodec{
  String type = 'ogg';
}
```

### CodecFactory
```dart
class CodecFactory{
  static ICodec extract(VideoFile videoFile){
    String type = videoFile.getCodecType();
    
    if(type == 'mp4'){
      return MPEG4CompressionCodec();
    }else{
      return OggCompressionCodec();
    }
  }
}
```

### VideoConversionFacade
```dart
class VideoConversionFacade{
  convertVideo(String fileName){
    VideoFile file = VideoFile(fileName);
    ICodec codec = CodecFactory.extract(file);
    print(codec);
  }
}
```
