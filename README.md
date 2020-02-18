# Decorator

## Attach additional responsibilities to an  object dynamically.

### Entrypoint
```dart
void main() {
  ITicket iTicket = BasicTicket();
  bool palace = true;
  bool train = false;
  
  if(palace){
    iTicket = PalaceDecorator(iTicket);
  }else if(train){
    iTicket = TrainDecorator(iTicket);
  }
  
  TicketProcessor().printTicketPrice(iTicket);
}
```

### TicketProcessor
```dart
class TicketProcessor{
  printTicketPrice(ITicket interface){
    print(interface.getTicketCost().toString());
  }
}
```

### ITicket
```dart
abstract class ITicket{
  double getTicketCost();
}
```

### IBonusCalculator
```dart
abstract class IBonusCalculator{
  calculateBonus();
}
```

### BasicTicket
```dart
class BasicTicket implements ITicket{
  double getTicketCost(){
    return 5.0;
  }
}
```

### TicketDecorator
```dart
abstract class TicketDecorator implements ITicket{
  ITicket iTicket;
  
  TicketDecorator(ITicket interface){
    this.iTicket = interface;
  }
  
  double getTicketCost(){
    return BasicTicket().getTicketCost();
  }
}
```

### PalaceDecorator
```dart
class PalaceDecorator extends TicketDecorator{
  ITicket iTicket;
  
  PalaceDecorator(ITicket interface) : super(interface){
    iTicket = interface;
  }
  
  double getTicketCost(){
    return iTicket.getTicketCost() + 5;
  }
}
```

### TrainDecorator
```dart
class TrainDecorator extends TicketDecorator{
  ITicket iTicket;
  
  TrainDecorator(ITicket interface) : super(interface){
    iTicket = interface;
  }
  
  double getTicketCost(){
    return iTicket.getTicketCost() + 10;
  }
}
```
