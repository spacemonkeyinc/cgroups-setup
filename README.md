cgroups-setup
=============

this package provides a cgroup-lite style package for cgroup configuration,
along with a utility for making cgroup configuration scripts.

in addition to the cgroup-mount and cgroup-umount commands, along with an init
script for mounting the cgroup hierarchy, this package provides
spacemonkey-cgroup-setup, which is ordinarily used like a script interpreter
itself.

for example, let's say you want to limit memory for a particular type of
process.

first you write a spacemonkey-cgroups-setup script (`example-cgroup-setup`)
like so:

```
#!/usr/bin/spacemonkey-cgroups-setup memory

echo 64M > memory.soft_limit_in_bytes
echo 96M > memory.limit_in_bytes
echo 128M > memory.memsw.limit_in_bytes
```

then, you run your script with the pid of the process you want to limit as its
first argument, like

```
example-cgroup-setup $DAEMON_PID
```

Often this last step is added to the start section of the init script of the
daemon process you want to manage.
