# omp-anthropic-quota

OMP statusline extension showing live Claude subscription (Pro/Max) quota: 5-hour window, 7-day window, and banked resets with the nearest expiry.

Fork of the OpenAI quota extension in [zznabil/omp-openai-quota](https://github.com/zznabil/omp-openai-quota), repurposed for the `anthropic` provider.

    Claude │ ⏱ 5h 95% · 2h │ ↻ 7d 99% · 2d 5h │ ◆ Banked resets 1 · 16d

## Install

Requires OMP with an authenticated `anthropic` provider. Copy the extension, then restart OMP:

    mkdir -p ~/.omp/agent/extensions
    cp agent/extensions/anthropic-quota.ts ~/.omp/agent/extensions/

## Behaviour

- Runs `omp usage --provider anthropic --json` (10 s timeout) on session start, after each turn and every 5 minutes.
- Shows the shared 5h and 7d windows; model-tiered limits (e.g. `7d:fable`) are ignored.
- With several Anthropic accounts, the first matching limit is used; accounts are not combined.
- Colour: green above 25% remaining, yellow at 25% or below, red at 10% or below.
- Missing values show `—`; a failed usage check shows `Claude quota unavailable`.
- Uses status key `anthropic-quota`, so it coexists with the OpenAI extension.

## Test

    bun test agent/extensions/anthropic-quota.test.ts
