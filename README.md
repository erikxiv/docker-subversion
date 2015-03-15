## subversion

A basic configuration of a subversion server with support for data
volumes.

This image will initialize a basic configuration of subversion.

You can configure the following by providing environment variables
to `docker run`:

- `SVN_REPONAME` sets the initial repository name. (e.g. if you provide `repos`
  here, you can access the initial repo at svn://<host>/repos)

For example, to start a container running svn,
with data stored in `/data/svn` on the host, use the following:

    docker run -v /data/svn:/var/svn \
               -e SVN_REPONAME=repos \
               -d erikxiv/subversion

You can find out which port the LDAP server is bound to on the host by running
`docker ps` (or `docker port <container_id> 3690`). You could then verify svn connectivity so:

    svn info svn://localhost:<host_port>/repos

**NB**: Please be aware that by default docker will make the svn port
accessible from anywhere if the host firewall is unconfigured.