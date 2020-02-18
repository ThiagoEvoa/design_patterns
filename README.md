# Strategy

## Define a family of algorithms, encapsulate each one, and make them interchangeable. Strategy lets the algorithm very independently from clients that use it.

### Entrypoint
```dart
void main() {
  FinanceCalculation calculation = new FinanceCalculation();
  calculation.calculateBonusByMerit();
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

### EmployeeBenefits
```dart
abstract class EmployeeBenefits{
  IBonusCalculator iBonusCalculator;
  
  setBonusCalculator(IBonusCalculator interface){
    iBonusCalculator = interface;
  }
  
  calculateBonus(){
    iBonusCalculator.calculateBonus();
  }
}
```

### IBonusCalculator
```dart
abstract class IBonusCalculator{
  calculateBonus();
}
```

### BonusCalculatorGrade
```dart
class BonusCalculatorGrade implements IBonusCalculator{
  calculateBonus(){
    print('BonusCalculatorGrade');
  }
}
```

### BonusCalculatorMerit
```dart
class BonusCalculatorMerit implements IBonusCalculator{
  calculateBonus(){
    print('BonusCalculatorMerit');
  }
}
```

