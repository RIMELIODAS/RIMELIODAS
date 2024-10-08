## Complete Code for Meliodas

```python
class Character:
    def __init__(self, name, character_class):
        self.name = name
        self.character_class = character_class
        self.level = 1
        self.hp = 100  # Starting hit points
        self.skills = []
        self.is_defending = False
        self.last_attack_damage = 0  # For Full Counter
        self.demon_mark_active = False
        self.assault_mode_active = False

    def level_up(self):
        self.level += 1
        self.hp += 10  # Increase HP on level up

    def take_damage(self, damage):
        if self.is_defending:
            damage = damage // 2  # Reduce damage when defending
            print(f"{self.name} defends the attack! Damage reduced to {damage}")
        self.hp -= damage
        self.last_attack_damage = damage  # Store last attack damage
        if self.hp <= 0:
            print(f"{self.name} has been defeated!")
        else:
            print(f"{self.name} HP: {self.hp}")

    def defend(self):
        self.is_defending = True
        print(f"{self.name} is defending!")

    def stop_defend(self):
        self.is_defending = False
        print(f"{self.name} stopped defending!")

    def activate_demon_mark(self):
        self.demon_mark_active = True
        print(f"{self.name} activates Demon Mark, enhancing abilities!")

    def deactivate_demon_mark(self):
        self.demon_mark_active = False
        print(f"{self.name} deactivates Demon Mark.")

    def enter_assault_mode(self):
        self.assault_mode_active = True
        print(f"{self.name} enters Assault Mode, gaining immense power!")

    def exit_assault_mode(self):
        self.assault_mode_active = False
        print(f"{self.name} exits Assault Mode.")

class Skill:
    def __init__(self, name, damage, special_effect=None):
        self.name = name
        self.damage = damage
        self.special_effect = special_effect

    def activate(self, attacker, enemy):
        if self.special_effect:
            self.special_effect(attacker, enemy)
        else:
            print(f"{attacker.name} uses {self.name}!")
            enemy.take_damage(self.damage)

# Special effects for skills
def full_counter(attacker, enemy):
    print(f"{attacker.name} activates Full Counter!")
    counter_damage = attacker.last_attack_damage * 2  # Deal double the last damage received
    enemy.take_damage(counter_damage)
    print(f"{attacker.name} counters and deals {counter_damage} damage!")

def hellblaze(attacker, enemy):
    print(f"{attacker.name} unleashes Hellblaze!")
    fire_damage = 25  # Fixed damage for demonstration
    enemy.take_damage(fire_damage)

def divine_slayer(attacker, enemy):
    print(f"{attacker.name} uses Divine Slayer!")
    fire_damage = 30  # Fixed damage
    enemy.take_damage(fire_damage)

# Example of creating Meliodas and his skills
meliodas = Character(name="Meliodas", character_class="Dragon Sin of Wrath")

# Define skills
full_counter_skill = Skill(name="Full Counter", damage=0, special_effect=full_counter)
sword_slash = Skill(name="Sword Slash", damage=15)
hellblaze_skill = Skill(name="Hellblaze", damage=0, special_effect=hellblaze)
divine_slayer_skill = Skill(name="Divine Slayer", damage=0, special_effect=divine_slayer)

# Add skills to Meliodas
meliodas.skills.append(full_counter_skill)
meliodas.skills.append(sword_slash)
meliodas.skills.append(hellblaze_skill)
meliodas.skills.append(divine_slayer_skill)

# Example of an enemy
class Enemy:
    def __init__(self, name, hp):
        self.name = name
        self.hp = hp
        self.last_attack_damage = 0

    def take_damage(self, damage):
        self.hp -= damage
        if self.hp <= 0:
            print(f"{self.name} has been defeated!")
        else:
            print(f"{self.name} HP: {self.hp}")

# Simulating a battle against a goblin
goblin = Enemy(name="Goblin", hp=30)

# Simulate an attack from the enemy
enemy_attack_damage = 10
goblin.last_attack_damage = enemy_attack_damage
meliodas.take_damage(enemy_attack_damage)  # Meliodas takes damage

# Meliodas uses Full Counter
meliodas.defend()  # Start defending
full_counter_skill.activate(meliodas, goblin)  # Activate Full Counter
meliodas.stop_defend()  # Stop defending

# Meliodas uses a regular attack
sword_slash.activate(meliodas, goblin)  # Meliodas attacks the goblin

# Meliodas uses Hellblaze
hellblaze_skill.activate(meliodas, goblin)  # Meliodas uses Hellblaze

# Meliodas uses Divine Slayer
divine_slayer_skill.activate(meliodas, goblin)  # Meliodas uses Divine Slayer
```

### Key Features Included

1. **Character Class**: Represents Meliodas with properties like name, level, HP, skills, defense capabilities, and modes (Demon Mark, Assault Mode).
  
2. **Skill Class**: Represents skills with a name, damage, and optional special effects.

3. **Special Effects**: Functions for skills such as **Full Counter**, **Hellblaze**, and **Divine Slayer**, showcasing their mechanics.

4. **Enemy Class**: Represents an enemy with the capability to take damage.

5. **Simulation**: The code simulates a battle where Meliodas interacts with an enemy, using his skills and abilities.
