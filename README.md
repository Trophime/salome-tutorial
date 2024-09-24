# A Salome tutorial

## Installation

The easiest way to install Salome is to retrieve the archive tarball from [Salome web site](https://www.salome-platform.org/).
Select the appropriate tarball for your OS.

To install Salome:

* unarchive the tarball in `/opt/SALOME`
* `cd /opt/SALOME`
* run `install_bin.sh`

To list the registered configs:

```bash
source sat/complete_sat.sh
sat config --list
```

To check your installation for a given config, eg. `SALOME-9.13.0-native`:

```bash
sat config SALOME-9.13.0-native --check_system
```

To run Salome testsuite:

```bash
[mesa_]salome test`
```

### Vscode devcontainer

You can use the attached devcontainer

### Docker

```bash
xhost +local:root
docker run [-runtime=nvidia --gpus all -e NVIDIA_DRIVER_CAPABILITIES=all] -it --rm  --name salome -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix trophime/salome:9.13.0-bookworm
```

### Singularity

```bash
singularity build docker://trophime/salome:9.13.0-bookworm salome-9.13.sif
singularity exec [--nv] salome-9.13.sif salome
```


## References

* [Salome web site](https://www.salome-platform.org/)
* [Main documentation](https://docs.salome-platform.org/latest/main/index.html)

Some courses and tutorials:

* [Tutorials](https://www.youtube.com/playlist?list=PLgvBxFyGVRbZZz4wVvP36xXQL-S81RZsc)
* [Salome Channel](https://www.youtube.com/channel/UCm7CSP3v1VF6brzmTlV9c3Q)
