# Strategy

## Define a family of algorithms, encapsulate each one, and make them interchangeable. Strategy lets the algorithm very independently from clients that use it.

### Entrypoint
```java
void main() {
  FinanceCalculation calculation = new FinanceCalculation();
  calculation.calculateBonusByMerit();
}
```

### FinanceCalculation
```java
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
```java
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
```java
interface class IBonusCalculator{
  calculateBonus();
}
```

### BonusCalculatorGrade
```java
class BonusCalculatorGrade implements IBonusCalculator{
  calculateBonus(){
    print('BonusCalculatorGrade');
  }
}
```

### BonusCalculatorMerit
```java
class BonusCalculatorMerit implements IBonusCalculator{
  calculateBonus(){
    print('BonusCalculatorMerit');
  }
}
```

