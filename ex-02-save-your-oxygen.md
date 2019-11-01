---
layout: default
title: Exercise 02. Don't Waste Oxygen
---

It was brought to our attention that none of the buildings on our new base had proper life-support system.

Any life support system includes several important sub-systems.
Most critical life-support sub-system is ventilation.
Ventilation is responsible for pressurizing the room by providing enough oxygen.

However, pressurization is impossible if the room is not airtight.

The room on our new base does have all components to make it airtight, but as soon as the `Main Door` is opened, all the oxygen escapes the room.

A few things have been done in order to implement that vital system on the new base:
- a vent was installed and connected to the `O2/H2 generator` inside the room
- a two-phase `Airtight Door` was installed that consists of `Airtight Door Internal` and `Airtight Door External`
- the `Main Door` was disabled to prevent oxygen from escaping by accident

The two-phase `Airtight Door` works by never having both the doors (`Internal` and `External`) open at any given time.

It is possible to enter and leave the room without letting oxygen out by using the two-phase `Airtight Door`, but there are a few problems when manually operating that door:
- it is easy to make a mistake and let oxygen out as the result of both doors (`Internal` and `External`) being open at the same time
- it is not optimal when operating the door manually as you may end up wasting time by waiting a little more that required for the door to be open/closed (humans are usually not good with precision)
- it is tiresome to operate it manually again and again, which increases the chances of making a mistake

Thankfully, we can automate that process using the installed `PB for Airtight Door` (Programmable Block).

Here is a rough algorithm to implement:
1. Monitor state of both `Airtight Door Internal` or `Airtight Door External`
2. When either of the doors is opened, give the person some time to enter the door
3. Close the opened door
4. Wait till the door is closed
5. Open the other door
6. Give the person some time to leave
7. Close the other door

You would still see some air escaping through `Airtight Door External` when it is opened, but amount of wasted oxygen is negligibly small.

It is up to you how to implement the algorithm, what variables or classes to use and how many of them to create.

However, you need to understand everything you do and be able to explain why you did what you did.

Good luck!

# Tips

## Ground rules

__Avoid long/infinite loops__, i.e. loops that never end or take very long time to complete.
If any of the methods in your script (including constructor) take longer than one second to execute, execution of the script is terminated by the game and the program in PB is disabled until it is recompiled (by clicking the `Recompile` button or updating the script).

__All variables must be initialized before use.__ If you try to use a variable that hasn't been assigned a value, you will get an error and the script will be terminated. You've had that problem before.

## Door interaction

The following code retrieves door object by its name:

```csharp
IMyDoor doorInt = GridTerminalSystem.GetBlockWithName("Airtight Door Internal") as IMyDoor;
```

You can find everything you need to interact with the doors (including status monitoring) [on this MDK wiki page](https://github.com/malware-dev/MDK-SE/wiki/Sandbox.ModAPI.Ingame.IMyDoor). 
For this exercise you can ignore all properties and methods that are annotated with _"Inherited from ..."_.
Also, always ignore properties and methods marked as _"Obsolete"_.

[On this MDK wiki page](https://github.com/malware-dev/MDK-SE/wiki/Sandbox.ModAPI.Ingame.DoorStatus) you can find all possible values door `Status` could have, with description.

## Delays

When you need to wait certain amount of time, you can use approach with `counter` used in [part 8 of the tutorial](08-mixed-runway-demo).

Remember that you need to set up `Runtime.UpdateFrequency` in constructor to make `Main` method execute periodically.

This code

```csharp
Runtime.UpdateFrequency = UpdateFrequency.Update10;
```

makes method `Main` execute once every 10 game ticks.

> Reminder: there are 60 game ticks in one second

## Debug your code

There is an LCD panel set up for you to help debug your code. It's name is `LCD Debug Panel`.

Here is a method you can add to your `Program` class to easily add messages to the panel, each message on the next line:

```csharp
private void Print(string text, bool first = false)
{
  IMyTextPanel lcd = GridTerminalSystem.GetBlockWithName("LCD Debug Panel") as IMyTextPanel;
  lcd.WriteText(text + "\n", !first);
}
```

Here is how to use that method in your code:

```csharp
Print("First line needs true", true);
Print("Second line doesn't need true");
Print(doorInt.Status.ToString());
Print(counter.ToString());
```

Here is what you will see on the screen:

```
First line needs true
Second line doesn't need true
Closed
24
```

Note that in order to make first line to appear where it is supposed to be, the screen must be cleared.
That is done by providing second argument to method `Print` as `true` when printing the first line.
Any following line doesn't need that argument.
