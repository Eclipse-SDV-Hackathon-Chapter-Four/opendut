![openDuT](assets/opendut-logo.png)

Eclipse openDuT enables testing ECUs without spanning wires between them. Connect them over the internet from across the country. Connect them into different testbenches at the click of a button. Or connect your virtual ECUs with real-world ECUs. OpenDuT allows you to test earlier and with more flexibility.

You can find the project documentation at: https://opendut.eclipse.dev/

At the Hackathon, you will be provided with an openDuT Backend instance and a few edge devices to hook up your network communication.

If you need help during the hackathon, use one of these channels:

- [SDV getting involved](https://eclipsesdv.org/get-involved/)
  - The link to join the SDV Slack workspace is on this page.
- [SDV Slack](https://sdvworkinggroup.slack.com/)
- OpenDuT Hack Coaches will provide hardware for your edge devices.

If you need help with OpenDuT specifically, mention `Reimar` in Slack.


## Add an edge device

1. Read the [setup documentation](https://opendut.eclipse.dev/book/user-manual/edgar/setup.html).
2. Download `opendut-edgar` from GitHub [here](https://github.com/eclipse-opendut/opendut/releases/tag/v0.10.2) or directly from the backend, as described in the documentation.
3. Create a `peer` for the edge device in our backend [OpenDuT-CARL](https://nc.opendut.net/peers).
4. Create a `SETUP_STRING` for your peer.
5. Set up your `opendut-edgar` instance. If you do not use CAN, you can skip the CAN setup:
```sh
opendut-edgar setup managed --skip-can <SETUP_STRING>
```

## Authentication

Access to the OpenDuT backend instance [OpenDuT-CARL](https://nc.opendut.net/peers) requires permissions.

### New opendut users

1. Log in once. New users will be greeted with this misleading error until access has been granted:
    ```
    We are sorry...
    Invalid username or password.
    ```
2. An administrator needs to assign the role `opendut-lea-client allowed-access`:
    1. Go to [User management](https://nc-auth.opendut.net/admin/master/console/#/opendut/users)
    2. Open **User details** → **Role mapping**
    3. Choose **Assign role** → **Filter by client roles** → assign `opendut-lea-client allowed-access`

