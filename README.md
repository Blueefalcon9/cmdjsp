# cmdjsp

![Java](https://img.shields.io/badge/jsp-reference-blue)
![License](https://img.shields.io/badge/license-MIT-green)

A minimal JSP command-execution webshell, kept as a **detection test artifact**.

## What this is for

This file exists to be *detected*, not deployed. It is a known-signature sample for validating that defensive
tooling actually fires:

- WAF and IDS/IPS rule testing
- Antivirus / EDR signature verification on a web server
- File integrity monitoring and webshell-scanner coverage checks
- Blue-team training and detection-engineering exercises

It is a widely published PoC pattern, not original work, and is reproduced here for that purpose.

## What it does

26 lines: renders a form, takes the `cmd` GET parameter, passes it to `Runtime.getRuntime().exec()` via
`cmd.exe /C`, and prints stdout to the page.

```java
Process p = Runtime.getRuntime().exec("cmd.exe /C " + cmd);
```

Unauthenticated remote command execution as the servlet container's user. Windows-only as written, because of
the hardcoded `cmd.exe`.

## Do not deploy this

There is no authentication, no authorization, no input validation, and no logging. Anyone who can reach the
URL gets a shell. If you place this on a host:

- Use an isolated lab with no route to production or the internet
- Remove it when you are finished — do not leave it on a system after a test
- Never place it on a client system outside an explicitly authorized engagement with a defined removal step

Dropping a webshell on a system you do not own is unauthorized access and a crime in most jurisdictions.
Leaving one behind after an authorized engagement is a serious scope and professional-conduct failure.

## License

MIT — see [LICENSE](LICENSE).
