# Adapter

## The adapter converts an interface of a class into another interface the client expects. Adapter lets classes work together that couldn't otherwise because of incompatible interfaces.

### Entrypoint
```dart
void main() {
  bool isAbcCalculator = true;
  Employee employee = Employee();
    employee.name = 'AbcBonusCalculator';
  
  if(isAbcCalculator){
    AbcBonusCalculator abcBonusCalculator = AbcBonusCalculator();
    Adapter adapter = Adapter(abcBonusCalculator);
    adapter.calculateBonus(employee);
  }else{
    FinanceCalculation calculation = new FinanceCalculation();
    calculation.calculateBonusByMerit(employee);  
  }  
}
```

### Employee
```dart
class Employee{
  String name;
}
```

### Adapter
```dart
class Adapter implements IBonusCalculator{
  AbcBonusCalculator abcBonusCalculator;
  
  Adapter(AbcBonusCalculator abcBonusCalculator){
    this.abcBonusCalculator = abcBonusCalculator;  
  }
  
  calculateBonus(Employee employee){
    abcBonusCalculator.computeBonus(employee);
  }
}
```

### AbcBonusCalculator
```dart
class AbcBonusCalculator{
  computeBonus(Employee employee){
    print(employee.name);
  }
}
```

### FinanceCalculation
```dart
class FinanceCalculation extends EmployeeBenefits{
  
  calculateBonusByGrade(Employee employee){
    this.setBonusCalculator(BonusCalculatorGrade());
    this.calculateBonus(employee);
  }
  
  calculateBonusByMerit(Employee employee){
    this.setBonusCalculator(BonusCalculatorMerit());
    this.calculateBonus(employee);
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
  
  calculateBonus(Employee employee){
    iBonusCalculator.calculateBonus(employee);
  }
}
```

### IBonusCalculator
```dart
abstract class IBonusCalculator{
  calculateBonus(Employee employee);
}
```

### BonusCalculatorGrade
```dart
class BonusCalculatorGrade implements IBonusCalculator{
  calculateBonus(Employee employee){
    print('BonusCalculatorGrade');
  }
}
```

### BonusCalculatorMerit
```dart
class BonusCalculatorMerit implements IBonusCalculator{
  calculateBonus(Employee employee){
    print('BonusCalculatorMerit');
  }
}
```
