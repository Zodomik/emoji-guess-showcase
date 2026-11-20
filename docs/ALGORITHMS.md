# Emoji Guess · Algorithms and implementation choices

## 1. A forgiving answer matcher

The matcher first folds case and diacritics, normalizes Turkish letter forms, removes punctuation and normalizes whitespace. It compares normalized strings, then compact forms without spaces, then a form with a leading English article removed.

If those checks fail, it calculates **Levenshtein edit distance** using two rolling rows. That uses `O(n × m)` time for input lengths `n` and `m`, with two row arrays rather than a full distance matrix.

The matcher allows a distance of one for answers of at most six characters and two for longer ones. A further branch accepts answers longer than eight characters when normalized similarity is at least 0.82.

This is a deterministic text rule, not an LLM or semantic embedding comparison. It accepts small surface differences rather than understanding arbitrary synonyms.

## 2. The answer UI and matcher work together

The game view model checks that all non-whitespace answer slots are filled before calling the fuzzy matcher. Consequently, a match that the utility could accept in isolation may still be rejected by that earlier length gate.

For example, punctuation/case normalization is useful in the actual flow, while some omitted-article or missing-letter cases can be constrained by slot length. The documentation distinguishes the utility’s rules from the full submission path.

## 3. Progress based on identity, not position

Completed puzzles are stored as category-plus-ID strings in a set. Replaying a completed puzzle does not increase the set’s size. Older count-only progress can be migrated by taking the corresponding prefix of the loaded puzzle list and storing those IDs.

Example: a category gains a new puzzle near its beginning. ID-based history still identifies the puzzles already completed; it does not blindly mark the first N items as completed on every load.

## 4. Infinity mode without immediate repeats

The client combines category content with extra infinity puzzles, filters out the played-ID set, then shuffles the remaining pool. When no unplayed puzzle remains, it resets that played set and begins another shuffled pass.

This is an exhaustion-and-reset rule. It does not promise a globally unique infinite sequence or prevent a repeat across the boundary between two complete passes.

## 5. Separate daily play and reward identities

Daily puzzle progress includes locale and date, so a player can have different played/correct counts for different language versions. Reward completion uses the date without the locale, with compatibility checks for older saved keys.

The distinction keeps language-specific play history while limiting the daily completion reward to one claim marker per day on that device. It is local reward bookkeeping rather than server-side account accounting.

## 6. Category loading and cache invalidation

The manifest supplies counts before all category arrays are decoded. A requested category is fetched and cached; subsequent memory-cache hits reuse it. Switching locale clears the cached manifest, category arrays and combined infinity pool. Successful remote responses are written to disk for later fallback.

The reviewed loader uses synchronous data retrieval internally. It should not be described as an actor-based, nonblocking networking pipeline. The useful design here is the content partitioning and locale-aware cache structure.

## 7. Hints and rewards

A random-letter hint builds candidate non-space positions and excludes already revealed positions, then chooses one and spends coins. Difficulty determines the base correct-answer reward; every fifth consecutive correct answer adds a streak bonus. These rules live in the game view model, separately from answer normalization and content loading.

[Architecture](ENGINEERING.md) · [Data layout](DATA_MODEL.md)
