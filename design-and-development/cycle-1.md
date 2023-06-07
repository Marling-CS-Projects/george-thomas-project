# 2.2.1 Cycle 1

## Design

For my first cycle it is important for me to create the groundwork of my project to build from. Therefore, in this cycle I will be setting up a basic project using kaboom.js. This will feature the map layout with no graphics.

Firstly, I assigned different symbols to be used as parts of the map. The first bit of code will display  what the map looks like and the location where the player starts. The design will use kaboom sprites to begin with as placeholders to my own designs.

### Objectives

* [x] Begin basic project using kaboom.js
* [x] Create map design for the start of the game and where the player spawns
* [x] Use Kaboom.js sprites to create an example screenshot

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

```javascript
// Start game
kaboom()

// Loads assets
loadSprite("player", "/sprites/bean.png") // The player
loadSprite("ground", "/sprites/grass.png") // The map floor
loadSprite("ghosty", "/sprites/ghosty.png") // The temporary enemy
loadSprite("ring", "/sprites/steel.png") // The boxing ring ropes (edges)

setBackground(33, 37, 42) // a temporary basic grey colour

const level = addLevel([
	// The map layout using symbols
	"           @  /     e /              ",
	"=====================================",

], {
	// The size of each symbol
	tileWidth: 64,
	tileHeight: 64,
	// The position of the furthest left block
	pos: vec2(0, 400),
	// Defines what each symbol represents (using kaboom sprites)
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
			body({ isStatic: true }),
			anchor("bot"),
		],
	},
})
```

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>
