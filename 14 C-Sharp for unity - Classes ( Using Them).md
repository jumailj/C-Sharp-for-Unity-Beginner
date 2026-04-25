
### Introduction 
Up until this point, we have been writing code as a single, long sequence of instructions. While this works for simple math problems, it is not how real-world software like your favorite video games or apps is built. Real software is built using **Object-Oriented Programming (OOP)**, a system where we break a massive program down into smaller, manageable "Objects" that work together.

#### The Concept: Blueprints vs Reality
The most important step in understanding C# is learning the difference between a **Class** and an **Object**.

- **The Class (The Plan):** Think of a recipe for a cake. You can read the recipe, but you can’t eat it. It’s just a set of instructions on how a cake _should_ be made. 

- **The Object (The Cake):** When you follow those instructions and bake the cake, you have an **Object**. It is real, it has a weight, a flavor, and it takes up space on your table.

##### Why do we need classes?  
As a developer, your biggest enemy is "Messy Code." Classes provide a way to organize your project so that it stays clean and logical as it grows.


**Division of Responsibility**
In a game, you don't want the code for "Shooting a Gun" mixed in with the code for "Calculating the Wind" or "Updating the Score." By using classes, you give every part of your program its own "Department."

- The **Player Class** is only responsible for the player's movement and health.
- The **Enemy Class** is only responsible for how the monster chases you.
- The **UI Class** is only responsible for drawing the buttons on the screen.


--- 

Before we go any further, it is important to understand what we are focusing on today.

We are **not** going to learn how to create our own new classes from scratch yet. Designing a blueprint is a big job that we will save for later. Instead, we are going to learn how to be "Power Users" of the tools C# has already built for us.

### The Focus: Using Predefined Classes

C# comes with a massive library of ready-to-use "blueprints" (Classes). Our goal is to learn how to:

1. **Identify** a tool we need (like the `Random` class for numbers).
2. **Request** a copy of that tool using the `new` keyword.
3. **Operate** that tool using its built-in methods.

### Creating an Object 
---
We'll begin our object-oriented journey by working with the Random class. This class is designed to generate random numbers, which is extremely useful in games but also has plenty of uses outside of games.

In C#, the `Random` class is our first real encounter with **Object-Oriented Programming**. Unlike the `Console` or `Math` classes, you cannot just use `Random` directly—you must build your own personal generator first.

**Console** and **Math** are **Static Classes**. This means they are "Shared Tools" that belong to the whole program. There is only ever **one** screen and **one** set of math rules, so C# builds them for you automatically. You don't need to make your own "personal" Console.

_**Static (Console/Math):** Like the **Sun** in the sky. It is just there for everyone to use. You don't "create" a new Sun every time you want light._

_**Instance (Random):** Like a **Flashlight**. If you want light in your specific corner, you have to go get your own flashlight (Object) and turn it on._


##### **Creating the Generator** 
When we work with objects, we use two steps: **Declaration** and **construction** 
- **Declaration** `Random dice;` This tells the computer, "i need a place to store a Random tool" 
- `Construction` `dice = new Random()` the `new` keyword runs a **Constructor**, which is a special setup method that "boots up" the object in memory. 

```c#
// Build the tool once at the top of your code
Random random = new Random(); 

// Use the tool many times
int a = random.Next();
int b = random.Next();

Console.WriteLine(a);
Console.WriteLine(b);

```

##### **Controlling the Numbers ( the "Next" overloads)** 
The `.Next()` method is **Overloaded**, meaning it has different "modes" depending on how many numbers you put in the parentheses.


**Mode A: No Limits**
Returns any positive whole number (from 0 to over 2 billion).

```c#
int bigNum = random.Next(); 
Console.WriteLine(bigNum);
```

**Mode B: The Maximum Limit**
Returns a number from **0** up to (but NOT including) your max number.

```c#
int upToFive = random.Next(6); // Possible results: 0, 1, 2, 3, 4, 5
Console.WriteLine(upToFive);
```

**Mode C: The Range (Min and Max)**
This is the most useful mode. It includes the first number, but stops **just before** the last number.

```c#
// The "Coordinate" Example
int x = random.Next(1, 11); // Results: 1 to 10
int y = random.Next(20, 31); // Results: 20 to 30

Console.WriteLine(x);
Console.WriteLine(y);
```

##### Working with Decimals (Floats & Doubles)
Sometimes you don't want whole numbers; you want decimals (like 0.5 or 0.75).

```c#
Random random = new Random();

float myFloat = random.NextSingle();  // Returns 0.0 to 1.0
double myDouble = random.NextDouble(); // Returns 0.0 to 1.0

// Pro Tip: To get a bigger decimal, just multiply it!
double randomPrice = random.NextDouble() * 100; // Returns 0.0 to 100.0
```

---
**_Simple Number Guessing Game_**
```c# 
// 1. Create the personal tool (The Object)
Random generator = new Random();

// 2. The tool picks a secret number between 1 and 10
int secretNumber = generator.Next(1, 11);

Console.WriteLine("I am thinking of a number between 1 and 10.");

int userGuess = 0;

// 3. Keep asking until the guess is correct
while (userGuess != secretNumber)
{
    Console.Write("Enter your guess: ");
    userGuess = Convert.ToInt32(Console.ReadLine());

    if (userGuess < secretNumber)
    {
        Console.WriteLine("Too low!");
    }
    else if (userGuess > secretNumber)
    {
        Console.WriteLine("Too high!");
    }
}

// 4. If the loop ends, it means they won!
Console.WriteLine("You got it! The number was " + secretNumber);

```

#### Stack and Heap 
--- 
Every time you run a C# program, the Operating System gives it a block of memory. C# splits that memory into two distinct areas that work in very different ways.

##### The Stack: The "High-Speed Desk"

The **Stack** is an extremely organized, "Last-In, First-Out" (LIFO) memory structure. Think of it like a physical stack of trays in a cafeteria.

- **How it works:** When you call a method, C# adds a "Frame" to the top of the stack. This frame contains all the local variables for that method.

- **Automatic Cleanup:** When the method finishes (reaches the `}`), the frame is "popped" off the stack. Everything inside it—every `int`, `bool`, and `float`—is instantly destroyed and the memory is reclaimed.

- **Speed:** It is incredibly fast because the computer always knows exactly where the next piece of data is (right on top).


##### The Heap: The "Open Warehouse"

The **Heap** is a large, messy pool of memory. It is where **Objects** live because they are often too big or stay alive too long to fit on the tiny Stack.

- **How it works:** When you use the keyword **`new`**, you are telling the computer: _"Find a big enough empty space in the Warehouse (Heap) to fit this object."_

- **The Address:** Because the Warehouse is so big, the computer gives you a "Reference" (an address or a map) so you can find the object later.

- **Cleanup:** The Heap is **not** cleaned up instantly. It is cleaned up by the **Garbage Collector (GC)**, a background process that looks for objects no one is using anymore and throws them away.


#### Value Types vs Reference Types
---

**A. Value Types (The "Simple" Data)**

Types like `int`, `bool`, `double`, and `char` are **Value Types**.

- The actual value (like the number `5`) is stored **directly on the Stack**.
- If you say `int x = y;`, the computer creates a **brand new copy** of that number.

```c#
void Square(int n) {
    n = n * n; // This only changes the COPY on the Stack
}

int x = 5;
Square(x);
// x is STILL 5. The original was never touched!
```


**B. Reference Types (The "Complex" Data)**

Types like `Random`, `string`, and **Arrays** are **Reference Types**.

- The **Actual Object** (the data) is on the **Heap**.
- If you say `Random r2 = r1;`, you are **not** making a new generator. You are just giving `r2` the same address/key to the same object in the Warehouse.

```c#
void ChangeName(Student s) {
    s.name = "jumail"; // We used the key to find the house and change the door!
}

Student myStudent = new Student();
myStudent.name = "Unknown";
ChangeName(myStudent);
// myStudent.name is now "Arjun"! The original was changed.
```

| **Type Category**   | **Examples**                         | **Where is the Data?**           |
| ------------------- | ------------------------------------ | -------------------------------- |
| **Value Types**     | `int`, `bool`, `char`, `float`       | On the **Stack** (The Desk).     |
| **Reference Types** | `Random`, `int[]` (Arrays), `string` | On the **Heap** (The Warehouse). |


### Garbage Collection: (The Cleanup Crew)
When we use the `new` keyword, we are taking up space in the **Heap** (the Warehouse). But if we keep creating objects and never throw them away, the computer will eventually run out of RAM and crash. In older languages like C++, programmers had to manually "delete" every object. In C#, we have a robot called the **Garbage Collector (GC)** that does it for us.


**How The GC Knows**

_The Garbage Collector follows one simple rule: **If nobody has a "key" (reference) to an object, the object is dead.**_

_The Garbage Collector doesn't run every single second (that would make your game laggy). Instead, it "wakes up" when:_
- The computer is running low on memory.
- The "Warehouse" (Heap) is getting too full.
- The program is idle and has nothing better to do.

_You can't force the GC to delete an object right now, but you can make an object "ready for death" by cutting your connection to it. You do this by setting the reference to `null`._
```c#
Random dice = new Random(); // Object is alive

dice = null; // We threw away the key! 
// The object is now floating in the Heap, waiting for the GC to find it.
```

