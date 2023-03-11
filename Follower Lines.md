This page is part of the [Skyrim Follower Dialogue Template](https://ko-fi.com/s/f19c1d59ac).

# Table of Contents
- [Dissection of Conditions](https://github.com/annakins/Skyrim/blob/main/Follower%20Lines.md#dissection-of-conditions)
- [Bleedout Lines](https://github.com/annakins/Skyrim/blob/main/Follower%20Lines.md#bleedout-lines)
- [Player Death Reactions](https://github.com/annakins/Skyrim/blob/main/Follower%20Lines.md#player-death-reactions)
- [Horse Riding](https://github.com/annakins/Skyrim/blob/main/Follower%20Lines.md#horse-riding)
- [Non-hostile Spell Reactions](https://github.com/annakins/Skyrim/blob/main/Follower%20Lines.md#non-hostile-spell-reactions)
- [A really awesome resource](https://deck16.net/post/22645519500/making-a-unique-voiced-follower-in-skyrim-part-1)
## A Quick Note
- You are free to edit the scripts below and personalize them. If your author name is Jane Jones and you love the number 13, then a good prefix would be `JJ13` for all your mods. Doing this just makes things easier for you to find.

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
- Bleedout works if your character is not *Essential*. There are ways to go around that, but they are not covered here.
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
- For **Completion**, this is the code to add in the Papyrus Fragment box: ```BleedoutVar.SetValue(0 as Float)```
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
- This is what I have, but your conditions will be different. Here, the quest is just checking if my followers are currently in my party.
- ![img](https://imgur.com/ChxYpcM.png)
- Let's make a scene in your **FollowQuest**.
- Since we covered scenes briefly in the *Bleedout* example, I'll simply show what the player death reaction scene would look like:
- ![img](https://imgur.com/JWOIaQS.png)
- There's nothing to add in the Papyrus fragments, so let's proceed.
- Let's go back to your ***PlayerDeathQuest***.
- Go into the Alias tab, and add an alias and script for the player.
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
- Create a global variable for your riding, like: *prefix + ridingvar*
- Variable type is short, with a value of 0. You'll find that most global variables will be this way.
- I will show you what I have, but you will see that there are extra variables that are specific to my follower. The globally important conditions are the Recruited variable, and the Riding variable.
![img](https://imgur.com/wDH21xR.png)
* * *
![img](https://imgur.com/BLNc1zu.png)
* * *
![img](https://imgur.com/q1tI65w.png)
* * *
![img](https://imgur.com/3ygjEeq.png)
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
- **You can do the above method, or you can create a scene, just like how we did the bleedout lines!** But let's not stop here just yet.
- Here's the thing. If you check the Magic Effect tab for *RestoreHealthFFSelfArea*, you will see that the *SayOnHitByMagicEffectScript* does not have a value for *CombatTopicToSay*. This means that **while you're in combat**, and you're trying to heal your follower, they won't react to your epic heals if you used the default **WICastMagicNonHostileSpell01** quest.
- ![img](https://imgur.com/EKCnEW6.png)
- You don't want to overwrite that Magic Effect, though, as that would mean you're editing a vanilla record. **You want to try to avoid that in certain cases**. 
- Now, we want to make it so our follower reacts to heals in combat, too. [Arcane University](https://wiki.beyondskyrim.org/wiki/Arcane_University:World_Interactions) covers how to do this very well. Scroll to *Spell Reactions*.
- Here is what we are going to do instead: Go to your *FollowQuest*, and then go to the *Combat* tab. And then select Hit.
- ![img](https://imgur.com/uNIjE4r.png)
- Add a new line: `Thank you.` You are welcome to record this any time.
- If you check a Magic Effect that's for a healing spell, you'll see the keyword, `MagicRestoreHealth`.
- ![img](https://imgur.com/TGf5mX2.png)
- Now, add that to your new `Thank you.` line!
- ![img](https://imgur.com/ezSPvo6.png)
- Now you have a combat and non-combat set of spell reactions.
- Personalize as much as you'd like. Have fun!