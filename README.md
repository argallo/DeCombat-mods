# DeCombat mods

DeCombat mod packs, one folder each under `mods/`. Every pack is Lua text, data and its own original assets: no
file from the game client, no asset taken from anywhere without a licence that allows it. The game's rules for
packs are in the DeCombat repository (`docs/MODDING_GUIDE.md`); this repository only has to build.

## Build

    python3 tools/modrepo.py build .            # validates, lints and packs every mod into dist/

`dc-modkit` comes from the DeCombat repository: `cargo install --git https://github.com/argallo/DeCombat dc-modkit --locked`, or pass the
binary with `--modkit`. Add `--rom <your client folder>` to check weapon rows against the real tables.

## Release

Tag `v<date or number>` and push the tag: the workflow builds the packs and publishes a release with every zip,
`packs.json` (id, version, sha256 per pack), `SHA256SUMS` and the rows ready to paste:

- `vanilla_plus_rows.json`: the review-list rows for a pull request against `community/vanilla_plus.json` (fill in
  `reviewer_note`);
- `known_mods.json`: the verified-badge rows for `community/community.json`;
- `server_toml_lines.txt`: `[[mods.set]]` / `[[mods.catalog]]` blocks for a server operator.

Operators install `<sha256>.zip` from the release into their lobby's mods folder; players download it from the
server. The sha256 of the published zip is the one in the row: a different byte is a different pack.

## Change a pack

Bump `version` in its `manifest.json` with every change that reaches players; a new version is a new row. Keep the
first screenshot a picture of your own making. `generators/<id>/` holds the scripts that drew a pack's art, when it
was drawn by code.
