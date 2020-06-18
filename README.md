# drone-rsync
[![drone-rsync on Docker Hub](https://img.shields.io/docker/automated/drillster/drone-rsync.svg)](https://hub.docker.com/r/drillster/drone-rsync/)

This is a pure Bash [Drone](https://github.com/drone/drone) >= 0.5 plugin to sync files to remote hosts.

For more information on how to use the plugin, please take a look at the docs:

- For Drone CI versions `< 1` : https://github.com/Drillster/drone-rsync/blob/master/0-DOCS.md
- For Drone CI versions `>= 1` : https://github.com/Drillster/drone-rsync/blob/master/1-DOCS.md

## Docker
Build the docker image by running:

```bash
docker build --rm=true -t drillster/drone-rsync .
```
#默认运行参数不是-a 而是-rtvz,前者是保留源文件权限，后者是保留目标文件权限（发布时比较实用）
## Usage
Execute from the working directory (assuming you have an SSH server running on 127.0.0.1:22):

```bash
docker run --rm \
  -e PLUGIN_KEY=$(private-key) \
  -e PLUGIN_HOSTS="127.0.0.1, 127.0.0.2, 127.0.0.3" \
  -e PLUGIN_PORTS="22, 23, 24" \
  -e PLUGIN_TARGET="./" \
  -e PLUGIN_PRESCRIPT="echo \"Prescript Done!\"" \
  -e PLUGIN_SCRIPT="echo \"Postscript Done!\"" \
  -e PLUGIN_ARGS="--blocking-io" \
  -v $(pwd):$(pwd) \
  -w $(pwd) \
  drillster/drone-rsync
```
