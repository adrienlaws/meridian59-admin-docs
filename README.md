# meridian59-admin-docs
Meridian 59 Administration Commands

Basics
Open Admin Console
`shift+4` opens the administration console

Move
```
go rid_<room name string from there>
```
check `blakston.khd` for the room name values

populate map of current room
```
show map
```

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
if you do show o 0 which is abbreviated show object 0 then it will show you all the properties and variables of the server object
You can see see piDay and piYear which you can edit in the admin GUI (shift+4) 
You can use the GUI to change it or just send the object the new value (example day 16) with:
set object 0 piDay INT 16

 2 hours = 1 meridian day
 24 hours = 12 meridian days
 240 meridian days = 1 meridian year
 1 meridian year = 240 meridian days = 20 earth days
Refresh the state of an object
send o [object id] somethingchanged
Create Item
dm get item [item name]
