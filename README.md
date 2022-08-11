# OpenVPN Server in docker

This is based on the [kylemanna docker image][1] and the related
[Digital Ocean Tutorial][2]. EASYRSA documentation can be foud [here][3]

## Use

To run the ovpn server just launch the `server` service. It will automatically
setup `easyrsa` and `openvpn server` on the first run. Server can be configured
via environment variables. See the related section in this document.

To generate the configuration file for a new client you have to launch the
`gen_client` service specifying the client name using the `CLIENT_NAME` env
var (e.g.: `docker-compose run -e CLIENT_NAME=my-new-client gen_client`). This
will create the OVPN configuration file to send to the new client; thus
the best way to use it is this:

> env CLIENT_NAME=my-new-client docker-compose --profile=client run --rm gen_client

## Configuration

The following configuration is available via environment variable

| ENVIRONMENT VARIABLE | DESCRIPTION                             | DEFAULT              |
|----------------------|-----------------------------------------|----------------------|
| PUBLIC_DNS           | Public DNS name of openvpn server       | NODEFAULT+MANDATORY  |
| PUBLIC_PORT          | Public UDP port of the listening server | 1194                 |
| REQ_CN               | Common Name for the CA cert req         | "Default OpenVPN CA" |

[1]: https://hub.docker.com/r/kylemanna/openvpn/
[2]: https://www.digitalocean.com/community/tutorials/how-to-run-openvpn-in-a-docker-container-on-ubuntu-14-04
[3]: https://easy-rsa.readthedocs.io/en/latest/advanced/
