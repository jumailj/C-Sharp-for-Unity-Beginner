### Introduction 
---
Until now, we have lived in a world where we used tools built by other people—like `Console`, `Random`, or `String`. But in game development, the "standard tools" aren't enough. C# doesn't come with a built-in "Player" or "Enemy" or "Inventory." **You have to build them.** Creating your own class is like moving from playing with a finished LEGO set to having a **3D printer**. You are no longer restricted by what C# gives you; you can now define exactly what a "Player" is, what they remember (Data), and what they can do (Actions).

Think of creating a class as drawing a Blueprint 
- The class is the paper drawing of the house, It doesn't take up space in the real world yet.
- The **Object** is the actual house built from that drawing. Once you have the blueprint, you can build 1,000 identical houses (Players) just by using the `new` keyword.

**Our First Project: The Player Class** 
In this tutorial, we are going to build a `Player` class from scratch. This isn't just a coding exercise—this is the foundation of every game you will ever make. Whether you are building a simple text adventure today or a massive 3D world in **MonoGame** tomorrow, the logic is the same:

- **Define the Data:** What does a player have? (Health, Name, Score).
- **Define the Actions:** What can a player do? (Jump, TakeDamage, LevelUp).

