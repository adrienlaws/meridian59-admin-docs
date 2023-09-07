# meridian59-admin-docs
Meridian 59 Administration Commands

### Contents
- [basics](https://github.com/adrienlaws/meridian59-admin-docs/edit/main/README.md#basics)

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
