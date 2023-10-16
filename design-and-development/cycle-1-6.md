# 2.2.7 Cycle 7

### Design

In this cycle, combat will be developed, a health bar will be added and the enemies/player will do damage. Additionally, the final boss will be developed so that it has more health is harder to defeat and does more damage.

### Objectives

* [x] Enemy combat
* [x] Implement health bar
* [x] Final boss interaction

### Usability Features

Non-functional aspects: Enemies that move in a way that is not too hard to defeat but is also not too easy for players.

### Key Variables

| Variable Name | Use                                                                                                                                                                                                                                                    |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| playerHealth  | States the players health which starts at 100                                                                                                                                                                                                          |
| healthBar     | For the player's health bar. Its properties are rect(playerHealth, 10), which means that it is the size of the player's current health, pos(10, 0), which is the position of the health bar above the player, colour(0), which makes the colour black. |

### Pseudocode

```
Set playerHealth to 100
Create a healthBar with width equal to playerHealth, height 10, and position (10, 0)

On player update:
    Set healthBar position to (player.x - 50, player.y - 160)
    Set healthBar width to playerHealth

    If playerHealth is less than or equal to 0:
        Go to "lose" state

Create an enemy with width 32, height 32, and position (125, 125)

On player collision with "enemy":
    Decrease playerHealth by 35
    If playerHealth is less than 0, set playerHealth to 0
    Set healthBar width to playerHealth 
    If playerHealth is less than 1:
        Go to "lose" state

On player collision with "boss":
    Decrease playerHealth by 67
    If playerHealth is less than 0, set playerHealth to 0
    Set healthBar width to playerHealth 
    If playerHealth is less than 1:
        Go to "lose" state
```

## Development

### Outcome

Full code for the health bar. This displays the code for the player's health, the health bar, and their responses to collisions with both the enemies and the boss.

```javascript
let playerHealth = 100;


let healthBar = add([
  rect(playerHealth, 10),
  pos(10, 0),
  colour(0),


]);
player.on("update", () => {

  healthBar.pos = player.pos.add(-50, -160);
  healthBar.width = playerHealth;

  if (playerHealth <= 0) {
    go("lose");
  }
});

player.onCollide("enemy", () => {
  playerHealth -= 35;

  if (playerHealth < 0) playerHealth = 0;
  healthBar.width = playerHealth; 
  if (playerHealth < 1) {
    go("lose");
  }
});
player.onCollide("boss", () => {
  playerHealth -= 67;

  if (playerHealth < 0) playerHealth = 0;
  healthBar.width = playerHealth; 
  if (playerHealth < 1) {
    go("lose");
  }
})
```

After picking up the water-bottle, the player now receives a + 35 health. This is an update that was required as the players health decreased on the same collision as defeating the enemy.

```javascript
    player.onGround((l) => {
        if (l.is("enemy")) {
            player.jump(JUMP_FORCE * 1.1);
            destroy(l);
            playerHealth += 35; //new addition
            const belt = add([
                sprite("belt"),
                pos(player.pos.x, 0),
                scale(2),
                "belt"
            ]);
```

### Challenges

The main challenge that I have faced during the development of the combat is the player taking damage when defeating the enemy. What I mean by that is when the player jumps and lands on the enemy, it is meant to just defeat the enemy and not do any damage to the player. Instead, when the player jumps onto the enemy, the player takes damage.

It took a while to find a fix and to change the code to prevent it from happening. In the end, the only solution that I found was to just add the same amount of health lost back. As a result, the player loses 35 health and gains it right back, all in the same collision. This fix worked well as there is no delay between losing and gaining the health, so you cannot see the health bar changing during that collision.

## Testing

### Tests

<table><thead><tr><th width="87">Test</th><th width="136">Instructions</th><th width="223">What I expect</th><th width="208">What actually happens</th><th>Pass/Fail</th></tr></thead><tbody><tr><td>1</td><td>Run code with the enemy combat included. Walk into the enemy and do not attempt to defeat the enemy.</td><td>Upon collision between the player and the enemy characters: the enemy will deal -35 damage to the player, the player to be defeated after 3 collisions as a result of the 100 total health becoming less than 0.</td><td>The player takes -35 damage each time a collision is made with the enemy. The player also is defeated after 3 collisions with the enemy.</td><td>Pass</td></tr><tr><td>2</td><td>Run code and get the player character to defeat the enemy.</td><td>The player will jump onto of the enemy and will defeat the enemy whilst taking no damage.</td><td>The player jumps on top of the enemy and the enemy is defeated. The player does not visibly take any damage as there is no health bar as of yet. Therefore this is technically a pass.</td><td>Pass</td></tr><tr><td>3</td><td>Run code after implementing health bar.</td><td>Health bar spawns as a black rectangle above the player. The health bar stays above the player at all times. The health bar is at the right height so that when the player takes the increase in size from the water-bottle the health bar is still on top of the players hitbox. The health bar decreases in size by a 1/3 each time a collision with the enemy is made. The health bar does not decrease in size when the player jumps on top of the enemy to defeat it.</td><td>All as expected apart from one problem: the players health bar decrease and the player takes damage when jumping on top of the enemy.</td><td>Fail</td></tr><tr><td>4</td><td>Run code with new fix for previous problem.</td><td>Players health/health bar does not decrease upon a collision where the player jumps on top of the enemy. The enemy is defeated as normal</td><td>The players health bar does not decrease and the enemy is defeated after the player jumps on top of the enemy.</td><td>Pass</td></tr></tbody></table>

### Evidence

Screen shot of the health bar being implemented.

* [x] Implement health bar

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

Testing the reactions of the health bar for all possible outcomes excluding the boss.

{% embed url="https://www.youtube.com/watch?v=NqaY7LWF050" %}

Testing the reactions of the health bar after fixes and including the boss interaction, which deals extra damage.

{% embed url="https://youtu.be/BQp1MbxqUZ4" %}

* [x] Enemy combat
* [x] Final boss interaction
