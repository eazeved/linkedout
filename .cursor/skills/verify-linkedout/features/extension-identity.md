# Extension identity

Users can tell they are in LinkedOut by the popup page title and the visible `LinkedOut` heading after the extension loads.

## Sub-features

- `identity-heading` shows an `h1` named `LinkedOut`.
- `identity-build` doctor reports a `buildRevision` that includes the manifest name `LinkedOut`.

## How to get to it (user POV)

- Open the LinkedOut popup from the browser toolbar action.

## Driving it with control-linkedout

Preconditions:

- Launch completed for `$LINKEDOUT_VERIFY_RUN_ID`.

- **Doctor identity.** Run `bun run verify:control -- doctor --run-id "$LINKEDOUT_VERIFY_RUN_ID"`. JSON includes `headingVisible: true` and `buildRevision` starting with `LinkedOut@`.
- **Open popup.** Run `bun run verify:control -- open-popup --run-id "$LINKEDOUT_VERIFY_RUN_ID"`. Heading `LinkedOut` is present.
- **Proof.** Run `bun run verify:control -- snapshot --run-id "$LINKEDOUT_VERIFY_RUN_ID" --path .cursor/skills/verify-linkedout/artifacts/extension-identity/popup.aria.txt` and `bun run verify:control -- screenshot --run-id "$LINKEDOUT_VERIFY_RUN_ID" --path .cursor/skills/verify-linkedout/artifacts/extension-identity/popup.png`. Artifacts include the `LinkedOut` heading.

## Gotchas

- If `buildRevision` still shows `wxt-react-starter`, the manifest name was not rebuilt — rerun launch without `--no-build`.
- Do not treat the WXT/React logos as product identity; the heading is the stable signal.
