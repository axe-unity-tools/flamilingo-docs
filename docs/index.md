<div class="fl-hero" markdown>

# Flamilingo

Localization for Unity with a visual translation workspace, scene coverage checks, and a small runtime API.

[Get started](getting-started.md){ .md-button .md-button--primary }
[Explore the user guide](user-guide.md){ .md-button }

</div>

Flamilingo keeps translation keys and language values together in the **Hub**. Add a text localization component to a TextMeshPro or legacy UI Text object, then use the inspector to assign its key. The Dashboard helps find scene and prefab text that is localized, missing a key, or intentionally ignored.

## What you can do

| Feature | Where to start |
| --- | --- |
| Add languages and choose JSON or CSV storage | [Getting started](getting-started.md) |
| Create keys, translate values, and preview in the Editor | [User guide](user-guide.md) |
| Keep JSON languages in Resources or convert them individually to Addressables | [Language storage](language-storage.md) |
| Change language or translate text from C# | [API reference](api.md) |
| Diagnose missing translations and loading problems | [FAQ](faq.md) |

## Current development target

Flamilingo is being developed and checked in **Unity 2022.3**. Unity 6 compatibility testing is planned. The optional Addressables workflow requires the Unity Addressables package; JSON languages stay in Resources unless you convert them.

For bugs, feature requests, or documentation corrections, visit [Support](support.md).
