# Suggested Code Solutions for PONG in mBlock
# ポングのおすすめのソリューション

### Information / 案内
This is a bilingual file that has official (possible) code solutions for the PONG substitute final game for *Python from Scratch.*

*Python from Scratch*のかわりの最終テストのためのオフィシャルのプログラミングソリューションです。２カ国語であります。


## The Ball Sprite / ボールスプライト
```Python
from mblock import event
import random
import time

x_direction = ["paddle1", "paddle2"]

@event.greenflag
def on_greenflag():
    speed = 5
    sprite.x, sprite.y = 0, 0
    sprite.point_towards(random.choice(x_direction))
    sprite.play("whistle")
    time.sleep(1)

    while True:
        sprite.forward(speed)
        if sprite.touching('paddle1'):
            sprite.play("Finger Snap")
            speed += .5
            if sprite.get_property('paddle1', 'direction') == 90:
                sprite.point_in_direction(127)
            if sprite.get_property('paddle1', 'direction') == -90:
                sprite.point_in_direction(48)

        if sprite.touching('paddle2'):
            sprite.play("Finger Snap")
            speed += .5
            if sprite.get_property('paddle2', 'direction') == 90:
                sprite.point_in_direction(-127)
            if sprite.get_property('paddle2', 'direction') == -90:
                sprite.point_in_direction(-48)

        sprite.bounce()
            
        if sprite.x <= -222 or sprite.x >= 222:
            sprite.play("whistle")
            time.sleep(2)
            sprite.x, sprite.y = 0, 0
            sprite.play_until_done("whistle")
            speed = 5
            time.sleep(2)
            sprite.point_towards(random.choice(x_direction))
            continue

        
```

## `paddle1`
```Python
from mblock import event
import time

speed = 8

@event.greenflag
def on_greenflag():
    sprite.x = -195
    sprite.y = 14
    score = 0

    while True:
        if sprite.is_keypressed('s'):
            sprite.y -= speed
            sprite.point_in_direction(90)
        if sprite.is_keypressed('w'):
            sprite.y += speed
            sprite.point_in_direction(-90)

        if sprite.y > 149:
            sprite.y = 149
        if sprite.y < -149:
            sprite.y = -149

        if sprite.get_property("Ball", "x") >= 222:
            score += 1
            time.sleep(2)
            continue

        if score == 12:
            sprite.say("勝った！！",2)
            sprite.say("GAME OVER!", 2)
            sprite.stop_all()

```

## `paddle2`
```Python
from mblock import event
import time

speed = 8

@event.greenflag
def on_greenflag():
    sprite.x = 196
    sprite.y = 17
    score = 0

    while True:
        if sprite.is_keypressed('down arrow'):
            sprite.y -= speed
            sprite.point_in_direction(90)
        if sprite.is_keypressed('up arrow'):
            sprite.y += speed
            sprite.point_in_direction(-90)

        if sprite.y > 149:
            sprite.y = 149
        if sprite.y < -149:
            sprite.y = -149

        if sprite.get_property("Ball", "x")  <= -222:
            score += 1
            time.sleep(2)
            continue

        if score == 12:
            sprite.say("勝った！！",2)
            sprite.say("GAME OVER!", 2)
            sprite.stop_all()


```

## `scoreboard_blue`
```Python
from mblock import event
import time

@event.greenflag
def on_greenflag():
    sprite.x, sprite.y = -60, 143
    sprite.set_costume("0")

    while True:
        if sprite.get_property("Ball", "x") >= 222:
            sprite.next_costume()
            time.sleep(4)
            continue

```

## `scoreboard_red`
```Python
from mblock import event
import time

@event.greenflag
def on_greenflag():
    sprite.x, sprite.y = 44, 143
    sprite.set_costume("0")

    while True:
        if sprite.get_property("Ball", "x") <= -222:
            sprite.next_costume()
            time.sleep(4)
            continue
        
```

End of file / 以上です