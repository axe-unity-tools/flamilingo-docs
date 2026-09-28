# API reference

The public runtime facade is `Axe.Flamilingo.Flamilingo`. Use it for language selection, translation lookups, and notifications. `FlamilingoManager` is a framework implementation detail and should not be called from game code.

## Static facade

| Member | Purpose |
| --- | --- |
| `CultureInfo CurrentLanguage` | Active language. |
| `IEnumerable<CultureInfo> GetAvailableLanguages()` | Cultures available from the configured storage. |
| `void LoadLanguage(CultureInfo cultureInfo)` | Load a language, persist it, and notify subscribers. |
| `string Translate(string key)` | Translate a key in the active language; returns the key when absent. |
| `string Translate(string key, TextCasing casing, CultureInfo culture = null)` | Translate and apply casing. |
| `void Subscribe(Action<CultureInfo> callback)` | Register a language-change callback; also invokes it immediately with the current language. |
| `void Unsubscribe(Action<CultureInfo> callback)` | Remove a callback. |

```csharp
using Axe.Flamilingo;
using System.Globalization;
using UnityEngine;

public sealed class LanguageExample : MonoBehaviour
{
    private void OnEnable() => Flamilingo.Subscribe(OnLanguageChanged);
    private void OnDisable() => Flamilingo.Unsubscribe(OnLanguageChanged);

    private void OnLanguageChanged(CultureInfo language)
    {
        Debug.Log($"Active language: {language.Name}");
        Debug.Log(Flamilingo.Translate("menu.play"));
    }

    public void SelectFrench() => Flamilingo.LoadLanguage(CultureInfo.GetCultureInfo("fr"));
}
```

## Text components

`FlamilingoTMP` and `FlamilingoUnityText` derive from `FlamilingoTextBase`. Their common methods include:

| Member | Purpose |
| --- | --- |
| `SetTranslationKey(string key, TextCasing casing = TextCasing.None)` | Assign a key and leave composite mode. |
| `GetTranslationKey()` | Read the assigned key. |
| `SetTranslationKeyCasing(TextCasing casing)` | Change text casing. |
| `SetParameter(string key, string value)` | Set one runtime composite placeholder. |
| `SetParameters(Dictionary<string, string> parameters)` | Set several runtime placeholders. |
| `ClearParameters()` | Clear runtime placeholder values. |
| `RefreshCompositeText()` | Recompute the composite text. |
| `SetAutoRefresh(bool enabled, float interval = 0.1f)` | Configure periodic composite refresh. |
| `IsUsingCompositeText()` / `GetCompositeTemplate()` | Inspect composite configuration. |

`TextCasing` is in `Axe.Flamilingo.Formatting`. Its values are `None`, `FirstLetterUppercase`, `FirstLetterLowercase`, `AllUppercase`, `AllLowercase`, and `TitleCase`.

```csharp
using Axe.Flamilingo;

public sealed class ScoreLabel : UnityEngine.MonoBehaviour
{
    public FlamilingoTMP Label;

    public void UpdateScore(int score)
    {
        Label.SetParameter("score", score.ToString());
        Label.RefreshCompositeText();
    }
}
```

The label above needs a composite template containing `{score}`, with that placeholder configured as a **Runtime Parameter** in the inspector.

## Custom Localizer

`FlamilingoCustomLocalizer` exposes `TargetComponent`, `PropertyName`, `DefaultObjectValue`, `DefaultPrimitiveValue`, and its `ValueMappings`. It also provides `AddObjectMapping`, `AddPrimitiveMapping`, `ClearMappings`, `Refresh`, `GetPropertyType`, and `IsPrimitiveType`.

Prefer configuring mappings in the inspector, which validates compatible targets and serializes them with the scene or prefab. When adding mappings in code, pass a language code that matches a supported culture (for example `fr`).

## Language dropdown

`FlamilingoLanguageDropdown` wraps a `TMP_Dropdown`. It provides `Initialize()`, `Refresh()`, `SetLanguage(CultureInfo)`, `SetLanguageByCode(string)`, `SelectedLanguage`, `Languages`, and `OnLanguageChanged`. Use the component's inspector to choose how language names are displayed.
