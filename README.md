ACCT — AliceSoft Character Completion Tracker

ACCT is a portable Windows Forms application for tracking character recruitment and character-clear progress in AliceSoft games. It keeps character data in JSON and saves player progress separately in `ProgressSaveFile` beside the application.

Character notes can point out missable events, betrayal conditions, or character-death risks. They are not a complete campaign walkthrough and cannot guarantee that every mistake or accidental death will be prevented. A full walkthrough is outside ACCT’s current scope.

## Features

- **Three-column character gallery** with search, completion-status filters, and a multi-select affiliation filter.
- **Character profiles** with recruitment information, character-clear steps, notes, event and CG lists, custom fields, and images.
- **Separate recruitment and character-clear checklists.** Informational notes and sub-bullets can be shown without adding progress checkboxes.
- **Keyboard navigation** through the gallery with the arrow keys when the search field is not focused.
- **Portable, per-game and per-profile progress** stored under `ProgressSaveFile` next to the application. Generated gallery thumbnails are cached there too.
- **JSON validation** from **Options → Validate JSON Files**. The report includes field paths and source locations where available; image-path problems are warnings, since missing portraits can be intentional.
- **Anchor Mode** from **Options → Anchor to AliceSoft Game**. Open a supported AliceSoft game in windowed mode, then use this option to place ACCT’s gallery and details beside the game and keep them aligned as the game window moves. Select **Exit Anchor Mode** to restore the normal layout.
- **English, Italian, Spanish, Simplified Chinese, and Japanese interface languages.** Database text is shown as written in JSON and is not translated. The Italian, Spanish, Chinese, and Japanese interface translations are machine-translated; English is the original interface language.

The interface is built with C# and Windows Forms on .NET Framework 4.8.

## Custom game data

Choose **Game → Custom Game...** and select a `characters.json`. Selecting `ui.json` in the same folder is also supported; ACCT uses the adjacent character database. Keep custom data and assets together, for example:

```text
My Custom Game/
  characters.json
  ui.json                 (optional)
  images/
  thumbnails/             (optional)
```

Image paths are relative to the folder containing `characters.json`. A thumbnail with the same filename in `thumbnails/` is used automatically; `ThumbnailPath` can specify another path. See [CUSTOM_GAMES.md](CUSTOM_GAMES.md) and [THUMBNAILS.md](THUMBNAILS.md) for the JSON format and image options.

The optional `CustomFields` list adds game-specific display-only labels and values. Section and field labels can be customized in `ui.json`. ACCT does not include an editor for `ui.json`.

A separate prototype for editing character records is in the repository at `tools/CharacterDatabaseEditor/`; it does not edit progress saves or `ui.json`.

## Progress and portability

Progress, selected game, collapsed-section preferences, and generated thumbnail cache are stored in `ProgressSaveFile` next to the executable. Custom-game progress is separated by database profile. Keep this folder when backing up or moving an installation whose progress you want to retain.

## Included games

- **DaiAkuji:** Built-in character database and portraits.
- **Custom Game:** Load a user-provided character database.

This build is dedicated to DaiAkuji and Custom Game. For the built-in DaiBanchou, DaiTeikoku, and Sengoku Rance databases, use the multi-game build.

## Getting started

1. Run `ACCT.exe` on Windows.
2. DaiAkuji opens by default.
3. Use the **Game** menu to load a custom database, or select a character in the gallery to view and update its information.



