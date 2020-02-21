# Adapter

## Definition
### Adapter is a structural design pattern, which allows incompatible objects to collaborate.

## Aplicability
### The Adapter pattern is pretty common in Java code. It’s very often used in systems based on some legacy code. In such cases, Adapters make legacy code with modern classes.

### Entrypoint
```dart
void main() {
  RoundHole roundHole = RoundHole(5);
  RoundPeg roundPeg = RoundPeg(5);
  
  if(roundHole.fits(roundPeg)){
    print('Fits');
  }
  
  SquarePeg smallSquarePeg = SquarePeg(2);
  SquarePeg largeSquarePeg = SquarePeg(20);
  
  SquarePegAdapter smallSquarePegAdapter = SquarePegAdapter(smallSquarePeg);
  SquarePegAdapter largeSquarePegAdapter = SquarePegAdapter(largeSquarePeg);
  
  if(roundHole.fits(smallSquarePegAdapter)){
    print('SquarePeg fits');
  }
  
  if(!roundHole.fits(largeSquarePegAdapter)){
    print('SquarePeg does not fit');
  }
}
```

### RoundHole
```dart
class RoundHole{
  double _radius;
  
  RoundHole(double radius){
    this._radius = radius;
  }
  
  double getRadius(){
    return _radius;
  }
  
  bool fits(RoundPeg roundPeg){
    return this.getRadius() >= roundPeg.getRadius();
  }
}
```

### RoundPeg
```dart
class RoundPeg{
  double _radius;
  
  RoundPeg(double radius){
    this._radius = radius;
  }
  
  double getRadius(){
    return _radius;
  }
}
```

### SquarePeg
```dart
class SquarePeg{
  double _width;
  
  SquarePeg(double width){
    this._width = width;
  }
  
  double getWidth(){
    return _width;
  }
  
  double getSquare(){
    return this._width * 2;
  }
}
```

### SquarePegAdapter
```dart
class SquarePegAdapter extends RoundPeg{
  SquarePeg _squarePeg;
  
  SquarePegAdapter(SquarePeg squarePeg): super(squarePeg.getWidth()){
    this._squarePeg = squarePeg;
  }
  
  double getRadius(){
    return ((_squarePeg.getWidth() / 2) * 2);
  }
}
```
