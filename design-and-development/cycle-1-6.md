# 2.2.7 Cycle 7

### Design

In this cycle, combat will be developed, a health bar will be added and the enemies/player will do damage. Additionally, the final boss will be developed so that it has more health is harder to defeat and does more damage.

### Objectives

* [x] Enemy combat
* [x] Healthbar
* [x] Final boss completion

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
Initialize playerHealth to 100
Create a red baseHealth rectangle at position (0, 0) with dimensions 100x10
Create a green healthBar rectangle at position (10, 0) with initial width based on playerHealth

Define an event handler for the player's "update" event:
  Position baseHealth and healthBar relative to the player's position
  Update healthBar's width to match playerHealth
  If playerHealth is less than or equal to 0, transition to the "lose" scene

Create an enemy rectangle with dimensions 32x32 at position (125, 125)

Define collision behavior for the player with objects tagged as "enemy":
  Reduce playerHealth by 35
  Ensure playerHealth is not less than 0
  Update healthBar's width to reflect the updated playerHealth
  If playerHealth is less than 1, transition to the "lose" scene

Destroy the baseHealth rectangle

```

## Development

### Outcome



```javascript
let playerHealth = 100;
let baseHealth = add([
  rect(100, 10),
  pos(0, 0),
  color(1, 0, 0),
]);
let healthBar = add([
  rect(playerHealth, 10),
  pos(10, 0),
  color(0, 1, 0),
]);
player.on("update", () => {
  
  baseHealth.pos = player.pos.add(-50, -160);
  healthBar.pos = baseHealth.pos;

  
  healthBar.width = playerHealth;
  
  if (playerHealth <= 0) {
    go("lose");
  }
});
let enemy = add([rect(32, 32), pos(125, 125), "enemy"]);

player.onCollide("enemy", () => {
  playerHealth -= 35;
  
  if (playerHealth < 0) playerHealth = 0;
  healthBar.width = playerHealth; 
  if (playerHealth < 1) {
    go("lose");
  }
});

destroy(baseHealth);
```



```javascript
```



```javascript
```



```javascript
```

### Challenges



## Testing

Evidence for testing

### Tests

<table><thead><tr><th width="87">Test</th><th width="127">Instructions</th><th width="223">What I expect</th><th width="208">What actually happens</th><th>Pass/Fail</th></tr></thead><tbody><tr><td>1</td><td></td><td></td><td></td><td></td></tr><tr><td>2</td><td></td><td></td><td></td><td></td></tr><tr><td>3</td><td></td><td></td><td></td><td></td></tr><tr><td>4</td><td></td><td></td><td></td><td></td></tr></tbody></table>

### Evidence

{% embed url="https://www.youtube.com/watch?v=NqaY7LWF050" %}

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>
