# Language storage

Flamilingo stores translation files in the Unity project. The default and simplest setup keeps languages in `Assets/Resources/Translations`, where the runtime can load them without an extra package.

## Choose a format

| Format | Layout | Addressables conversion |
| --- | --- | --- |
| JSON (One File Per Language) | One `.json` file for each language | Supported |
| CSV (One File Per Language) | One `.csv` file for each language | Not available |
| CSV (Single File) | One shared `.csv` file | Not available |

Choose the format in **Flamilingo Settings → General → Translation storage**. The editor offers to migrate translation data when you switch formats. Review the resulting files before deleting any old copies from version control.

## Optional Addressables workflow

The Addressables page is available when the Unity Addressables package and Flamilingo's Addressables integration are active. In **Settings → General**, enable Addressables. Open **Hub → Addressables** to view the languages in **Local · Resources** and **Addressable** columns.

For a JSON language, click **Make addressable**. Flamilingo moves its file from `Assets/Resources/Translations` to `Assets/Flamilingo/AddressablesTranslations`, registers it in the default Addressables group, and records its address in runtime settings. Other languages remain local. Use **Verify** to test loading a converted language. Use **Make local** to move it back to Resources.

You can edit an Addressable language's key in the Hub. The runtime settings and Addressables entry must refer to the same key; use the Hub's **Update** action rather than renaming only one side.

!!! note "Build and delivery"
    Build Addressables content using your project's normal Addressables build workflow before testing a player build. Converted languages are loaded through Addressables at runtime. This implementation waits synchronously for the `TextAsset`, so test load time on target devices, especially when content is remote.

## Runtime language choice

At startup, Flamilingo checks for a saved player choice, then the system language, then the configured default language, and finally the first available language. If a saved language is no longer supported, Flamilingo clears that preference.

Call `Flamilingo.LoadLanguage(...)` to change languages explicitly. Missing translation keys return the key itself; a missing language file produces a Console error. See [FAQ](faq.md) for checks.
