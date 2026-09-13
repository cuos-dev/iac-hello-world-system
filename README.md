# CuOS Hello World

A complete CuOS system in two files. This is the
[Container Service](https://github.com/cuos-dev/cuos/blob/development/docs/development-guide.md#container-service)
level: CuOS IaC runs as the CuOS Init App and deploys what this repository
describes, so there is no image to build and no container to write.

| File | What it is |
|---|---|
| `system.json` | The system: images, network, access. Includes `cuos-release/release.json` for the pinned CuOS versions. |
| `docker-compose.yml` | The services. Here: a welcome page on port 80, plus the WebUI, the fleet agent and the dev container from `cuos-release`. |

**The repository is its own deployment source.** `iac_repo_url` in `system.json`
points back here, so the running system pulls its service definitions from the
same place its configuration came from. Push to the branch named in
`iac_repo_branch`, and the system follows.

## Build it

```sh
git clone --recurse-submodules https://github.com/cuos-dev/iac-hello-world-system.git
cd iac-hello-world-system
./cuos-release/tool.sh image system.json
```

`cuos-release` is a submodule of this repository — that is the recommended way
to consume it, so your system definition and the tooling that builds it are
versioned together.

The result lands in `output/`; `./cuos-release/tool.sh name system.json` prints
the file name. Writing it to a disk, wrapping it in an ISO installer or exporting
it as an LXC container is all in the
[cuos-release README](https://github.com/cuos-dev/cuos-release#readme).

## Make it yours

- Replace the `welcome` service in `docker-compose.yml`.
- Point `iac_repo_url` at your own fork, and `os_root_authorized_keys` at your
  own SSH key — the one committed here is the maintainer's.
- `os_ssh_server` and `dev-keys` are on for convenience. Turn them off for
  anything that is not a toy.

## Next

- [Development Guide](https://github.com/cuos-dev/cuos/blob/development/docs/development-guide.md)
  — the four levels, and when to leave this one
- [system.json reference](https://github.com/cuos-dev/cuos/blob/development/docs/common/system-json-reference.md)
