This page is part of the [Skyrim Follower Dialogue Template](https://ko-fi.com/s/f19c1d59ac).

# Table of Contents
- [Dissection of Conditions](https://github.com/annakins/Skyrim/blob/main/Follower%20Features.md#dissection-of-conditions)
- [Bleedout Lines](https://github.com/annakins/Skyrim/blob/main/Follower%20Features.md#bleedout-lines)
- [Player Death Reactions](https://github.com/annakins/Skyrim/blob/main/Follower%20Features.md#player-death-reactions)
- [Horse Riding](https://github.com/annakins/Skyrim/blob/main/Follower%20Features.md#horse-riding)
- [Non-hostile Spell Reactions](https://github.com/annakins/Skyrim/blob/main/Follower%20Features.md#non-hostile-spell-reactions)
- [Trust System + Reactions to Player Actions](https://github.com/annakins/Skyrim/blob/main/Follower%20Features.md#trust-system--reactions-to-player-actions)
- [Patchless integration](https://github.com/annakins/Skyrim/blob/main/Follower%20Features.md#patchless-integration)
- [List of idle animations for dialogue](https://www.youtube.com/watch?v=ws6EaXQMBgs)
- [A really awesome resource](https://deck16.net/post/22645519500/making-a-unique-voiced-follower-in-skyrim-part-1)
## A Quick Note
- You are free to edit the scripts below and personalize them. If your author name is Jane Jones and you love the number 13, then a good prefix would be `JJ13` for all your mods. Doing this just makes things easier for you to find.
- This document assumes that you have been following Joseph Russell's tutorials.
- If you have used this document at all, first: awesome. I hope it really helped you. Second: Please consider spreading the word about it. This sort of information should be more available in the Skyrim community.

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
- By default, bleedout dialogue works if your character is not *essential*. If your character is set to *essential*, find a spot to add the following: `Actorname.AllowBleedoutDialogue(true)`. For me, I placed it in one of the first dialogue options when an actor is recruited (so, something that does not repeat).
- Make a bleedout variable.

![img](https://imgur.com/1GyiUAY.png)
- Go into your follower's **FollowQuest**.
- Add a new scene. Check the box for `Interruptible`.
- Right-click and **Add Phase at End**.
- Add your follower as an actor.
- Add another phase.
- Phase 1 should have `IsBleedingOut` on your follower's alias, on **Start**.

![img](https://imgur.com/Ttex7J2.png)
- For **Completion**, feel free to be creative, of course. But this is what I have for Katana:

![img](https://imgur.com/jGkIpCt.png)
- Here's the code so you can copy it: 
```
Follower.GetActorReference().AddItem(RestoreHealth04, 1, true)
Follower.GetActorReference().EquipItem(RestoreHealth04 as form, false, false)
Follower.GetActorReference().RestoreActorValue("Health", 100 as Float)
FollowerBleedoutVar.SetValue(1 as Float)
```
- Make sure to define the properties.

![img](https://imgur.com/ACtvVAa.png)
- Here's what Phase 2 has on **Start**:

![img](https://imgur.com/S9TAZUX.png)
- For **Completion**, this is the code to add in the Papyrus Fragment box: ```BleedoutVar.SetValue(0 as Float)```
- Don't forget to define your properties, basically every time you have scripts.
- Now, go to the *Quest Aliases*, and select your follower. 
- Add a new script, name it with your prefix + `bleedoutlinesscript`, like so:

![img](https://imgur.com/TavkgZV.png)
- Here's the code:
```
Scriptname BleedoutLinesScript extends ReferenceAlias  

scene property FollowerBleedout auto

Event OnEnterBleedout()
Utility.Wait(3)
FollowerBleedout.Start()
endEvent
```
- Select the bleedout scene you just created in the properties. 
- You're done!

## Player Death Reactions
- Create a new quest. Name it prefix + `PlayerDeathQuest`.
- This is what I have, but your conditions will be different. Here, the quest is just checking if my followers are currently in my party.

![img](https://imgur.com/ChxYpcM.png)
- Let's make a scene in your **FollowQuest**.
- Since we covered scenes briefly in the *Bleedout* example, I'll simply show what the player death reaction scene would look like:

![img](https://imgur.com/JWOIaQS.png)
- There's nothing to add in the Papyrus fragments, so let's proceed.
- Let's go back to your ***PlayerDeathQuest***.
- Go into the Alias tab, and add an alias and script for the player.

![img](https://imgur.com/clo8Mx0.png)
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


![img](https://imgur.com/BLNc1zu.png)


![img](https://imgur.com/q1tI65w.png)


![img](https://imgur.com/3ygjEeq.png)
- For the sake of this tutorial, let's make sure you have a horse. Duplicate one of the horses, like `EncHorseSaddledBrown`.
- Of course, name it the way you want to.

![img](https://imgur.com/YV5xuyG.png)
- Check the boxes that make sense for you. This is what I have for Cappy. For *ActorBase*, I also have `EncHorseSaddledBrown` selected.
- In the other tabs, like *Traits*, you can leave them as is. You can change what makes sense to your character's horse later, if you wish.
- Make sure to drag your horse into the area of your choice, in the render window. *Just a friendly reminder (if you need it) that any accidental clicks can be saved, so make sure to do a clean-up on xEdit later.*

![img](https://imgur.com/hZvWxOo.gif)
- Let's go to your **FollowQuest**.
- Select your follower's alias.
- Add both the FollowerNoMount and FollowerRide packages in there. **NOTE: The order matters.**

![img](https://imgur.com/VJkZzWq.png)
- Do the same with your horse. The Stay package should be above the Follow package.
- Now, select the player in the *Quest Alias* tab.
- Add a mount script with your prefix.

![img](https://imgur.com/Ukp4Pmk.png)
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
- When the player mounts, so does the follower - and if the horse is not near you, they get moved to where you are.
- Define your properties after!

## Non-hostile Spell Reactions
- Make a new MGEF.

![img](https://imgur.com/ogenSnd.png)
- Add a script:
```
Scriptname GetHealedScript extends activemagiceffect  

Scene Property GetHealedScene Auto  

Event OnEffectStart(Actor akTarget, Actor akCaster)
GetHealedScene.Start()
EndEvent
```
- In your **FollowQuest**, add a scene.
- Have fun and get creative with when you'd like your follower to say certain things, with conditions.

![img](https://imgur.com/F08nzvY.png)
- Go back to the MGEF you just made and define the scene property with this one.
- Make a new spell.

![img](https://imgur.com/QQl3vES.png)

![img](https://imgur.com/EnFb1hn.png)
- Make sure to add it to your actor's list of spells.
- Now, we want to make it so our follower reacts to heals in combat, too. 
- Go to your **FollowQuest**, and then go to the *Combat* tab. And then select Hit.

![img](https://imgur.com/uNIjE4r.png)
- Add a new line: `Thank you.` Or whatever you want.
- If you check a Magic Effect that's for a healing spell, you'll see the keyword, `MagicRestoreHealth`.

![img](https://imgur.com/TGf5mX2.png)
- Now, add that to your new `Thank you.` line!

![img](https://imgur.com/ezSPvo6.png)
- Hurray! You have a combat and non-combat set of spell reactions.
- Personalize as much as you'd like. Have fun!

## Trust System + Reactions to Player Actions
- Create a config quest.
- In your **FollowQuest**'s controller script, add: `ConfigQuest.Start()` under `SetFollower`, like so: 
```
Quest Property ConfigQuest Auto

Function SetFollower(ObjectReference FollowerRef)
     actor FollowerActor = FollowerRef as Actor
     FollowerActor.RemoveFromFaction(DismissedFollowerFaction)
     If FollowerActor.GetRelationshipRank(PlayerREF) <3 && FollowerActor.GetRelationshipRank(PlayerREF) >= 0
          FollowerActor.SetRelationshipRank(PlayerREF, 3)
     EndIf
     FollowerActor.SetPlayerTeammate()
     FollowerAlias.ForceRefTo(FollowerActor)
     FollowerActor.EvaluatePackage()
     FollowerRecruited.SetValue(1)
	 ConfigQuest.Start()
EndFunction
```
- Add a script onto your config quest:
```
Scriptname ConfigScript extends Quest  

ControllerScriptName property DataStorage auto
GlobalVariable property PlayerReactionsVar auto
ReferenceAlias Property RNPC auto
Scene Property PlayerReactionsScene auto

Function Setup()	
	;====You might have other code here====
	RegisterForSingleUpdate(UpdateInterval)
EndFunction

Event OnUpdate()
If RNPC.GetActorReference().HasLOS(Game.GetPlayer())
UpdateStats()
Else
	DataStorage.UpdateAllStats()
	PlayerReactionsVar.SetValue(0)
EndIf
	RegisterForSingleUpdate(UpdateInterval)
EndEvent

function UpdateStats()

	;==============INCREASE==============
	int LocationsDiscovered = Game.QueryStat("Locations Discovered")
	if LocationsDiscovered > DataStorage.PStat_LocationsDiscovered
		DataStorage.PStat_LocationsDiscovered = LocationsDiscovered
		DataStorage.IncreaseRateMinor()	
	endif
	;==============DECREASE==============	
	
	int Murders = Game.QueryStat("Murders")
	if Murders > DataStorage.PStat_Murders
		DataStorage.PStat_Murders = Murders	
		DataStorage.DecreaseRateMajor()
		PlayerReactionsVar.SetValue(13)
		PlayerReactionsScene.Start()
	endif
endFunction
```
- To save space, I've only added these two stats. One to showcase increasing trust, and the other to decrease trust.
- Refer to this document to see what other stats you can use: [QueryStat](https://ck.uesp.net/w/index.php?title=QueryStat_-_Game)
- In the *Quest Stages* tab, add this:

![img](https://imgur.com/ZjOdsO5.png)
- In your **FollowQuest**'s controller script (the one with functions like `Function SetFollower(ObjectReference FollowerRef)`, `Function FollowerWait()`), add:
```
;==============Relationship System==============

Quest Property ConfigQuest Auto

;property Warm = 6.0 auto conditional hidden
;property Friendly = 2.0 auto conditional hidden
;property Civil = 0.0 auto conditional hidden
;property Cautious = -5.0 auto conditional hidden

;; BEGIN ASSESSMENTS
;  Affects opinion of the player over the course of the relationship
float MinRating = -5.0
float MaxRating = 10.0

float[] relationship

float __relationshiplevel = -5.0 conditional
float Property PlayerAssessmentRelationship
	float function get()
		return __relationshiplevel
	endfunction
	function set(float newValue)
		__relationshiplevel = ClampFloat(newValue, MinRating, MaxRating)
	endfunction
EndProperty

;; END ASSESSMENTS

float __assessmentAnchorRelationship = 5.0

;; BEGIN UTILITY FUNCTIONS

int Function ClampInt(int value, int min, int max)
	if (value > max)
		value = max
	endif
	if (value < min)
		value = min
	endif
	return value
EndFunction

float Function ClampFloat(float value, float min, float max)
	if (value > max)
		value = max
	endif
	if (value < min)
		value = min
	endif
	return value
EndFunction

Function ModAssessment(int assessmentIndex, float amount)
	if (assessmentIndex == 1)
		PlayerAssessmentRelationship += amount
	endif
EndFunction

;;; ASSESSMENT INCREMENTS AND FUNCTIONS
float __minorAssessment = 0.05
float __moderateAssessment = 0.2
float __majorAssessment = 0.5

Function IncreaseRateMinor()
	ModAssessment(1, __minorAssessment)
	EndFunction

Function IncreaseRateModerate()
	ModAssessment(1, __moderateAssessment)
EndFunction

Function IncreaseRateMajor()
	ModAssessment(1, __majorAssessment)
EndFunction

Function DecreaseRateMinor()
	ModAssessment(1, -__minorAssessment)
EndFunction

Function DecreaseRateModerate()
	ModAssessment(1, -__moderateAssessment)
EndFunction

Function DecreaseRateMajor()
	ModAssessment(1, -__majorAssessment)
EndFunction

;;; END ASSESSMENT INCREMENTS AND FUNCTIONS

int __historySize = 10  						

bool __isSetup = false
Function Setup(int forceNPC=0)

	if (__isSetup)
		return
	endif
	__isSetup = true	
	relationship = new float[10]	

	int count = 0
	while (count < __historySize)
		relationship[count] = __assessmentAnchorRelationship		
		count += 1
	endwhile
	RegisterForSingleUpdate(SecondsBetweenPeriodicUpdates)
EndFunction

int Property SecondsBetweenPeriodicUpdates auto

Event OnUpdate()
	int count = 0
	while (count < (__historySize - 1))	
		relationship[count] = relationship[count+1]
		count += 1
	endwhile
	relationship[__historySize - 1] = __relationshiplevel	
	RegisterForSingleUpdate(SecondsBetweenPeriodicUpdates)
EndEvent

;==============QueryStat==============
;==============INCREASE==============
int property PStat_LocationsDiscovered = 0 auto hidden

;==============DECREASE==============
int property PStat_Murders = 0 auto hidden

function UpdateAllStats()
	PStat_LocationsDiscovered = Game.QueryStat("Locations Discovered")
	PStat_Murders = Game.QueryStat("Murders")
endFunction

;==============DEV NOTES==============
;For PlayerReactionsVar
;1 - Locations Discovered
;2 - Murders

```
- Let's go back and look at the properties we'll need to define, as well as how to even get the scripts running in the first place.
- Make a global variable: `PlayerReactionsVar`. Variable type is short, and value is 0.
- Config script: `UpdateInterval` is 1.
- Config script: for `ReferenceAlias RNPC`, you'd pick your follower's reference alias that is in your **FollowQuest**.
- Config script: see where it says `ControllerScriptName property DataStorage auto`? That should be referring to your **FollowQuest**'s script.
- **FollowQuest** script: `SecondsBetweenPeriodicUpdates` is 30.
- As mentioned at the very top of this document, you will need to rename these generic properties to suit your needs.
- These two scripts from two different quests need each other.
- Make a new scene. It can be in your **FollowQuest**: `PlayerReactionsScene`.

![img](https://imgur.com/P2VGEsy.png)
![img](https://imgur.com/CO00dtK.png)
- The global you have here should match your dev notes. You'll need to keep track of that somewhere. For Katana, she responds to acts of murder with the `PlayerReactionsVar` == 13. 
- Examples of how you'd use the trust level in dialogue:

![img](https://imgur.com/UBAlxV2.png)
- This prevents the player from trading with the follower.

![img](https://imgur.com/sg65gi4.png)
- Now, note the difference in the `GetVMQuestVariable` condition.
- You should now be able to use the template provided in this document to allow reactions, trust increases, as well as decreases. Your system will be different from what I have, so you may want to change a bunch of floats. Like these: 
```
float MinRating = -5.0
float MaxRating = 10.0
float __minorAssessment = 0.05
float __moderateAssessment = 0.2
float __majorAssessment = 0.5
```
## Patchless integration
- Create a mod handler quest. Start game enabled and run once boxes checked.
- Make a new reference alias.
- Specific reference: Player. 

![img](https://imgur.com/88JTUNh.png)
- Add a script in that alias.
```
ScriptName ModChecker Extends ReferenceAlias

Actor Property Follower Auto
ReferenceAlias Property FollowerAlias Auto
GlobalVariable Property FollowerRecruited Auto

Function ModCheck(ReferenceAlias FollowerAlias, Int FormID, String FileName)
  If FollowerAlias.getref() == None
    If Game.GetFormFromFile(FormID, FileName)
      ObjectReference FollowerRef = Game.GetFormFromFile(FormID, FileName) as ObjectReference
      FollowerAlias.ForceRefTo(FollowerRef)
    EndIf
  EndIf
EndFunction

Event OnInit()
  Self.CheckAllMods()
EndEvent

Event OnPlayerLoadGame()
  If FollowerAlias.getref() == None && FollowerRecruited.GetValue() == 1 as Float
    Follower.ForceRefTo(Follower as ObjectReference)
  EndIf
  Self.CheckAllMods()
EndEvent

Function CheckAllMods()
	Utility.wait(3 as Float)
	Self.ModCheck(InigoAlias, 35561, "Inigo.esp")
EndFunction
```

- See the number `35561`? You get that DEC number by using a programmer calculator. You need the REF ID of the actor:

![img](https://imgur.com/7Ars1Lt.png)
- On your **FollowQuest**, add a reference alias for... let's just say Inigo.

![img](https://imgur.com/11zMBcg.png)
![img](https://imgur.com/Ru6o9OK.png)
- You don't need to select anything for fill type since it's forced via script.
- Side note: To check the box for *Allow Reserved* if it's greyed out, press `CTRL SHIFT R`.

![img](https://imgur.com/z0cMyqi.png)
- Let's pretend you want your follower to begin the interaction with Inigo. Let's do this via the Idle tab.

![img](https://imgur.com/1BC3qto.png)

- This is something you'll want to customize, naturally.
- You don't see it in the picture, but I also have `IsSneaking == 0.` You can also do `GetRandomPercent`. Up to you! Check the box for Random, and then maybe even have a `GetStage` going for a quest that will handle that actor's stages.
- In the *End: Papyrus Fragment*, you're going to want a `Scene.Start()`.
- With that said, let's make a quest for Inigo.
- Some mod authors make them *Start Game Enabled*, but you can alternatively do a `Quest.Start()` where you have the first ever `Scene.Start()`.
You will be using the *Quest Stages* tab as memory. "Has this scene been played? Because we don't want it to play again."

![img](https://imgur.com/m99gxeQ.png)

- At the very last stage, you can have a script: `Quest.Stop()`.
- Of course, you do not have to follow this format. This is up to you.
- Remember to make your first scene with your follower and the other actor! At this point, it's rinse and repeat.

## Combat to Normal (Unique)
- WIP 
- I'm just going to share what I have because it's faster. Say you have followers that don't like it when you hunt deer.

