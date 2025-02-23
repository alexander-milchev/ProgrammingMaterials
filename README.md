# BattleSystem

Given in this repository is a simple prototype for a battle system, utilising many mechanics that we will be working on in the real game. I have done my best to make it as presentable as possible while keeping it minimalistic and easy to debug. If you do find any bugs at any point in your work with this system, or if you have a question about it that I have not made clear, you can go ahead and contact me directly, or by submitting a question in the discord server.

## General Rules of the Battle System.

The way the battle system will work is by utilising the Speed stat of each character. 

## The Task:

To begin work, please clone this repository to a private repo of your own or simply on your machine.

We would like you to implement 1 playable character and 1 playable enemy as your task, which we will be judging you by. You must implement any new functions or events that you find necessary to make the implementation work as is written in the design kit provided. You are also allowed to make changes to existing functions or events within reason, but you must record all changes you make with reasons given.

For certain keywords there are explanations in the Glossary below

### Ally Character:

Must be implemented inheriting from AllyUnitBase. You can see the AllyDummy as an example that I have implemented for testing. 

The format for unit information is as follows:
    Character name: class (Weapon name) - Stats

    Passive Name and description (Part of your task is to figure out how to implement Passives. If you are completely stuck I can give ideas for how I'd do it, but I do want to see how you go about implementing them yourself.)

    Ability 1

    Ability 2

    Ability 3

    Ultimate

    Normal Attack
    Special Attack

For the sake of these character kits, you can leave the Weapon stats as empty (+0 for Strength and Spiritual Aptitude and x1 for speed)

**You must choose one of the following kits to implement:**

1) 
    Yua: Provoker (Shield) - 4269 HP, 612 ST, 635 SA, 99 Armor (STC), 70 SR (STC), 100 Essence (STC), 5% CR,  175 Ult Charge, 81 Speed
    **PROTECTION Protocol** (Passive): Once per battle, if an ally other than Yua falls to or below 40% max HP, immediately **Provoke** for 2 turns and grant the ally a 20% max HP Shield for 3 turns.

    **SHIELD Distribution** (17 Essence Cost): Grant all allies a 80% SA Shield for 3 turns.

    **SHIELD Conversion** (12 Essence Cost): As a **Free Action**, sacrifice 20% current HP to gain a Shield equal to the amount of HP sacrificed for 3 turns.

    **PROVOKE Initiative** (30 Essence Cost): **Provoke** for 2 turns. When being struck by an enemy while **PROVOKE Initiative** is active, debuff their ST and SA by 15% of base for 1 turn.

    **COMBINED SHIELD Bash** (Ult): Remove all allied Shields to strike an enemy for 600% ST + 400% of the removed Shields as Physical Damage.

    Normal Attack: Strike an enemy for 100% ST Physical Damage.
    Special Attack: Strike an enemy for 60% ST Physical Damage and heal for 10% missing HP.

2) 
    Yua: Executioner (Sniper Rifle) - 1801 HP, 1793 ST, 638 SA, 12 Armor, 7 SR, 100 Essence (STC), 10 EREG (STC), 35 CR, 140 Ult Charge, 119 Speed
    **Crippling Bullets** (Passive): Damaging an enemy to reduce their HP to or below 50% applies **Mangled** for 2 turns, once per enemy per battle.

    **Tactical Advantage** (13 Essence Cost): Strike an enemy, dealing x% ST Physical Damage, then Advance the next action by 20%

    **Eagle Strike** (8 Essence Cost): As a Free Action once per turn, gain **Eagle Strike**.
    **Eagle Strike** - If the next attack critically strikes, it deals 2x damage instead of 1.75x damage and Eagle Strike is dispelled. Otherwise, dispell Eagle Strike.

    **Lethal Directive** (30 Essence Cost): Target an enemy. At the start of the next turn, deal 300% ST Physical Damage to the targeted enemy and end the turn. Lethal Directive has 50% **Execute**.

    **Synthetic Erasure** (Ult): As a **Free Action**, deal 60% current HP Physical Damage to an enemy, up to a maximum of 25.000 pre-mitigation damage.

    Normal Attack: Strike an enemy for 100% ST Physical Damage.
    Special Attack: Strike an enemy and two adjacent enemies for 30% ST Physical Damage.

### Enemy Characters

Must be implemented inhereting from EnemyUnitBase. You can look at EnemyDummy as an example that I have implemented for testing.

The format for unit information is as follows:
    Kit: Stats

    Enemy Name
    List of Abilities
    ...

    Behaviour:
    If Else statements that define the behaviour of this enemy. This would be implemented inheriting from EnemyActionSystem. Again, see dummy for example on how that would look.

**You must choose one of the following to implement**

1) 
    Kit: 15000 HP, 160 ST, 160 SA, 150 AR, 150 SR, 110 Speed

    Battlecaster Oni (Allrounder)
    **Cone of Frost** - Deal 25% SA Spiritual Damage to all enemies and apply 10% **Slow** for 2 turns.

    **Icicle** - Hit an enemy, dealing 125% SA Spiritual Damage and increase SA by 25% permanently

    **Cold Touch** - Hit an enemy ONCE for 50% SA + 50% ST Physical Damage and apply 10% **Slow** for 2 turns.


    Behaviour:
    If number of enemies without **Slow** applied by self >= 2 and last used **Cone of Frost** > 3 turns ago
        Use **Cone of Frost**
    Else If the speed of the fastest enemy > own speed and not slowed and fastest enemy is targetable (Not being provoked to another enemy or untargetable in another way)
        Use **Cold Touch** on them
    Else Alternate **Icicle** and **Cold Touch** (prioritising not slowed targets)

2) 
    Kit: 10500 HP, 240 ST, 120 SA, 110 AR, 100 SR, 120 Speed

    Ravager Oni (Assassin)
    **Hunter's Mark** - Gain **Intangible** and target an enemy, apply a 20% DMG Taken debuff on them for 2 turns.

    **Feast Rush** - Hit an enemy, dealing 150% ST damage once, then again dealing 50% ST + 10% missing HP damage.

    **Bloody Claws** - Hit enemy twice for 45% ST damage. Advance own action by 10%


    Behaviour:
    If **Hunter's Mark** last used > 3 turns ago
        Use **Hunter's Mark** on lowest HP enemy
    Else If Last ability used was **Hunter's Mark** and the debuffed enemy is still targetable or last used > 4 turns ago
        Use **Feast Rush**
    Else **Bloody Claws** random enemy.

### Glossary

 - Provoke: Prevents allies without Provoke from being targetted.
 - Free Action: Does not end your turn after using it.
 - Mangled: Prevents affected character from being healed from any source.
 - Intangible: Prevents affected character from being a valid target. Loses Intangible as soon as any other action is used.

### Additions

If you would like to make any additions to the system, or would like to design something yourself, you are welcome to do so, be it to test the system further or otherwise. You are also welcome to turn in any extra functionality and we can consider it as audition material.

# Operational Guidelines

When you first launch the program, only the Character selection section should be enabled. You can hereby add instances of characters you wish to use for the battle test. Pressing any of the long buttons at the top will make a new instance of a character. After that you must press "Add Character" to add them to either the Ally team or the Enemy team.

You may remove the last added Ally or Enemy with the 2nd and 3rd buttons respectively. When you are done creating your teams for the test you can press Start Battle.

Any time it is the Ally's turn, the different ally action buttons will become available. Pressing one will initiate the specified action, if possible. If the chosen skill requires targets to be selected, the targetting buttons under the character Icons will be enabled.

During targetting, each button will toggle its respective character as a "target". Pressing the Confirm Targets button will tell you if you have selected more or less than 1 character, as currently most target skills require targetting 1 unit only.

After you confirm a correct number of targets, all buttons should be disabled except the Confirm button. This will allow you to confirm that the skill did what you believe it should be doing. By pressing confirm you will continue to the next turn.

During an Enemy turn, They should print out the name of the move they used in the top left corner. After this you will have to confirm that what you think should be happening did happen before pressing the Confirm button again.

## System Details

Some of the more important detils about the inner workings of the system are as follows:

Battle Manager holds the functions for getting the next turn character or getting characters as viable targets. New functions can be added as seen fit. 

Each unit has an action system component attached to them. The Action System dictates how a turn is taken and when the actual action gets done. This would be an ideal place to check for **End of Turn Effects**, **Start of Turn Effects** or other such "Events" relating to a character's turn.

Enemy Action Systems also have an Enemy Decision Making function. This holds the behavioural flowchart of the enemy.

Status Effects are split into 2 types: Buffs & Debuffs and Non-Scaling Statuses.

A Buff or Debuff will have a target stat. This could be something like Strength or Speed or it could be Damage Taken or Healing Received. Anything that can have a numerical value will be a Buff/Debuff.

Non-scaling statuses will hold everything else, such as **Stun**, **Intangible**, **Provoke**, etc. Basically anything else. Stun and Intangible are **NOT** currently implemented.

Shields are not considered Status Effects and are instead their own thing.

Whenever working with enemy decision making/targetting, if an attack targets "Ally" logically, you must target an Enemy in the program code, and vice versa, as Ally Units are stored separately from Enemy Units in the Battle System.