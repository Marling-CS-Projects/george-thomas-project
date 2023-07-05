# 2.2.2 Cycle 2

### Design

In the second cycle, I am to further develop my map and create the boxing. This will the allow my project to properly expand. What I mean by that is multiple areas of the game can be developed as a result of the map being completed. These things include: controls and player movement, enemy spawn and movement, combat, and more.

### Objectives

* [x] Extend map
* [x] Create boxing rings

### Usability Features

Non-functional aspects: As the map develops, keep it being easy to understand and traverse for players.

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



```javascript
const level = addLevel([
	// Design the level layout with symbols
	"=              =",
        "=              =",
        "=              =",
], {
	// The size of each block
	tileWidth: 64,
	tileHeight: 64,
	// The position of the most left block
	pos: vec2(900, 785),
	// Define symbol meaning
	tiles: {
"=": () => [
    sprite("steel"),
    area(),
    body({ isStatic: true }),
    anchor("bot"),
 ],

	},
})
```



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



<pre class="language-javascript"><code class="lang-javascript"><strong>add([
</strong>    rect(width(), 48),
    outline(4),
    area(),
    pos(0, height() - 25),
    body({ isStatic: true})
])
</code></pre>



### Challenges



## Testing



### Tests

<table><thead><tr><th width="87">Test</th><th width="127">Instructions</th><th width="223">What I expect</th><th width="208">What actually happens</th><th>Pass/Fail</th></tr></thead><tbody><tr><td>1</td><td>Run code</td><td>Player spawns in the bottom left hand side of the screen slightly above the ground</td><td>As expected</td><td>Pass</td></tr><tr><td>2</td><td>Run code again</td><td>Map flour to load and be the whole length of the screen</td><td>As expected</td><td>Pass</td></tr><tr><td>3</td><td>Run code after additions</td><td>Player spawns and lands on new boundary </td><td>Player spawns in correct spot. However, player does not fall to the floor and land</td><td>Fail</td></tr><tr><td>4</td><td>Run code with fixed gravity</td><td>Player spawns and lands on the boundary</td><td>As expected - the player falls, lands and does not go through the boundary</td><td>Pass</td></tr></tbody></table>

### Evidence

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

This image above displays what my map looks like on spawn using Kaboom.js sprites. This therefore completes my objective:

* [x] Create map design for the start of the game and where the player spawns

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

This image above shows that the gravity has been implement and the player falls from spawn point to land on the ground.

* [x] Implement gravity
