---
layout: default
title: Introduction
---
# Introduction

First, let’s create a new project and call it **SEIntro**:
1.  Open **Visual Studio 2019**
2.  Select menu **File > New > Project**
3.  Select **Installed > Visual C# > Space Engineers > Ingame Script**
4.  Give it name **SEIntro**
5.  Click **OK** and then **Create New Project**

There are two types of comments in C# – single-line and multi-line.
Single-line comments are created using double slash.
```csharp
// This is a single-line comment
```
Multi-line comments start with **/\*\*** and end with **\*\*/**
```csharp
/**
 * This is a multi-line comment
 **/
```

Below is the contents of the **Program.cs** file that you’re presented with in a new project. In this example 
I left comments that are generated automatically with a new project as single-line comments, and also added 
multi-line comments to explain some other things.

{% highlight csharp linenos %}
/**
 * These statements declare what namespaces and classes your script
 * requires.
 * None of the statements in this standard generated list will be
 * included in the resulting script. You'll see.
 **/
using Sandbox.Game.EntityComponents;
using Sandbox.ModAPI.Ingame;
using Sandbox.ModAPI.Interfaces;
using SpaceEngineers.Game.ModAPI.Ingame;
using System.Collections.Generic;
using System.Collections;
using System.Linq;
using System.Text;
using System;
using VRage.Collections;
using VRage.Game.Components;
using VRage.Game.GUI.TextPanel;
using VRage.Game.ModAPI.Ingame.Utilities;
using VRage.Game.ModAPI.Ingame;
using VRage.Game.ObjectBuilders.Definitions;
using VRage.Game;
using VRage;
using VRageMath;

/**
 * This is namespace.
 * In Programmable Blocks it won't be used.
 **/
namespace IngameScript
{
    /**
     * This is a class called Program.
     * It extends another class called MyGridProgram.
     * 
     * In Programmable Blocks you mostly won't use classes.
     * The methods inside this class (Program, Save and Main) are used
     * in Programmable Blocks and constitute a script.
     **/
    partial class Program : MyGridProgram
    {

        /**
         * This is constructor.
         * Constructors are used to instantiate a class which creates
         * objects (also called instance of a class).
         * It is easy to recognize constructors - they are methods that
         * don't have return type and are named exactly as the class they
         * are in (in this case - Program).
         * 
         * Since this constructor doesn't require any parameters, it is
         * called "default constructor".
         * Default constructor is not required. Could be just removed if
         * it has no code, in which case it would be generated implicitly.
         * In Programmable Blocks you will mostly have a default
         * constructor, or none at all.
         **/
        public Program()
        {
            // The constructor, called only once every session and
            // always before any other method is called. Use it to
            // initialize your script. 
            //     
            // The constructor is optional and can be removed if not
            // needed.
            // 
            // It's recommended to set Runtime.UpdateFrequency 
            // here, which will allow your script to run itself without a 
            // timer block.

            /**
             * You can use the following to tell Programmable Block to
             * run periodically. "Update1" means "every game tick",
             * "Update10" - "every 10 ticks" and "Update100" - "every 100
             * ticks".
             * If UpdateFrequency is not set, script will be run only once,
             * whether you click the Run button or it is triggered by
             * something else like Sensor or Timer.
             **/
            Runtime.UpdateFrequency = UpdateFrequency.Update1;
        }

        /**
         * This is a method. You can tell it apart from constructor by the
         * return type, which in this case is "void" (method doesn't return
         * anything).
         * This method is not required and can be used to persist some
         * variables. You might need that for certain things. Ask me if
         * you're interested in persisting script variables between runs.
         **/
        public void Save()
        {
            // Called when the program needs to save its state. Use
            // this method to save your state to the Storage field
            // or some other means. 
            // 
            // This method is optional and can be removed if not
            // needed.
        }

        /**
         * This is the only required part of the script. See the description
         * below for details.
         **/
        public void Main(string argument, UpdateType updateSource)
        {
            // The main entry point of the script, invoked every time
            // one of the programmable block's Run actions are invoked,
            // or the script updates itself. The updateSource argument
            // describes where the update came from. Be aware that the
            // updateSource is a  bitfield  and might contain more than 
            // one update type.
            // 
            // The method itself is required, but the arguments above
            // can be removed if not needed.
        }
    }
}
{% endhighlight %}

