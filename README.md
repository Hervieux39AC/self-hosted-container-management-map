# Self-Hosted Container Management Map

> **Decision:** Choose how much state the control plane should own: container inspection, Compose files, multi-host deployment, an app-store appliance, a PaaS, or Kubernetes management.

**For:** Home-lab and small-team operators who have outgrown raw Compose commands.  

This is a non-commercial, source-traceable decision guide. It normalizes upstream declarations; it does not claim that repository reachability proves functionality, security, maintenance, or fitness.

**Start here:** [Download the runtime and escape-hatch matrix](assets/container-control-plane-map.csv) — twelve projects, located upstream evidence, and explicit unknowns.

## Choose by workload


- Inspect/manage containers and endpoints: Portainer CE, after separating CE from Business features.
- Keep Compose files central: Dockge.
- Home-server app catalogue: Yacht, Runtipi, or CasaOS, each with different host and app-store assumptions.
- Git-to-app PaaS: CapRover, Coolify, Dokku, or Dokploy.
- Multi-server automation: Komodo; Kubernetes fleet management: Rancher.

## Choose the smallest control plane

Docker-socket authority can be root-equivalent. Export files and identify volumes before making the dashboard the only deployment record.

## Control-plane ownership map


- **Container and Compose control** — Portainer, Dockge, and Yacht operate close to existing Docker/Compose state; compare file ownership and socket privileges.
- **Home-server platforms** — Cosmos, Runtipi, and CasaOS add app catalogues, routing, or host services; back up the platform state and the applications separately.
- **Application PaaS** — CapRover, Coolify, Dokku, and Dokploy own builds, deployments, domains, and sometimes databases; exportability matters.
- **Fleet control** — Komodo orchestrates builds/deployments across servers; Rancher manages Kubernetes clusters and is not a Docker-Compose dashboard.


## Runtime and escape-hatch matrix

| Project | Role | Runtime and host reach | Deployment source of truth | Persistent state and privilege |
|---|---|---|---|---|
| Portainer | container dashboard | Portainer Community Edition is a free, lightweight container management UI for Docker, Swarm, Podman, Kubernetes, and ACI environments. It is provided as-is, at… | Portainer Business Edition builds on the same open-source base and adds the features, hardening, and commercial support that production and enterprise environme… | Unknown in the frozen upstream README |
| Dockge | Compose manager | A fancy, easy-to-use and reactive self-hosted docker compose.yaml stack-oriented manager. | A fancy, easy-to-use and reactive self-hosted docker compose.yaml stack-oriented manager. | Unknown in the frozen upstream README |
| Yacht | home-lab container UI | - direct Docker API hosts added manually in the UI - agent-managed hosts where a yacht-agent container connects back to the main Yacht server | Yacht is a container management UI with a focus on templates and 1-click deployments. | - mounts the local Docker socket |
| Komodo | multi-server deployment control plane | A tool to build and deploy software across many servers. | A tool to build and deploy software across many servers. | Unknown in the frozen upstream README |
| Cosmos | home-server platform | No vendor-locking: Unlike solution that tightly couple their applications to the containers, Cosmos can manage apps created from anywhere all the same, and conv… | App Store 📦📱 To easily install and manage your applications, with simple installers, automatic updates and security checks. This works alongside manual installa… | Unknown in the frozen upstream README |
| CapRover | application PaaS | ✔ Docker Swarm under the hood for containerization and clustering | Easiest app/database deployment platform and webserver package for your NodeJS, Python, PHP, Ruby, Go applications. | Easiest app/database deployment platform and webserver package for your NodeJS, Python, PHP, Ruby, Go applications. |
| Coolify | application PaaS | Coolify is an open-source, self-hostable platform for deploying any application, database, or service on your own servers. It is an alternative to Heroku, Netli… | Coolify is an open-source, self-hostable platform for deploying any application, database, or service on your own servers. It is an alternative to Heroku, Netli… | Coolify is an open-source, self-hostable platform for deploying any application, database, or service on your own servers. It is an alternative to Heroku, Netli… |
| Dokku | Git-push PaaS | Docker-powered single-host PaaS | Mini-Heroku/PaaS deployment model | Unknown in the frozen upstream README |
| Rancher | Kubernetes management platform | Container management platform; Kubernetes operations | Kubernetes fleet, not a Compose editor | Please see Installation Requirements for hardware and software requirements. |
| Runtipi | home-server app platform | Runtipi is a personal homeserver orchestrator that makes it easy to manage and run multiple services on a single server. It is based on Docker and comes with a … | Runtipi is a personal homeserver orchestrator that makes it easy to manage and run multiple services on a single server. It is based on Docker and comes with a … | Unknown in the frozen upstream README |
| CasaOS | home-cloud dashboard | - Easily install numerous Docker apps | - Over 100,000 apps from the Docker ecosystem can be easily installed | - The cost of computing power and storage was decreasing fast. |
| Dokploy | application PaaS | - Docker Compose: Native support for Docker Compose to manage complex applications. - Multi Node: Scale applications to multiple nodes using Docker Swarm to man… | Dokploy is a free, self-hostable Platform as a Service (PaaS) that simplifies the deployment and management of applications and databases. | Dokploy is a free, self-hostable Platform as a Service (PaaS) that simplifies the deployment and management of applications and databases. |

Values are short excerpts from the frozen upstream README, not feature-test scores. The CSV retains the located evidence for each cell. “Unknown” means the retrieved document did not establish that axis; it is not a claim that the feature is absent.

## Assemble the minimal stack


Export one stack, stop the control plane, and prove you can still identify images, environment, volumes, networks, domains, and secrets. Treat Docker socket access as root-equivalent. Back up platform database/config plus application volumes, and test restoring them in the correct order.


## Adoption notes by project

### Portainer

- **Choose it for:** Teams wanting a broad management UI.
- **License at the frozen source:** [zlib for CE; separate commercial Business Edition](https://raw.githubusercontent.com/portainer/portainer/08a5576af343fe330ae57f9a9d16b5085df37097/LICENSE).
- **Adoption test:** Upstream separates Community Edition from Business features such as advanced RBAC/support; verify exact CE needs and back up platform state.
- **Source:** [portainer/portainer](https://github.com/portainer/portainer).

### Dockge

- **Choose it for:** Operators who want Compose files to remain visible and portable.
- **License at the frozen source:** [MIT](https://raw.githubusercontent.com/louislam/dockge/0329dabb5003f206d4fd9f7403a6af26d7138497/LICENSE).
- **Adoption test:** Test file ownership, compose-version compatibility, socket permissions, and recovery without Dockge.
- **Source:** [louislam/dockge](https://github.com/louislam/dockge).

### Yacht

- **Choose it for:** Home labs wanting templates and lightweight host management.
- **License at the frozen source:** [GPL-3.0](https://raw.githubusercontent.com/Yacht-sh/Yacht/dd5058baa0e7f9e77ae1c24b68b4b13411cac14e/LICENSE).
- **Adoption test:** Use the maintained Yacht-sh canonical repository, not the old SelfhostedPro fork; Linux is verified upstream and other platforms remain evaluation work.
- **Source:** [Yacht-sh/Yacht](https://github.com/Yacht-sh/Yacht).

### Komodo

- **Choose it for:** Small teams operating several application hosts.
- **License at the frozen source:** [GPL-3.0](https://raw.githubusercontent.com/moghtech/komodo/780ac68b992094a9fccd5fffb760e0c84fd3c3d1/LICENSE).
- **Adoption test:** Canonical repository moved from mbecker20/komodo to moghtech/komodo; test agent trust, backups, and rollback outside the demo.
- **Source:** [moghtech/komodo](https://github.com/moghtech/komodo).

### Cosmos

- **Choose it for:** Home labs wanting one integrated control surface.
- **License at the frozen source:** [Apache-2.0 with Commons Clause 1.0; not plain OSI-open-source licensing](https://raw.githubusercontent.com/azukaar/Cosmos-Server/fa0a6523888d05c2b62540777aa29b0e875f1940/LICENCE).
- **Adoption test:** Apache-2.0 plus Commons Clause is source-available/restricted, not unqualified OSI open source; broad gateway scope increases blast radius.
- **Source:** [azukaar/Cosmos-Server](https://github.com/azukaar/Cosmos-Server).

### CapRover

- **Choose it for:** Heroku-like application deployment on owned servers.
- **License at the frozen source:** [Apache-2.0](https://raw.githubusercontent.com/caprover/caprover/309b588425128f1d0d105373c3f90979a26bae5e/LICENSE).
- **Adoption test:** Document Swarm dependency, build/image path, domain/TLS state, app definitions, and volume restore before adoption.
- **Source:** [caprover/caprover](https://github.com/caprover/caprover).

### Coolify

- **Choose it for:** Teams wanting a broad self-hosted application platform.
- **License at the frozen source:** [Apache-2.0](https://raw.githubusercontent.com/coollabsio/coolify/91b7e3e509dee1eb5cee7c41fe151be03b03092e/LICENSE).
- **Adoption test:** Inventory all managed secrets, proxies, databases, and volumes; test export and rollback rather than assuming Git alone recreates state.
- **Source:** [coollabsio/coolify](https://github.com/coollabsio/coolify).

### Dokku

- **Choose it for:** Operators wanting a small Heroku-style host.
- **License at the frozen source:** [MIT](https://raw.githubusercontent.com/dokku/dokku/a0de8c22b4f75d54ddb587f65f6d9ccf456ebcc8/LICENSE).
- **Adoption test:** Plugin compatibility and host state are part of backup; test app export, proxy/TLS, storage, and rollback.
- **Source:** [dokku/dokku](https://github.com/dokku/dokku).

### Rancher

- **Choose it for:** Organizations managing Kubernetes rather than Compose.
- **License at the frozen source:** [Apache-2.0](https://raw.githubusercontent.com/rancher/rancher/531c5f6744731c4a279374ac00a8c442a8c40fdb/LICENSE).
- **Adoption test:** It is not a Docker UI substitute; use a supported stable release and scope cluster credentials, backups, upgrades, and downstream failure.
- **Source:** [rancher/rancher](https://github.com/rancher/rancher).

### Runtipi

- **Choose it for:** Home users prioritizing a guided app catalogue.
- **License at the frozen source:** [GPL-3.0](https://raw.githubusercontent.com/runtipi/runtipi/881559aebc745eb61cb2e35e7b351ddac25caa7e/LICENSE).
- **Adoption test:** Upstream says volunteer support/security are not guaranteed and active development may contain bugs; avoid prerelease builds for critical data.
- **Source:** [runtipi/runtipi](https://github.com/runtipi/runtipi).

### CasaOS

- **Choose it for:** Beginners wanting an approachable home-server surface.
- **License at the frozen source:** [Apache-2.0](https://raw.githubusercontent.com/IceWhaleTech/CasaOS/e099dd6b4982a264663df2536a55bfea2ae5448a/LICENSE).
- **Adoption test:** Confirm which component owns apps, files, users, and upgrades; back up application data outside the dashboard database.
- **Source:** [IceWhaleTech/CasaOS](https://github.com/IceWhaleTech/CasaOS).

### Dokploy

- **Choose it for:** Small teams wanting a modern self-hosted PaaS.
- **License at the frozen source:** [Apache-2.0 outside /proprietary; that directory, if present, uses LICENSE_PROPRIETARY](https://raw.githubusercontent.com/Dokploy/dokploy/3b13bcde8dca8b4ec0e4d48445b2aa1b0c183449/LICENSE.MD).
- **Adoption test:** Select a documented stable release instead of assuming canary stability. Apache terms exclude /proprietary if present; check LICENSE_PROPRIETARY and rehearse volume/proxy recovery.
- **Source:** [Dokploy/dokploy](https://github.com/Dokploy/dokploy).

## Recover without the dashboard

1. Export images, Compose/app definitions, environment and volume ownership.
2. Record which service holds socket, host-root and remote-agent credentials.
3. Stop the control plane and recover one app from raw files and volume data.
4. Restore platform config/database before reconnecting managed hosts.

## What this guide covers

Deployment control-plane ownership, not a code forge or a Kubernetes security benchmark.

## Located sources and update policy

[`sources.json`](sources.json) binds each cited declaration to a commit, document, exact line range and local snapshot hash. [`assets/projects.json`](assets/projects.json) holds the normalized roles and decision axes. Current HEAD reachability is recorded separately; it is not a maintenance or security assessment. Licensing is version- and directory-specific. Re-read the selected release before adoption.

Run the local evidence and package checks, then opt into public-source reachability:

```bash
python3 scripts/verify_sources.py
python3 scripts/verify_sources.py --online
```

These checks validate source binding, excerpts, hashes, language, the decision asset and nonempty public content. They do not certify feature behavior, migration success or restore success. No popularity score, paid placement or affiliate ranking is used. Restricted-license and historical examples are explicit contrasts, not silently recommended open-source defaults.
