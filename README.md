# meridian59-admin-docs
Meridian 59 Administration Commands

### Contents
- [Basics](#Basics)

### Basics

`shift+4` opens the administration console from the Meridian 59 client.<br>
You must have permissions to do so.<br>
![image](https://github.com/adrienlaws/meridian59-admin-docs/assets/4023541/50a1ce77-817b-4368-bc75-03e8a630072a)


Move

```
go rid_<room_name_string>
```
Example: `go rid_tos`

Or use this command in the administration console

```
send object <player object number> teleportto rid int <room id>
```
Example: `go rid_tos`

check `blakston.khd` for the room id values

Link to [blakston.khd](https://github.com/Meridian59/Meridian59/blob/b22dceea862f85cc53772d93ffd815329da11b62/kod/include/blakston.khd#L359) from the official Meridian 59 repository.

---

Go on a tour of all rooms
```
dm start tour
```

Populate map of current room

```
show map
```

![image](https://github.com/adrienlaws/meridian59-admin-docs/assets/4023541/e19a9613-5744-44c1-a0f9-0933d18cde16)

---

Get spells or skills
```
dm get spells
```
```
dm get skills
```

---

Boost stats
```
dm boost stats
```

---

Create monsters
```
dm create [monster name]
```

---

Refresh the state of an object
```
send o [object id] somethingchanged
```

---

## Time

Set game day year day hour etc

object 0 is the server itself
if you do 
```
show o 0
```
which is abbreviated
```
show object 0
```
then it will show you all the properties and variables of the server object

You can see see `piDay` and `piYear` which you can edit in the Administration Cient Window (`shift+4`) <br>
You can use the GUI to change it or just send the object the new value (example day 16) with:<br>
```
set object 0 piDay INT 16
```

| Meridian Time | Equivalent |
|:-------------|:-------------|
| 1 Meridian day | 2 Earth hours |
| 12 Meridian days | 24 Earth hours | 
| 1 Meridian year | 240 Meridian days |
| 1 Meridian year | 20 Earth days |

---

Create Item
```
dm get item [item name]
```

---


Create Special Items
```
DM create itematt <itematt>
```
EXAMPLE: "DM create itematt cold"

itematt word | description
|:-|:-|
blinder | blind
paralyzer | hold
vamper | vamp weap
twister | GMT
transcendant | soft white light
bonker | bonk weap
expert | random justice weaponon, can be weak or good, its random
spellcasters <name> | makes weapon special, example 'spellcasters acid'
durable | more durable
duke | duke
cold | icy
shock | zap
twister | gmt
punisher | justice weapon
transcendant | Soft white light
paralyzer | hold
blinder | blind
fire | tof
vamper | vamp
acider | acid touch

Color Item
Black (int 44)
Dark Green (int 37)
Crimson splash (int 42)

### Admin Name Colors
Green Bard/Admin Name:
```
set o <playerobj#> pbImmortal INT 2
```

or use the DM command:
```
DM Zandramas, in your infinite wisdom, please make me important.
```
---

Yellow Game Creator Name:
In the $ Menu type:
create o creator
<Copy the creators Object number it gives you>
create resource <New Name>
<Copy the Resource number it gives you>
set o <creatorobject#> vrname resource <resource#>
create account admin USERNAME PASSWORD
(If you want to apply this to a new account, if not skip to the next step and use a different account #)
<Copy the Account Number it gives you>
set account o <account#> <creatorobject#>

---

Yellow Name Only Quick Disguses:
```
DM armor
```
```
DM shrub
```
```
DM tree
```
```
DM ghost
```
```
DM stool
```
```
DM priestess
```
```
DM ant
```
```
DM red ant
```
```
DM human
```
```
DM cow
```
```
DM spider
```
```
DM troll
```
```
DM shadow
```
### Character Building

Single Character Building
NOTE: Nearly all Send o commands can be done globally as well with a Send c user instead and vice
versa, so just experiment with other things that aren't listed here.

Single Skills:
```
send o <playerobject#> adminsetskill num int <skill#> ability int <%ofskill> List Here
```

Single Spells:
```
send o <playerobject#> adminsetspell num int <spell#> ability int <%ofspell> List here
```

Give Player Defined Weaponcraft Skills at certain level and %:
```
send o <playerobj#> giveplayerallskills level int <maxlevel> iability int <%>
```
Give Player Defined Spell School at certain level and %:
```
send o <playerobject#> giveplayerallspells school int <sch#> level int <max_level> iability int<%>
```
Give Player all Weaponcraft Skills:
```
send o <playerobject#> giveplayerallskills
```
Give Player all Regular Spells:
```
send o <playerobject#> giveplayerallspells
```
Give Player Single Spell Schools:
```
send o <playerobject#> giveplayerallspells school int SS_<schoolname>
```
Remove all spells/skills:
```
send o <playerobj#> removeallskills
```
```
send o <playerobj#> removeallspells
```
Remove Single Spells:
```
send o <playerobj#> RemoveSpell num int <spell#> isDM int <1 or 0>
```
note: (The isDM int <1 or 0> part isn't always required)

Remove Single Skills:
```
send o <playerobj#> RemoveSkill num int <skill#>
```

Remove Inaccesable Spells:
```
send o <playerobj#> RemoveInaccessibleSpells
```
Clear all spells:
```
send o <playerobj#> ClearSpellList
```
Clear single schools:
These don't seem to work
```
send o <PlayerObj#> StripSpellsOfSchool school int <School#>
```
Add to spell to other schools:
```
send o <PlayerObj#> AddToSchools school int <School#> change int <NewSchool#>
```
School Numbers:
|School|Number|
|:-|:-|
Shally |1|
Qor|2
Kranny|3
Faren|4
Riija|5
Jala|6


Infinite Inventory and stomach:
```
set object <PlayerObj#> piBulk_hold $ 0
```
```
set object <PlayerObj#> piWeight_hold $ 0
```
```
set object <PlayerObj#> piStomach $ 0
```
Bio Inscription:
```
send o <playerobject#> sethonorstring string quote <message>
```
Give Player Permanant HP Boost:
```
send object <playerobject#> GainBaseMaxHealth amount int <HPamount>
```
Permanently Bond Player to a Mana Node:
```
send o <mananode#> meld who o <playerobject#>
```
Permanently Bond Player to Every Mana Node:
```
send c mananode meld who o <playerobject#>
```
Boost a Players Might Permanently:
```
send o <playerobject#> AddMight points int <#ofpoints>
```
Boost a Players Intellect Permanently:
```
send o <playerobject#> AddIntellect points int <#ofpoints>
```
Boost a Players Stamina Permanently:
```
send o <playerobject#> AddStamina points int <#ofpoints>
```
Boost a Players Aim Permanently:
```
send o <playerobject#> AddAim points int <#ofpoints>
```
Boost a Players Agility Permanently:
```
send o <playerobject#> AddAgility points int <#ofpoints>
```
Boost a Players Mysticism Permanently:
```
send o <playerobject#> AddMysticism points int <#ofpoints>
```
Give Penalties to a Log Off Ghost:
```
send object <logoffobject#> InflictPenalties
```
#### Global Character Building
Give Every Player all Skills (even offline users) :
```
send c user giveplayerallskills
```
Give Every Player Single Skills (even offline users) :
```
send c user adminsetskill num int <skill#> ability int <%ofskill>
```
Give Every Player Single Spells (even offline users):
```
send c user adminsetspell num int <spell#> ability int <%ofspell>
```
Bio Inscription for All Players (even offline users) :
```
send c user sethonorstring string quote <message>
```
Change everyones karma:
```
send class <player#> addkarma amount <KarmaAmount>
```
(set amount to $ 0 to make it nil)
Rescue all players:
```
send c user admingotosafety
```
Give All Players a Temporary HP Boost:
```
send c player GainHealth amount int <#ofhps>
```
Permanantly Bond Every Player to a Mana Node:
```
send o <mananode#> meld who c user
```
Permanantly Bond Every Player to Every Mana Node:
```
send c mananode meld who c user
```
Give All Players Mana Boost Semi-Permanant:
```
send c user GainMana amount int <ManaAmount>
```
(ao3/soth/node restores default mana)

Boost All Players Vigor to 200 (works like eating something):
```
send c user EatSomething filling int 0 nutrition int 200
```
Give Every Player Single Spell Schools (even offline users):
```
send o <playerobject#> giveplayerallspells school int SS_<schoolname>
```
Give Every Player all Spells (even offline users) :
```
send c user GivePlayerAllSpells level INT 6
```
(You can also put 7 to give the player the slitherbolt spell also)


### Creating Different Items
Create Statues:
First create a statue somewhere:
```
Create o statue
```

Then in the $ menu type:
```
show instance statue
```
Look for the last object number it shows then type:
```
show o <laststatueobject#>
```
Then the first thing you should edit is the Weapon and Shield lines to Nil.
Otherwise if someone enters the room or you type reset then the room the statue is in will freeze up.
Now you can edit the statues Toupee, Head, Eyes, Arms, etc to the same as whatever it is in the
character you want the statue of same lines in the $ menu.
After you've done that change the poOriginal line to the Character you want the statue to be of Object#
Statue Editing Info and Poses

Create Signs:
First either Buy or Create a "Junk" class item that Pacal sells.
Then edit the change the vrName and vrIcon lines to:
sign_name_rsc and sign_icon_rsc
Then in the $ menu type:
```
Create resource <sign description>
```
and then edit the vrDesc to the resource number you get.
Now drop the sign where you want and change the poOwner line to Nil so nobody can pick it up and it
won't disappear.
Here's a list of different signs you can use on Junk Items:
Normal Sign:
sign_name_rsc
sign_icon_rsc
Raza Sign:
sign_name_rsc
sign_newbie_icon_rsc
Assassin Game Sign:
sign_name_rsc
assassinsign_name_rsc
(Not all Junk items that Pacal sells works with this always. Books and Glass Pendants seem to work
good every time. Try changing the vrIcon line first)
Create any item:
Create o OrnamentalObject
Then just set its vrName, Icon and Desc to any resource to make it look like that item.
List of resources
Create a simple Edge Exit List anywhere:
Create a portal and make it go where you want then change it's icon to:
admin_icon_blank
This will make the portal invisible so it will look like an area edge exit.
Create a Food Dispenser (feast hall object):
create o fooddispenser
send o <roomobject#> teleport what o <fooddispenserobject#>
Now move it where you want with the move button and change the vrname, icon and desc to make it look
like an item, once you have done that, set the poTemplate line to the object number of the item you want
it to give out.
Create Globe of Seeing:
Globe you look in:
create o viewpointglobe
send o <roomobject#> teleport what o <ViewGlobeOobject#>
(Put it in the room you want it in)
Globe you see out of:
Create o targetglobe
send o <roomobject#> teleport what o <TargetGlobeObject#>
Now move them to where you want and change the view globe targetglobe line to the targetglobe's object
number.
The piRange line determines how far away from the globe you can be to use it.
(Viewing and Target globes Name, Icon and Desc lines can be changed, so you could set them up to
look like another object and spy on rooms!)
Delete items:
Send o <ItemObj#> delete
Make walking NPCs:
To make an NPC walk is simple. First choose which NPC you want to enable walking on an then look at
it's properties in the admin window.
Scroll down until you see the line which says piBehavior. Changing the INT will determine how the NPC
reacts.
1 = Random Walking.
2 = Enables you to attack, but the NPC won't move or attack you.
3 = Makes it a standard, static NPC.
4 = Lets you attack the NPC, but it will only fight back if you hit it.
5 = Random Walking.
6 = Unable to move, but will attack if you walk near it.
7 = Makes it a standard, static NPC.
8 = Turns the NPC into an enemy that follows and attacks you.
9 = Makes the NPC follow you.
10 = Attacks you if provoked, but doesn't move.
That's a small selection of behavior types. If you want to mimic a certain monster behavior, just look at it
in the admin window and copy the monsters behavior number to your NPC.
An NPC that has proper walking graphics already made for it, is the Street Urchin. To get this, just type in
the admin window:
Create o TosUrchin
and then;
send o <RoomObjNumber> teleport what o <NewUrchinObjNumber>
But any NPC can be made to move, look in the Default Class Name Reference for some NPC class
names, or just if you can't find one you want in the list, just look at an NPC ingame through the admin
window to find it's class name. You can also set the NPC's hit points to whatever you want so it stands a
better chance of survival.
Globe Numbers:
When making new a globe, use these numbers to determine which type of globe it is:
% newsgroup IDs
 NID_GENERAL = 1 %% NID is currently unplaced anywhere.
 NID_NEW_USERS = 2
 NID_GAME = 3 %% guilds now use their RID_ numbers as
 NID_JUSTICAR = 4
 NID_ADVENTURE = 5 %% bard/actor only newsball
 NID_ANNOUNCEMENTS = 9 %% their NIDs. Do not assign them their
 NID_GUILD_CHARTER = 10 %% own NID.
 NID_GODROOM = 14
 NID_TOS_HALL = 20
 NID_BAR_HALL = 21 %% Adventurer's Hall Newsballs
 NID_JAS_HALL = 22
 NID_COR_HALL = 23
 NID_MAR_HALL = 24
 NID_KOC_HALL = 24

### Reference
- Admin_Name_Colours.pdf
- Character_Building.pdf

#### not implemented or documented
- Auto-Updates.pdf

### Attribution
- Haven
- Diggie
- Others (please let me know I will add you)
- [Official Meridian 59 documentation and repository](https://github.com/Meridian59/Meridian59)
