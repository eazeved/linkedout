# Popup counter

The popup shows a LinkedOut heading and a button that increments a local click count when activated.

## Sub-features

- `counter-open` opens the extension popup document.
- `counter-increment` increases the visible count by one per click.
- `counter-label` keeps the accessible name `Increment count` while the visible label shows `count is N`.

## How to get to it (user POV)

- Open the LinkedOut toolbar action popup (verification opens `popup.html` directly in the loaded extension).

## Driving it with control-linkedout

Preconditions:

- A healthy launch for `$LINKEDOUT_VERIFY_RUN_ID` (`doctor` reports `ok: true`).
- Popup heading `LinkedOut` is visible.

- **Open popup.** Navigate to the popup document. Run `bun run verify:control -- open-popup --run-id "$LINKEDOUT_VERIFY_RUN_ID"`. The heading `LinkedOut` is visible.
- **Read initial count.** Read the increment control. Run `bun run verify:control -- text --run-id "$LINKEDOUT_VERIFY_RUN_ID" --role button --name "Increment count"`. Stdout JSON `text` is `count is 0` on a fresh popup.
- **Increment.** Activate the control. Run `bun run verify:control -- click --run-id "$LINKEDOUT_VERIFY_RUN_ID" --role button --name "Increment count"`.
- **Confirm new count.** Read the control again. Run `bun run verify:control -- text --run-id "$LINKEDOUT_VERIFY_RUN_ID" --role button --name "Increment count"`. Stdout JSON `text` is `count is 1`.
- **Proof.** Capture ARIA and screenshot. Run `bun run verify:control -- snapshot --run-id "$LINKEDOUT_VERIFY_RUN_ID" --path .cursor/skills/verify-linkedout/artifacts/popup-counter/popup.aria.txt` and `bun run verify:control -- screenshot --run-id "$LINKEDOUT_VERIFY_RUN_ID" --path .cursor/skills/verify-linkedout/artifacts/popup-counter/popup.png`. Artifacts show heading `LinkedOut` and `count is 1`.

## Gotchas

- Reloading `open-popup` resets React state; expect `count is 0` again after a fresh open.
- Match the button by accessible name `Increment count`, not by the changing visible `count is N` string alone when clicking.
- A screenshot without a before/after text read is incomplete proof for this feature.
