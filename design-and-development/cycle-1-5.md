# 2.2.6 Cycle 6

### Design

In this cycle, I will develop my boxing win record system. This will involve a boxing "belt" which will appear once the player has defeated the enemy. The boxing record will appear on the top left of the screen and will just be a single digit representing how many enemies the player has defeated.

Additionally, in this cycle, I will add my new "water bottle" power-up. This powerup will make the player increase in size so that it is easier to defeat the enemy. It will become easier because it will increase the player's hitbox so that it is easier to jump and land on the enemy. This is important because that will eventually be how the enemy is defeated.

As I am required to defeat the enemy to test both of these additions, this cycle will include development on the collisions with the enemy. This means that there needs to be code that allows for a collision between the bottom of the player's hitbox and the top of the enemy hitbox. This will defeat the enemy and will allow for both the boxing record and the new power-up to be added.

### Objectives

* [x] Boxing record
* [x] New powerup
* [x] Enemy to be able to be defeated&#x20;

### Usability Features

Non-functional aspects: The design of both the power-up and the "belt" will be drawn so that it fits the theme of the retro-style boxing game.

### Key Variables

| Variable Name | Use |
| ------------- | --- |
|               |     |
|               |     |
|               |     |

### Pseudocode

```
When the player character is on the ground and collides with an object (l):
    If the collided object (l) is labelled as "enemy":
        Increase the player's jump height by 10%.
        Destroy the enemy object (l).
        Create a conveyor belt object (belt) with a belt sprite, positioned at the player's x-coordinate and at the top of the screen.
        Scale the conveyor belt object by a factor of 2.
        Start a loop that runs every 0.01 seconds:
            Move the conveyor belt downward by 1 unit.
            If the conveyor belt goes below the screen's height:
                Destroy the conveyor belt object.
        Increment the coin count (coins) by 1.
        Update the displayed coin count on the screen (coinsLabel) to reflect the new coin count as a string.

Define a label for displaying the player's coin count (coinsLabel):
    Display the current value of coins at position (24, 24).
    Scale the label by a factor of 2.
    Fix the label in its position on the screen.

Define a function named big:
    Initialize variables: timer to 0, isBig to false, and destScale to 3.
    Define an object with the following properties and methods:
        - id: "big"
        - Requires the "scale" component.
        - Update method:
            If isBig is true:
                Decrement the timer by the time elapsed (dt).
                If the timer reaches or goes below 0, call the smallify method.
            Interpolate the object's scale towards destScale over time, making it grow or shrink smoothly.
        - isBig method: Returns the value of isBig.
        - smallify method:
            Set destScale to 3.
            Reset the timer to 0.
            Set isBig to false.
        - biggify method (with a time parameter):
            Set destScale to 5.
            Set the timer to the specified time.
            Set isBig to true.

Define an object with the following properties and components:
    - Sprite: water
    - Scale: 2
    - Area component
    - Anchor at the bottom
    - Body component
    - Offscreen component (with the option to hide when offscreen)
    - Tag: "water"

When the player character collides with an object labelled as "water" (a):
    Destroy the collided water object (a).
    Make the player character bigger (biggify) for 5 seconds.

Initialize a variable coinPitch to 0.

During the game update:
    If coinPitch is greater than 0:
        Reduce coinPitch by a value proportional to the time elapsed (dt), but ensure it doesn't go below 0.

```

## Development

### Outcome

Loading the newly made sprites:

```javascript
loadPedit("belt", "/sprites/belt.pedit")
loadPedit("water", "/sprites/water.pedit")
```

Code for the collision between the enemy and the player.&#x20;

```javascript
player.onGround((l) => {
    if (l.is("enemy")) {
        player.jump(JUMP_FORCE * 1.1);
        destroy(l);
        const belt = add([
            sprite("belt"), 
            pos(player.pos.x, 0),  
            scale(2),
            "belt"  
        ]);
        loop(0.01, () => {  
            belt.pos.y += 1; 
            if (belt.pos.y > height()) {
                destroy(belt);  
            }
        });
       
        coins += 1;
        coinsLabel.text = coins.toString();
    }
});
```



```javascript
    const coinsLabel = add([
        text(coins),
        pos(24, 24),
        scale(2),
        fixed(),
    ])
```



<pre class="language-javascript"><code class="lang-javascript"><strong>function big() {
</strong>    let timer = 0
    let isBig = false
    let destScale = 3
    return {

        id: "big",

        require: ["scale"],

        update() {
            if (isBig) {
                timer -= dt()
                if (timer &#x3C;= 0) {
                    this.smallify()
                }
            }
            this.scale = this.scale.lerp(vec2(destScale), dt() * 6)
        },

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
</code></pre>



```javascript
        "#": () => [
            sprite("water"),
            scale(2),
            area(),
            anchor("bot"),
            body(),
            offscreen({ hide: true }),
            "water",
```



```javascript
    player.onCollide("water", (a) => {
        destroy(a)
        player.biggify(5)
    })

    let coinPitch = 0

    onUpdate(() => {
        if (coinPitch > 0) {
            coinPitch = Math.max(0, coinPitch - dt() * 100)
        }
    })
```

### Challenges



## Testing

Evidence for testing

### Tests

<table><thead><tr><th width="87">Test</th><th width="127">Instructions</th><th width="223">What I expect</th><th width="208">What actually happens</th><th>Pass/Fail</th></tr></thead><tbody><tr><td>1</td><td></td><td></td><td></td><td></td></tr><tr><td>2</td><td></td><td></td><td></td><td></td></tr><tr><td>3</td><td></td><td></td><td></td><td></td></tr><tr><td>4</td><td></td><td></td><td></td><td></td></tr></tbody></table>

### Evidence

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

{% embed url="https://youtu.be/WT3bBDnDhDY" %}

