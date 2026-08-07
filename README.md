# MDAnalysis Dashboard - Mini Workshop

Welcome to the [mdadash](https://github.com/MDAnalysis/mdadash) mini workshop.

## Setup instructions

### Docker (Recommended)

If you have [Docker](https://www.docker.com/) installed in your system:

```sh
docker run -it -p 8000:8000 ghcr.io/pardhavmaradani/mdadash-demo:latest
```

Access the dashboard locally at: http://localhost:8000

If local port `8000` is not available for any reason, you can change the port forwarding rule as `-p any_available_local_port:8000` in the command above (Eg: `-p 8001:8000`).

### GitHub Codespaces

You can create a GitHub codespace by clicking on the badge below:

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/PardhavMaradani/mdadash-demo)

Once the codespace is fully setup, it will automatically launch a preview browser window showing the dashboard in the editor area.

If the preview browser doesn't show up or if you closed it, you can click on the `PORTS` tab of the bottom panel and follow the link for the 'mdadash server port' to open the dashboard.
