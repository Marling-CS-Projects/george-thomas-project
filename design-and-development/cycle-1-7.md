# 2.2.8 Cycle 8

### Design

In this cycle, the design of the game will be developed. The player and enemy characters will be designed in a retro boxing-style fashion. The map floor and the ropes will be designed in a similar style to fit the game. Finally, this cycle will include development on the "Win" scene where there will be a fun design and words to display the player's win record.

I want to also make a few adjustments to the map layout in this cycle. This is because after some test runs in previous cycles, the map layout either encounters some errors, or the map layout does not make much sense in some areas. ([Map Changes](cycle-1-7.md#map-changes))

### Objectives

* [x] Character Design/Style Development
* [x] Map Design/Style Development
* [x] "Win" Scene Development
* [x] Improve the Map-Layout

### Usability Features

Non-functional aspects: The style of my characters/map etc will be made sure to fit the PEGI rating of 3. The style and designs will also be made so that they fit the desired theme which is retro video game style.

### Key Variables

| Variable Name                  | Use                                            |
| ------------------------------ | ---------------------------------------------- |
| boxer1, boxer2, boxer3, boxer4 | Spawns the boxer characters on the "Win" scene |
| enemy1, enemy2, enemy3, enemy4 | Spawns the enemy characters on the "Win" scene |
| boss1                          | Spawns the boss character on the "Win" scene   |

### Pseudocode

```
Procedure WinScene():
    DisplayText("_____________________________________________________________", 0, 1, 2, (33, 73, 196))
    DisplayText("AAAAAAAND NEEEWWWWWW", 700, 90, 1, (135, 206, 235))
    DisplayText("Congratulations! You are the NEW Boxing World Champion!", 400, 120, 1, (135, 206, 235))
    DisplayText("You made it with a boxing record of " + wins + " wins!", 500, 150, 1, (135, 206, 235))
    DisplayText("_____________________________________________________________", 0, 400, 2, (33, 73, 196))

    boxer1 = CreateBoxer(1050, 0, 5)
    boxer2 = CreateBoxer(600, 0, 5)
    boxer3 = CreateWater(1400, 0, 5)
    boxer4 = CreateBoxer(400, 0, 5)
    enemy1 = CreateEnemy(250, 0, 5)
    enemy2 = CreateEnemy(1800, 0, 5)
    enemy3 = CreateEnemy(700, 0, 5)
    enemy4 = CreateEnemy(100, 0, 5)
    boss1 = CreateBoss(800, 0, 7)

    Loop:
        MoveBoxer(boxer1, 0.01)
        MoveBoxer(boxer2, 0.03)
        MoveBoxer(boxer3, 0.005)
        MoveBoxer(boxer4, 0.005)
        MoveEnemy(enemy1, 0.03)
        MoveEnemy(enemy2, 0.03)
        MoveEnemy(enemy3, 0.01)
        MoveEnemy(enemy4, 0.001)
        MoveBoss(boss1, 0.01)

        If boxer1.pos.y > height() Then
            Destroy(boxer1)
        End If
        If boxer2.pos.y > height() Then
            Destroy(boxer2)
        End If
        If boxer3.pos.y > height() Then
            Destroy(boxer3)
        End If
        If boxer4.pos.y > height() Then
            Destroy(boxer4)
        End If
        If enemy1.pos.y > height() Then
            Destroy(enemy1)
        End If
        If enemy2.pos.y > height() Then
            Destroy(enemy2)
        End If
        If enemy3.pos.y > height() Then
            Destroy(enemy3)
        End If
        If enemy4.pos.y > height() Then
            Destroy(enemy4)
        End If
        If boss1.pos.y > height() Then
            Destroy(boss1)
        End If

End Procedure
```

## Development

### Outcome

Here are the screenshots of the style designs for the player character, the enemy character, and the boss character.

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption><p>Player Character Design</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption><p>Enemy Character Design</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption><p>Boss Character Design</p></figcaption></figure>

Here is a screenshot to display the new designs for the boxing ring. It fits the feel of retro and simple.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Underneath is the code for the "Win" scene. It includes the text that is displayed in the centre of the scene. The code also includes the spawning of the characters on the win scene for aesthetics.

```javascript
scene("win", () => {
    add([
        text("_____________________________________________________________"),
        pos(0,1),
        scale(2),
        fixed(),
        color(33,73,196),

    ])
    add([
        text("AAAAAAAND NEEEWWWWWW"),
        pos(700,90),
        scale(1),
        fixed(),
        color(135,206,235),

    ])
    add([
        text("Congratulations! You are the NEW Boxing World Champion!"),
        pos(400,120),
        scale(1),
        fixed(),
        color(135,206,235),

    ])
    add([
        text("You made it with a boxing record of " + wins + " wins!"),
        pos(500, 150),
        scale(1),
        fixed(),
        color(135,206,235),

    ])
    add([
        text("_____________________________________________________________"),
        pos(0,400),
        scale(2),
        fixed(),
        color(33,73,196),

    ])
    const boxer1 = add([
        sprite("boxer"),
        pos(1050, 0),
        scale(5),
        "belt"
    ]);
    loop(0.01, () => {
        boxer1.pos.y += 1;
        if (boxer1.pos.y > height()) {
            destroy(boxer1);
        }
    });

    const boxer2 = add([
        sprite("boxer"),
        pos(600, 0),
        scale(5),
        "belt"
    ]);
    loop(0.03, () => {
        boxer2.pos.y += 1;
        if (boxer2.pos.y > height()) {
            destroy(boxer2);
        }
    });

    const boxer3 = add([
        sprite("water"),
        pos(1400, 0),
        scale(5),
        "belt"
    ]);
    loop(0.005, () => {
        boxer3.pos.y += 1;
        if (boxer3.pos.y > height()) {
            destroy(boxer3);
        }
    });
    const boxer4 = add([
        sprite("boxer"),
        pos(400, 0),
        scale(5),
        "belt"
    ]);
    loop(0.005, () => {
        boxer4.pos.y += 1;
        if (boxer4.pos.y > height()) {
            destroy(boxer4);
        }
    });

    const enemy1 = add([
        sprite("enemy"),
        pos(250, 0),
        scale(5),
        "belt"
    ]);
    loop(0.03, () => {
        enemy1.pos.y += 1;
        if (enemy1.pos.y > height()) {
            destroy(enemy1);
        }
    });

    const enemy2 = add([
        sprite("enemy"),
        pos(1800, 0),
        scale(5),
        "belt"
    ]);
    loop(0.03, () => {
        enemy2.pos.y += 1;
        if (enemy2.pos.y > height()) {
            destroy(enemy2);
        }
    });

    const enemy3 = add([
        sprite("enemy"),
        pos(700, 0),
        scale(5),
        "belt"
    ]);
    loop(0.01, () => {
        enemy3.pos.y += 1;
        if (enemy3.pos.y > height()) {
            destroy(enemy3);
        }
    });
    const enemy4 = add([
        sprite("enemy"),
        pos(100, 0),
        scale(5),
        "belt"
    ]);
    loop(0.001, () => {
        enemy4.pos.y += 1;
        if (enemy4.pos.y > height()) {
            destroy(enemy4);
        }
    });
    const boss1 = add([
        sprite("boss"),
        pos(800, 0),
        scale(7),
        "belt"
    ]);
    loop(0.01, () => {
        boss1.pos.y += 1;
        if (boss1.pos.y > height()) {
            destroy(boss1);
        }
    });


})
```

This code shows the addition of the "wait" function, were the game ends and cuts to the "Win" scene 2 seconds after the player defeats the boss.

```javascript
player.onGround((l) => {
        if (l.is("boss")) {
            player.jump(JUMP_FORCE * 1.1);
            destroy(l);
            playerHealth += 67;
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
            wait(4, () => {
                destroy(belt);
            });
            wins += 1;
            const winsLabel = add([
                text("Win record: " + wins + " - 0"),
                pos(24, 24),
                scale(2),
                fixed(),
            ]);
            wait(2, () => {
                go("win");
            });
        }
    });
```

### Map Changes

Here is the code for the map changes that I have made. As mentioned in the description of this cycle, I wanted to make some changes to the map layout that I believe were necessary. Firstly, I originally stuck to my plan to have a tunnel for the second to last level. This was because it suited real-life boxing and therefore made sense to add to my game. However, due to the water bottle power-up increasing the player's size, the player would take the power-up but then get stuck trying to get into the tunnel. Secondly, I didn't end up liking my planned final level, it just didn't feel right with the roof that it had before. As a result, I have changed it to better fit being the final grand stadium for the boss fight.

```javascript
const LEVELS = [
    [
        "                              ",
        "                              ",
        "                              ",
        "                        #     ",
        "         r              r     ",
        "         r      >       r    @",
        "=========----------------=====",
    ],
    [
        "                                 ",
        "                                 ",
        "                                 ",
        "                        #        ",
        "         r              r        ",
        "         r          >   r      @ ",
        "=========----------------========",
    ],
    [
        "                                                ",
        "                                                ",
        "                                                ",
        "                        #                       ",
        "         r              r                       ",
        "         r           >  r                      @",
        "=========----------------=====   ==   ==   ==  =",
    ],
    [
        "                                                    ",
        "                                                    ",
        "                                                  @ ",
        "                        #                       === ",
        "         r              r                ===        ",
        "         r           >  r         ===               ",
        "=========----------------======                     ",
    ],
    [
        "                                          ",
        "                                          ",
        "                                          ",
        "                                          ",
        "                                          ",
        "=======                                   ",
        "                             #            ",
        "              r              r            ",
        "              r           0  r            ",
        "            ==----------------==          ",
        "            ====================          ",
        "            ====================          ",
        "            ====================          ",
        "            ====================          ",
        "            ====================          ",
    ],

]
```

### Challenges

One challenge in this cycle was deciding on how to style the characters. I questioned whether I wanted to design them myself or use outside resources for ideas. I thought because I designed the water bottle and the boxing "belt", I would have the skills to draw the boxers themselves. However, after some attempts at drawing the characters, I realised that I do not have the skills to draw the characters in a way that I like to fit my game. Therefore, I decided to go with premade character designs for the player and enemy characters. However, as for the boss character design, I half drew it by taking the main idea from the pre-made ones and made a few changes.

Another challenge in this cycle was dealing with what to do after realising that the original plan for the layout of some of the levels was incorrect. Therefore, I adjusted some of the levels repeatedly until I found the perfect format for them.

An additional challenge in this cycle was deciding how I wanted to design the "win" scene. I had already planned what I was going to write on the scene but I found it a challenge to design the end scene. After some variations, I went for the falling characters of the game as I think it is quite amusing and fits the retro video game style.

## Testing

Evidence for testing

### Tests

<table><thead><tr><th width="87">Test</th><th width="127">Instructions</th><th width="223">What I expect</th><th width="208">What actually happens</th><th>Pass/Fail</th></tr></thead><tbody><tr><td>1</td><td></td><td></td><td></td><td></td></tr></tbody></table>

### Evidence

This video tests the new map layout after the changes that were made:

{% embed url="https://youtu.be/OvomQt1ujWA" %}

* [x] Improve the Map-Layout

A video testing the "Win" Scene. It is displayed after a wait of 2 seconds from defeating the final boss:

{% embed url="https://youtu.be/FpdxiaKUEa0" %}

Here is a video displaying a full run of the game. It includes all the movement, combat, power-ups, HUD, boss fight, and the "Win" scene:

{% embed url="https://youtu.be/1WdXdGfHWCc" %}
