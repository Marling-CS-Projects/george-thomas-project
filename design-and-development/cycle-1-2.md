# 2.2.3 Cycle 3

### Design

For my third cycle, It is very important for me to add the movement into the game. My objectives for this cycle would be to make the player movable, correct the gravity if needed, and adjust the camera to side-scrolling.

I also will be adding a background colour change, adding a plain coloured background.

### Objectives

* [x] Player movement
* [x] Side-scrolling camera
* [x] Add background colour

### Usability Features

Non-functional aspects: Making my movement use controls/key-binds that are easy to understand for players. This is because my focus does not include making my game hard to get used to for players.

Mechanics: The arrow keys and space bar will be used for movement. Space bar = Jump, Left/right arrow keys = left/right.

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
Define a constant SPEED with a value of 480

On the "space" key press event:
  - If the player is on the ground:
    - Make the player jump

On the "left" key down event:
  - Move the player to the left with a speed of -SPEED in the horizontal direction

On the "right" key down event:
  - Move the player to the right with a speed of SPEED in the horizontal direction

On the player's update event:
  - Update the camera position to follow the player's world position

On the player's physics resolve event:
  - Update the camera position to follow the player's world position

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

Movement is a crucial part of my game so it has been great to complete it. This allows me to develop more in the future. Player movement can lead to player combat, to AI movement, to AI combat and to eventually the final battle in the game.

Here is the code for the new dark grey background colour:

```javascript
kaboom({
	background: [90, 90, 90],
})
```

### Challenges

A challenge that I faced in this cycle was the speed. This was because speed was an important decision to make because it plays a massive role in the combat of the game which is the main part of it. After some trials with different speeds. The specific speed of 480 in repl library worked out the best. As a result, the player does not look completely unrealistic when moving.&#x20;

## Testing

### Tests

<table><thead><tr><th width="87">Test</th><th width="127">Instructions</th><th width="223">What I expect</th><th width="208">What actually happens</th><th>Pass/Fail</th></tr></thead><tbody><tr><td>1</td><td>Run code</td><td>Player will move from inputs using the left and right arrow keys at set speed</td><td>As expected</td><td>Pass</td></tr><tr><td>2</td><td>Run code with changed constant speed</td><td>Player will move left/right at a decided speed of 480</td><td>As expected</td><td>Pass</td></tr><tr><td>3</td><td>Run code after addition of jumping</td><td>Player will jump after the space-bar is pressed and will land at a realistic velocity</td><td>Player jumps - however players gravity is too strong so floats in the air too much</td><td>Fail</td></tr><tr><td>4</td><td>Run code with new background colour</td><td>Dark grey backround colour applied</td><td>Dark grey backround colour applied</td><td>Pass</td></tr></tbody></table>

### Evidence

This short clip displays testing of the player's movement, including jumping, and the side-scrolling camera:

{% embed url="https://youtu.be/2XcHmnbCc7o" %}

* [x] Player movement
* [x] Side-scrolling camera
