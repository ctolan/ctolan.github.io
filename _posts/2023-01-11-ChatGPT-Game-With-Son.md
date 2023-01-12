*still a draft*

Hello,

First post of 2023 and its a good one. I am creating a Python based figthing game together with/for my son. With all the discussion of ChatGPT I decided to give it a go and see what it can do.
![ChatGPT Game 1]({{ site.url }}/images/ChatGPT-game-1.png)


```python

class Player:
    def __init__(self, name, health, attack1, attack2, attack3):
        self.name = name
        self.health = health
        self.Attack = {"1": attack1, "2": attack2, "3": attack3}
    def choose_attack(self):
        choice = input(f"{self.name}, choose your attack (1, 2, or 3): ")
        return self.Attack[choice]
    def reduce_health(self, amount):
        self.health -= amount


class Attack:
    def __init__(self, name, damage):
        self.name = name
        self.damage = damage
    def __str__(self):
        return self.name


player1 = Player("Patrick", 100, Attack("Punch", 20), Attack("Kick", 30), Attack("Uppercut", 40))
player2 = Player("Conor", 100, Attack("Slash", 25), Attack("Stab", 35), Attack("Smash", 45))

players = [player1, player2]

while True:
    for player in players:
        print(f"{player.name}'s health: {player.health}")
        attack = player.choose_attack()
        other_player = players[1] if player == players[0] else players[0]
        print(f"{player.name} uses {attack}!")
        other_player.reduce_health(attack.damage)
        if other_player.health <= 0:
            print(f"{other_player.name} has been defeated!")
            exit()
```

Plays out as 

```shell
>>> while True:
...     for player in players:
...         print(f"{player.name}'s health: {player.health}")
...         attack = player.choose_attack()
...         other_player = players[1] if player == players[0] else players[0]
...         print(f"{player.name} uses {attack}!")
...         other_player.reduce_health(attack.damage)
...         if other_player.health <= 0:
...             print(f"{other_player.name} has been defeated!")
...             exit()
... 
Patrick's health: 100
Patrick, choose your attack (1, 2, or 3): 2
Patrick uses Kick!
Conor's health: 70
Conor, choose your attack (1, 2, or 3): 3
Conor uses Smash!
Patrick's health: 55
Patrick, choose your attack (1, 2, or 3): 3
Patrick uses Uppercut!
Conor's health: 30
Conor, choose your attack (1, 2, or 3): 2
Conor uses Stab!
Patrick's health: 20
Patrick, choose your attack (1, 2, or 3): 2
Patrick uses Kick!
Conor has been defeated!
```
