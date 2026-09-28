# User guide

## Hub and settings

Open the Hub at **Window → Flamilingo → Hub**. Its main pages are Welcome, Dashboard, Translations, Addressables (when available), and Help. Project settings are at **Window → Flamilingo → Settings**.

### General settings

General settings control the translation file format, default language, edit-mode key display, backups, logging, and automatic translation service. Select a service before entering its endpoint or credentials. Service credentials are stored in machine-local Unity `EditorPrefs`; do not commit them to source control.

The editor currently includes MyMemory, LibreTranslate, Google Translate, DeepL Free, DeepL Pro, and Azure Translator integrations. External services can have their own limits, credentials, and costs. Use **Test connection** to check the configured service before bulk translation.

### Languages

The Languages page shows available and supported cultures. Search by code, English name, or native name, then stage **Add** or **Remove** actions. Changes take effect when you click **Save changes**; **Discard** clears staged changes. Removing a language deletes its translation file, so enable **Create backups** when you want the editor to save a copy first.

## Dashboard

The Dashboard scans the open scene for localizable text components. Enable **Include prefabs** to include prefab assets in the same list; each result is tagged **Scene** or **Prefab**. Use the search field and status filters to narrow the list.

Rows show a status such as **Localized**, **Missing**, **Issue**, or **Ignored**. **Select** pings the component. Depending on the row, you can add or remove localization, or mark text as ignored. Use **Rescan** after changing project content if a row has not updated yet.

## Translations

The left list shows keys and their completed/total language counts. Use **Search keys**, **Missing only**, and pagination to find a key. Select it to edit the key name and each language's value on the right. **Save changes** writes edits; **Discard** drops unsaved edits. You can also duplicate or delete the selected key.

The **Preview** control changes text in the Editor to the selected language. It does not run in Play mode. When preview is off, edit-mode text follows the **Show keys in edit mode** preference.

Automatic translation actions appear only after a translation service is configured. Review generated wording before shipping a build.

## Text component inspector

`FlamilingoTMP` works with TextMeshPro, and `FlamilingoUnityText` works with legacy UI Text. Enter a key or open **Browse and search keys…** to choose one. The inspector reports whether the key exists and offers **Create key** and **Edit in Hub** actions. It also provides an edit-mode Preview toggle and language picker.

### Composite text

Enable **Composite text** when a sentence needs dynamic pieces. A template can contain named placeholders such as `Hello, {playerName}!`. After editing the template, leave the text field so the inspector updates its parameter list. Each placeholder can use a translation key, a static value, a runtime parameter, or a component reference. Set a runtime parameter from code with `SetParameter` or `SetParameters`.

The component can refresh composite text automatically at a configured interval, or you can call `RefreshCompositeText()` when a value changes. Keep the interval appropriate for the content rather than refreshing every frame by default.

## Custom Localizer

`FlamilingoCustomLocalizer` changes a selected component property or field by language. Add it to the same GameObject as the target component, then choose **Target property → Component** and **Property or field**. Enter a **Fallback** value and add language mappings. Each mapping has a language and a value. The fallback applies when the current language has no usable mapping.

The inspector supports compatible Unity object references and supported value types. For object references, assign assets of the property type; for text and other supported values, enter the value in the field. The package generates preservation information for reflected members used in IL2CPP builds. Validate the result in a player build when localizing reflected properties.

## Language selection

The **GameObject → UI → Flamilingo → Language Selection** menu adds the supplied dropdown prefab. `FlamilingoLanguageDropdown` populates its options from the configured languages and follows language changes made elsewhere. It can display codes, native names, English names, or combinations, and can sort options alphabetically.

Use `Flamilingo.LoadLanguage(...)` to change language without a dropdown. The selection is persisted in `PlayerPrefs`. For details, see the [API reference](api.md).

## Sample content

The Welcome page can create sample translations and select the optional Showcase scene when the sample is present in the package. Open the sample in a copy or save your current scene before switching to it.
