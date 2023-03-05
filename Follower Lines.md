This page is part of the Skyrim Follower Dialogue Template, which is found here. 

# Table of Contents
- Dissection of Conditions
- Bleedout Lines
- Player Death Reactions
- Horse Riding
- Non-hostile Spell Reactions


## Dissection of Conditions


## Bleedout Lines
- Make a bleedout variable.
- ![img](https://imgur.com/1GyiUAY.png)
- Go into your follower's FollowQuest.
- Add a new scene. Check the box for `Interruptible`.
- Right-click and **Add Phase at End**.
- Add your follower as an actor.
- Add another phase.
- Phase 1 should have `IsBleedingOut` on your follower's alias, on **Start**.
- ![img](https://imgur.com/Ttex7J2.png)
- For **Completion**, feel free to be creative, of course. But this is what I have for Katana:
- ![img](https://imgur.com/jGkIpCt.png)
- Here's the code so you can copy it: 
```Follower.GetActorReference().AddItem(RestoreHealth04, 1, true)
Follower.GetActorReference().EquipItem(RestoreHealth04 as form, false, false)
Follower.GetActorReference().RestoreActorValue("Health", 100 as Float)
FollowerBleedoutVar.SetValue(1 as Float)
```
- Make sure to define the properties.
- ![img](https://imgur.com/ACtvVAa.png)
- Here's what Phase 2 has on **Start**.
- Go to the Quest Aliases, and select your follower. 
- Add a new script 
## Player Death Reactions

## Horse Riding

## Non-hostile Spell Reactions