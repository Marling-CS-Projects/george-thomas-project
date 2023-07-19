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

I had to make changes from the original gravity that I had of 2400 to 1500. This is because I wanted my jumping to be more realistic. I wanted a more realistic feel as the player jumps into the boxing ring, not floating into it.

```javascript
setGravity(1500);
```

Movement is a crucial part of my game so it has been great to complete it. This allows me to develop at more in the future. Player movement can lead to player combat, to AI movement, to AI combat and to eventually the final battle in the game.

### Challenges

A challenge that I faced in this cycle was deciding on the gravity and the speed of the player. The gravity was very important to change in this cycle because before the change, the player would near enough float into the boxing rings, jumping well over the temporary 'ropes'. The speed was also an important decision to make because it plays a massive role in the combat of the game which is the main part of it. After some trials with different speeds. The specific speed of 480 in repl library worked out the best. As a result, the player does not look completely unrealistic when moving.&#x20;

## Testing

### Tests

<table><thead><tr><th width="87">Test</th><th width="127">Instructions</th><th width="223">What I expect</th><th width="208">What actually happens</th><th>Pass/Fail</th></tr></thead><tbody><tr><td>1</td><td>Run code</td><td>Player will move from inputs using the left and right arrow keys at set speed</td><td>As expected</td><td>Pass</td></tr><tr><td>2</td><td>Run code with changed constant speed</td><td>Player will move left/right at a decided speed of 480</td><td>As expected</td><td>Pass</td></tr><tr><td>3</td><td>Run code after addition of jumping</td><td>Player will jump after the space-bar is pressed and will land at a realistic velocity</td><td>Player jumps - however players gravity is too strong so floats in the air too much</td><td>Fail</td></tr><tr><td>4</td><td>Run code with fixed gravity</td><td>Player will jump after the space-bar is pressed and will land at a realistic velocity</td><td>As expected</td><td>Pass</td></tr></tbody></table>

### Evidence

Enter Video that was made for movement

*
*
