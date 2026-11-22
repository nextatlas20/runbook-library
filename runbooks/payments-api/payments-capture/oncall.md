# Escalation — payments-api

Rotation: sre-payments-primary

1. Page the primary through `#oncall-payments`.
2. Escalate to the acquiring bank relationship owner if a single acquirer is
   responsible for more than 80% of the failures.
3. Loop in finance operations before any manual capture replay above 500 EUR.
