# State

## Definition
### State is a behavioral design pattern that allows an object to change the behavior when its internal state changes.

## Aplicability
### The pattern extracts state-related behaviors into separate state classes and forces the original object to delegate the work to an instance of these classes, instead of acting on its own.

### Entrypoint
```dart
void main() {
  Player player = Player();
  
  print(player.getState().onPlay());
  print(player.getState().onNext());
  print(player.getState().onPrevious());
  print(player.getState().onLock());
  print(player.getState().onPlay());
}
```

### State
```dart
abstract class State{
  Player player;
  
  State(Player player){
    this.player = player;
  }
  
  String onLock();
  String onPlay();
  String onNext();
  String onPrevious();
}
```

### LockState
```dart
class LockState extends State{
  LockState(Player player): super(player){
    player.setPlaying(false);
  }
  
  String onLock(){
    if(player.isPlaying()){
      player.changeState(ReadyState(player));
      return 'Stop playing';
    }else{
      return 'Locked';
    }
  }
  
  String onPlay(){
    player.changeState(ReadyState(player));
    return 'Ready';
  }
  
  String onNext() {
    return 'Locked';
  }
  
  String onPrevious(){
    return 'Locked';
  }
}
```

### ReadyState
```dart
class ReadyState extends State{
  ReadyState(Player player): super(player);
  
  String onLock(){
    player.changeState(LockState(player));
    return 'Locked';
  }
  
  String onPlay(){
    String action = player.startPlayback();
    player.changeState(PlayingState(player));
    return action;
  }
  
  String onNext(){
    return 'Locked';
  }
  
  String onPrevious(){
    return 'Locked';
  }
}
```

### PlayingState
```dart
class PlayingState extends State{
  PlayingState(Player player): super(player);
  
  String onLock(){
    player.changeState(LockState(player));
    player.setCurrentTrackAfterStop();
    return 'Stop playing';
  }
  
  String onPlay(){
    player.changeState(ReadyState(player));
    return 'Paused';
  }
  
  String onNext(){
    return player.nextTrack();
  }
  
  String onPrevious(){
    return player.previousTrack();
  }
}
```

### Player
```dart
class Player{
  State _state;
  bool _playing = false;
  List _playList = [];
  int _currentTrack = 0;
  
  Player(){
    this._state = ReadyState(this);
    setPlaying(true);
    for(int i = 1; i <= 12; i++){
      _playList.add(i);
    }
  }
  
  changeState(State state){
    this._state = state;
  }
  
  State getState(){
    return _state;
  }
  
  setPlaying(bool playing){
    this._playing = playing;
  }
  
  bool isPlaying(){
    return _playing;
  }
  
  String startPlayback(){
    return 'Playing ${_playList[_currentTrack]}';
  }
  
  String nextTrack(){
    _currentTrack++;
    
    if(_currentTrack > _playList.length - 1){
      _currentTrack = 0;
    }
    
    return 'Playing ${_playList[_currentTrack]}';
  }
  
  String previousTrack(){
    _currentTrack--;
    
    if(_currentTrack < 0){
      _currentTrack = _playList.length -1;
    }
    
    return 'Playing ${_playList[_currentTrack]}';
  }
  
  setCurrentTrackAfterStop(){
    this._currentTrack = 0;
  }
}
```

