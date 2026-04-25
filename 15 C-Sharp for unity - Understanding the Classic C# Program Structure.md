
Until now, we have been using "Top-Level Statements" ( writing code directly in the file). But Professional Software especially **Game Engines** like MonoGame or Unity uses a structured "Mansion" Layout.


**How to create a classic Project** 

If you are using the Command Line (Terminal), you need to tell C# specifically to build the "Main" structure.

The Command: 
```c#
dotnet new console --use-program-main -n "Project-Name"
```
_Why use this flag?_ : By default, modern C# hides the "extra" code to make it look simple this flag tells C# to "show me everything" so we can learn how the program actually starts 


**The Anatomy of the code** 
Let's look at the code snippet and break down every single "room" in this mansion. 

```c#
namespace HelloWorld 
{
    class Program /* you can name this class whatever you want*/
    {
        static void Main(string[] args) /*Entry Point*/
        {
            Console.WriteLine("Hello, World!");
        }
    }
}
```

**The `namespace` (The neighborhood)** 
The `namespace` is a container. It tells the computer that all the classes inside it belong to the same project. 

- why we need it: It prevents "Name collisions" you might have a class named `Player` and a different library might have a class named `Player`. The namespace keeps them in separate "neighborhoods" so they don't get mixed up. 

**The `class Program` ( The House)** 
In C# code cannot float around in space. Every piece of logic must live inside a class. 
- **The Container**: Think of the class as building. The building holds all our tools (Methods) and information ( Fields) 

**The `static void Main()`**
this is the most important part of the entire program. It is called the **Entry Point** 

- `static` This means the computer can run this method immediately without having to "build" the `Program` class first It just exists as soon as the app starts.
- `void` This means the method performs an actions but doesn't "give back" a result ( like a number). 
- `strting[] args`: This is a "suitcase" that can hold extra instructions sent to the program when it starts (like opening a specific file). 

#### Why move away from Top-Level Statements? 
- **Organization**: As our games get bigger, we will have 10, 20, or 100 files. without a `namespace` and `class` structure, it would be impossible to keep track of them. 
- **Explicit Control**: you can see exactly where the program starts and where it ends. 
- **Preparation for gaming**: Frameworks like MonoGames use this exact structure. 

---
_Example-1_ 

```c#
using System;

namespace GuessingGame 
{
    class Program
    {
        static void Main(string[] args)
        {
            // --- ALL LOGIC LIVES INSIDE THESE BRACES ---
            
            Random generator = new Random();
            int secretNumber = generator.Next(1, 11);
            int userGuess = 0;

            Console.WriteLine("--- THE CLASSIC GUESSING GAME ---");
            Console.WriteLine("I am thinking of a number between 1 and 10.");

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

            Console.WriteLine("You got it! The number was " + secretNumber);
        }
    }
}
```

_Example-2_
```c#
using System;

namespace GameProject
{
    // --- ZONE 1: THE YARD (Namespace) ---
    // Enums live here so EVERY class in the project can see them.
    enum GameState { Start, Playing, GameOver }

    class Program
    {
        // --- ZONE 2: THE HOUSE (Class) ---

        static void Main(string[] args)
        {
            // --- ZONE 3: THE WORKROOM (Method) ---
            
            // We create a variable using our Enum type
            GameState currentStatus = GameState.Start;

            Console.WriteLine("--- WELCOME TO THE ENGINE ---");

            if (currentStatus == GameState.Start)
            {
                Console.WriteLine("The game is currently in the START phase.");
                
                // Transition to the next state
                currentStatus = GameState.Playing;
            }

            if (currentStatus == GameState.Playing)
            {
                Console.WriteLine("Now the game is PLAYING. Get ready!");
            }
        }
    }
}
```

"In the beginning, we wrote code like a **shopping list** (Top-Level). Now, we write code like a **city map** (Classic). It's more complex, but it's the only way to build a world as big as a video game."


In modern C#, **Top-Level Statements** are simply a "shortcut" where the compiler automatically wraps your loose lines of code inside a hidden **Program class** and a hidden **Main method** behind the scenes.

Because the computer is hard-wired to only start a program through a `static void Main` entry point, it builds this "invisible skeleton" for you so that your code remains valid.

Moving to the **Classic Structure** isn't actually adding new complexity—it is simply you taking over the job of writing that skeleton yourself to have full control over your project's organization.

