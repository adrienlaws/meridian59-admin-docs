
# Meridian 59 Administration Commands
:heavy_exclamation_mark: Use at your own risk :heavy_exclamation_mark:

Contributions / PRs are welcome!
### Administration Methods

There are 5 ways to run admin commands in Meridian 59
1. the normal client text window area
2. the client administration console (shift+4)
3. the server administration console on the server itself (Windows only - not on Linux)
4. the maintenance port
5. using the 'load' command to run admin commands from a text file that the server reads in


#### The Client Administration Console (shift+4)

Open the Client Administration Console using `shift+4` \
You must be logged on as an admin to do so.

![image](https://github.com/adrienlaws/meridian59-admin-docs/assets/4023541/50a1ce77-817b-4368-bc75-03e8a630072a)


### Commands

There are 3 levels of commands
- Player
- DM
- Admin

### DM Commands

|Command|Description|
|:-|:-|:-|
`go <room string>` | you can use go 50 (using the id directly) instead of needing to use the rid strings

### Lighting
|Command|Description|
|:-|:-|
`dm place dynamic light` | only usable by administrator and up though
`dm place candle`
`dm place candelabra`
`dm place brazier`
`dm place lamp`
`dm place firepit`

dm create item attribute attributenamehere
dm anonymous
dm shadow
dm relic 1 (or 2, 3, 4, 5)
dm mortal (fun fact, you can do "s mortal" as well. was sloppily done)
dm immortal (same as above)
dm logoffghost on
dm logoffghost off
dm logoffghost temp off
dm event sign
dm monster monstername (you got this one I think)
dm totem
dm appeal off
dm appeal on
dm guest appeal off (probably defunct)
dm guest appeal on (same)
dm stealth on
dm stealth off
dm rumble
dm good
dm evil
dm neutral
dm monster budget (???)
dm monster authorize (???)
dm none (???)
dm clear abilities
dm clear inventory
dm get money
dm pk enable (makes you attackable)
dm pk disable (makes you angeled I think?)
dm pk lock (cannot attack/be attacked I think)
dm pk unlock (removes pk lock)

### Time
|Command|Description|Notes|
|:-|:-|:-|
`dm morning`
`dm afternoon`
`dm evening`
`dm night`
`dm restore time`

dm call monster (unsure?  does it force room spawns?)
dm plain (change to normal form)
dm human (same as above I think?)
dm disguise ant (or other monster name)
dm get items (you covered this)
dm get `misc|gems|reagents|food|weapons|armor|ammo|wands|rings|sundries|games|necklaces|potions|scrolls|wands|masks`
dm hidden
dm blank


---

Go to a specific room

```
go <room string>
```
Example: `go rid_tos`

The room string value is from `blakston.khd`\
example: `RID_TOS = 50`

`RID_TOS` is the room string value to use with the `go` command\
`50` is the equivalent room id (RID) used in other commands

Note: You can alternatively use `go 50` (using the room id directly) instead of using the rid strings


Check [blakston.khd](https://github.com/Meridian59/Meridian59/blob/b22dceea862f85cc53772d93ffd815329da11b62/kod/include/blakston.khd#L359) for room values from the official Meridian 59 repository.

---

Send an object to a specific room id
```
send object <object number> teleportto rid int <room id>
```
Check [blakston.khd](https://github.com/Meridian59/Meridian59/blob/b22dceea862f85cc53772d93ffd815329da11b62/kod/include/blakston.khd#L359) for the room id (RID) values from the official Meridian 59 repository.


---

admin command reference
`kod\object\active\holder\nomoveon\battler\player\user\dm\admin.kod`



Start tour of all rooms
```
dm start tour
```

Stop tour
```
dm end tour
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

Room Monster Rates
Mob spawns have 3 controls

   `piMonster_count_max` = 30 
    `piInit_count_min` = 5 
    `piInit_count_max` = 10
    
This means the room will have 5-10 mobs when u user enters it and will spawn up to 30

---

Refresh the state of an object
```
send o [object id] somethingchanged
```

---

## Lists
There are two major data structures in use within Meridian 59\
- Lisp-like nodes on the server
- Linked-lists in the client

### Viewing lists and list-nodes
Show a list and walk all the nodes (see everything in the list)
```show list <listid>```

Show a node in the list
```show listnode <nodeid>```

Example showing the monsters that spawn at the main gate of cor noth on my test server
```show list 23294```

OUTPUT
```
:<
: [
: [
: CLASS SpiderBaby
: INT 75
: ]
: [
: CLASS Centipede
: INT 25
: ]
: ]
:>
```

Now seeing it with `show listnode` instead of `list`
```show listnode 23294```

OUTPUT
```
:< first = LIST 23290
:  rest = LIST 23293
:>
```
When we look at the node we see that per the documentation on Cons https://en.wikipedia.org/wiki/Cons, the following is true
- the listnode contains it's own listnode value for it's first slot, then the rest of the list (if applicable) in the `rest` slot
- in this case the subnode of this listnode numbered `23294` is `23290`

Now let's see what's in listnode `23290`
`show listnode 23290`

OUTPUT
```
:< first = CLASS SpiderBaby
:  rest = LIST 23289
:>
```

Checking the 23289 listnode in the `rest`

`show listnode 23289`

OUTPUT
```
:< first = INT 75
:  rest = $ 0
```
This means that the listnode contains only `int 75` (the spawn rate % for `SpiderBaby`) and then ends since `rest` is set to `$ 0`

![image](https://github.com/adrienlaws/meridian59-admin-docs/assets/4023541/1ae82405-b6ab-41bd-96fd-9f50d14a0cd5)

### modifying room .kod spawn lists
edit room .kod example `g4.kod` for main gate of cor noth\
change `plMonsters` = `[ [&SpiderBaby, 75], [&Centipede, 25] ];` to something different\
Example: `plMonsters` = `[ [&Troll, 75], [&Spider, 25] ];`\
build the kod folder (for windows systems run ``` nmake ``` in the /kod folder)\
run `reload system` in the admin console\
get the room object number and `send recreate example send object 7003 recreate`\
the screen will flash and new mobs will appear as the room is reconstructed\

### adding a single monster class in a room
Create spawnrate value for new mob spawn class type\
```
create listnode int 100 $ 0
```
OUTPUT: `Created list node [spawn rate list id]`

Create monster class to spawn and associate with spawnrate value - example mob classes "ant" "troll"\
```
create listnode class [mob class name] list [spawn rate list id]
```
`Created list node [mob class list id]`

Create list of lists to populate room plMonsters parameter

```
create listnode list [mob class list id] $ 0
```
OUTPUT: `Created list node [room mob list]`

Assign list to room
```
set object [room obj id] plMonsters LIST [room mob list id]
```

Kill all old monsters
```
cast armageddon
```

Wait and see if the new mobs spawn

### adding 2 monster classes in a room
Create spawnrate value for new mob spawn class type
```
create listnode int [value] $ 0
```
OUTPUT: `Created list node [spawn rate list id]`\
For [value] use 1-100, this is the % spawnrate.

Create monster class to spawn and associate with spawnrate value\
example mob classes "ant" "troll"
```
create listnode class [mob class name] list [spawn rate list id]
```

OUTPUT: `Created list node [FIRST mob class list id]`

Create list of first monster list and save this list id for later
```
create listnode list [FIRST mob class list id] $ 0
```
OUTPUT: `Created list node [FIRST room mob list]`\
If you only want one monster in the room, you are done. Use LIST [FIRST room mob list] for plMonsters in the room.

Create spawnrate value for SECOND mob spawn class type
create listnode int [value] $ 0
Created list node [SECOND spawn rate list id]
Both this and the previous [value] should add up to 100 total.

Create SECOND monster class to spawn and associate with SECOND spawnrate value
create listnode class [mob class name] list [SECOND spawn rate list id]
Created list node [SECOND mob class list id]

Create list of lists to populate room plMonsters parameter
create listnode list [SECOND room mob list] list [FIRST mob class list id]
Created list node [room mob list]
Order here is important, the SECOND list must be listed first.

Assign list to room
set object [room obj id] plMonsters LIST [room mob list id]

Kill all old monsters
cast armageddon

Wait and see if the new mobs spawn 


### adding 3 monsters classes to a room

If you want to add a third monster

Follow all above steps prior to Assign list to room and be sure your [value] are set up to add up to 100 with a third variable. Also, be sure to save the [room mob list] id from above, you will need it to complete these steps.

Create spawnrate value for THIRD mob spawn class type
create listnode int [value] $ 0
Created list node [THIRD spawn rate list id]

Create THIRD monster class to spawn and associate with THIRD spawnrate value
create listnode class [mob class name] list [THIRD spawn rate list id]
Created list node [THIRD mob class list id]

Create list of lists to populate room plMonsters parameter
create listnode list [THIRD mob class list id] list [room mob list]
Created list node [FINAL room mob list id] with all 3 mobs and spawn rates.
Order here is important, the THIRD monster list must come before the room mob list.

Assign list to room
set object [room obj id] plMonsters LIST [FINAL room mob list id]

Kill all old monsters
cast armageddon

Wait and see if the new mobs spawn 

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

### use xlat to create new content
open blakston.khd and look for the xlat list.  they'll say stuff like XLAT_GRAY_TO_??? or XLAT_BLUE_TO_??? so you just look at the thing you're trying to recolor and make sure the color shown matches the graphic you're trying to recolor

and if an object has, say, both blue and red bits and you want to recolor both, there's a way to get a combined value:

send o 0 EncodeTwoColorXlat color1 int AAA color2 int BBB

#### code version
```
local iCombinedColor;

iCombinedColor = Send(SYS, @EncodeTwoColorXlat, #color1=AAA, #color2=BBB);
```


### Delete a user from an account
```
delete user userObjectId
```

### How to hide from the who list and be completely invisible 
```
DM Hidden
```

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

Place dynamic light\
only usable by administrator and up
```
dm place dynamic light
```

there's a dm place dynamic light too - only usable by administrator and up though
```
dm place candle
```

```
dm place candelabra
```

```
dm place brazier
```

Create Statues:\
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
Then the first thing you should edit is the Weapon and Shield lines to Nil.\
Otherwise if someone enters the room or you type reset then the room the statue is in will freeze up.\
Now you can edit the statues Toupee, Head, Eyes, Arms, etc to the same as whatever it is in the
character you want the statue of same lines in the $ menu.\
After you've done that change the poOriginal line to the Character you want the statue to be of Object#
Statue Editing Info and Poses.

Create Signs:
First either Buy or Create a "Junk" class item that Pacal sells.
Then edit the change the vrName and vrIcon lines to:
sign_name_rsc and sign_icon_rsc
Then in the $ menu type:
```
Create resource <sign description>
```
and then edit the vrDesc to the resource number you get.\
Now drop the sign where you want and change the poOwner line to Nil so nobody can pick it up and it won't disappear.\

Here's a list of different signs you can use on Junk Items:
Normal Sign:
```
sign_name_rsc
```

```
sign_icon_rsc
```

Raza Sign:
```
sign_name_rsc
```

```
sign_newbie_icon_rsc
```

Assassin Game Sign:
```
sign_name_rsc
```

```
assassinsign_name_rsc
```

(Not all Junk items that Pacal sells works with this always.\
Books and Glass Pendants seem to work good every time. Try changing the `vrIcon` line first)

Create any item:\
```
Create o OrnamentalObject
```
Then just set its `vrName`, `Icon` and `Desc` to any resource to make it look like that item.\

List of resources\

Create a simple Edge Exit List anywhere:\

Create a portal and make it go where you want then change it's icon to:
`admin_icon_blank`

This will make the portal invisible so it will look like an area edge exit.

Create a Food Dispenser (feast hall object):
```
create o fooddispenser
```
```
send o <roomobject#> teleport what o <fooddispenserobject#>
```
Now move it where you want with the move button and change the `vrname`, `icon` and `desc` to make it look like an item.
Once you have done that, set the `poTemplate` line to the object number of the item you want it to give out.

Create Globe of Seeing:\
Globe you look in:
```
create o viewpointglobe
```

```
send o <roomobject#> teleport what o <ViewGlobeOobject#>
```

(Put it in the room you want it in)

Globe you see out of:\
```
Create o targetglobe
```

```
send o <roomobject#> teleport what o <TargetGlobeObject#>
```
Now move them to where you want and change the view globe targetglobe line to the targetglobe's object number.\
The `piRange` line determines how far away from the globe you can be to use it.\
(Viewing and Target globes Name, Icon and Desc lines can be changed, so you could set them up to look like another object and spy on rooms!)

Delete items:
```
Send o <ItemObj#> delete
```

Make walking NPCs:

First choose which NPC you want to enable walking on an then look at its properties in the admin window.\
Scroll down until you see the line which says piBehavior. Changing the INT will determine how the NPC
reacts.


|INT|Behavior|
|:-|:-|
1 | Random Walking.
2 | Enables you to attack, but the NPC won't move or attack you.
3 | Makes it a standard, static NPC.
4 | Lets you attack the NPC, but it will only fight back if you hit it.
5 | Random Walking.
6 | Unable to move, but will attack if you walk near it.
7 | Makes it a standard, static NPC.
8 | Turns the NPC into an enemy that follows and attacks you.
9 | Makes the NPC follow you.
10 | Attacks you if provoked, but doesn't move.

That's a small selection of behavior types. If you want to mimic a certain monster behavior, just look at it
in the admin window and copy the monsters behavior number to your NPC.\
An NPC that has proper walking graphics already made for it, is the Street Urchin.\ To get this, just type in
the admin window:
```
Create o TosUrchin
```
and then:
```
send o <RoomObjNumber> teleport what o <NewUrchinObjNumber>
```
But any NPC can be made to move, look in the Default Class Name Reference for some NPC class names, or just if you can't find one you want in the list, just look at an NPC ingame through the admin window to find it's class name. You can also set the NPC's hit points to whatever you want so it stands a better chance of survival.



#### Globe Numbers
When making new a globe, use these numbers to determine which type of globe it is:

|Newsglobe ID|INT|Comment|
|:-|:-|:-|
 NID_GENERAL | 1 | NID is currently unplaced anywhere
 NID_NEW_USERS | 2
 NID_GAME | 3 | guilds now use their RID_ numbers as their NIDs. Do not assign them their own NID
 NID_JUSTICAR | 4
 NID_ADVENTURE | 5 | bard/actor only newsglobe
 NID_ANNOUNCEMENTS | 9
 NID_GUILD_CHARTER | 10
 NID_GODROOM | 14
 NID_TOS_HALL | 20
 NID_BAR_HALL | 21 | Adventurer's Hall newsglobes
 NID_JAS_HALL | 22
 NID_COR_HALL | 23
 NID_MAR_HALL | 24
 NID_KOC_HALL | 24

### Reference
- Admin_Name_Colours.pdf
- Character_Building.pdf

#### in process
- Creating_Different_Items.pdf
#### not implemented or documented
- General_Admin_Commands.pdf
- General_Char_Commands.pdf
- Hair_Skin_Item_Coloring_Reference.pdf
- Map_Numbers.pdf
- New_Class_Creation.pdf
- NPC_Info.pdf
- Tips_and_Tricks.pdf
- DM_Commands.pdf

#### Probably not implementing here
- Auto-Updates.pdf
- Client_Editing.pdf
- Creating_Different_Items.pdf
- Editing_Things_via_Hex.pdf

### Attribution and Contributions :mega:
- Aesica
- Essun
- Haven
- Diggie
- Mayhem
- Zaphod
- Others (please let me know I will add you)
- [Official Meridian 59 documentation and repository](https://github.com/Meridian59/Meridian59)
