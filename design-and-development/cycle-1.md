# 2.2.1 Cycle 1

## Design

For my first cycle it is important for me to create the groundwork of my project to build from. Therefore, in this cycle I will be setting up a basic project using kaboom.js. This will feature the map layout with no graphics.

### Objectives

\[describe the cycle]

* [x] Do a thing
* [x] Do another thing

### Usability Features

### Key Variables

| Variable Name | Use                   |
| ------------- | --------------------- |
| foo           | does something useful |

### Pseudocode

```
procedure do_something
    
end procedure
```

## Development

### Outcome

### Challenges

Description of challenges

## Testing

Evidence for testing

### Tests

| Test | Instructions  | What I expect     | What actually happens | Pass/Fail |
| ---- | ------------- | ----------------- | --------------------- | --------- |
| 1    | Run code      | Thing happens     | As expected           | Pass      |
| 2    | Press buttons | Something happens | As expected           | Pass      |

### Evidence

// Extend our game with multiple scenes

// Start game kaboom()

// Load assets loadSprite("player", "/sprites/bean.png") loadSprite("ground", "/sprites/grass.png") loadSprite("ghosty", "/sprites/ghosty.png") loadSprite("ring", "/sprites/steel.png")

setGravity(2400)

setBackground(33, 37, 42)

const SPEED = 480

// Design 2 levels const WORLD = \[ \[ "@ / e / ", "==============", ], ]

// Define a scene called "game". The callback will be run when we go() to the scene // Scenes can accept argument from go() scene("game", ({ levelIdx, score }) => {

```
// Use the level passed, or first level
const world = addLevel(WORLD[levelIdx || 0], {
	tileWidth: 64,
	tileHeight: 64,
	pos: vec2(100, 300),
	tiles: {
		"@": () => [
			sprite("player"),
			area(),
			body(),
			anchor("bot"),
			"player",
		],
		"=": () => [
			sprite("ground"),
			area(),
			body({ isStatic: true }),
			anchor("bot"),
		],
		"e": () => [
			sprite("ghosty"),
			area(),
			anchor("bot"),
			"ghosty",
		],
		"/": () => [
			sprite("ring"),
			area(),
			anchor("bot"),
			"ring",
		],
		
	},
})

// Get the player object from tag
const player = world.get("player")[0]

// Movements
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

player.onCollide("danger", () => {
	player.pos = level.getPos(0, 0)
	// Go to "lose" scene when we hit a "danger"
	go("lose")
})

player.onCollide("coin", (coin) => {
	destroy(coin)
	play("score")
	score++
	scoreLabel.text = score
})

// Fall death
player.onUpdate(() => {
	if (player.pos.y >= 480) {
		go("lose")
	}
})

// Enter the next level on portal
player.onCollide("portal", () => {
	play("portal")
	if (levelIdx < LEVELS.length - 1) {
		// If there's a next level, go() to the same scene but load the next level
		go("game", {
			levelIdx: levelIdx + 1,
			score: score,
		})
	} else {
		// Otherwise we have reached the end of game, go to "win" scene!
		go("win", { score: score })
	}
})

// Score counter text
const scoreLabel = add([
	text(score),
	pos(12),
])
```

})

scene("lose", () => {

```
add([
	text("You Lose"),
	pos(12),
])

// Press any key to go back
onKeyPress(start)
```

})

scene("win", ({ score }) => {

```
add([
	text(`You grabbed ${score} coins!!!`, {
		width: width(),
	}),
	pos(12),
])

onKeyPress(start)
```

})

function start() { // Start with the "game" scene, with initial parameters go("game", { levelIdx: 0, score: 0, }) }

start()
