# 2.2.6 Cycle 6

### Design

In this cycle, I will develop my boxing win record system. This will involve a boxing "belt" which will appear once the player has defeated the enemy.

### Objectives

* [x] Boxing record
* [x] New powerup

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
import kaboom from "kaboom";
import "kaboom/global";




kaboom({
	background: [90, 90, 90],
})

// load assets
loadPedit("boxer", "/sprites/boxer.pedit")
loadSprite("bag", "/sprites/bag.png")
loadPedit("enemy", "/sprites/enemy.pedit")
loadSprite("grass", "/sprites/grass.png")
loadSprite("steel", "/sprites/steel.png")
loadSprite("portal", "/sprites/portal.png")
loadPedit("belt", "/sprites/belt.pedit")
loadPedit("water", "/sprites/water.pedit")


setGravity(3200)

// custom component controlling enemy patrol movement
function patrol(speed = 150, dir = 1) {
	return {
		id: "patrol",
		require: [ "pos", "area" ],
		add() {
			this.on("collide", (obj, col) => {
				if (col.isLeft() || col.isRight()) {
					dir = -dir
				}
			})
		},
		update() {
			this.move(speed * dir, 0)
		},
	}
}

// custom component that makes stuff grow big
function big() {
	let timer = 0
	let isBig = false
	let destScale = 3
	return {
		// component id / name
		id: "big",
		// it requires the scale component
		require: [ "scale" ],
		// this runs every frame
		update() {
			if (isBig) {
				timer -= dt()
				if (timer <= 0) {
					this.smallify()
				}
			}
			this.scale = this.scale.lerp(vec2(destScale), dt() * 6)
		},
		// custom methods
		isBig() {
			return isBig
		},
		smallify() {
			destScale = 3
			timer = 0
			isBig = false
		},
		biggify(time) {
			destScale = 5
			timer = time
			isBig = true
		},
	}
}

// define some constants
const JUMP_FORCE = 1320
const MOVE_SPEED = 480
const FALL_DEATH = 2400

const LEVELS = [
	[
		"                              ",
		"                              ",
		"                              ",
		"                              ",
		"         -              -     ",
		"         -      >       - $  @",
		"=========----------------=====",
	],
	[
		"                                    ",
		"                                    ",
		"                                    ",
		"      #     -              -        ",
		"            -              -        ",
		"           --         >    - $    @ ",
		"============----------------========",
	],
	[
		"                                             ",
		"          #                    $             ",
		"                              ---            ",
		"      -              -                       ",
		"     --              -                       ",
		"    ---           >  -                      @",
		"======----------------=====  ===  ===  ===  =",
	],
    [
		"                                          ----------",
		"          #                              --         ",
		"                                        --         @",
		"      -              -           --------      -----",
		"     --              -                        --    ",
		"    ---           >  -           $           --     ",
		"======----------------===========-------------      ",
	],
	[
		"--------------------------------------------",
        "    -                                       ",
		"    -                                       ",
		"--- -               #                       ",
		"  - -           -              -            ",
		"  -            --              -            ",
		"  -           ---           0  -   $     @  ",
		"==---==========-----------------============",
	],
    
]

// define what each symbol means
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
			anchor("bot"),
			body(),
			patrol(),
			offscreen({ hide: true }),
			"enemy",
		],
		"$": () => [
			sprite("belt"),
            scale(2),
			area(),
			pos(0, -9),
			anchor("bot"),
			offscreen({ hide: true }),
			"belt",
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
			sprite("water"),
            scale(2),
			area(),
			anchor("bot"),
			body(),
			offscreen({ hide: true }),
			"water",
		],
		">": () => [
			sprite("enemy"),
            scale(3),
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

scene("game", ({ levelId, coins } = { levelId: 0, coins: 0 }) => {

	// add level to scene
	const level = addLevel(LEVELS[levelId ?? 0], levelConf)

	// define player object
	const player = add([
		sprite("boxer"),
		pos(0, 0),
		area(),
		scale(3),
		body(),
		big(),
		anchor("bot"),
	])

	// action() runs every frame
	player.onUpdate(() => {
		// center camera to player
		camPos(player.pos)
		// check fall death
		if (player.pos.y >= FALL_DEATH) {
			go("lose")
		}
	})

	player.onBeforePhysicsResolve((collision) => {
		if (collision.target.is(["platform", "soft"]) && player.isJumping()) {
			collision.preventResolution()
		}
	})

	player.onPhysicsResolve(() => {
		// Set the viewport center to player.pos
		camPos(player.pos)
	})

	// if player onCollide with any obj with "danger" tag, lose
	player.onCollide("danger", () => {
		go("lose")

	})

	player.onCollide("portal", () => {
		// play("portal") 000000000
		if (levelId + 1 < LEVELS.length) {
			go("game", {
				levelId: levelId + 1,
				coins: coins,
			})
		} else {
			go("win")
		}
	})

	player.onGround((l) => {
		if (l.is("enemy")) {
			player.jump(JUMP_FORCE * 1.1)
			destroy(l)
			addKaboom(player.pos)
		}
	})

	player.onCollide("enemy", (e, col) => {
		// if it's not from the top, die
		if (!col.isBottom()) {
			go("lose")

		}
	})

	// player grows big onCollide with an "apple" obj
	player.onCollide("water", (a) => {
		destroy(a)
		// as we defined in the big() component
		player.biggify(5)
	})

	let coinPitch = 0

	onUpdate(() => {
		if (coinPitch > 0) {
			coinPitch = Math.max(0, coinPitch - dt() * 100)
		}
	})

	player.onCollide("belt", (c) => {
		destroy(c)
		// play("coin", {
			// detune: coinPitch,
		// })
		// coinPitch += 100
		coins += 1
		coinsLabel.text = coins
	})

	const coinsLabel = add([
		text(coins),
		pos(24, 24),
        scale(2),
		fixed(),
	])

	function jump() {
		// these 2 functions are provided by body() component
		if (player.isGrounded()) {
			player.jump(JUMP_FORCE)
		}
	}

	// jump with space
	onKeyPress("space", jump)

	onKeyDown("left", () => {
		player.move(-MOVE_SPEED, 0)
	})

	onKeyDown("right", () => {
		player.move(MOVE_SPEED, 0)
	})

	onKeyPress("down", () => {
		player.weight = 3
	})

	onKeyRelease("down", () => {
		player.weight = 1
	})

	onGamepadButtonPress("south", jump)

	onGamepadStick("left", (v) => {
		player.move(v.x * MOVE_SPEED, 0)
	})

	onKeyPress("f", () => {
		setFullscreen(!isFullscreen())
	})

})

scene("lose", () => {
	add([
		text("You Lose"),
	])
	onKeyPress(() => go("game"))
})

scene("win", () => {
	add([
		text("You Win"),

	])
	onKeyPress(() => go("game"))
})

go("game")
```

Defining symbols and setting them as enemies.

```javascript
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

