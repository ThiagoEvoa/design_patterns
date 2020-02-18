# State

## Allow an object to alter its behavior when its internal state changes. The object will appear to change its class. 

### Entrypoint
```dart
void main() {
  Account account = Account(state: ActiveState());
  account.issueBook();
  
  account.onTimeElapsed();
  print(account.getState());
  account.issueBook();
}
```

### Account
```dart
class Account{
  static AccountState currentState;
  
  Account({AccountState state}){
    currentState = state;
  }
  
  setState(AccountState state){
    currentState = state;
  }
  
  getState(){
    return currentState;
  }
  
  issueBook(){
    currentState.issueBook();
  }
  
  onTimeElapsed(){
   currentState.onTimeElapsed(); 
  }
}
```

### AccountState
```dart
abstract class AccountState{
  issueBook(){}
  onTimeElapsed(){}
}
```

### ActiveState
```dart
class ActiveState implements AccountState{
  issueBook(){
    print('ActiveState: issueBook');
  }
  
  onTimeElapsed(){
    print('ActiveState: onTimeElapsed');
    Account().setState(CancelledState());
  }
}
```

### CancelledState
```dart
class CancelledState implements AccountState{
  issueBook(){
    print('CancelledState: issueBook');
  }
  
  onTimeElapsed(){
    print('CancelledState: onTimeElapsed');
    Account().setState(ActiveState());
  }
}
```

