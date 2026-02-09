# API Security

## Never Expose Secrets

- Do not echo API keys in logs.
- Use environment variables for credentials.

## Suggested Layout

- Store shared env vars in `$CODEX_HOME/.env` (or `~/.codex/.env` if unset).
- Use wrapper scripts in `$CODEX_HOME/scripts/` to load credentials and call APIs.

## Example Wrapper Invocation

```
$CODEX_HOME/scripts/secure-api.sh service list-items
```

## Checklist

- Credentials never printed
- Inputs validated before API calls
- Errors handled with clear messages
