# runbook-library

Operational runbooks for HelioWorks services, kept as plain markdown so that
they can be reviewed, diffed and mirrored by automation.

## Layout

Contributors draft a runbook on their own branch under
`runbooks/<service>/<slug>/`:

```
runbooks/<service>/<slug>/
  runbook.md       # front matter + the procedure itself
  oncall.md        # escalation path and rotation
  dashboards.md    # optional observability links
```

A release branch mirrors the runbooks that passed the quarterly certification
sweep into `runbooks/certified/<service>/<slug>/`.

## Contributing

1. Branch off `main` and name the branch `<team>/<author>/<slug>`.
2. Copy `templates/runbook.template.md` into your runbook directory.
3. Fill in every front-matter field and write the escalation notes.
4. Open a review request. Nothing lands on `main` until the certification
   sweep for the quarter is closed.

## Front matter

`service`, `title`, `owner`, `severity` and `last_reviewed` are mandatory. The
`owner` is the accountable person, not the team alias.
