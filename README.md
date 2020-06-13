# Setup script for Redash with Docker on Ubuntu 18.04.

This is a reference setup for Redash on a single Ubuntu 18.04 server, which uses Docker and Docker Compose for deployment and management.

This is the same setup we use for our official images (for AWS & Google Cloud) and can be used as reference if you want to manually setup Redash in a different environment (different OS or different deployment location).

- `setup.sh` is the script that installs everything and creates the directories.
- `docker-compose.yml` is the Docker Compose setup we use.
- `packer.json` is Packer configuration we use to create the Cloud images.

## FAQ

### Can I use this in production?

For small scale deployments -- yes. But for larger deployments we recommend at least splitting the database (and probably Redis) into its own server (preferably a managed service like RDS) and setting up at least 2 servers for Redash for redundancy. You will also need to tweak the number of workers based on your usage patterns.

### How do I upgrade to newer versions of Redash?

See [Upgrade Guide](https://redash.io/help/open-source/admin-guide/how-to-upgrade).

### How do I use `setup.sh` on a different operating system?

You will need to update the `install_docker` function and maybe other functions as well.

# centos7 部署

首先 docker、docker-compose、git 要安装好

```bash
cd /srv/git
git clone https://github.com/steedos/setup --branch steedos
```

安装 pwgen：

```bash
wget https://sourceforge.net/projects/pwgen/files/pwgen/2.08/pwgen-2.08.tar.gz
tar zxvf pwgen-2.08.tar.gz
cd pwgen-2.08
./configure && make && make install
```

执行 setup.sh:

```bash
cd setup
chmod 755 setup.sh
./setup.sh
```

启动服务：

```bash
cd data
docker-compose up -d
```
