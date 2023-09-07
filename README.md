# meridian59-admin-docs
Meridian 59 Administration Commands

## Basics
`shift+4` opens the administration console from the Meridian 59 client.<br>
You must have permissions to do so.<br>
![image](https://github.com/adrienlaws/meridian59-admin-docs/assets/4023541/50a1ce77-817b-4368-bc75-03e8a630072a)


Move
```
go rid_<room name string from there>
```
check `blakston.khd` for the room name values
[blakston.khd](https://github.com/Meridian59/Meridian59/blob/b22dceea862f85cc53772d93ffd815329da11b62/kod/include/blakston.khd#L359) from the official Meridian 59 repository.
---
populate map of current room
```
show map
```
![image](https://github.com/adrienlaws/meridian59-admin-docs/assets/4023541/e19a9613-5744-44c1-a0f9-0933d18cde16)


Get spells / skills
```
dm get spells
```

```
dm get skills
```

Boost Stats
```
dm boost stats
```

Create Monsters
```
dm create [monster name]
```

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

You can see see `piDay` and `piYear` which you can edit in the Administration Cient Window (`shift+4`) 
You can use the GUI to change it or just send the object the new value (example day 16) with:
set object 0 piDay INT 16

2 hours = 1 meridian day
24 hours = 12 meridian days
240 meridian days = 1 meridian year
1 meridian year = 240 meridian days = 20 earth days

Refresh the state of an object
```
send o [object id] somethingchanged
```

Create Item
```
dm get item [item name]
```

Create Special Items
DM create itematt <this is where blinder or paralyzer ect go>
blinder = blind
paralyzer = hold
vamper = vamp weap
twister = GMT
Transcendant = soft white light
Bonker = bonk weap
expert = random justice weaponon, can be weak or good, its random
spellcasters "name" =makes weapon special, example 'spellcasters acid'
durable = more durable
duke = duke
cold = icy
shock= zap
twister = gmt
punisher = justice weapon
transcendant = Soft white light
paralyzer = hold
blinder = blind
fire = tof
vamper = vamp
acider = acid touch
EXAMPLE: "DM create itematt cold"

Color Item
Black (int 44)
Dark Green (int 37)
Crimson splash (int 42)

