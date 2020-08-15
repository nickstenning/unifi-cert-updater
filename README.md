# unifi-cert-updater

If you have a Unifi system, you may wish to provide it with TLS certificates
from an external source.

In my case, I have a [pfSense] router which uses the [ACME package] to manage
and automatically renew Let's Encrypt certificates for a variety of systems,
including my Unifi controller.

The scripts in this repository can be used to automate the process of updating
the certificates used by the Unifi controller when a new certificate is issued.

[pfSense]: https://www.pfsense.org/
[ACME package]: https://docs.netgate.com/pfsense/en/latest/certificates/acme-package.html

## How it works

1. Give the pfSense root user passwordless SSH access to the Unifi controller.
2. Put `update-cloudkey-cert` in `/root/bin` on the pfSense router with
   appropriate (executable) permissions.
3. Put `update-cert` in `/root/bin` on the Unifi Cloud Key.
4. Configure a post-update action on the pfSense router which calls
   `update-cloudkey-cert`:

   ![](img/cert-update-action.png)

5. You're done!

## License

Everything in this repository is shared without warranty under the terms of the
3-Clause BSD License, a copy of which is provided in `LICENSE`.
