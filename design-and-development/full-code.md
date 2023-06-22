# Full Code

```javascript
import kaboom from "kaboom"
import "kaboom/global"

kaboom();

// Load assets
loadSprite("player", "/sprites/bean.png"); // The player
loadSprite("ground", "/sprites/grass.png"); // The map floor
loadSprite("ghosty", "/sprites/ghosty.png"); // The temporary enemy
loadSprite("ring", "/sprites/steel.png"); // The boxing ring ropes (edges)

setBackground(33, 37, 42); // Set a temporary basic grey color

setGravity(2400);

const SPEED = 480;
let isPlayerGrounded = true;

const player = add([
  sprite("player"),
  pos(0, 0),
  area(),
  body(),
  "player"
]);

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
  "=": [sprite("ground"), area(), "ground"],
  "@": [area(), body(), "player"],
  "e": [sprite("ghosty"), area(), "enemy"],
  "/": [sprite("ring"), area(), "ring"]
});

player.collides("ring", () => {
  // Handle collision with ring (optional)
});

keyPress("space", () => {
  if (isPlayerGrounded) {
    player.jump();
    isPlayerGrounded = false;
  }
});

keyDown("left", () => {
  player.move(-SPEED, 0);
});

keyDown("right", () => {
  player.move(SPEED, 0);
});

player.collides("ground", (ground) => {
  const bottomOfPlayer = player.pos.y + player.height / 2;
  const topOfGround = ground.pos.y - ground.height / 2;

  if (bottomOfPlayer <= topOfGround) {
    isPlayerGrounded = true;
  }
});

player.collides("enemy", () => {
  player.pos = level.defaultPos;
});

```
