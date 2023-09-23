# 2.2.5 Cycle 5

### Design

In this cycle, I will be adding enemies and their movement. It is important that they spawn in the correct place, that being inside of the ring, and it is important that they move around the ring. I will use more symbols and temporary designs from kaboom.js.

The enemy will spawn at the opposite end of the boxing ring and will patrol the boxing ring. The same will apply to the boss.

### Objectives

* [x] Spawn in enemies
* [x] Enable movement for enemies

### Usability Features

Non-functional aspects: I want my enemies to not be too challenging for the player to defeat. After all, the PEGI rating is low to allow young children to play if they desire. With that being said, the enemy will move at a speed which is not too fast nor too slow.

### Key Variables

| Variable Name                               | Use                                                                                                                                                                                                                      |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| LEVELS                                      | This is an array of level layouts, where each level is represented as an array of strings. It defines the layout of the game levels.                                                                                     |
| "0"                                         | This is a symbol used in the level layout strings, representing the spawn point for the "boss." When this symbol is encountered in the level layout, it creates a boss entity.                                           |
| ">"                                         | This is a symbol used in the level layout strings, representing a normal enemy. When this symbol is encountered in the level layout, it creates a standard enemy entity.                                                 |
| sprite("boss")                              | This defines the sprite for the boss entity, using the image "boss.png."                                                                                                                                                 |
| sprite("ghosty")                            | This defines the sprite for the standard enemy entity, using the image "ghosty.png."                                                                                                                                     |
| area()                                      | This creates a collision area for the enemy entities.                                                                                                                                                                    |
| anchor("bot")                               | This sets the anchor point of the enemy entities to the bottom.                                                                                                                                                          |
| body()                                      | This creates a physics body for the enemy entities.                                                                                                                                                                      |
| patrol()                                    | This represents a function or component that defines patrol behaviour for the enemies.                                                                                                                                   |
| offscreen({ hide: true })                   | This likely defines an offscreen behavior for the entities, hiding them when they go offscreen.                                                                                                                          |
| "enemy"                                     | This is a tag or identifier for the enemy entities, allowing for collision detection with player entities.                                                                                                               |
| player.onCollide("enemy", (e, col) => {...} | This sets up a collision event handler for the player entity when it collides with an entity tagged as "enemy." If the collision is not on the bottom side of the player, it likely triggers a game over state ("lose"). |

### Pseudocode

```
Load sprite "enemy" from "/sprites/ghosty.png"
Load sprite "boss" from "/sprites/bag.png"

Define LEVELS as an array of level layouts, where each level is represented as an array of strings.

Define behaviours for specific symbols used in the level layouts:
- When encountering "0" in the level layout:
  - Create an entity with the following attributes:
    - Display the "boss" sprite
    - Define a collision area
    - Anchor at the bottom
    - Create a physics body
    - Apply a patrol behaviour
    - Set offscreen behaviour to hide
    - Tag the entity as "enemy"

- When encountering ">" in the level layout:
  - Create an entity with the following attributes:
    - Display the "ghosty" sprite
    - Define a collision area
    - Anchor at the bottom
    - Create a physics body
    - Apply a patrol behaviour
    - Set offscreen behaviour to hide
    - Tag the entity as "enemy"

Define an event handler for when the player collides with entities tagged as "enemy":
  - If the collision is not on the bottom side of the player:
    - Transition to the "lose" state or perform a game-over action

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

Declaring what each symbol represents. The "0" represents the spawn for the "boss" which is the final enemy. The ">" is the normal enemy.

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
	player.onCollide("enemy", (e, col) => {
		if (!col.isBottom()) {
			go("lose")

		}
	})
```

### Challenges

One big challenge in this section was figuring out how to make the enemy walk towards the player inside of the ring. Therefore I have changed my plan slightly, the boss will be the one that walks towards the player, which will be developed in future.

## Testing

Evidence for testing

### Tests

<table><thead><tr><th width="87">Test</th><th width="127">Instructions</th><th width="223">What I expect</th><th width="208">What actually happens</th><th>Pass/Fail</th></tr></thead><tbody><tr><td>1</td><td>Run code</td><td>Player spawns in the bottom left hand side of the screen slightly above the ground</td><td>As expected</td><td>Pass</td></tr><tr><td>2</td><td>Run code again</td><td>Map flour to load and be the whole length of the screen</td><td>As expected</td><td>Pass</td></tr><tr><td>3</td><td>Run code after additions</td><td>Player spawns and lands on new boundary </td><td>Player spawns in correct spot. However, player does not fall to the floor and land</td><td>Fail</td></tr><tr><td>4</td><td>Run code with fixed gravity</td><td>Player spawns and lands on the boundary</td><td>As expected - the player falls, lands and does not go through the boundary</td><td>Pass</td></tr></tbody></table>

### Evidence

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>
