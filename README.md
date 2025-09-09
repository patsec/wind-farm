# Wind Farm Controller

This repo contains the relevant Docker and [OT-sim](https://github.com/patsec/ot-sim) configuration files required to simulate a wind farm controller. The wind farm controller is configured to monitor and control up to 10 wind turbines deployed using the [wind turbine](https://github.com/patsec/wind-turbine) model.

## Getting Started

This project was designed to be deployed using [Development Containers](https://containers.dev), such as GitHub Codespaces or locally in VS Code directly. Codespaces (free) is the recommended deployment system and is documented here.

In addition, one or more [wind turbines](https://github.com/patsec/wind-turbine) will need to be deployed to make a deployment of this project interesting. To achieve this when using Codespaces, a [Tailscale](https://tailscale.com) mesh network can be used to add this wind farm controller and the wind turbine(s) to the same network no matter where in Codespaces they end up being deployed. A Tailscale account can be [created](https://login.tailscale.com/start) for free, and an [authentication key](https://login.tailscale.com/admin/settings/keys) can be generated for use by the OT-sim Tailscale module to add this wind farm controller and the wind turbine(s) to the Tailscale mesh network.

> [!IMPORTANT]
> Refer to the [wind turbine](https://github.com/patsec/wind-turbine) project README for additional details on configuring and deploying wind turbines using Codespaces and Tailscale for use with this wind farm controller.

Once an [authentication key](https://login.tailscale.com/admin/settings/keys) has been generated, you can configure Codepsaces to automatically use it with each deployment of this wind farm controller project by adding it as a [Codespace user secret](https://github.com/settings/codespaces) for your GitHub user. Note that the name of the secret must be `OTSIM_TAILSCALE_AUTHKEY`.

![](media/codespaces-secret.png)

After adding your Tailscale authentication key as a Codespaces user secret, click on the green `<> Code` button and then the `Codespaces` tab from the main GitHub page for this [repo](https://github.com/patsec/wind-farm). From there, click `Create codespace on main`, which will deploy a new codespace in the browser based on the `main` branch of this repo (this may take several minutes).

![](media/new-codespace.png)

Once the codespace is fully deployed, there should be one port automatically mapped in the browser instance of VS Code.

> [!TIP]
> If you click on the Docker extension that's added to the browser instance of VS Code, you'll also be able to see when the controller container has started.
>
> ![](media/container-list.png)

> [!NOTE]
> If the codespace takes more than a few minutes to come up, it may be that the codespace was deployed in a region other than `US East`, which is the only region the prebuild is available in. You can select the region to deploy the codespace to when you create a new codespace by clicking the `...` instead of `Create codespace on main` and then `+ New with options...`.
>
> ![](media/new-custom-codespace.png)
>
> Or... just [click here](https://github.com/codespaces/new?repo=770516031&ref=main&hide_repo_select=true).

> [!WARNING]
> In some cases, the port does not automatically get mapped. When this happens, the port needed for this model (`1880`) can be manually added via the `PORTS` tab.
>
> ![](media/manual-ports.gif)

## Interacting With the Model

Once the codespace is deployed, you can access the wind farm UI by navigating to the `PORTS` tab, hovering over the `Forwarded Address` for the `Farm HMI`, and clicking on the `Globe` icon. This will open up the UI in a different browser tab.

> [!IMPORTANT]
> When opening the `Farm HMI`, you will need to manually add the `/ui` path onto the end of the URL of the newly opened tab.

As wind turbine models get deployed on the same Tailscale mesh network, they will start to show up as connected in the Wind Farm UI.

> [!IMPORTANT]
> The wind farm controller is configured to communicate with wind turbines with specific DNS names (`wtg-1, wtg-2, ...`). The wind turbine project has separate codespace configurations that configure each turbine with the appropriate DNS name in Tailscale. Refer to the [wind turbine](https://github.com/patsec/wind-turbine) project README for additional details on deploying separate codespace configurations for use with this wind farm controller.
