# 2.2.6 Cycle 6

### Design

In this cycle, I will implement powerups. And a "win record collector". By this I mean an object that the player collects and it will count as the players boxing record every time they beat a level. They will be collected at the end of each level just before the portal. The boxing record will appear in the top left of the screen. The object at the moment will be kaboom.js design temporarily.



{% file src="../.gitbook/assets/2023-09-06 18-43-58.mkv" %}

### Objectives

* [x] Boxing record
* [x] New powerups

### Usability Features

Non-functional aspects: Enemies that move in a way that is not too hard to defeat but is also not too easy for players.

### Key Variables

| Variable Name | Use |
| ------------- | --- |
|               |     |
|               |     |
|               |     |

### Pseudocode

```


```

## Development

### Outcome

Loading temporary sprites for the enemies

```javascript
loadSprite("enemy", "/sprites/ghosty.png")
loadSprite("boss", "/sprites/bag.png")
```

Adding symbols for enemies

```javascript
const LEVELS = [
	[
		"                                 ",
		"                                 ",
		"                                 ",
		"                                 ",
		"            -              -     ",
		"            -      >       -    @",
		"============----------------=====",
	],
	[
		"                                            ",
		"                                            ",
		"                                            ",
		"            -              -                ",
		"            -              -                ",
		"           --         >    -              @ ",
		"============----------------================",
	],
	[
		"                                                   ",
		"                                                   ",
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
		"          ---           >  -                       --     ",
		"============----------------============------------      ",
	],
	[
		"--------------------------------------------",
		"    -                                       ",
		"--- -                                       ",
		"  - -           -              -            ",
		"  - -          --              -            ",
		"  -           ---           0  -         @  ",
		"==---==========-----------------============",
	],
    
]
```

Defining symbols and setting them as enemies.

```javascript
		"0": () => [
			sprite("boss"),
			area(),
			anchor("bot"),
			body(),
			patrol(),
			offscreen({ hide: true }),
			"enemy",
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
	},
}
```



```javascript
	player.onCollide("danger", () => {
		go("lose")
```

### Challenges

One big challenge in this section was figuring out how to make the enemy walk towards the player inside of the ring. Therefore I have changed my plan slightly, the boss will be the one that walks towards the player, which will be developed in future.

## Testing

Evidence for testing

### Tests

<table><thead><tr><th width="87">Test</th><th width="127">Instructions</th><th width="223">What I expect</th><th width="208">What actually happens</th><th>Pass/Fail</th></tr></thead><tbody><tr><td>1</td><td>Run code</td><td>Player spawns in the bottom left hand side of the screen slightly above the ground</td><td>As expected</td><td>Pass</td></tr><tr><td>2</td><td>Run code again</td><td>Map flour to load and be the whole length of the screen</td><td>As expected</td><td>Pass</td></tr><tr><td>3</td><td>Run code after additions</td><td>Player spawns and lands on new boundary </td><td>Player spawns in correct spot. However, player does not fall to the floor and land</td><td>Fail</td></tr><tr><td>4</td><td>Run code with fixed gravity</td><td>Player spawns and lands on the boundary</td><td>As expected - the player falls, lands and does not go through the boundary</td><td>Pass</td></tr></tbody></table>

### Evidence

