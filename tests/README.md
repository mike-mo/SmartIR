# Isolated command regression tests

From the repository root, in a virtual environment:

```text
python -m pip install -r tests/requirements.txt
python -B -m unittest discover -s tests -v
```

These tests import the actual `climate.py` and `controller.py` modules. They use
the standard library's `unittest` runner, synthetic command strings, and small
Home Assistant boundary substitutes in `support.py`. No Home Assistant instance,
network service, credentials, or IR hardware is used.

The fake service registry distinguishes enqueueing from awaited completion.
Explicit gates exercise delayed sends, deferred failures and concurrent requests.
Tests also cover state retention, lookup validation before a preamble, partial
preamble failure, controller payloads, HTTP errors, cancellation, Off settings,
restoration and sensor callbacks.

This is not full Home Assistant integration validation. Integration startup,
entity-service schemas, actual restore persistence, event-bus scheduling,
Pronto conversion helpers and physical IR behavior are not exercised. Direct
invalid-input tests do not imply those inputs can pass Home Assistant's service
schemas. Successful fake transport does not imply appliance acknowledgement.

The suite runs on Python 3.13. Testing against Home Assistant 2026.8.3 itself
requires Python 3.14.2 or newer and a supported Home Assistant environment.
