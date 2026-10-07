Phase 6B-T3 — Waiting on your attachment
I can't attach files (no API; the composer is yours). Everything else is staged and verified.
Fixture verified
/tmp/opencode/vr-t3-image.png
bytes : 25,058            ✅ matches expected
sha256: 4b64d63e740c19686d1c13dcce2ec1e17bcff94732383a0a0ee358ecb30770fe   ✅ matches
mode   : 600
Harness /tmp/opencode/t3_forensics.py ready (11,816 B), not run. It makes its own read-only snapshot and cleans up after.
Your two steps
1. Attach /tmp/opencode/vr-t3-image.png — confirm the picker shows vr-t3-image.png, not a screenshot.
2. Send image + prompt in ONE message. Exact text:
deskripsikan gambar ini PROMPT-CANARY-6B-A73184C1EEDE
Two things to check before you hit send, given how T2 went:
the text is actually in the composer alongside the attachment (T2's messages all stored only '[Image 1] ' — the typed text was dropped twice)
the image canary is not in that text — it lives only in pixels
⚠️ Disclosure: printing the canary here means it also lands in this parent session as part of my message. That's parent-side only and doesn't affect any assertion — the child receives only the fixed instruction plus the image.
Then reply "done" and I'll run the harness exactly once. All four gates first; if any fails → INVALID and no assertions run. Otherwise dual-channel discrimination: PROMPT canary must be absent from every child part, the child FilePart bytes, child reasoning, and the vision response; the IMG canary may appear, and I'll classify it as image-derived recognition evidence rather than leakage.
No T4 or any other test will be started.
Compliance
No plugin, config, package, or database modification. No restart, no kill, no model change, no credential access. Fixture and canaries unmodified. Harness not executed. Light on resources — this turn ran no DB snapshot.
