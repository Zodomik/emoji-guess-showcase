![Emoji Guess — A few emojis. One satisfying answer.](assets/hero.svg)

<p align="center">
  <a href="https://apps.apple.com/us/app/emoji-guess-fun-emoji-puzzle/id6762650151"><strong>View on the App Store ↗</strong></a> &nbsp; · &nbsp;
  <a href="docs/ENGINEERING.md">Engineering notes</a> &nbsp; · &nbsp;
  <a href="https://github.com/Zodomik">More by Oğuz Tonyalı</a>
</p>

## Emoji Guess

A native word puzzle game about decoding emoji combinations. Movies, music, idioms and more become quick challenges with hints, rewards and daily progression.

Built and published by **[Oğuz Tonyalı](https://github.com/Zodomik)**. This repository is a public product and engineering showcase; the application source is maintained privately.

## A look inside

<p align="center">
  <img src="assets/screen-01.jpg" width="30%" alt="Emoji Guess official App Store preview 1" />
  <img src="assets/screen-02.jpg" width="30%" alt="Emoji Guess official App Store preview 2" />
  <img src="assets/screen-03.jpg" width="30%" alt="Emoji Guess official App Store preview 3" />
</p>

*Official product previews from the [App Store listing](https://apps.apple.com/us/app/emoji-guess-fun-emoji-puzzle/id6762650151).*

## What you can do

- Emoji puzzles across multiple topics and categories.
- Coins, hints, skips and progression rewards.
- Daily challenges and streak tracking.
- Localized content and forgiving answer matching.

## Technology

| Area | Technologies | Role in the product |
| --- | --- | --- |
| Interface | Swift, SwiftUI | Home, puzzle and result flows with responsive game state. |
| Content | Node.js HTTP API, JSON, Foundation | Remote locale/category content with memory and disk caches. |
| Answer evaluation | Unicode normalization, Levenshtein distance | Case/diacritic handling and limited typo tolerance. |
| Product integrations | Firebase Analytics, Google Mobile Ads | Gameplay analytics and advertising integration. |
| Device feedback | UIKit, AudioToolbox, Network | Haptics, audio feedback and connectivity observation. |

## Implementation notes

SwiftUI client; dependency-free Node.js HTTP content server; locale/category JSON storage; device disk cache and UserDefaults progress.

- Unicode normalization and rolling-row Levenshtein answer matching.
- Stable puzzle IDs and migration from count-based progress.
- Locale-specific daily progress with a shared per-date reward marker.

| Read more | What is covered |
| --- | --- |
| [Architecture and frameworks](docs/ENGINEERING.md) | Runtime components, backend structure and framework responsibilities |
| [Database and local data](docs/DATA_MODEL.md) | Entities, relationships, constraints and persistence choices |
| [Algorithms and implementation choices](docs/ALGORITHMS.md) | Calculations, example flows and the limits of each approach |

## Try the product

**[Open Emoji Guess on the App Store](https://apps.apple.com/us/app/emoji-guess-fun-emoji-puzzle/id6762650151)** · Requires iOS 17.0 or later.

Availability and purchase options are shown in the store. For product support, use the developer links on the App Store listing.

---

[All published apps](https://apps.apple.com/us/developer/oguz-tonyali/id1880078720) · [Developer profile](https://github.com/Zodomik) · [Media credits](assets/SOURCES.md)
