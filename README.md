# Fix Antigravity Region Error on Windows (V2RayN)

Fix `User location is not supported for the API use` without tunneling all system traffic through a VPN.

## 1. Find your local proxy port

In V2RayN, find the local HTTP/mixed proxy port. This guide uses `10809`.

## 2. Set proxy environment variables

Open PowerShell and run:

```powershell
[Environment]::SetEnvironmentVariable("HTTP_PROXY", "http://127.0.0.1:10809", "User")
[Environment]::SetEnvironmentVariable("HTTPS_PROXY", "http://127.0.0.1:10809", "User")
[Environment]::SetEnvironmentVariable("http_proxy", "http://127.0.0.1:10809", "User")
[Environment]::SetEnvironmentVariable("https_proxy", "http://127.0.0.1:10809", "User")
```

Replace `10809` if your local proxy uses a different port.

## 3. Restart Antigravity

Fully close Antigravity and reopen it. If the variables are not picked up, sign out of Windows and sign back in.

## How it works

Antigravity's `language_server.exe` may bypass the proxy configured for the main application. These environment variables tell applications that support them to send HTTP and HTTPS requests through V2RayN's local proxy.

Only applications that use these variables are affected. **You do not need to tunnel all system traffic.**

<p align="center">
  <img src="https://github.com/user-attachments/assets/3a062e95-fbdb-41b8-afcf-e9d1660268ef" width="900" alt="Antigravity working through V2RayN proxy">
</p>

## Notes

- V2RayN must be running.
- The selected V2RayN route determines the proxy's exit IP.
- These variables apply to other applications that honor them, not just Antigravity.
- This fix was tested with Windows 11, Antigravity 2.25.0, and V2RayN using port `10809`.
