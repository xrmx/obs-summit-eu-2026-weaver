# Observability Summit EU 2026: Testing Your Telemetry Output With OpenTelemetry Weaver

This repository contains a small OpenTelemetry demo built around a Python
Flask application that rolls six-sided dice. It shows the progression from
automatic instrumentation to application-defined telemetry backed by custom
semantic conventions.

## Repository contents

| Path | Description |
| --- | --- |
| [`rolldice/`](rolldice/) | Baseline Flask application instrumented automatically with the OpenTelemetry Python distribution. |
| [`rolldice-custom/`](rolldice-custom/) | Extended version of the application with a custom `roll` span, a `dice.rolls` counter, and the `roll.value` attribute. |
| [`custom-registry/`](custom-registry/) | Weaver semantic-convention registry for the custom dice telemetry, including model definitions, documentation templates, generated docs, and live-check configuration. |

The custom registry imports the standard OpenTelemetry HTTP conventions and
adds conventions for the dice-roll operation. Its generated reference
documentation is available in
[`custom-registry/docs/metrics.md`](custom-registry/docs/metrics.md) and
[`custom-registry/docs/spans.md`](custom-registry/docs/spans.md).

## Requirements

- Python 3.11
- [uv](https://docs.astral.sh/uv/)
- [Weaver](https://github.com/open-telemetry/weaver), when validating or
  generating the custom semantic-convention registry

## Run the examples

Each application is an independent Python project. Its `env` file contains the
OpenTelemetry runtime configuration.

Run the baseline application:

```bash
cd rolldice
uv run --env-file env opentelemetry-instrument flask run
```

Run the custom-telemetry application:

```bash
cd rolldice-custom
uv run --env-file env opentelemetry-instrument flask run
```

With either application running, roll the dice at
<http://127.0.0.1:5000/rolldice>. An optional `player` query parameter is
included in the application log:

```bash
curl "http://127.0.0.1:5000/rolldice?player=alice"
```

## Work with the custom registry

From `custom-registry/`, use the included Makefile targets:

```bash
make check-model  # Validate the registry model
make docs         # Regenerate the Markdown reference documentation
make live-check   # Check emitted telemetry against the registry
```

The registry source is in `custom-registry/model/`. The templates under
`custom-registry/templates/` control the generated Markdown output.
