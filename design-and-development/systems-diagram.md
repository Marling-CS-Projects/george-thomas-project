# 2.1 Design Frame

## Systems Diagram

```
***
```

![NOT MY COMPLETED SYSTEMS DIAGRAM](https://github.com/Marling-School/alevel-project-template/blob/docs/.gitbook/assets/System%20Diagram.jpg)

This systems diagram outlines the key components of the game that will be created during the development stage. Each section has been further divided into smaller sub-sections to facilitate a gradual and systematic construction of the game. The development process will involve selecting one or two sections at a time to focus on, allowing for a step-by-step assembly of the game. This breakdown aligns with the identified success criteria, ensuring that each section contributes to the overall achievement of the game's goals.

Explanation:

1. Game World: This component represents the virtual world in which the game takes place. It consists of various levels, platforms, obstacles, enemies, and interactive elements.
2. Player Controller: This component handles player input, using keyboard commands. It receives input from the player and translates it into actions within the game world, controlling the player's character.
3. Input: This component captures input from the player, such as keyboard presses or controller movements. It relays the input to the Player Controller for processing.
4. Physics: This component simulates the physical interactions within the game world. It governs the movement of the player character, collisions with platforms and enemies, gravity, and other physical forces.

## Usability Features

Usability holds significant importance in my game as I aim to make it accessible to a wide range of players. During the development of my project, I will prioritize five key points of usability to ensure the best possible user experience. These key points are:

### Effective

To enhance the user experience, it is crucial for players to achieve their goals with completeness and accuracy. To facilitate this, I will focus on ensuring that players easily understand the objective of each level and how to reach the goal. I will employ clear visual cues and indicators to make the goal highly visible, eliminating any confusion regarding the destination players need to reach.

#### Aims

* Create a clear goal to reach to determine the end of a level
* Create a clear goal for any multiplayer modes

### Efficiency

The speed and accuracy to which a user can complete the goal. To do this, I will create a menu system which is easy to navigate through in order for to find what you are looking for. The information which is more important can be found with less clicks.

#### Aims

* Create a menu system that is quick and easy to navigate through
* Create a controls system that isn't too complicated but allows the player to do multiple actions

### Engaging

The solution is engaging for the user to use. To do this, I will create 5 levels and an online multiplayer mode to keep the players engaged and allow them to have fun while playing the game. Using vector style art will also make the game nicer to look at than blocks, so will draw more people in, keeping them engaged.

#### Aims

* Create a series of levels to work through
* Create a multiplayer mode to play
* Incorporate a style of game art the suits the game

### Error Tolerant

The solution should have as few errors as possible and if one does occur, it should be able to correct itself. To do this, I will write my code to manage as many different game scenarios as possible so that it will not crash when someone is playing it.

#### Aims

* The game doesn't crash
* The game does not contain any bugs that damage the user experience

### Easy To Learn

The solution should be easy to use and not be over complicated. To do this, I will create simple controls for the game. I will make sure that no more controls are added than are needed in order to keep them as simple as possible for the players.

#### Aims

* Create a list of controls for the game
* Create an in-level guide that helps players learn how to play the game

## Pseudocode for the Game

### Pseudocode for game

This is the basic layout of the object to store the details of the game. This will be what is rendered as it will inherit all important code for the scenes.

```
object Game
    type: Phaser
    parent: id of HTML element
    width: width
    height: height
    physics: set up for physics
    scenes: add all menus, levels and other scenes
end object

render Game to HTML web page
```

### Pseudocode for a level

This shows the basic layout of code for a Phaser scene. It shows where each task will be executed.

```
class Level extends Phaser Scene

    procedure preload
        load all sprites and music
    end procedure
    
    procedure create
        start music
        draw background
        create players
        create platforms
        create puzzle elements
        create enemies
        create obstacles
        create finishing position
        create key bindings
    end procedure
    
    procedure update
        handle key presses
        move player
        move interactable objects
        update animations
        check if player at exit
    end procedure
    
end class
```
