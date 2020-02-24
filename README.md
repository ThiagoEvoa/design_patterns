# Prototype

## Definition
### Prototype is a creational design pattern that allows cloning objects, even complex ones, without coupling to their specific classes.

## Aplicability
### All prototype classes should have a common interface that makes it possible to copy objects even if their concrete classes are unknown. Prototype objects can produce full copies since objects of the same class can access each other’s private fields.

### Entrypoint
```dart
void main() {
  Circle circle = Circle();
  circle.x = 10;
  circle.y = 20;
  circle.radius = 15;
  Circle anotherCircle = Circle.fromCircle(circle).clone() as Circle;
  
  Rectangle rectangle = Rectangle();
  rectangle.height = 10;
  rectangle.width = 10;
  Rectangle anotherRectangle = Rectangle.fromRectangle(rectangle).clone() as Rectangle;
  
  compare(Shape shape1, Shape shape2){
    if(shape1.equals(shape2)){
     print('$shape1 and they are the same');
    }else{
      print('$shape1 but they are not the same');
    }
  }
  
  compare(circle, anotherCircle);
}
```

### Shape
```dart
abstract class Shape{
  int x;
  int y;
  
  Shape();
  
  Shape.fromShape(Shape shape){
    if(shape != null){
      this.x = shape.x;
      this.y = shape.y;
    }
  }
  
  Shape clone();
  
  bool equals(dynamic object){
    if(!(object is Shape)) return false;
    Shape shape2 = object as Shape;
    return shape2.x == x && shape2.y == y;
  }
}
```

### Circle
```dart
class Circle extends Shape{
  int radius;
  
  Circle();
  
  Circle.fromCircle(Circle shape): super(){
    if(shape != null)
      this.radius = shape.radius;
  }
  
  Shape clone(){
    return Circle.fromCircle(this);
  }
  
  bool equals(dynamic object){
    if(!(object is Circle) || (!super.equals(object))) return false;
    Circle shape2 = object as Circle;
    return shape2.radius == radius;
  }
}
```

### Rectangle
```dart
class Rectangle extends Shape{
  int width;
  int height;
  
  Rectangle(); 
  
  Rectangle.fromRectangle(Rectangle shape) : super(){
    if(shape != null){
      this.width = shape.width;
      this.height = shape.height;      
    }
  }
  
  Shape clone(){
    return Rectangle.fromRectangle(this);
  }
  
  bool equals(dynamic object){
    if(!(object is Rectangle) || (!super.equals(object))) return false;
    Rectangle shape2 = object as Rectangle;
    return shape2.width == width && shape2.height == height;
  }
}
```
