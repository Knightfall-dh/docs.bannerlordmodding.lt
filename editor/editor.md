# Editor

## Versions

- Crashes - 1.1.4/1.1.6
- Works - 1.2.5beta


<br>
## Notes

- On map save overwrites settlements.xml (crashes if this file is not present)
- On map save Editor does not write/update/generate settlements_distance_cache.bin


<br>
## Problems/Solutions


!!! tip "Use [ButterLib](/modules/mods_for_devs) or [attach dnSpy](/resources/dnspy) to the game to catch the crashes. Do not use both at the same time, dnSpy gets confused."

### Does not start

- Version mismatch with the base game - does not start at all, no process - install same version
- Hanged previous process - Close on Steam or check the Task Manager, kill the old process

### Editor Crashes

- When deleting used texture. After crash/restart Texture appears deleted

#### Crash on the map save

- When there is some error in the XML files (settlements.xml?)

- Last line in the log: opening ../../Modules/MODULE_NAME/ModuleData/settlements.xml - missing settlements.xml




### Game crashes

- Not fully saved map - could be the reason that game was active/loaded/in progress when map was saved. Exit the game, then save the map in the Editor. Check map folder, should see following files:

![](https://imgur.com/VYlzH6c.png)

??? failure "System.AccessViolationException"
    **at Vec2 SandBox.MapScene.GetNavigationMeshCenterPosition(PathFaceRecord face)**<br>
    **at Settlement ..DefaultMapDistanceModel.GetClosestSettlementForNavigationMesh(PathFaceRecord face)**
    <br><br>
    REASON1: CUSTOM_settlements.xml does not match settlements.xml


??? failure "System.NullReferenceException"
    **DefaultMapDistanceModel.GetDistance(Settlement fromSettlement, Settlement toSettlement)**
    <br><br>
    REASON1: Wrongly assigned Settlement, Kingdom without a settlement. Attach dnSpy, it will show faction.FactionMidSettlement == null. Fix your XML.
    <br><br>
    REASON2: Problems with Navmesh. Inaccessible settlements. Old/mismatching settlements_distance_cache.bin - fix navmesh, regenerate settlements_distance_cache.bin


### Hangs on map save in the Editor

- Too much terrain editing (Smoothing?). Export heightmap before trying to save after a lot of Smoothing.

![](https://imgur.com/MMmqYCn.png)

To cancel the Save, use X from the Taskbar:

![](https://imgur.com/qOfC2xV.png)

Try to save again.

### Controls stops to work

Reload/Restart?
