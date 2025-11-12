* Install Raspberry Pi OS
Run:
---
rpi-imager
---

from menu:
---
Raspberry Pi OS (other)
---

select:
---
Raspberry Pi OS Lite (64-bit) (trixie)
---

configure with the gear wheel:
---
- Set hostname: raspberrypi
- Enable SSH: Use password authentication
- Set userame and password:
  Username: witness
  Password: <your_password>
- Set locale settings:
  Timezone: Europe/Stockholm
  Keyboardlayout: se
- Disable telemetry
---

Write the sdcard.

When finished, run "sync" to make sure all data is flushed
before removing the sdcard.

* When booting the Raspberry Pi, put the cable for the display
  in the micro-HDMI connector most distant from the USB-C connector.

* Login locally and set IP address:
Run:
---
sudo nmtui
---

use:
---
ipv4 address: 192.168.146.98
ipv4 gateway: 192.168.146.1
ipv4 dns:     192.168.146.1
ipv6 disable
--

* Copy your ssh pub key to Raspberry Pi
Run:
---
ssh-copy-id witness@<IP>
---

* Run ansible

The ansible version used to deploy this configuration was "ansible [core 2.17.14]".

To provision a specific witness:
---
ansible-playbook -i hosts.ini -u witness site.yml -v --limit <witness_name_from_hosts.ini>
---
example:
---
ansible-playbook -i hosts.ini -u witness site.yml -v --limit test_witness_1
---
