# 2.2.1 Cycle 1

### Design

For my first cycle it is important for me to create the groundwork of my project to build from. Therefore, in this cycle I will be setting up a basic project using Kaboom.js. This will feature the ground of the game, where the player will spawn. This ground boundary will eventually have the boing rings on.

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

<pre><code><strong>import kaboom
</strong>import assests
</code></pre>

## Development

### Outcome

This cycle has created the map floor for my game, which has enabled me to spawn my player on it. The graphics however, are still a work in progress as the floor is plain white and the player is the "bean" which is a premade sprite from kaboom.js. I split this cycle's code into 3 small and simple sections.

```javascript
import kaboom from "kaboom"
import "kaboom/global"

kaboom();

// Load asset

loadSprite("bean", "/sprites/bean.png"); // The player
```

This section above starts the game and loads the player icon. In this case it is the "bean".

<pre class="language-javascript"><code class="lang-javascript"><strong>setGravity(2400);
</strong>
const player = add([
  sprite("bean"),
  pos(120, 80),
  area(),
  body(),
  "player"
])
</code></pre>

This section above determines the spawn location and the gravity that the player experiences. This will be crucial for movement in future cycles

<pre class="language-javascript"><code class="lang-javascript"><strong>add([
</strong>    rect(width(), 48),
    outline(4),
    area(),
    pos(0, height() - 25),
    body({ isStatic: true})
])
</code></pre>

This final section creates the map floor. Currently in just plain white.

### Challenges

My first big challenge of the development for my project was familiarizing myself with how to use Kaboom.js through Repl.&#x20;

## Testing

Evidence for testing

### Tests

| Test | Instructions  | What I expect     | What actually happens | Pass/Fail |
| ---- | ------------- | ----------------- | --------------------- | --------- |
| 1    | Run code      | Thing happens     | As expected           | Pass      |
| 2    | Press buttons | Something happens | As expected           | Pass      |

### Evidence

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

This image above displays what my map looks like on spawn using Kaboom.js sprites. This therefore completes my objective:

* [x] Create map design for the start of the game and where the player spawns

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

This image above shows how the player spawns, above ground. Therefore the gravity that I have implemented is used so that the player drops to the ground.

* [x] Implement gravity
