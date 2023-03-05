This page is part of the Skyrim Follower Dialogue Template.

# Table of Contents
- [Dissection of Conditions](https://github.com/annakins/Skyrim/blob/main/Follower%20Lines.md#dissection-of-conditions)
- [Bleedout Lines](https://github.com/annakins/Skyrim/blob/main/Follower%20Lines.md#bleedout-lines)
- [Player Death Reactions](https://github.com/annakins/Skyrim/blob/main/Follower%20Lines.md#player-death-reactions)
- [Horse Riding](https://github.com/annakins/Skyrim/blob/main/Follower%20Lines.md#horse-riding)
- [Non-hostile Spell Reactions](https://github.com/annakins/Skyrim/blob/main/Follower%20Lines.md#non-hostile-spell-reactions)


## Dissection of Conditions
![img](https://imgur.com/xvPOoyw.png)
- This is what this says: 
    - Katana will randomly ask the player to share ale, but the chances of this line popping up are less than 5 out of 100
    - The player needs to have 5 or more ale in their inventory
    - Katana will only say this if she's less than 500 units away from the player
    - The location that they're in needs to NOT be in a clearable place (meaning this keyword is placed on locations that can be marked as "cleared" after the boss has been killed)
    - Katana will only say this if the player is not sneaking
    - The line won't pop up again until after 24 game hours, and even then, the chances are fairly low due to the conditions set (unless you have a habit of being in the same place, with 5 or more ale on your person)

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
```
Follower.GetActorReference().AddItem(RestoreHealth04, 1, true)
Follower.GetActorReference().EquipItem(RestoreHealth04 as form, false, false)
Follower.GetActorReference().RestoreActorValue("Health", 100 as Float)
FollowerBleedoutVar.SetValue(1 as Float)
```
- Make sure to define the properties.
- ![img](https://imgur.com/ACtvVAa.png)
- Here's what Phase 2 has on **Start**:
- ![img](https://imgur.com/VlfEXCP.png)
- For **Completion**, this is the code to add in the Papyrus Fragment box: ```AK69KatanaHealBleedoutVar.SetValue(0 as Float)```
- Don't forget to define your properties, basically every time you have scripts.
- Here's what your scene page should look like:
- ![img](https://imgur.com/5wr2pL3.png)
- Now, go to the Quest Aliases, and select your follower. 
- Add a new script, name it with your prefix + `bleedoutlinesscript`, like so:
- ![img](https://imgur.com/TavkgZV.png)
- Here's the code:
```
Scriptname BleedoutLinesScript extends ReferenceAlias  

scene property FollowerBleedout auto

Event OnEnterBleedout()
Utility.Wait(4)
FollowerBleedout.Start()
endEvent
```
- Select the bleedout scene you just created in the properties. 
- You're done!

## Player Death Reactions
- Create a new quest. Name it prefix + `PlayerDeathQuest`.
- This is what I have, but your conditions will be different. What I have here, it's just checking for if the followers I've made are recruited.
- ![img](https://imgur.com/ChxYpcM.png)
- Let's make a scene in your **FollowQuest**.
- Since we covered scenes briefly in the *Bleedout* example, I'll simply show what the player death reaction scene would look like:
- ![img](https://imgur.com/JWOIaQS.png)
- There's nothing to add in the Papyrus fragments, so let's proceed.
- Let's go back to your ***PlayerDeathQuest***.
- Go into the Alias tab, and add one for the player.
- ![img](https://imgur.com/clo8Mx0.png)
- Here's the script:
```
Scriptname PlayerDeathScript extends ReferenceAlias  

scene property PlayerDiedReaction auto
GlobalVariable property FollowerRecruited auto

function OnDying(Actor akKiller)
if (FollowerRecruited.GetValue() ==1) 
PlayerDiedReaction.Start()
endif
endFunction
```
- Define your properties accordingly, and you're done!


## Horse Riding
- Let's ensure that you have the following:
    - FollowerNoMount package
    - FollowerRide package
    - HorseFollow package
    - HorseStay package
- Create a global variable for your riding, like: *prefix + ridingvar*. - Variable type is short, with a value of 0. You'll find that most global variables will be this way.
- I will show you what I have, but you will see that there are extra variables that are specific to my follower. The globally important conditions are the Recruited variable, and the Riding variable.
- ![img](https://imgur.com/wDH21xR.png)
- ![img](https://imgur.com/BLNc1zu.png)
- ![img](https://imgur.com/q1tI65w.png)
- ![img](https://imgur.com/3ygjEeq.png)
- Let's go to your **FollowQuest**.
- Select your follower's alias.
- Add both the FollowerNoMount and FollowerRide packages in there. **NOTE: The order matters.**
- ![img](https://imgur.com/VJkZzWq.png)
- Do the same with your horse. The Stay package should be above the Follow package.
- Now, select the player in the Quest Alias tab.
- Add a mount script with your prefix.
- ![img](https://imgur.com/Ukp4Pmk.png)
- Here's a basic code to get you started:
```
Scriptname MountScript extends ReferenceAlias

actor property Follower auto
actor property Player auto
actor property Horse auto
faction property CurrentFollowerFaction auto
globalvariable property FollowerRidingVar auto
globalvariable property FollowerRecruited auto

function OnInit()
	self.RegisterForAnimationEvent(Player as objectreference, "tailHorseMount")
	self.RegisterForAnimationEvent(Player as objectreference, "tailHorseDismount")
endFunction

function OnPlayerLoadGame()
	self.RegisterForAnimationEvent(Player as objectreference, "tailHorseMount")
	self.RegisterForAnimationEvent(Player as objectreference, "tailHorseDismount")
endFunction

function OnAnimationEvent(objectreference akSource, String asEventName)
	if akSource == Player as objectreference
		if Follower.IsInFaction(CurrentFollowerFaction)
			Follower.EvaluatePackage()
		endIf
	endIf
	if Player.IsOnMount() && (FollowerRecruited.GetValue() ==1) && FollowerRidingVar.GetValue() == 1 as Float
		Utility.Wait(3)
		Follower.OnAnimationEvent(none, "tailHorseMount")
		Utility.Wait(3)
	endIf
		If Follower.GetActorValue("WaitingForPlayer") == 0
			If asEventName == "tailHorseMount" && !Follower.IsOnMount()				
				if (Follower.GetDistance(Horse) >= 2048) && (FollowerRecruited.GetValue() ==1) 				
				Horse.setAlpha(0.1)
				Horse.MoveTo(Player as objectreference, -500.000 * Math.Sin(Player.GetAngleZ()), -500.000 * Math.Cos(Player.GetAngleZ()))							
				Utility.Wait(0.1)
				Horse.setAlpha(1)					
				endif					
				Utility.Wait(0.3)
				Follower.OnAnimationEvent(none, "tailHorseMount")
				Utility.Wait(0.3)
				Follower.EvaluatePackage()
			EndIf	
			If asEventName == "tailHorseDismount"				
				if (Horse.GetDistance(Game.GetPlayersLastRiddenHorse()) <= 700)					
				Utility.Wait(3)
				Follower.Dismount()
				Follower.EvaluatePackage()
				Endif
			EndIf
		Else
			Return
		EndIf	
endFunction
```
- Define your properties after!

## Non-hostile Spell Reactions
- In the filter box, look up `wicast`. 
- ![img](https://imgur.com/zR33hXj.png)
- Select **WICastMagicNonHostileSpell01**.
- Go to Player Dialogue.
- You'll see there are branches like *WICastMagicNonHostileSpellHealing*. And there's dialogue already existing for Skyrim NPCs. You can add your follower's dialogue here, but just make sure that you properly define who's speaking.
- ![img](https://imgur.com/lZnVtNB.png)
