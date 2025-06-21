
## S - Single Responsibility Principle 
## O - Open/Closed  Principle
## L - Liskov Substitution Principle
## I - Interface Segmented Principle
## D - Dependency Inversion Principle


### Advantages of these Principle

1. Avoid duplicate code
2. Easy to maintain 
3. Easy to understand 
4. Flexible software
5. Readuce complexity


### SRP

A Class should have only 1 reason to change

```java
class Marker {
  String name;
  String color;
  int year;
  int price;

  public Marker(String name, String color, int year, int price) {
    this.name = name;
    this.color = color;
    this.year = year;
    this. price = price; 
  }
}


class Invoice {
  private Marker marker;
  private int quantity;

  public Invoice(Marker marker, int quantity) {
     this.marker = marker;
     this.quantity = quantity;
  }

  public int calculateTotal() {
     int price = (( marker.price) * this.quantity);
     return price;
  }

  public void printInvoice() {
    //print the Invoice 
  }

  public void saveToDB() {
   // Save the data to db
  
  }
}


// Above Invoice class have multiple reasons to change calculateTotal change, printInvoice change, saveToDb change so it voilates SRP

// Solution

class InvoiceDao {
  Invoice invoice;

  public InvoiceDao(Invoice invoice) {
    this.invoice = invoice;
  }

  public void saveToDB() {
    // Save into DB
  }
}

class InvoicePrinter {
  Invoice invoice;

  public InvoicePrinter(Invoice invoice) {
    this.invoice = invoice;
  }

  public void print() {
    // print
  }
}

// Moved other two to different handle their responsibilty seperately
```


### OCP 

Open for Extension but Closed for Modification

Now InvoiceDao is tested and moved to production and now we want to add saveToFile functionality in Invoice if we add this method to same InvoiceDao class it will voilate OCP as 
the remaining code is already tested and we're modifying it.

Solution 
Move InvoiceDao with abstract method save that needs to be implemented by classes that are implementin this interface, by this we can easily create any new type of save to invoiceDao without affecting previous classes.

```java
interface InvoiceDao {  
    public void save(Invoice invoice);  
}  
  
class DatabaseInvoiceDao implements InvoiceDao {  
  
    @Override  
    public void save(Invoice invoice) {  
        // save to DB  
    }  
}  
  
class FileInvoiceDao implements InvoiceDao {  
  
    @Override  
    public void save(Invoice invoice) {  
        // save to File  
    }  
}
```

### LSP 

If Class B is subtype of Class A, then we should be able to replace object of A with B without breaking behaviour of the program.

**Subclass should extend the capability of parent class not narrow it down

```java
interface Bike {  
    void turnOnEngine();  
    void accelerate();  
}  

// this subclass can replace the parent class as this implements both the fuction provided by parent
class Motorcycle implements Bike {  
  
    boolean isEngineOn;  
    int speed;  
  
  
    @Override  
    public void turnOnEngine() {  
        // turn on engine !  
        isEngineOn = true;  
    }  
  
    @Override  
    public void accelerate() {  
        // increase the speed  
        speed = speed + 10  
    }  
}  
  
// this will voilate LSP as turnOnEngine() function from parent class throwing exception and it is narrowing down the functionality provided by parent class
class Bicycle implements Bike {  
  
    @Override  
    public void turnOnEngine() {  
        throw new AssertionError("there is no engine");  
    }  
  
    @Override  
    public void accelerate() {  
        // do something  
    }  
}
```

eg. Rectangle and Square


ISP

Interface should be such, that client should not implement unecessary functions they do not need


```java

// Voilates ISP 
interface RestaurantEmployee {  
    void washDishes();  
    void serveCustomers();  
    void cookFood();  
}  
  
class Waiter implements RestaurantEmployee {  
  
    @Override  
    public void washDishes() {  
        // not my job  
    }  
  
    @Override  
    public void serveCustomers() {  
        System.out.println("Serving the customer");  
    }  
  
    @Override  
    public void cookFood() {  
        // not my job  
    }  
}

// now breaking down into properInterface

interface WaiterInterface {
  void takeOrder();
}

interface ChefInterface {
  void cookFood();
}
```


### DIP

Class should depend on interfaces rather than concrete classes

```java
class Macbook {  
    private final WiredKeyboard keyboard;  
    private final WiredMouse mouse;  
  
    public Macbook() {  
        keyboard = new WiredKeyboard();  
        mouse = new WiredMouse();  
    }  
}

// Solution pass interface rather than assigning concrete classes so if in future we want other implementation of object we can easily add it e.g want to add bluetooth keyboard and mouse


class Macbook {
 private final Keyboard keyboard;
 private final Mouse mouse;

 public Macbook(Keyboard keyboard, Mouse mouse) {
   this.keyboard = keyboard;
   this.mouse = mouse;
 }
}
```