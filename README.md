# model-costs

Pricing-aware model picker for **pi** (https://pi.dev). The built-in `/model`
selector does not show pricing — this extension adds a model picker that shows
the real cost of each model before you switch.

## Features

- **`/model-cost [query]`** — model picker with:
  - per-1M-token input/output cost
  - context window and max output tokens
  - cache read/write rates and pricing tiers
  - reasoning support and modality (text / text+image)
  - same flow as `/model`: arrows to navigate, type to fuzzy-filter, `Tab`
    toggles all/scoped (when scoped models are configured), `Enter` selects,
    `Esc` cancels
  - `Ctrl+S` cycles cost sort: default → in↑/↓ → out↑/↓ → total↑/↓
    (total = input + output); the footer legend shows the active sort
- **Footer status** — pricing of the currently active model in the footer
  (disable it by setting `SHOW_STATUS = false` in the source).

The current model is marked with a ✓ — pinned to the top in default sort,
at its ranked position in cost sorts.

![model-cost picker](images/model-cost.png)

## Install

> Fork of
> [MaurizioFaeddaDev/model-costs](https://github.com/MaurizioFaeddaDev/model-costs)
> — adds `Ctrl+S` cost sorting. Upstream installs keep working; use below to
> switch to this fork (run only one copy — both register `/model-cost`).

```bash
# check what you have
pi list

# from upstream npm -> this fork
pi remove npm:pi-model-costs
pi install git:github.com/bizzkoot/model-costs

# from upstream git -> this fork
pi remove git:github.com/MaurizioFaeddaDev/model-costs
pi install git:github.com/bizzkoot/model-costs

# update this fork later
pi update git:github.com/bizzkoot/model-costs

# switch back to upstream (npm or git)
pi remove git:github.com/bizzkoot/model-costs
pi install npm:pi-model-costs
# or: pi install git:github.com/MaurizioFaeddaDev/model-costs
```

To try this fork without installing:

```bash
pi -e git:github.com/bizzkoot/model-costs
```

> `pi remove` needs the exact source string shown by `pi list`.

> Only interactive (`tui`) mode supports the custom picker. In print/RPC mode
> the command notifies you that it is unavailable.

## Usage

```bash
/model-cost              # browse all models
/model-cost claude       # fuzzy-filter by provider/id/name
/model-cost $0.00        # fuzzy-filter by cost
```

Inside the picker, `Ctrl+S` cycles the cost sort; the footer legend shows
the active sort, e.g. `ctrl+s sort (in↑)`.

`/model-cost` extends the built-in `/model` selector; the actual model switch
still goes through pi's normal `setModel` path, so API keys are resolved the
same way.

## License

MIT
