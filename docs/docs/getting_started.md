## Installing QM

The first step to getting started with QM is installation.

Fedora or CentOS:
On Fedora and CentOS-Stream systems (with EPEL repository enabled), QM can be directly installed via:

```bash
dnf install qm
```

### RPM Mirrors

Looking for a specific version of QM?
Search in the mirrors list below.

[CentOS Automotive SIG - qm package - noarch](https://mirror.stream.centos.org/SIGs/9-stream/automotive/aarch64/packages-main/Packages/q/)

## User Namespaces

QM runs without user namespaces by default. The `qm` RPM provides the `userns` tool, which provides support to enable or disable running QM with user namespaces.

```shell
# Configure QM to run with user namespaces (default values)
$ /usr/share/qm/userns enable

# ... or use a different UID/GID offset
$ /usr/share/qm/userns enable --id-offset 4000000000
```

After enabling it, make sure to reload the systemd units so the service is properly generated from the quadlet file and its drop-in configurations:

```shell
systemctl daemon-reload
systemctl restart qm
```

If everything went well, the `ps` output should now display QM processes with a `qm_` prefix, e.g. `qm_root` or `qm_dbus`.
