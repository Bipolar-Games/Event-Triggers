# Bipolar Event Triggers

## Overview
In Unity, the EventTrigger component allows you to easily register UI events from the EventSystem. However, a major issue with EventTrigger is that it implements all event interfaces, causing it to capture all types of input events (clicks, scrolls, pointer movements, etc.), even if only one specific event type is needed. This can block other UI elements from detecting certain events, leading to undesirable behavior.

## The Problem
When using Unity's default EventTrigger, adding an event such as pointer click to a UI button will also cause the button to intercept other events like scroll. As a result, UI elements behind the button (such as a scrollable window) cannot detect scrolling input, which negatively affects usability or requires additional workarounds.

## The Solution
This module provides an alternative approach by splitting the EventTrigger functionality into multiple components, each handling only a single event type. Instead of a monolithic EventTrigger that captures everything, you can now add only the specific event listeners you need to each UI element.

### For example:
- A button can have only a PointerClickEventTrigger, allowing it to detect clicks without interfering with scroll events.
- A background window can have a ScrollEventTrigger, allowing it to detect scrolling even when a button is in front of it.

This approach ensures that UI elements only capture the events they are meant to handle, preventing unintended event blocking and improving interaction flow.

## Installation
1) Download or clone this repository.
2) Add the scripts to your Unity project.
3) Attach the appropriate event trigger components to your UI elements instead of using Unity's default EventTrigger.

## Usage
1) Add the event trigger component(s) needed:
 - PointerClickEventTrigger for click detection.
 - ScrollEventTrigger for scroll detection.
 - PointerEnterEventTrigger for hover detection.
 - And so on...
2) Configure the event listeners in the Inspector or via script.
3) Remove the default EventTrigger component from the object if present

### Example
```csharp 
using UnityEngine;
using Bipolar.EventTriggers;

public class ExampleUsage : MonoBehaviour
{
    private void Start()
    {
        PointerClickEventTrigger clickTrigger = GetComponent<PointerClickEventTrigger>();
        clickTrigger.OnEventTriggered += (pointerData) => Debug.Log("Button clicked!");
    }
}
```
## Benefits
- Prevents event conflicts: Ensures that UI elements only capture the necessary events.
- Improves flexibility: Enables fine-grained control over event handling in complex UI layouts.
- Enhances maintainability: Encourages a modular approach to event management.
