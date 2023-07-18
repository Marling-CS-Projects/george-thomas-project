# 2.2.2 Cycle 2

### Design

In the second cycle, I want to further develop my map and create the boxing. This will the allow my project to properly expand. What I mean by that is multiple areas of the game can be developed as a result of the map being completed. These things include: controls and player movement, enemy spawn and movement, combat, and more.

### Objectives

* [x] Extend map
* [x] Create boxing rings

### Usability Features

Non-functional aspects: As the map develops, keep it being easy to understand and traverse for players.

### Key Variables

| Variable Name | Use                      |
| ------------- | ------------------------ |
| const ring    | creates the boxing rings |

### Pseudocode

```
DO THIS
```

## Development

### Outcome

In this small cycle, the aim was to create the boxing rings that the player would have to jump over. In the rings will spawn the enemies, and they will be repeated over and over again.&#x20;

```javascript
const ring = addLevel([
	// Design the level layout with symbols
	" =              =",
        " =              =",
        "=================",
], {
	// The size of each block
	tileWidth: 64,
	tileHeight: 64,
	// The position of the most left block
	pos: vec2(850, 785),
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



### Challenges

My challenge with this task is deciding to carry on with the flour that I have go so far. The plain white block that I currently have has turned out to be quite problematic. I say this because, I am having difficulties extending it. It is not impossible, however quite time consuming.

## Testing

### Tests

<table><thead><tr><th width="87">Test</th><th width="127">Instructions</th><th width="223">What I expect</th><th width="208">What actually happens</th><th>Pass/Fail</th></tr></thead><tbody><tr><td>1</td><td>Run code</td><td>Player spawns in sky and falls to the flour</td><td>As expected</td><td>Pass</td></tr><tr><td>2</td><td>Run code again</td><td>Boxing rings spawn and the player sees one side of boxing ring from spawn</td><td>As expected</td><td>Pass</td></tr><tr><td>3</td><td>Run code again after adjusting spawn location temporarily</td><td>Player spawns entire boxing ring</td><td>As expected</td><td>Pass</td></tr><tr><td>4</td><td>Unhappy with boxing ring height and flour - Changes made - run code</td><td>Player spawns in original position. Boxing ring has a better flour and a better way to get in it.</td><td>As expected - boxing rings look better</td><td>Pass</td></tr><tr><td>5</td><td>Change spawn to the temporary one again to check full boxing ring</td><td>Player spawns and sees the whole new boxing ring</td><td>As expected</td><td>Pass</td></tr></tbody></table>

### Evidence

This first picture shows what the first ring looks like from spawn.

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

This picture shows the boxing ring changes:

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

This image below shows the full boxing ring from the temporary spawn point:

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

* [x] Create boxing rings
* [x] Extend map
