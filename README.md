# Equipment-Drop
Counter-Strike Sourcemod plugin allows players drop their items

the plugin resolved a bug of item duplication.

Video explanation [here](http://www.youtube.com/watch?v=tl1013Fr4_Y)

Code explanation below
```sp
        //CS:S  iGame = 1
        //CS:GO iGame = 2
        
        new nSequence = GetEntProp(weapon, Prop_Data, "m_nSequence");
        if(...)
        {
            if(nSequence == 0 || nSequence == 1 || (nSequence == 6 && iGame == 1) || (nSequence == 3 && iGame == 2)) // Block nade duplicating by dropping a nade when player is uping his arm (right before throwing).

            or

            if((nSequence != 5 && iGame == 1) || (nSequence != 2 && iGame == 2)) // Block nade duplicating by dropping a nade when player is uping his arm (right before throwing).
            {
                //codes of dropping a weapon... 
            }
        }
    }
}  
```

```
The m_nSequence values of a nade

in CS:S,

0 = Player in handling a nade.
1 = When a player gets ready to throw his nade. (pin has been pulled)
5 = When a nade has been thrown.
6 = When a player takes his nade out of his holder. (switch active weapon into a grenade)

in CS:GO,

0 = Player in handling a nade.
1 = When a player gets ready to throw his nade. (pin has been pulled)
2 = When a nade has been thrown.
3 = When a player takes his nade out of his holder. (switch active weapon into a grenade)
```

## Console Variables
* sm_equipment_drop_allows_enable: Enable Equipment Drop. (Def: 1)
* sm_equipment_drop_allows_knife: Plugin allows players to drop their Knives. (Def: 1)
* sm_equipment_drop_allows_hegrenade: Plugin allows players to drop their HE Grenades. (Def: 1)
* sm_equipment_drop_allows_flashbang: Plugin allows players to drop their Flashbangs. (Def: 1)
* sm_equipment_drop_allows_smokegrenade: Plugin allows players to drop their smokegrenades. (Def: 1)
* sm_equipment_drop_allows_zeus: Plugin allows players to drop their Zeus x27s (CS:GO Only) (Def: 1)
* sm_equipment_drop_allows_incgrenade: Plugin allows players to drop their Incendiary Grenades (CS:GO Only) (Def: 1)
* sm_equipment_drop_allows_molotov: Plugin allows players to drop their Molotov Cocktails (CS:GO Only) (Def: 1)
* sm_equipment_drop_allows_decoygrenade: Plugin allows players to drop their Decoy Grenades (CS:GO Only) (Def: 1)
　
* sm_equipment_drop_allowed_team: Team index to allow to drop. (Def: 1)
  - 1 = Both
  - 2 = Terrorists
  - 3 = Counter-Terrorists
* sm_equipment_drop_allows_admin_only: Administrator flags to allow to drop. (leave this empty when you would NOT like to set.) (Def: )
　
* sm_equipment_drop_allow_time: The time when players can drop their Equipments. (* Second(s) later.) (Def: 0.0)
  - 0 = Until the time set as sm_equipment_drop_disallow_time (but it is 0, Allows Always).
* sm_equipment_drop_allow_time = sm_equipment_drop_disallow_time => Allow
* sm_equipment_drop_disallow_time: The time when players can NOT drop their Equipments. (* Second(s) later.) (Def: 0.0)
  - 0 = Disable This Cvar
* sm_equipment_drop_allow_time = sm_equipment_drop_disallow_time => Allow
* sm_equipment_drop_notify_drop_time: Notify at the time when players can or can not drop their Equipments. (Def: 1)
  - 0 = Disable Notifying
  - 1 = Notify
  - 2 = Notify + Round startup Notifying
* sm_equipment_drop_notify_to_all: (Def: 0)
  - 0 = Only allowed player can see notifications.
  - 1 = Every player can see notifications.

## Installation
Compile Equipment Drop.sp file, then put Equipment Drop.smx in addons/sourcemod/plugins.

Put EquipmentDrop.cfg in cfg/sourcemod and equipment_drop.phrases.txt in addons/sourcemod/translations. (if you need it)

(if you use Allow (or Disallow or Both) Drop Time and notifying settings, you'll need the phrases file.)
  
## Changelog (MM/DD/YYYY)
#### 1.9(07/11/2014)
```
Grenade offset values are now up-to-date.
```
#### 1.8(10/08/2013)
```
Grenade offset values are now up-to-date.

Removed unused codes.
```
#### 1.7(03/30/2013)
```
Equipment Drop support team and administrator classification from now on.

Added CVar 'sm_equipment_drop_allowed_team' for team classification.
Added CVar 'sm_equipment_drop_allows_admin_only' for administrator classification.
Added Cvar 'sm_equipment_drop_notify_to_all'.

Changed CVar name 'sm_equipment_drop_notify_time' into 'sm_equipment_drop_notify_drop_time'.
```
#### 1.6(02/25/2013)
```
Added Allow (or Disallow or Both) Drop Time and notifying for this settings

So, follow 3 cvars have been added.

sm_equipment_drop_allow_time
sm_equipment_drop_disallow_time
sm_equipment_drop_notify_time

and plus one,

sm_equipment_drop_allows_enable has been added for your convenience.

Now, you need to make sure equipment_drop.phrases.txt is in your addons/sourcemod/translations

but, you don't need this phrases file if you set sm_equipment_drop_notify_time to 0 or above three cvars to default value.
```
#### 1.5b(01/25/2013)
```
Now blocks Zeus x27 spamming.
(as a player drop his zeus right after firing... zeus has been dropped, but players can't pick it up.)
```
#### 1.5(01/25/2013)
```
CS:GO supports added!

follow 4 cvars have been added.

sm_equipment_drop_allows_zeus
sm_equipment_drop_allows_incgrenade
sm_equipment_drop_allows_molotov
sm_equipment_drop_allows_decoygrenade
```
#### 1.4b(01/25/2013)
```
AutoExecConfig(true, "Equipment Drop"); => AutoExecConfig(true, "EquipmentDrop");

'Equipment Drop.cfg' couldn't be loaded.
```
#### 1.4 (01/21/2013)
```
Tidied codes.
New ConVars added.
* sm_equipment_drop_allows_knife
* sm_equipment_drop_allows_hegrenade
* sm_equipment_drop_allows_flashbang
* sm_equipment_drop_allows_smokegrenade

default values are all 1, it determine if allows dropping that kind of items or not.
```
#### 1.3.5 (01/06/2013)
```
Silenced the 'tick' sound when a player drop a item with more than 2, server-sidely.
```
#### 1.3b (09/08/2012)
```
Dropping a item is fires events now.
```
#### 1.3 (06/20/2012)
```
The tries from privious version worked very well.

Did some modify codes, decided keep use this solution.

The plugin now work has smoothler view model animation than other plugins those released now
by removing flickering animation while dropping a item with more than 2

fixed a bug which occurrs when a player drop a item
which player has 2 and more of it,the items are all gone, but just 1 of it's dropped.
```
#### 1.1-Test (06/19/2012)
```
Tried another solution, by checking state with the value of m_nSequence.

Expecting it solved the bug perfectly, but I'm not quite sure for that.
```
#### 1.0 (Initial Version) (06/19/2012)
```
Initial Version,
the plugin doesn't require gamedata file includes signature and vtable data.

Resolved item duplication bug by it's count.
It was the issue when player drop a item right after throwing, it duplicated even though it's thrown away.

Players cannot drop item when it's count is 0.
So, when player has 2 of same nades, it's not gonna block the bug for now.
also I'm working for another solution.
```
