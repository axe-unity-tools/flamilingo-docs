# Frequently asked questions

## Why does the key appear instead of translated text?

Check that the key exists in **Hub → Translations**, that the current language has a nonempty value, and that the text component uses that key. The runtime returns the key when it cannot find a translation. In Edit mode, also check **Settings → Show keys in edit mode** and whether Preview is enabled.

## Why is a text object missing from the Dashboard?

Click **Rescan**, clear the search field, and check the status filters. Scene objects are scanned by default. Enable **Include prefabs** to scan prefab assets; prefab rows have a **Prefab** tag.

## Why is Preview not changing my text?

Select a supported preview language and confirm the component key has a translation for it. Preview works in Edit mode; runtime localization controls the text during Play mode. If a component uses composite text, inspect its template and parameter sources as well.

## Where are translation files stored?

Local files are under `Assets/Resources/Translations`. The exact file layout depends on the JSON or CSV format selected in Settings. Converted JSON languages move to `Assets/Flamilingo/AddressablesTranslations`. See [Language storage](language-storage.md).

## Can I use Addressables for only some languages?

Yes, with the JSON per-language format. Convert individual languages in **Hub → Addressables**. Unconverted languages remain in Resources. Install and configure Unity Addressables before conversion, and build Addressables content for player builds.

## Why is an Addressable language missing in a build?

Check that the Addressables package is installed, the language appears in the Addressable column, **Verify** succeeds in the Editor, and Addressables content was built for the target. If you changed an address outside Flamilingo, update the key in the Hub so runtime settings match it.

## Which Unity version should I use?

Current Flamilingo development targets Unity **2022.3**. Unity 6 compatibility work is planned, so validate your own Unity 6 project before relying on it in production.

## How do I report a problem?

See [Support](support.md). Include the Unity version, Flamilingo workflow, steps to reproduce, and the relevant Console message. Avoid posting API keys or private translation content in a public issue.
