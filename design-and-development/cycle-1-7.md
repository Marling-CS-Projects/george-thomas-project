# 2.2.8 Cycle 8

### Design

In this cycle, the design of the game will be developed. The player and enemy characters will be designed in a retro boxing-style fashion. The map floor and the ropes will be designed in a similar style to fit the game. Finally, this cycle will include development on the "Win" scene where there will be a fun design and words to display the player's win record.

### Objectives

* [x] Character Design/Style Development
* [x] Map Design/Style Development
* [x] "Win" Scene Development

### Usability Features

Non-functional aspects: The style of my characters/map etc will be made sure to fit the PEGI rating of 3. The style and designs will also be made so that they fit the desired theme which is retro video game style.

### Key Variables

| Variable Name                  | Use |
| ------------------------------ | --- |
| boxer1, boxer2, boxer3, boxer4 |     |
| enemy1, enemy2, enemy3, enemy4 |     |
| boss1                          |     |

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

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

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



```javascript
```



```javascript
```

### Challenges



## Testing

Evidence for testing

### Tests

<table><thead><tr><th width="87">Test</th><th width="127">Instructions</th><th width="223">What I expect</th><th width="208">What actually happens</th><th>Pass/Fail</th></tr></thead><tbody><tr><td>1</td><td></td><td></td><td></td><td></td></tr></tbody></table>

### Evidence

