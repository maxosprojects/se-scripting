---
layout: default
---
# 04. Basic colorful runway

Let's go back to your first script where you had set up a runway with lights turning on and off in waves to make it noticeable from a few kilometers away.
We are going to make a similar runway, except this one will gradually change colors from blue to red and back. No waves yet.

---

`Some content skipped for now. Will fill out later.`

`You can still find the resulting code we made for Basic Colorful Runway listed below for your reference.`

---

```csharp
namespace IngameScript
{
    partial class Program : MyGridProgram
    {
        List<IMyInteriorLight> lights = new List<IMyInteriorLight>();
        int red = 254;
        int blue = 0;
        int red1 = -2;
        int blue1 = 2;

        public Program()
        {
            Runtime.UpdateFrequency = UpdateFrequency.Update1;
            IMyBlockGroup group = GridTerminalSystem.GetBlockGroupWithName("Runway Lights");
            group.GetBlocksOfType(lights);
            lights.Sort((x, y) => x.DisplayNameText.CompareTo(y.DisplayNameText));
            foreach (IMyInteriorLight light in lights)
            {
                light.Color = Color.Blue;
            }
        }

        public void Main(string argument, UpdateType updateSource)
        {
            red = red + red1;
            blue = blue + blue1;

            foreach (IMyInteriorLight light in lights)
            {
                light.Color = new Color(red, 0, blue);
            }

            if (red.Equals(0))
            {
                red1 = 2;
            }
            if (red.Equals(254))
            {
                red1 = -2;
            }
            if (blue.Equals(0))
            {
                blue1 = 2;
            }
            if (blue.Equals(254))
            {
                blue1 = -2;
            }

            Echo("" + red + " " + blue);
        }
    }
}
```
