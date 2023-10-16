# 2.2.4 Cycle 4

### Design

In this cycle, I will be developing the map. Firstly I aim to implement a level system. This will be important for my game and it will take it to the next level. Once the player has spawned in the first level, the player will have to enter the first boxing ring to take on the first AI opponent. After the first opponent is defeated, the player will exit the boxing ring and enter a portal to the next level. The portal design will be developed in future but is currently a kaboom.js design. The player will then be taken to the next level and this process will be repeated.

Additionally, I aim for each level to have a different design, this will make the game far more interesting.

### Objectives

* [x] Implement level system through portals
* [x] Improve the design of the levels
* [x] Add more levels with unique designs

### Usability Features

Non-functional aspects: The game will become far more developed once there are more levels which are all different.

### Key Variables

| Variable Name          | Use                             |
| ---------------------- | ------------------------------- |
| const level = addLevel | allows for multiple levels      |
| const levelConf        | defining the symbols            |
| const LEVELS           | The actual layout of the levels |

### Pseudocode

<pre><code>Define the level configuration:
  - Tile width: 64
  - Tile height: 64
  - Define tile types:
    - "=" tile:
      - Display "grass" sprite
      - Create a collision area
      - Create a static physics body
      - Anchor at the bottom
      - Set offscreen behavior to hide
      - Tag as "platform"
    - "-" tile:
      - Display "steel" sprite
      - Create a collision area
      - Create a static physics body
      - Set offscreen behavior to hide
      - Anchor at the bottom
    - "@" tile:
      - Display "portal" sprite
      - Create a collision area with a scale of 0.5
      - Anchor at the bottom
      - Set position to (0, -12)
      - Set offscreen behavior to hide
      - Tag as "portal"
      
Define LEVELS as an array of level layouts, where each level is represented as an array of strings.

Level 1 layout:
  - Row 1:  "                                 ",
  - Row 2:  "                                 ",
  - Row 3:  "                                 ",
  - Row 4:  "                                 ",
  - Row 5:  "            -              -     ",
  - Row 6:  "            -              -    @",
  - Row 7:  "============----------------=====",

Level 2 layout:
  - Row 1:  "                                        ",
  - Row 2:  "                                        ",
  - Row 3:  "                                        ",
  - Row 4:  "            -              -            ",
  - Row 5:  "            -              -            ",
  - Row 6:  "           --              -         @  ",
  - Row 7:  "============----------------============",

Level 3 layout:
  - Row 1:  "                                                   ",
  - Row 2:  "                                                   ",
  - Row 3:  "                                    ---            ",
  - Row 4:  "            -              -                       ",
<strong>  - Row 5:  "           --              -                       ",
</strong><strong>  - Row 6:  "          ---              -                      @",
</strong>  - Row 7:  "============----------------=====  ===  ===  ===  =",

Level 4 layout:
  - Row 1:  "                                                 ---------",
  - Row 2:  "                                                --       @",
  - Row 3:  "                                               --     ----",
  - Row 4:  "            -              -                  --     --   ",
  - Row 5:  "           --              -            -------     --    ",
  - Row 6:  "          ---              -                       --     ", 
  - Row 7:  "============----------------============------------      ",

Level 5 layout:
  - Row 1:  "--------------------------------------------",
  - Row 2:  "    -                                       ",
<strong>  - Row 3:  "--- -                                       ",
</strong>  - Row 4:  "  - -           -              -            ",
  - Row 5:  "  - -          --              -            ",
  - Row 6:  "  -           ---              -         @  ",
<strong>  - Row 7:  "==---==========-----------------============",
</strong></code></pre>

## Development

### Outcome

Defining new symbols and making changes to older ones.

```javascript
const levelConf = {
	tileWidth: 64,
	tileHeight: 64,
	tiles: {
		"=": () => [
			sprite("grass"),
			area(),
			body({ isStatic: true }),
			anchor("bot"),
			offscreen({ hide: true }),
			"platform",
		],
		"-": () => [
			sprite("steel"),
			area(),
			body({ isStatic: true }),
			offscreen({ hide: true }),
			anchor("bot"),
		],
		"@": () => [
			sprite("portal"),
			area({ scale: 0.5 }),
			anchor("bot"),
			pos(0, -12),
			offscreen({ hide: true }),
			"portal",
		],
	},
}
```

This code shows the improved layout of the first level and the 4 new levels of the game all with unique layouts. The symbols indicate where everything goes.

```javascript
const LEVELS = [
	[
		"                                 ",
		"                                 ",
		"                                 ",
		"                                 ",
		"            -              -     ",
		"            -              -    @",
		"============----------------=====",
	],
	[
		"                                            ",
		"                                            ",
		"                                            ",
		"            -              -                ",
		"            -              -                ",
		"           --              -              @ ",
		"============----------------================",
	],
	[
		"                                                   ",
		"                                                   ",
		"                                    ---            ",
		"            -              -                       ",
		"           --              -                       ",
		"          ---              -                      @",
		"============----------------=====  ===  ===  ===  =",
	],
    [
		"                                                 ---------",
		"                                                --       @",
		"                                               --     ----",
		"            -              -                  --     --   ",
		"           --              -            -------     --    ",
		"          ---              -                       --     ",
		"============----------------============------------      ",
	],
	[
		"--------------------------------------------",
		"    -                                       ",
		"--- -                                       ",
		"  - -           -              -            ",
		"  - -          --              -            ",
		"  -           ---              -         @  ",
		"==---==========-----------------============",
	],
    
]
```

Code to move the player to the next level once the player collides with the portal

```javascript
	player.onCollide("portal", () => {
		if (levelId + 1 < LEVELS.length) {
			go("game", {
				levelId: levelId + 1,

			})
		} else {
			go("win")
		}
	})
```

Code that links the scenery to the level itself. Also the position of the player when teleported to the next level.

```javascript
scene("game", ({ levelId, coins } = { levelId: 0, coins: 0 }) => {

	// add level to scene
	const level = addLevel(LEVELS[levelId ?? 0], levelConf)

	// define player object
	const player = add([
		sprite("bean"),
		pos(0, 0),
		area(),
		scale(1),
		body(),
		big(),
		anchor("bot"),
	])
```

### Challenges

One challenge that I came across during this cycle was the white border that I had previously made. I have now removed it due to multiple reasons; Firstly, the white border was a lot harder to adjust and extend which ended up being too time-consuming. Secondly, the white border was not the smartest idea for my game as I wanted to use the symbol code to indicate the layout of levels. Thirdly, I wasn't the biggest fan of how it looked, especially with how the boxing rings looked on top of it. As a result, the number of symbols used has increased and the design of the levels looks far more professional.

## Testing

Evidence for testing

### Tests

<table><thead><tr><th width="87">Test</th><th width="127">Instructions</th><th width="223">What I expect</th><th width="208">What actually happens</th><th>Pass/Fail</th></tr></thead><tbody><tr><td>1</td><td>Run code</td><td>New level design to run well, not crash, and have everything that is intended to be in. For example the new map flour</td><td>Player spawns on new map which looks correct</td><td>Pass</td></tr><tr><td>2</td><td>Run code and move around to test portals and new levels</td><td>Player collides with portal correctly and spawns to the other level correctly</td><td>Player walks into the portal but spawns underneath the level</td><td>Fail</td></tr><tr><td>3</td><td>Run code after correcting the false spawn point though the portals</td><td>Player walks through portal and spawns above ground</td><td>Player collides with portal and spawns above the ground.</td><td>Pass</td></tr><tr><td>4</td><td>Check all the new levels by traversing the map</td><td>All levels look well formatted and all have the unique designs</td><td>All levels are there, however the look of some of them are not that good. </td><td>Fail</td></tr><tr><td>5</td><td>Change the design on some of the levels</td><td>All levels look well formatted and all have the unique designs</td><td>Levels all look alot better.</td><td>Pass</td></tr></tbody></table>

### Evidence

Level one design with the portal at the end

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Level two:

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

Level 3:

<figure><img src="../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

Level 4:

<figure><img src="../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

Level 5:

<figure><img src="../.gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>
