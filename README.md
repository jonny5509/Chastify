# Chastify for Home Assistant

A Home Assistant custom integration for the **Chastify Developer API**.

The integration connects Home Assistant to Chastify using a user-wide DEV API key and exposes session/lock information, sensors, controls, and API-backed services.

> **Important:** Chastify remains responsible for authentication, authorization, permissions, and server-side restrictions. This integration does not bypass those controls.

## ✨ Features

- 🏠 HACS-compatible Home Assistant custom integration
- ⚙️ Home Assistant Config Flow setup
- 🔑 User-wide Chastify DEV API key authentication
- ☁️ Cloud polling of the current Chastify session/lock
- 🔒 Lock title and timing information
- ⏱️ Locked time and maximum remaining time
- ⭐ Task points
- 🧊 Frozen status
- 🔓 Ready-to-unlock status
- 🤝 Trusted status
- 📋 Task-assigned status
- 🔄 Manual refresh control
- ➕ Add time
- ➖ Remove time
- ⏱️ Apply time
- 🧊 Freeze / unfreeze
- 📝 Custom lock-log entries
- 🧩 Generic Chastify action service
- 📱 Generic documented device-command service

## 📋 Requirements

- Home Assistant with support for custom integrations
- [HACS](https://hacs.xyz/) for the recommended installation method
- A Chastify account
- A Chastify **user-wide DEV API key**
- Network access from Home Assistant to the Chastify API

## 📦 Installation

### HACS

1. Open **HACS → Integrations**.
2. Search for **Chastify**.
3. Install the integration.
4. Restart Home Assistant.
5. Go to **Settings → Devices & services → Add Integration**.
6. Search for **Chastify** and complete setup.

If the repository is not listed in HACS, add this repository as a custom repository:

`https://github.com/jonny5509/Chastify`

### Manual installation

1. Clone or download this repository.
2. Copy `custom_components/chastify` into:
   `/config/custom_components/chastify`
3. Restart Home Assistant.
4. Add **Chastify** from **Settings → Devices & services**.

## 🔑 Authentication

Chastify uses a **user-wide DEV API key**.

Create the key in Chastify under:

**Developer API → User-wide DEV API keys**

The key is shown once, so store it securely.

Treat the API key like a password:

- Do not commit it to Git.
- Do not put it in public configuration files.
- Do not share it in screenshots, logs, issues, or support requests.

The integration sends the key to the Chastify API for authenticated requests.

## 🛠️ Services

| Service | Purpose |
| --- | --- |
| `chastify.action` | Send a general Chastify action |
| `chastify.apply_time` | Apply time through the lock API |
| `chastify.add_time` | Add time to the current lock |
| `chastify.remove_time` | Remove time from the current lock |
| `chastify.freeze` | Freeze the current lock |
| `chastify.unfreeze` | Unfreeze the current lock |
| `chastify.log_custom` | Create a custom lock-log entry |
| `chastify.device_command` | Send a documented Chastify device command |

The generic services are intentionally flexible so supported API functionality can be exposed without creating a dedicated Home Assistant service for every API operation.

Only use commands and parameters supported by the Chastify API.

## 🌐 API coverage

The integration uses the Chastify user-wide DEV token API:

`https://chastify.net/api/apps/v1/`

Current integration coverage includes:

- `GET /session`
- `POST /action`
- `POST /lock/apply-time`
- `POST /lock/freeze`
- `POST /lock/unfreeze`
- `POST /logs/custom`
- `POST /device-command`

API behaviour and permissions are controlled by Chastify. The integration cannot override authentication, authorization, or server-side restrictions.

## 📊 Entities

### Session and lock information

The integration exposes information such as:

- Lock title
- Remaining time
- Locked time
- Maximum remaining time
- Task points

### Binary sensors

- Frozen
- Ready to unlock
- Trusted
- Task assigned

A refresh control is also available for an immediate update.

Entity availability depends on the current Chastify session and the data returned by the API.

## 🧪 Troubleshooting

### Authentication fails

Check that:

1. The DEV API key is correct.
2. It is a **user-wide** DEV API key.
3. The key has not been revoked or replaced.
4. Home Assistant can reach the Chastify API.

### Entities are unavailable

Check the Home Assistant logs and confirm that Chastify is returning a valid session response. Some entities depend on information that is only available when a relevant session or lock exists.

### A generic API command fails

Verify the endpoint, HTTP method, command, and parameters against the Chastify API documentation. Generic services cannot make an unsupported Chastify command valid.

## 🔄 Updates

### HACS

Use the normal HACS update process, then restart Home Assistant.

### Manual

Replace the installed `custom_components/chastify` directory with the updated version and restart Home Assistant.

After an update, check **Settings → Devices & services → Chastify** and the Home Assistant logs if behaviour changes unexpectedly.

## 🧑‍💻 Development

The repository contains the Home Assistant custom integration under:

```text
custom_components/chastify/
```

GitHub Actions are included for HACS and Home Assistant Hassfest validation.

When developing changes:

1. Keep the integration domain as `chastify`.
2. Preserve Home Assistant Config Flow compatibility.
3. Never log API keys or other credentials.
4. Validate changes with GitHub Actions before release.

## 📁 Repository

Source code and issue tracking:

https://github.com/jonny5509/Chastify

## 📄 License

MIT License. See [LICENSE](LICENSE).
