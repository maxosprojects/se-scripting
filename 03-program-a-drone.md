---
layout: default
title: 03. Program a drone
---

This time we're going to program a drone to fly and pick up resources from one place and drop them off in another.
This is a fairly simple task as SE already provides an autopilot function implemented in Remote Control (__RC__) blocks.

To set up autopilot you need to have GPS coordinates that the RC must follow. It isn't particularly easy to get the GPS coordinate precisely, so we're going to involve a PB script to help us do that.

First, you need to make a simple small grid drone with six thrusters to keep the drone in the air and one thruster in each of the directions including one to push the drone down.
It also needs a few small reactors (just enough to power all thrusters at the same time at full thrust), an antenna (with broadcast radius of 50km), a PB, and RC named "RC Robot", a Connector and two timers.

---

`Some content skipped for now. Will fill out later.`

`You can still find the resulting code we made for the Drone listed below for your reference.`

---

```csharp
namespace IngameScript
{
    partial class Program : MyGridProgram
    {
        private IMyRemoteControl remoteControl;

        public Program()
        {
            remoteControl = GridTerminalSystem.GetBlockWithName("RC Robot") as IMyRemoteControl;
        }

        public void Main(string argument, UpdateType updateSource)
        {
            Vector3D coord = remoteControl.CenterOfMass;
            MyWaypointInfo waypoint = new MyWaypointInfo(argument, coord);
            remoteControl.AddWaypoint(waypoint);
        }
    }
}
```
