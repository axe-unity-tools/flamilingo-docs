# Getting started

This guide takes you from an imported Flamilingo package to a working translated text object in Unity 2022.3.

## 1. Import Flamilingo

Import the Flamilingo asset into your Unity project. The package files should be under `Assets/Flamilingo`. TextMeshPro is required for `FlamilingoTMP`; the legacy `UnityEngine.UI.Text` component uses `FlamilingoUnityText`.

Open **Window → Flamilingo → Hub**. The Welcome page summarizes the workflow. Open **Window → Flamilingo → Settings** (or use **Open settings** in the Hub) to configure the project.

## 2. Choose storage and languages

In **Flamilingo Settings → General**, select one of these translation formats:

- **JSON (One File Per Language):** One editable JSON asset per language. This is also the format that supports the optional Addressables conversion.
- **CSV (One File Per Language):** Separate CSV files for each language.
- **CSV (Single File):** One CSV table shared by all languages.

The editor offers a migration when you change formats. Commit or back up translation files before a large migration.

Open **Settings → Languages**, add the languages your game supports, and click **Save changes**. Then select a **Default language** in General settings. If the saved player choice and system language are unavailable, Flamilingo uses this default; if none is configured, it uses the first available language.

## 3. Create a key

Open **Hub → Translations** and click **+ New key**. Enter a stable key such as `menu.play` and provide its initial value. Select the key in the list to fill values for the other languages, then click **Save changes**.

The Translations page shows coverage for each key. Use **Search keys** and **Missing only** to find unfinished entries. If you configure an automatic translation service in Settings, **Translate missing** and per-key translation actions become available.

## 4. Localize a text object

Select a GameObject with `TMP_Text` or legacy UI `Text`. Add `FlamilingoTMP` or `FlamilingoUnityText` on the same GameObject. You can also use **Flamilingo → Localize** from the text component's context menu or the Dashboard's **Localize** action.

In the Flamilingo component inspector:

1. Enter a translation key or click **Browse and search keys…**.
2. Check the **Key found** status.
3. Choose a **Casing** option if needed.
4. Enable **Preview** and select a language to inspect the result without entering Play mode.

Preview is an editor aid. Enter Play mode to test the runtime language behavior.

## 5. Switch languages

For a ready-made selector, use **GameObject → UI → Flamilingo → Language Selection**. The generated object uses a TextMeshPro dropdown and the `FlamilingoLanguageDropdown` component.

You can also switch languages in code:

```csharp
using Axe.Flamilingo;
using System.Globalization;

Flamilingo.LoadLanguage(CultureInfo.GetCultureInfo("fr"));
```

Flamilingo saves that choice in `PlayerPrefs` and reapplies localized content when the language changes. See the [API reference](api.md) for translation lookups and change callbacks.

## Next steps

- Scan scene objects and optional prefabs in the [Dashboard](user-guide.md#dashboard).
- Localize component values other than text with the [Custom Localizer](user-guide.md#custom-localizer).
- Review [language storage](language-storage.md) before converting JSON languages to Addressables.
