### ::
```
class Box {
   public:
      double length;      // Length of a box
      double breadth;     // Breadth of a box
      double height;      // Height of a box
   
      double getVolume(void) {
         return length * breadth * height;
      }
};
```
If you like, you can define the same function outside the class using the scope resolution operator (::) as follows −
```
double Box::getVolume(void) {
   return length * breadth * height;
}
```
