# Quadlets

English | [Suomi](readme.fi.md)

![Quadlets](./docs/img/quadlets-building.webp)

Ready-made Quadlets for [Podman](https://podman.io/) and [PodShift](https://github.com/vellamo-dev/podshift).

A Quadlet is a small recipe file that describes an app, a volume, a network or an image. Quadlets are a [Podman feature](https://docs.podman.io/en/latest/markdown/podman-systemd.unit.5.html): Podman turns each file into a systemd service, so the app starts on boot, restarts when needed and is managed like any other service on the system.

## What is in this project

A collection of Quadlets you can download and use. Each one is a single file, or a folder of files when an app needs several parts, such as a web app with its own database.

- `catalog/apps/`: one folder per app with all its files and a short `readme.md`.
- `catalog/singles/`: standalone Quadlets, sorted by type (`container`, `volume`, `network`, `image`).

## Use with PodShift

1. Install [PodShift](https://github.com/vellamo-dev/podshift) on your server.
2. Install [PodShift UI](https://github.com/vellamo-dev/cockpit-podshift), the PodShift page for [Cockpit](https://cockpit-project.org/).
3. Download a Quadlet file, or the files of an app folder, from this project.
4. Open **PodShift** in Cockpit, go to the **Drop Quadlet** tab, and drop the file onto the page.

PodShift checks the file, installs it and starts the app. The **Drop History** and **Install log** on the same tab show how it goes.

PodShift UI accepts one file at a time, at most 50 KB: `.container`, `.volume`, `.network`, `.image` or `.zip`.

## Use with Podman

Quadlets without PodShift variables (see below) also work with Podman on its own. Place them in a Quadlet folder, such as `~/.config/containers/systemd/` for a user, and reload systemd. See the [Podman Quadlet documentation](https://docs.podman.io/en/latest/markdown/podman-systemd.unit.5.html) for details.

## PodShift variables

Some Quadlets here are made for PodShift. They use PodShift variables, whose names start with `TSV_`, for values that differ from server to server, such as the environment (`TSV_ENV`, for example `dev`, `staging` or `prd`) or the server's IP addresses (`TSV_NW1` to `TSV_NW8`). PodShift replaces them with the server's real values when it installs the Quadlet.

Plain Podman does not know these variables. Some of them can be given with an *environment file*, but Podman does not replace variables everywhere in a Quadlet, so using these Quadlets without PodShift is limited. See [PodShift's scope](https://github.com/vellamo-dev/podshift/blob/main/docs/scope.md) for the variables PodShift offers.

## Related projects

| Project | What it is |
|---|---|
| [Podman](https://podman.io/) | The container engine that runs Quadlets. |
| [PodShift](https://github.com/vellamo-dev/podshift) | Turns a small server into one that sets itself up, keeps itself secure, and updates your apps automatically. |
| [PodShift UI](https://github.com/vellamo-dev/cockpit-podshift) | The optional Cockpit page for PodShift, where you can see your server and install apps by dropping Quadlets. |

## Licence

AGPL-3.0-or-later; see `LICENSE`.
