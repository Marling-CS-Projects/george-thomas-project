# 2.2.1 Cycle 1

### Design

For my first cycle it is important for me to create the groundwork of my project to build from. Therefore, in this cycle I will be setting up a basic project using Kaboom.js. This will feature the ground of the game, where the player will spawn. This ground boundary will eventually have the boxing rings on.

Using Kaboom.js which is on Repl, I aimed to complete 4 different objectives in this cycle. These objectives were to give myself a groundwork to build my project from.&#x20;

### Objectives

* [x] Begin basic project using kaboom.js
* [x] Spawn bean
* [x] Implement gravity
* [x] Implement the map floor

### Usability Features

Non-functional aspects: Make the map include graphics that are user-friendly for all users.

### Key Variables

| Variable Name | Use                           |
| ------------- | ----------------------------- |
| setGravity    | sets the gravity for the bean |
| loadSprite    | loads the bean                |
| const player  | spawn location for the bean   |

### Pseudocode

```
Initialize Kaboom library

Load sprite "bean" from "/sprites/bean.png"

Set gravity to 3200

Create a player entity with the following properties:
  - Sprite: "bean"
  - Position: (120, 80)
  - Collision area
  - Physics body
  - Tag: "player"

Create a ground entity with the following properties:
  - Rectangle shape with a width equal to the screen width and a height of 48
  - Outline with a thickness of 4
  - Collision area
  - Position at the bottom of the screen (0, screen height - 25)
  - Static physics body

```

## Development

### Outcome

This cycle has created the map floor for my game, which has enabled me to spawn my player on it. The graphics, however, are still a work in progress as the floor is plain white and the player is the "bean, " a premade sprite from kaboom.js. I split this cycle's code into 3 small and simple sections.

```javascript
import kaboom from "kaboom"
import "kaboom/global"

kaboom();

// Load asset

loadSprite("bean", "/sprites/bean.png"); // The player
```

This section above starts the game and loads the player icon. In this case, it is the "bean".

<pre class="language-javascript"><code class="lang-javascript"><strong>setGravity(3200);
</strong>
const player = add([
  sprite("bean"),
  pos(120, 80),
  area(),
  body(),
  "player"
])
</code></pre>

This section above determines the spawn location and the gravity that the player experiences. This will be crucial for movement in future cycles.

<pre class="language-javascript"><code class="lang-javascript"><strong>add([
</strong>    rect(width(), 48),
    outline(4),
    area(),
    pos(0, height() - 25),
    body({ isStatic: true})
])
</code></pre>

This final section creates the map floor, currently in plain white.

### Challenges

My first big challenge in the development of my project was familiarizing myself with how to use Kaboom.js through Repl. I had no past experience of coding using kaboom on Repl. This meant that I had to do some practice and watch some quick tutorials to get my head around the online library.

## Testing

Evidence for testing

### Tests

<table><thead><tr><th width="87">Test</th><th width="127">Instructions</th><th width="223">What I expect</th><th width="208">What actually happens</th><th>Pass/Fail</th></tr></thead><tbody><tr><td>1</td><td>Run code</td><td>Player spawns in the bottom left hand side of the screen slightly above the ground</td><td>As expected</td><td>Pass</td></tr><tr><td>2</td><td>Run code again</td><td>Map flour to load and be the whole length of the screen</td><td>As expected</td><td>Pass</td></tr><tr><td>3</td><td>Run code after additions</td><td>Player spawns and lands on new boundary </td><td>Player spawns in correct spot. However, player does not fall to the floor and land</td><td>Fail</td></tr><tr><td>4</td><td>Run code with fixed gravity</td><td>Player spawns and lands on the boundary</td><td>As expected - the player falls, lands and does not go through the boundary</td><td>Pass</td></tr></tbody></table>

### Evidence

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

The image above displays what my map looks like on spawn using Kaboom.js sprites. This therefore completes my objective:

* [x] Create a map design for the start of the game and where the player spawns

<figure><img src="../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

This image above shows that gravity has been implemented and the player falls from the spawn point to land on the ground.

* [x] Implement gravity
