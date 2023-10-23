# 2.1 Design Frame

<figure><img src="../.gitbook/assets/Systems Diagram 2.PNG" alt=""><figcaption></figcaption></figure>

## Systems Diagram

This systems diagram outlines the key components of the game that will be created during the development stage. Each section has been further divided into smaller sub-sections to facilitate a gradual and systematic construction of the game. The development process will involve selecting one or two sections at a time to focus on, allowing for a step-by-step assembly of the game. This breakdown aligns with the identified success criteria, ensuring that each section contributes to the overall achievement of the game's goals.

Explanation:

1. Mechanics: This includes the player's controls for the movement and combat between the enemies. Mechanics also include the AI movement and their combat. For my game, this includes how the enemies will move inside of the boxing rings. It will also include how the enemies will go towards the player and will attempt to attack. Mechanics will also include how the display will follow the player as they traverse the map.
2. Menu and Time Record: apart from an obvious menu for my game, this section will also include the timing system where players will attempt to beat their best times to complete the game.
3. Map Layout: This section will include the layout of the separate boxing rings. Furthermore, this section will include what the power-ups are and where they will be spawned.
4. Graphics: This includes what the different parts of my game look like. What I mean by that is the design of the different characters like the player, enemies and the boss. Furthermore, the design of the power-ups, boxing rings and the background.
5. Non-functional aspects: refer to the system qualities. Therefore, this section will include things such as the FPS, enjoyability, and keeping to the PEGI rating.

## Usability Features

Usability holds significant importance in my game as I aim to make it accessible to a wide range of players. During the development of my project, I will prioritize five key points of usability to ensure the best possible user experience. These key points are:

### Effective

To enhance the user experience, it is crucial for players to achieve their goals with completeness and accuracy. To facilitate this, I will focus on ensuring that players easily understand the objective of each level and how to reach the goal. I will make sure my map is designed and formatted in a way that is easy to understand so that players know where to go.

#### Aims

* Create a map layout that can be easily understood by players

### Efficiency

The speed and accuracy with which a user can complete the goal. To do this, I will use easy-to-understand controls that all gamers will be used to. I will also aim to make a menu that is easy to navigate for players to find what they need in the shortest time possible.

#### Aims

* Create a menu system that is quick and easy to navigate through
* Use controls that are easy to understand for gamers of all ages

### Engaging

The solution is engaging for the user to use and the solution gives an enjoyable experience for all players. To do this, I will create an incentive for players to keep playing the game after their first attempt. Furthermore, I will design the characters and the map so that they have an engaging style that also fits the theme of the game.

#### Aims

* Have a level system so that the player has to work towards the final level
* Implement a timer for players to have an incentive to beat their time
* Include in-game art that is engaging and fits the style of the game

### Error Tolerant

The solution should feature little to no errors whilst playing. To make sure that this is the case, I will test the code and put it under a lot of stress to check for errors. If an error occurs, I will correct the code to make sure that it doesn't keep happening.

#### Aims

* The game doesn't crash
* There are no bugs/errors during the player's experience whilst playing.

### Easy To Learn

The solution's features such as power-ups should be easy to understand for players. To make sure of these, I need to make sure that all of the features are simple and easy to understand for gamers of all age groups.

#### Aims

* Make all additional features simple so that they are easy to understand
* Make the game not too challenging for players

## Pseudocode for the Game

### Pseudocode for game

Using Kaboom.js, this is the basic layout of the game and the spawn of the player character.

```
Initialise Kaboom library

Load sprite "bean" from "/sprites/bean.png"

Set gravity to 3200

Create a player entity with the following properties:
  - Sprite: "bean"
  - Position: (120, 80)
  - Collision area
  - Physics body
  - Tag: "player"
```

### Pseudocode for a level

The code below is the pseudocode for the basic first-level map on Kaboom. This code will not represent the final map layout that will be coded on Javascript but it gives a basic idea of how it will work.

```
Create a level named "ring" with the following layout:
  - Row 1: " =              ="
  - Row 2: " =              ="
  - Row 3: "================="

Level Configuration:
  - Tile width: 64
  - Tile height: 64
  - Position: (850, 785)

Define tile types:
  - "=" tile:
    - Display a "steel" sprite
    - Define a collision area
    - Create a static physics body
    - Anchor it at the bottom
```
