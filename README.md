# homebrew-voxinq

A [Homebrew](https://brew.sh) tap for [Voxinq](https://github.com/ikasast/voxinq-meeting) —
self-hosted meeting minutes: record in the browser, transcribe and summarize on your own
machine.

```bash
brew install ikasast/voxinq/voxinq
voxinq setup     # dependencies, build, transcription and speaker-separation environments
voxinq start
```

## ⚠️ This formula has not been installed from

It is written from Homebrew's documented behaviour and reviewed, but **nobody has run
`brew install` on it** — there is no Mac available to the person who wrote it. The pieces
underneath it are tested: the release archive, and the `voxinq setup` and `voxinq start` that
follow, all verified on Windows, and the equivalent Scoop package verified end to end.

What that leaves untested is the formula itself — the `install` block, the wrapper it writes,
and whether `depends_on "python@3.11"` lands somewhere `voxinq setup` finds.

If you try it, [an issue](https://github.com/ikasast/voxinq-meeting/issues) saying what happened
is genuinely useful, working or not.

## What comes with it

| | |
| --- | --- |
| PostgreSQL | bundled — nothing to install or configure |
| Node, Python | Homebrew dependencies |
| An LLM for minutes | not included: `brew install ollama`, or point Settings → LLM at a cloud model |

Your data lives in `~/Library/Application Support/voxinq`, outside the install, so upgrading or
removing the formula cannot delete it.

`voxinq setup` is a separate step because it takes several minutes and downloads speech models.
Doing that inside `brew install` would mean minutes with nothing to look at and no way to
resume. It is re-runnable, and it is also how you finish an upgrade.

## What to expect on a Mac

On Apple silicon, transcription runs on Metal and keeps up with live speech. On an Intel Mac it
runs on the CPU, which is slower than speech — there Voxinq records the meeting and transcribes
it in one pass at the end, at the same quality.

Speaker separation uses ONNX models that need no account. pyannote, the more accurate backend,
needs CUDA and so does not apply here.

## Updating the formula

`Formula/voxinq.rb` is copied from
[`packaging/homebrew/voxinq.rb`](https://github.com/ikasast/voxinq-meeting/tree/main/packaging)
in the main repository, which is where it is edited. The release workflow prints the `url` and
`sha256` to update it with.
