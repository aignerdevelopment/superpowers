# Superpowers — pinned source for harnessator

A governed **[harnessator](https://github.com/aignerdevelopment/harnessator)
source**, produced by `harnessator harvest` from
[obra/superpowers](https://github.com/obra/superpowers) at commit
`2ce8aa15d05b` (v7.0.1). The skills are **Jesse Vincent's**, MIT licensed —
the `LICENSE` file here travels with them verbatim, as the license requires.
Nothing in `skills/` was edited: every directory is byte-identical to
upstream, and every component's `origin` in `harnessator.toml` records the
exact upstream commit it came from.

## Why this repo exists

Upstream is a Claude-Code-first plugin that also ships per-harness
integrations. This mirror adds one thing: a source manifest, so teams can
consume the skills through harnessator's pinning, scope layers, provenance
and policy checks instead of per-tool copies. If the upstream ever carries
its own manifest, this repo becomes unnecessary — point your source at
obra/superpowers directly and delete this one.

## Consume it

```sh
harnessator source add https://github.com/aignerdevelopment/superpowers.git --ref v7.0.1
harnessator enable superpowers:core      # or superpowers:default (all skills)
harnessator setup
```

`superpowers:core` = using-superpowers, test-driven-development,
systematic-debugging, brainstorming. `superpowers:default` = every skill currently upstream - live, via `[discover]`.

Notes on behaviour: skills are materialized unchanged (symlinks into the
pinned checkout); cross-skill references like
`../using-superpowers/references/…` resolve because the skills land as
siblings. Upstream's session-start bootstrap (its plugin hook that
auto-injects `using-superpowers`) is plugin machinery and is **not**
carried — skills load through each harness's native skill discovery.

## Update policy

Re-harvest from an upstream tag: clone at the tag, run
`harnessator harvest --name superpowers ./skills`, restore the package
block and `profiles.core`, refresh this README's commit line, commit, tag
`v<upstream version>`. One reviewable commit per upstream release;
consumers move by updating their lock, not by surprise.
