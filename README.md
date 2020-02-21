# Strategy

## Definition
### Strategy is a behavioral design pattern that turns a set of behaviors into objects and makes them interchangeable inside original context object.

## Aplicability
### The original object, called context, holds a reference to a strategy object and delegates it executing the behavior. In order to change the way the context performs its work, other objects may replace the currently linked strategy object with another one.

### Entrypoint
```dart
void main() {
  bool isCreditCard = true;
  PayStrategy payStrategy;
  
  if(isCreditCard)
    payStrategy = PayByCreditCard();
  PayByPayPal();
  
  payStrategy.pay(2000);
  payStrategy.collectPaymentDetails();
}
```

### FinanceCalculation
```dart
class FinanceCalculation extends EmployeeBenefits{
  
  calculateBonusByGrade(){
    this.setBonusCalculator(BonusCalculatorGrade());
    this.calculateBonus();
  }
  
  calculateBonusByMerit(){
    this.setBonusCalculator(BonusCalculatorMerit());
    this.calculateBonus();
  }
}
```

### PayStrategy
```dart
abstract class PayStrategy{
  pay(double paymentAmount);
  collectPaymentDetails();
}
```

### IBonusCalculator
```dart
abstract class IBonusCalculator{
  calculateBonus();
}
```

### PayByPayPal
```dart
class PayByPayPal implements PayStrategy{
  pay(double paymentAmount){
    print('Ammount: $paymentAmount');
  }
  
  collectPaymentDetails(){
    print('Payment details: payed with paypal');
  }
}
```

### PayByCreditCard
```dart
class PayByCreditCard implements PayStrategy{
  pay(double paymentAmount){
    print('Ammount: $paymentAmount');
  }
  
  collectPaymentDetails(){
    print('Payment details: payed with creditcard');    
  }
}
```

