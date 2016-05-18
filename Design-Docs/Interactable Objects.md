# Interactable Objects
Cooper Riehl

### Table of Contents
1. [Abstract](#abstract)
2. [Overview](#overview)
3. [Details](#details)
    1. [Subsection 1](#subsection-1)
    2. [Subsection 2](#subsection-2)

### Abstract

This document details a general-purpose script for interactable objects in the game world. All interactable objects should have common behavior, even if their direct effects are different. For example, the process to activate a button, turn a lever or talk to someone should all be the same, even though the *results* of the interaction are certainly not.

### Overview

Interactable objects will function using two different scripts. The first of these is the `Interactable` interface, which provides details for how interactable objects should function. The second is a modification to the `Player` script, where the Player has a reference to a single `Interactable` object. When the player collides with an object, it will check to see if the object has an `Interactable` script. If so, the `Player` script will update its reference to the object. Then, if the player presses the Interact button and the player is in a state to interact with the object, it will call the `Interactable` object's `Interact()` function.

### Details

#### Interactable

The `Interactable` interface provides a single virtual function, `Interact()`. This function must be implemented by anything that allows the player to interact with it.

**Example:** Dialogue using Interactable
```C#
public class Dialogue : Interactable
{
    public string actorName;    // Set this value in the editor

    public void Interact()
    {
        DialogueEngine.Start(actorName);
    }
}
```

**Example:** Button that opens a Door using Interactable
```C#
public class DoorButton : Interactable
{
    public Door door;
    
    public void Interact()
    {
        door.Open();
    }
}
