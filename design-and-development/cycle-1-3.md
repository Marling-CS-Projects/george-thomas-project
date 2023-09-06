# 2.2.4 Cycle 4

### Design

In this cycle, I will be developing the map. Firstly I aim to implement a level system. This will be important for my game and it will take it to the next level. Once the player has spawned in the first level, the player will have to enter the first boxing ring to take on the first AI opponent. After the first opponent is defeated, the player will exit the boxing ring and enter a portal to the next level. The portal design will be developed in future but is currently a kaboom.js design. The player will then be taken to the next level and this process will be repeated.

Additionally, I aim for each level to have a different design, this will make the game far more interesting.

I also will be adding a background colour change, adding a plain coloured background.

### Objectives

* [x] Implement level system through portals
* [x] Improve the design of the levels
* [x] Add more levels with unique designs
* [x] Add background colour

### Usability Features

Non-functional aspects: The game will become far more developed once there are more levels which are all different.

### Key Variables

| Variable Name          | Use                             |
| ---------------------- | ------------------------------- |
| const level = addLevel | allows for multiple levels      |
| const levelConf        | defining the symbols            |
| const LEVELS           | The actual layout of the levels |

### Pseudocode

```


```

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
		"0": () => [
			sprite("bag"),
			area(),
			body({ isStatic: true }),
			offscreen({ hide: true }),
			anchor("bot"),
		],
		"$": () => [
			sprite("coin"),
			area(),
			pos(0, -9),
			anchor("bot"),
			offscreen({ hide: true }),
			"coin",
		],
		"^": () => [
			sprite("spike"),
			area(),
			body({ isStatic: true }),
			anchor("bot"),
			offscreen({ hide: true }),
			"danger",
		],
		"#": () => [
			sprite("apple"),
			area(),
			anchor("bot"),
			body(),
			offscreen({ hide: true }),
			"apple",
		],
		">": () => [
			sprite("ghosty"),
			area(),
			anchor("bot"),
			body(),
			patrol(),
			offscreen({ hide: true }),
			"enemy",
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
		"            -      >       -  $ @",
		"============----------------=====",
	],
	[
		"                                            ",
		"                                            ",
		"                                            ",
		"            -              -                ",
		"            -              -                ",
		"           --         >    -     $        @ ",
		"============----------------================",
	],
	[
		"                                                   ",
		"                                     $             ",
		"                                    ---            ",
		"            -              -                       ",
		"           --              -                       ",
		"          ---           >  -                      @",
		"============----------------=====  ===  ===  ===  =",
	],
    [
		"                                                 ---------",
		"                                                --       @",
		"                                               --     ----",
		"            -              -                  --     --   ",
		"           --              -            -------     --    ",
		"          ---           >  -              $        --     ",
		"============----------------============------------      ",
	],
	[
		"--------------------------------------------",
		"    -                                       ",
		"--- -                                       ",
		"  - -           -              -            ",
		"  - -          --              -            ",
		"  -           ---           >  -     $   @  ",
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

Code for dark grey background

<pre class="language-javascript"><code class="lang-javascript"><strong>kaboom({
</strong>	background: [90, 90, 90],
})
</code></pre>

### Challenges

One challenge that I came across during this cycle was the white border that I had previously made. I have now removed it due to multiple reasons; Firstly, the white border was a lot harder to adjust and extend which ended up being too time-consuming. Secondly, the white border was not the smartest idea for my game as I wanted to use the symbol code to indicate the layout of levels. Thirdly, I wasn't the biggest fan of how it looked, especially with how the boxing rings looked on top of it. As a result, the number of symbols used has increased and the design of the levels looks far more professional.

## Testing

Evidence for testing

### Tests

<table><thead><tr><th width="87">Test</th><th width="127">Instructions</th><th width="223">What I expect</th><th width="208">What actually happens</th><th>Pass/Fail</th></tr></thead><tbody><tr><td>1</td><td>Run code</td><td>New level design to run well, not crash, and have everything that is intended to be in. For example the new map flour</td><td>Player spawns on new map which looks correct</td><td>Pass</td></tr><tr><td>2</td><td>Run code with new background colour</td><td>Dark grey backround colour applied</td><td>Dark grey backround colour applied</td><td>Pass</td></tr><tr><td>3</td><td>Run code and move around to test portals and new levels</td><td>Player collides with portal correctly and spawns to the other level correctly</td><td>Player walks into the portal but spawns underneath the level</td><td>Fail</td></tr><tr><td>4</td><td>Run code after correcting the false spawn point though the portals</td><td>Player walks through portal and spawns above ground</td><td>Player collides with portal and spawns above the ground.</td><td>Pass</td></tr><tr><td>5</td><td>Check all the new levels by traversing the map</td><td>All levels look well formatted and all have the unique designs</td><td>All levels are there, however the look of some of them are not that good. </td><td>Fail</td></tr><tr><td>6</td><td>Change the design on some of the levels</td><td>All levels look well formatted and all have the unique designs</td><td>Levels all look alot better.</td><td>Pass</td></tr></tbody></table>

### Evidence

Level one design with the portal at the end

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Level two:

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Level 3:

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

Level 4:

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

Level 5:

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>
