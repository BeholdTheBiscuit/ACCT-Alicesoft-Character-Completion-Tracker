# ACCT — AliceSoft Character Completion Tracker

ACCT is a portable Windows desktop application for tracking character recruitment and character-clear progress in AliceSoft games. It currently includes a DaiAkuji database and can load a user-provided database for a **Custom Game**.

ACCT helps organize character information, checklists, and progress in one place. Character notes may call out missable events, betrayal conditions, or risks such as a character dying, but they are not a complete campaign walkthrough and cannot guarantee that every mistake or accidental death will be prevented. A full walkthrough is outside ACCT's current scope.

## Features

- **Visual character gallery:** Browse character portraits in a gallery that uses two columns when there is room. Portrait overlays show progress: no tint for not started, green for in progress, and a subtle gray wash for completed.
- **Search and filters:** Search by character name, filter by completion status, and filter by affiliation.
- **Character profiles:** View general information, capture instructions, character-clear requirements, CG entries, and other notes. Optional sections can be collapsed.
- **Separate checklists:** Track multi-step capture instructions and character-clear requirements independently. Capture progress does not count toward character-clear completion.
- **Manual completion:** Use **Mark as completed** for a character with a clear checklist when you want to mark that clear complete manually. Characters without a character-clear checklist are treated as completed by default.
- **Custom game databases:** Load a custom `characters.json` without changing the built-in DaiAkuji database. Custom profiles keep their progress separate.
- **Portable data:** Progress and application preferences are stored in `ProgressSaveFile` next to the application.
- **Faster repeat launches:** Generated gallery thumbnails are cached in `ProgressSaveFile\ThumbnailCache` and rebuilt automatically when their source image or crop settings change.
- **Localized interface:** Choose English, Italian, Spanish, Simplified Chinese, or Japanese from the Language menu. Character database text is shown as written in its JSON file and is not translated.

The Italian, Spanish, Chinese, and Japanese interface translations are machine-translated and may contain errors or awkward phrasing. English is the original interface language.

## Supported games

- **DaiAkuji:** Included character database and portraits.
- **Custom Game:** Load a character database supplied or edited by the user.

Other AliceSoft games, including DaiTeikoku, DaiBanchou, and Sengoku Rance, are not currently included as ready-to-use databases. They may be added as custom databases, subject to the data format and any game-specific information the user supplies.

## Getting started

1. Run `ACCT.exe` on Windows.
2. The DaiAkuji database is selected by default.
3. To load another database, choose **Game > Custom Game...** and select its `characters.json` file.
4. Use the gallery and filters to find characters, then update their capture or character-clear checklists as you play.

The application is built with Windows Forms on .NET Framework 4.8. Use a Windows system with the .NET Framework 4.8 runtime to run it.

## Custom game data

Keep a custom game's database and assets together. For example:

```text
My Custom Game/
  characters.json
  images/
    Example_Character.jpg
  thumbnails/
    Example_Character.jpg
```

Select `characters.json` through **Game > Custom Game...**. Image paths in the JSON are relative to the folder containing that file. ACCT supports standard character fields such as `Area`, `CaptureRegion`, `HowToObtain`, `LoyaltyType`, `Range`, `Skill`, `CGList`, `OtherNotes`, `CaptureRequirements`, and `Requirements`. Fields that do not apply to a game may be omitted or left empty.

### Custom fields

Use the optional `CustomFields` list for game-specific details that do not have a standard ACCT field. Entries appear beside the character portrait in the order listed:

```json
"CustomFields": [
  { "Label": "Weapon", "Value": "Katana" },
  { "Label": "Starting region", "Value": "Owari" }
]
```

Custom fields are edited directly in `characters.json`; ACCT does not currently include an in-app database editor. They are display-only and do not create additional filters.

### Character portraits and thumbnails

Set `ImagePath` to the full-size portrait, for example `images/Example_Character.jpg`. ACCT looks for a thumbnail with the same filename in the database's `thumbnails` folder. If it does not find one, it generates a gallery thumbnail from the full-size portrait.

To use a thumbnail in a different location, set `ThumbnailPath` for that character. The optional `Thumbnail` crop settings can adjust generated thumbnails. See [THUMBNAILS.md](THUMBNAILS.md) for details.

For a complete custom database setup guide, see [CUSTOM_GAMES.md](CUSTOM_GAMES.md).

## Progress and portability

ACCT stores progress, collapsed-section preferences, and the selected game in `ProgressSaveFile` next to the application. Custom-game progress is kept in a separate subfolder for each selected database file. Keep `ProgressSaveFile` when moving, backing up, or copying the application if you want to keep its saved progress and preferences.

Custom-game profiles are identified by the database file's path. Moving or renaming a custom database file creates a separate profile with its own progress.

## Technology

- C# and .NET Framework 4.8
- Windows Forms
- JSON serialization through `System.Web.Script.Serialization`
