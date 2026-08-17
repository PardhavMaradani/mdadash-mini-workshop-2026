# MDAnalysis Dashboard - Mini Workshop

Welcome to the [mdadash](https://github.com/MDAnalysis/mdadash) mini workshop.

## Setup instructions

### Docker (Recommended)

If you have [Docker](https://www.docker.com/) installed in your system:

```sh
docker pull ghcr.io/pardhavmaradani/mdadash-demo:latest
docker run -it -p 8000:8000 ghcr.io/pardhavmaradani/mdadash-demo:latest
```

Access the dashboard locally at: http://localhost:8000

> Note: If local port `8000` is not available for any reason, you can change the port forwarding rule as `-p any_available_local_port:8000` in the command above (Eg: `-p 8001:8000`).

### GitHub Codespaces

You can create a GitHub codespace by clicking on the badge below (Use **Ctrl / Cmd + Click** to open in new tab. A `4-core` 'Machine type' is recommended):

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/PardhavMaradani/mdadash-mini-workshop-2026)

Once the codespace is fully setup, it will automatically launch a preview browser window showing the dashboard in the editor area.

> Note: If the preview browser doesn't show up or if you closed it, you can click on the `PORTS` tab of the bottom panel and follow the link for the 'mdadash server port' to open the dashboard.

You can stop / delete the Codespace after use in either of the following ways:
- Click the "Code" button in this repo, switch to the "Codespaces" tab and select the codespace to stop / delete
- Go to your [GitHub Codspaces](https://github.com/codespaces) and select the codespace to stop / delete

## Demo setup

The above docker image and Codespace contain the following demo setup:

- GROMACS Simulation
  - System: Lysozyme in water
  - Atoms: 30,423 | Waters: 9,467 | Ions: 62
  - IMDv3 streaming enabled on port 8889
  - IMD params:
    ```
    IMD-group       = System
    IMD-version     = 3
    IMD-nst         = 10
    IMD-time      	= Yes
    IMD-coords		= Yes
    IMD-vels		= Yes
    IMD-forces		= Yes
    IMD-box			= Yes
    IMD-unwrap		= Yes
    IMD-energies	= Yes
    ```
- [mdadash](https://github.com/MDAnalysis/mdadash) trajectory input pointing to above live simulation
  - `--trajectory imd://localhost:8889`
