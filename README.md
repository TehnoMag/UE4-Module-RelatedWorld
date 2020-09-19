# Unreal Engine 4 - Related World module

## About
This module will allow you to load several maps on server side of you game and replicate its to a one persistent level on a client side, or use it as a offscreen worlds in a standalone game (you need spawn actor with scene capture component for get render from this world)

## Installation
- Clone latest sources into **Source/RelatedWorld** directory of you project
- Edit **{ProjectName}{TargetType}.Target.cs** file in **Source** directory and add next code into *{ProjectName}{TargetType}Target* function
```c#
ExtraModuleNames.AddRange(new string[] { "RelatedWorld" });
```
- Into **{ProjectName}.uproject** add next code into Modules section
```json
{
  "Name": "RelatedWorld",
  "Type": "Runtime",
  "LoadingPhase": "Default"
}
```

- Into **Config/DefaultEngine.ini** add next code into **[/Script/Engine.Engine]** section
```ini
!NetDriverDefinitions=
NetDriverDefinitions=(DefName="GameNetDriver",DriverClassName="/Script/RelatedWorld.RwIpNetDriver",DriverClassNameFallback="/Script/RelatedWorld.RwIpNetDriver")
+NetDriverDefinitions=(DefName="DemoNetDriver",DriverClassName="/Script/Engine.DemoNetDriver",DriverClassNameFallback="/Script/Engine.DemoNetDriver")

[/Script/RelatedWorld.RwIpNetDriver]
ReplicationDriverClassName="/Script/RelatedWorld.RwReplcationGraphBase"
```

- Make sure plugin **OnlineSubsystemUtils** is on
- Make sure plugin **ReplicationGraph** is on
- Make sure option **EnableMultiplayerWorldOriginRebasing** is on
- Recompile you project

## Notes
- I strongly not recommend use built in replication graph, duy it was added only for experimental purpose.

## Simple Usage
https://cdn.discordapp.com/attachments/644401603088089119/727580647643807855/2020-06-30_20-44-15.png
