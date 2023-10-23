# Full Code

```javascript
import kaboom from "kaboom";
import "kaboom/global";

let wins: number = 0;


kaboom({
    background: [90, 90, 90],
})


loadPedit("boxer", "/sprites/boxer.pedit")
loadPedit("enemy", "/sprites/enemy.pedit")
loadPedit("ring", "/sprites/ring.pedit")
loadSprite("portal", "/sprites/portal.png")
loadPedit("belt", "/sprites/belt.pedit")
loadPedit("water", "/sprites/water.pedit")
loadPedit("rope", "/sprites/rope.pedit")
loadPedit("floor", "/sprites/floor.pedit")
loadPedit("boss", "/sprites/boss.pedit")

setGravity(3200)


function patrol(speed = 500, dir = 1) {
    return {
        id: "patrol",
        require: ["pos", "area"],
        add() {
            this.on("collide", (obj, col) => {
                if (col.isLeft() || col.isRight()) {
                    dir = -dir
                }
            })
        },
        update() {
            this.move(speed * dir, 0)
        },
    }
}


function big() {
    let timer = 0
    let isBig = false
    let destScale = 3
    return {

        id: "big",

        require: ["scale"],

        update() {
            if (isBig) {
                timer -= dt()
                if (timer <= 0) {
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


const JUMP_FORCE = 950
const MOVE_SPEED = 480
const FALL_DEATH = 2400

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


const levelConf = {
    tileWidth: 64,
    tileHeight: 64,
    tiles: {
        "=": () => [
            sprite("floor"),
            area(),
            body({ isStatic: true }),
            anchor("bot"),
            offscreen({ hide: true }),
            "platform",
        ],
        "-": () => [
            sprite("ring"),
            area(),
            body({ isStatic: true }),
            offscreen({ hide: true }),
            anchor("bot"),
        ],
        "r": () => [
            sprite("rope"),
            area(),
            body({ isStatic: true }),
            offscreen({ hide: true }),
            anchor("bot"),
        ],
        "0": () => [
            sprite("boss"),
            scale(3),
            area(),
            anchor("bot"),
            body(),
            patrol(),
            offscreen({ hide: true }),
            "boss",
        ],
        "^": () => [
            sprite("spike"),
            area(),
            body({ isStatic: true }),
            anchor("bot"),
            offscreen({ hide: true }),
            "danger",
        ],
        "#": () => [
            sprite("water"),
            scale(2),
            area(),
            anchor("bot"),
            body(),
            offscreen({ hide: true }),
            "water",
        ],
        ">": () => [
            sprite("enemy"),
            scale(3),
            area(),
            anchor("bot"),
            body(),
            patrol(),
            offscreen({ hide: true }),
            "enemy",
        ],
        "@": () => [
            sprite("portal"),
            area({ scale: 0.5 }),
            anchor("bot"),
            pos(0, -12),
            offscreen({ hide: true }),
            "portal",
        ],
    },
}

scene("game", ({ levelId, wins } = { levelId: 0, wins: 0 }) => {


    const level = addLevel(LEVELS[levelId ?? 0], levelConf)


    const player = add([
        sprite("boxer"),
        pos(0, 0),
        area(),
        scale(3),
        body(),
        big(),
        anchor("bot"),
    ])



    
let playerHealth = 100;


let healthBar = add([
  rect(playerHealth, 10),
  pos(10, 0),
  color(0),


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
});



    player.onUpdate(() => {

        camPos(player.pos);

        if (player.pos.y >= FALL_DEATH) {
            go("lose");
        }
    });
    player.onBeforePhysicsResolve((collision) => {
        if (collision.target.is(["platform", "soft"]) && player.isJumping()) {
            collision.preventResolution();
        }
    });
    player.onPhysicsResolve(() => {

        camPos(player.pos);
    });

    player.onCollide("danger", () => {
        go("lose");
    });
    player.onCollide("portal", () => {

        if (levelId + 1 < LEVELS.length) {
            go("game", {
                levelId: levelId + 1,
                wins: wins,
            });
        } else {
            go("win");
        }
    });
    player.onGround((l) => {
        if (l.is("enemy")) {
            player.jump(JUMP_FORCE * 1.1);
            destroy(l);
            playerHealth += 35;
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
        }
    });
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
;

player.onCollide("water", (a) => {
        destroy(a)
        player.biggify(5)
        playerHealth += 35;
    })

    player.onCollide("belt", (c) => {
        destroy(c)
        wins += 1
        winsLabel.text = wins
    })

function jump() {

        if (player.isGrounded()) {
            player.jump(JUMP_FORCE)
        }
    }


    onKeyPress("space", jump)

    onKeyDown("left", () => {
        player.move(-MOVE_SPEED, 0)
    })

    onKeyDown("right", () => {
        player.move(MOVE_SPEED, 0)
    })

    onKeyPress("down", () => {
        player.weight = 3
    })

    onKeyRelease("down", () => {
        player.weight = 1
    })

    onGamepadButtonPress("south", jump)

    onGamepadStick("left", (v) => {
        player.move(v.x * MOVE_SPEED, 0)
    })

    onKeyPress("f", () => {
        setFullscreen(!isFullscreen())
    })
})


scene("lose", () => {
    add([
        text("You Lose"),
    ])
    onKeyPress(() => go("game"))
})

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
        text("You made it with a boxing record of " + "5" + " wins!"),
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
        sprite("boxer"),
        pos(1400, 0),
        scale(5),
        "belt"
    ]);
    loop(0.05, () => {
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
    loop(0.05, () => {
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
    loop(0.01, () => {
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
    loop(0.001, () => {
        boss1.pos.y += 1;
        if (boss1.pos.y > height()) {
            destroy(boss1);
        }
    });


})

go("game")
```
