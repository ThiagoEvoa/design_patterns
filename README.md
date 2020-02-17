# Strategy

## Define a family of algorithms, encapsulate each one, and make them interchangeable.

```java
void main() {
 FinanceCalculation calculation = new FinanceCalculation();
  
  calculation.calculateBonusByMerit();
}

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

abstract class EmployeeBenefits{
  IBonusCalculator iBonusCalculator;
  
  setBonusCalculator(IBonusCalculator interface){
    iBonusCalculator = interface;
  }
  
  calculateBonus(){
    iBonusCalculator.calculateBonus();
  }
}

interface class IBonusCalculator{
  calculateBonus();
}

class BonusCalculatorGrade implements IBonusCalculator{
  calculateBonus(){
    print('BonusCalculatorGrade');
  }
}

class BonusCalculatorMerit implements IBonusCalculator{
  calculateBonus(){
    print('BonusCalculatorMerit');
  }
}
´´´
