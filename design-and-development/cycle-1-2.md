# 2.2.3 Cycle 3

### Design

For my third cycle, It is very important for me to add the movement into the game. My objectives for this cycle would be to make the player movable, correct the gravity if needed, and adjust the camera to side-scrolling.

### Objectives

* [x] Player movement
* [x] Check gravity
* [x] Side-scrolling camera

### Usability Features

Non-functional aspects: Making my movement use controls/key-binds that are easy to understand for players. This is because my focus does not include making my game hard to get used to for players.

Mechanics: The arrow-keys and space bar will be used for movement. Space bar = Jump, Left/right arrow keys = left/right.

### Key Variables

| Variable Name            | Use                                                                                                                                                     |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| const SPEED              | keeps a constant speed of 480                                                                                                                           |
| onKeyPress               | listens for "space" and has a callback function. It executes the callback function when "space" is pressed.                                             |
| onKeyDown                | listens for down events rather than key press events. It also takes a key string and a callback function                                                |
| player.isGrounded        | checks that the player is grounded                                                                                                                      |
| player.onUpdate          | callback function is executed whenever the player updates                                                                                               |
| player.onPhysiscsResolve | event listener for the 'player' object's physics resolution event. The provided callback function is executed when physics are resolved for the player. |
| camPos                   | takes the 'player' object's world position and updates the camera position accordingly.                                                                 |

### Pseudocode

```


```

## Development

### Outcome

Movement has been added and works just how I wanted. The code below shows how key presses are detected for 'space' and 'left/right arrow keys'. The code also shows the chosen speed of 480.

```javascript
const SPEED = 480

onKeyPress("space", () => {
  if (player.isGrounded()) {
     player.jump()
   }
})

onKeyDown("left", () => {
  player.move(-SPEED, 0)
})

onKeyDown("right", () => {
  player.move(SPEED, 0)
})

```

This cycle has also implemented a "side-scrolling" camera mechanic. The code below shows this:

```javascript
player.onUpdate(() => {
    camPos(player.worldPos())
})

player.onPhysicsResolve(() => {
    camPos(player.worldPos())
})
```



### Challenges

My first big challenge of the development for my project was familiarizing myself with how to use Kaboom.js through Repl. I had no past experience of coding using kaboom on Repl. This meant that I had to do some practice and watch some quick tutorials to get my head around the online library.

## Testing

Evidence for testing

### Tests

<table><thead><tr><th width="87">Test</th><th width="127">Instructions</th><th width="223">What I expect</th><th width="208">What actually happens</th><th>Pass/Fail</th></tr></thead><tbody><tr><td>1</td><td>Run code</td><td>Player spawns in the bottom left hand side of the screen slightly above the ground</td><td>As expected</td><td>Pass</td></tr><tr><td>2</td><td>Run code again</td><td>Map flour to load and be the whole length of the screen</td><td>As expected</td><td>Pass</td></tr><tr><td>3</td><td>Run code after additions</td><td>Player spawns and lands on new boundary </td><td>Player spawns in correct spot. However, player does not fall to the floor and land</td><td>Fail</td></tr><tr><td>4</td><td>Run code with fixed gravity</td><td>Player spawns and lands on the boundary</td><td>As expected - the player falls, lands and does not go through the boundary</td><td>Pass</td></tr></tbody></table>

### Evidence

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

This image above displays what my map looks like on spawn using Kaboom.js sprites. This therefore completes my objective:

* [x] Create map design for the start of the game and where the player spawns

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

This image above shows that the gravity has been implement and the player falls from spawn point to land on the ground.

* [x] Implement gravity
