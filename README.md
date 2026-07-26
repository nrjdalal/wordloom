# wordloom

**Find short, pronounceable names for brands, products, and projects.**

[![Twitter](https://img.shields.io/twitter/follow/nrjdalal?label=%40nrjdalal_dev)](https://twitter.com/nrjdalal)
[![npm](https://img.shields.io/npm/v/wordloom?color=red&logo=npm)](https://www.npmjs.com/package/wordloom)
[![downloads](https://img.shields.io/npm/dt/wordloom?color=red&logo=npm)](https://www.npmjs.com/package/wordloom)
[![stars](https://img.shields.io/github/stars/nrjdalal/wordloom?color=blue)](https://github.com/nrjdalal/wordloom)
[![license](https://img.shields.io/npm/l/wordloom)](https://www.npmjs.com/package/wordloom)

`wordloom` is a CLI for exploring names that feel like they could be real words. It follows letter patterns learned from 100k+ English words, then checks generated candidates against WordNet so real dictionary words can show their meanings inline.

```sh
npx wordloom --length 5 --prefix no
npx wordloom --length 5 --prefix re --suffix t
npx wordloom --contains bel
```

Use a sound, fragment, beginning, or ending you already like and keep narrowing until the results fit.

## Use it to name anything

- **Startups and brands** — explore memorable names around a sound you like
- **Apps and products** — discover short names that feel intentional
- **CLI tools and libraries** — find names developers can remember and type
- **Side projects** — brainstorm without starting from a blank page
- **Creative writing** — generate fictional places, companies, or technologies

## Quick start

Run without installing:

```sh
npx wordloom
```

Or install globally:

```sh
npm install -g wordloom
wordloom --help
```

Default length is `5`. Supported lengths are `2` through `8`.

## Examples

```sh
wordloom --prefix no                       # names starting with "no"
wordloom --suffix ut                       # names ending in "ut"
wordloom --contains bel                    # names containing "bel"
wordloom --length 5 --prefix z --suffix da # combine length, prefix, and suffix
wordloom --length 5 --prefix no --suffix el
wordloom --length 6 --prefix absent        # dictionary match with a meaning
```

For example, the exact `absent` match includes its WordNet meaning:

```text
┌───┬────────┬──────────────────────────────────────────────┐
│   │ name   │ meaning                                      │
├───┼────────┼──────────────────────────────────────────────┤
│ 1 │ absent │ verb: go away or leave; adjective: not      │
│   │        │ being in a specified place                   │
└───┴────────┴──────────────────────────────────────────────┘
```

Broad queries can return a lot of results because `wordloom` enumerates every matching candidate. Add more constraints to narrow the output, or pipe it through standard shell tools such as `less`.

## Why wordloom?

- **Pronounceable, not random** — names follow real English letter transitions derived from [CMUdict](https://github.com/cmusphinx/cmudict)
- **Built-in meaning check** — dictionary matches show their [WordNet](https://wordnet.princeton.edu/) definitions inline
- **Precise filtering** — combine exact length, prefix, suffix, and substring constraints
- **Fast and offline** — the language model ships with the package, with no API calls or API keys
- **Terminal-native** — clean table output with dictionary matches highlighted in interactive terminals

## Options

```text
-l, --length <number>         Exact name length to generate (2-8, default: 5)
-c, --contains <text>         Literal substring to require anywhere in the name
-p, --prefix <prefix>         Literal starting prefix to validate and continue from
-s, --suffix <suffix>         Literal ending suffix to require
-h, --help                    Show help
-v, --version                 Show version
```

All text filters accept letters only and can be combined. If no candidate satisfies the constraints, `wordloom` prints `No results found.`

## How it works

`wordloom` learns which letters naturally follow each other in English by analyzing 100k+ words from [CMUdict](https://github.com/cmusphinx/cmudict). Generation follows observed letter transitions rather than choosing characters independently, which is why candidates feel more word-like than random strings.

Each result is checked against [WordNet](https://wordnet.princeton.edu/). If a candidate is also a dictionary word, its meaning is shown inline.

The pre-built model and dictionary data ship with the package, so everything runs locally.

## A note on naming

`wordloom` generates naming candidates. It does not check domains, trademarks, company registrations, usernames, or package-name availability. Do the appropriate availability and trademark checks before choosing a name for a real product or business.

## For maintainers

Regenerating the model is only needed when refreshing the checked-in data sources:

```sh
bun install
bun run derive:model
bun run build
bun test
bun run lint
bun run format:check
```

Generated data lives in [bin/cmudict-model.ts](./bin/cmudict-model.ts) and [bin/wordnet-definitions.ts](./bin/wordnet-definitions.ts).

## License

MIT
