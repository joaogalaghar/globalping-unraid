# Globalping Probe for Unraid

A community-maintained Unraid Docker template for the official
[Globalping probe](https://github.com/jsdelivr/globalping-probe).

Host a probe on your Unraid server and contribute to a worldwide network for
ping, traceroute, MTR, DNS and HTTP measurements. Tests run from your Internet
connection using the official `globalping/globalping-probe` image.

This is an independent community integration, not an official Globalping or
Unraid project.

## Useful links

| Resource | Link |
| --- | --- |
| Globalping website | [globalping.io](https://globalping.io/) |
| Dashboard | [dash.globalping.io](https://dash.globalping.io/) |
| View, start or adopt probes | [Globalping Probes](https://dash.globalping.io/probes) |
| Official probe source | [jsdelivr/globalping-probe](https://github.com/jsdelivr/globalping-probe) |
| Official Docker image | [globalping/globalping-probe](https://hub.docker.com/r/globalping/globalping-probe) |
| Template support | [GitHub Issues](https://github.com/joaogalaghar/globalping-unraid/issues) |

## Configuration

| Setting | Default |
| --- | --- |
| Image | `globalping/globalping-probe:latest` |
| Container name | `globalping-probe` |
| Network | `host` |
| Logging driver | `local` |
| Restart policy | `always` |
| Privileged mode | Disabled |
| `GP_ADOPTION_TOKEN` | Optional; empty by default |
| WebUI | `https://dash.globalping.io/probes` |

No port mappings, port forwarding, appdata volume or Docker socket mount are
required for this deployment. The WebUI button opens the hosted Globalping
Probes page; the container does not provide a local web interface.

## Installation

### Community Applications

1. Open the **Apps** tab in the Unraid WebGUI.
2. Search for **Globalping**.
3. Select the Globalping probe application and click **Install**.
4. Optionally enter your **Adoption token** to associate the probe with your
   Globalping account. See the instructions below.
5. Keep **Network Type: Host** and **Privileged: Off**, then click **Apply**.
6. Enable **Auto-Start** on the Docker page if you want Unraid to start the
   container automatically.
7. Check the container logs as described in **Verify the installation** below.

Docker's `always` restart policy and Unraid's Auto-Start setting are separate:
`always` also restarts the container when the Docker daemon restarts.

## Associate the probe with your account

1. Sign in to the [Globalping dashboard](https://dash.globalping.io/).
2. Open [Probes](https://dash.globalping.io/probes).
3. Use **Start a probe** and follow the Docker setup instructions to obtain
   the adoption token shown as `GP_ADOPTION_TOKEN`.
4. Paste that value into the **Adoption token (optional)** field in the Unraid
   container configuration and click **Apply**.
5. Return to the Probes page and confirm that the probe appears in your account.

For a probe that is already running, the Probes page also provides an
**Adopt a probe** option. The container can run without an adoption token.

Keep your token out of public files. The input is masked in the Unraid form,
but the value is still stored in the local template and Docker environment.

## Verify the installation

1. Open the **Docker** tab in Unraid.
2. Click the **Globalping container icon** to open its menu.
3. Click **Logs**.
4. Check that the probe connects successfully and that no recurring connection
   errors appear.

If you entered an adoption token, also confirm that the probe is online on the
[Probes page](https://dash.globalping.io/probes).

## Existing probes

Globalping allows one probe per public IPv4 address or IPv6 `/64` prefix.
If you already run a probe on the same connection, preserve its token and
settings before replacing that installation. Avoid leaving both probes active.

See the [upstream hosting requirements](https://github.com/jsdelivr/globalping-probe#limitations)
for the full rules.

## Updates

Use Unraid's normal container update controls to refresh the Docker image.
The probe also updates its application code internally; this does not update
the underlying container image.

## Repository files

| File | Purpose |
| --- | --- |
| `templates/globalping-probe.xml` | Docker template and adoption token field |
| `templates/icon.png` | Globalping icon used by the Unraid template |
| `ca_profile.xml` | Community Applications repository profile |
| `README.md` | Installation and usage documentation |
| `LICENSE` | MIT license for this template repository |

## Support

- For template and Unraid installation issues, open an issue in
  [this repository](https://github.com/joaogalaghar/globalping-unraid/issues).
- For issues with the probe itself, use the
  [upstream Globalping issue tracker](https://github.com/jsdelivr/globalping-probe/issues).

When reporting a problem, include your Unraid version, the error message and
relevant logs, with tokens and other sensitive values removed.

## License

The files authored for this template repository are licensed under the
[MIT License](LICENSE). The upstream Docker image, Globalping software, name and
logo retain their respective terms. The icon in `templates/icon.png` is sourced
from the [official Globalping website](https://globalping.io/icons/android-chrome-512x512.png)
and is not covered by this repository's MIT license.
