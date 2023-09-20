# Simple Case Ansible #1(Personal Use)

Ansible offers open-source automation that is simple, flexible, and powerful.

## Installing Ansible

1. in terminal type install ansible, in here i am using homebrew on MacOS.
```
brew install ansible
```

2. after installing compleated check if ansible properly installed or not.
```
ansible --version
```

3. for me here the ansible.cfg is not created by default, so we need to create it.
```
sudo ansible-config init --disabled -f ini > ansible.cfg      
```

after this the ansible.cfg will be created, you can create it in whatever folder you want, as long as you run the command there. the path also will be saved automaticly in ansible path.
you can check it again and see with ansible --version.

4. now we going to make the inventory and playbook. the inventory is a plcae we used to store our devices and the playbook is a plcae we use to store our action/command, etc.
   you can use whatever text editor you desire.
5. below is the inventory "hosts_ios,yaml".

```
[routers]
router1 ansible_host=sandbox-iosxe-latest-1.cisco.com ansible_user=admin ansible_password=C1sco12345
router2 ansible_host=sandbox-iosxr-1.cisco.com ansible_user=admin ansible_password=C1sco12345

[routers:vars]
ansible_connection=network_cli
ansible_network_os=ios
ansible_port=22
```

5. now we create our playbook "show_ver_ios.yaml", i will execure command "show_version".
```
---
- name: Show Data
  hosts: routers
  gather_facts: no

  tasks:
  - name: GATHERING FACTS
    ios_facts:
      gather_subset: hardware

  - name: run show version
    ios_command:
      commands: show version
    register: show_version
  
  - name: display show run version
    debug:
      var: show_version
```

6. now we execure the ansible with command below in terminal, make sure your terminal is inside the ansible work folder.

```
ansible-playbook show_ver_ios.yaml -i hosts-ios
```
7. below is the result in terminal

```
PLAY [Show Data] ***********************************************************************************************************************************************************************************************

TASK [GATHERING FACTS] *****************************************************************************************************************************************************************************************
ok: [router1]
ok: [router2]

TASK [run show version] ****************************************************************************************************************************************************************************************
ok: [router2]
ok: [router1]

TASK [display show run version] ********************************************************************************************************************************************************************************
ok: [router2] => {
    "show_version": {
        "changed": false,
        "failed": false,
        "stdout": [
            "Fri Sep  1 05:47:05.459 UTC\nCisco IOS XR Software, Version 7.3.2\nCopyright (c) 2013-2021 by Cisco Systems, Inc.\n\nBuild Information:\n Built By     : ingunawa\n Built On     : Wed Oct 13 20:00:36 PDT 2021\n Built Host   : iox-ucs-017\n Workspace    : /auto/srcarchive17/prod/7.3.2/xrv9k/ws\n Version      : 7.3.2\n Location     : /opt/cisco/XR/packages/\n Label        : 7.3.2-0\n\ncisco IOS-XRv 9000 () processor\nSystem uptime is 1 week 1 day 8 hours 46 minutes"
        ],
        "stdout_lines": [
            [
                "Fri Sep  1 05:47:05.459 UTC",
                "Cisco IOS XR Software, Version 7.3.2",
                "Copyright (c) 2013-2021 by Cisco Systems, Inc.",
                "",
                "Build Information:",
                " Built By     : ingunawa",
                " Built On     : Wed Oct 13 20:00:36 PDT 2021",
                " Built Host   : iox-ucs-017",
                " Workspace    : /auto/srcarchive17/prod/7.3.2/xrv9k/ws",
                " Version      : 7.3.2",
                " Location     : /opt/cisco/XR/packages/",
                " Label        : 7.3.2-0",
                "",
                "cisco IOS-XRv 9000 () processor",
                "System uptime is 1 week 1 day 8 hours 46 minutes"
            ]
        ]
    }
}
ok: [router1] => {
    "show_version": {
        "changed": false,
        "failed": false,
        "stdout": [
            "Cisco IOS XE Software, Version 17.09.02a\nCisco IOS Software [Cupertino], Virtual XE Software (X86_64_LINUX_IOSD-UNIVERSALK9-M), Version 17.9.2a, RELEASE SOFTWARE (fc4)\nTechnical Support: http://www.cisco.com/techsupport\nCopyright (c) 1986-2022 by Cisco Systems, Inc.\nCompiled Wed 30-Nov-22 02:47 by mcpre\n\n\nCisco IOS-XE software, Copyright (c) 2005-2022 by cisco Systems, Inc.\nAll rights reserved.  Certain components of Cisco IOS-XE software are\nlicensed under the GNU General Public License (\"GPL\") Version 2.0.  The\nsoftware code licensed under GPL Version 2.0 is free software that comes\nwith ABSOLUTELY NO WARRANTY.  You can redistribute and/or modify such\nGPL code under the terms of GPL Version 2.0.  For more details, see the\ndocumentation or \"License Notice\" file accompanying the IOS-XE software,\nor the applicable URL provided on the flyer accompanying the IOS-XE\nsoftware.\n\n\nROM: IOS-XE ROMMON\nCat8000V uptime is 14 hours, 40 minutes\nUptime for this control processor is 14 hours, 41 minutes\nSystem returned to ROM by reload\nSystem image file is \"bootflash:packages.conf\"\nLast reload reason: reload\n\n\n\nThis product contains cryptographic features and is subject to United\nStates and local country laws governing import, export, transfer and\nuse. Delivery of Cisco cryptographic products does not imply\nthird-party authority to import, export, distribute or use encryption.\nImporters, exporters, distributors and users are responsible for\ncompliance with U.S. and local country laws. By using this product you\nagree to comply with applicable laws and regulations. If you are unable\nto comply with U.S. and local laws, return this product immediately.\n\nA summary of U.S. laws governing Cisco cryptographic products may be found at:\nhttp://www.cisco.com/wwl/export/crypto/tool/stqrg.html\n\nIf you require further assistance please contact us by sending email to\nexport@cisco.com.\n\nLicense Level: \nLicense Type: Perpetual\nNext reload license Level: \n\nAddon License Level: \nAddon License Type: Subscription\nNext reload addon license Level: \n\nThe current throughput level is 20000 kbps \n\n\nSmart Licensing Status: Smart Licensing Using Policy\n\ncisco C8000V (VXE) processor (revision VXE) with 1980715K/3075K bytes of memory.\nProcessor board ID 9UWS2FADP45\nRouter operating mode: Autonomous\n3 Gigabit Ethernet interfaces\n32768K bytes of non-volatile configuration memory.\n3965344K bytes of physical memory.\n5234688K bytes of virtual hard disk at bootflash:.\n\nConfiguration register is 0x2102"
        ],
        "stdout_lines": [
            [
                "Cisco IOS XE Software, Version 17.09.02a",
                "Cisco IOS Software [Cupertino], Virtual XE Software (X86_64_LINUX_IOSD-UNIVERSALK9-M), Version 17.9.2a, RELEASE SOFTWARE (fc4)",
                "Technical Support: http://www.cisco.com/techsupport",
                "Copyright (c) 1986-2022 by Cisco Systems, Inc.",
                "Compiled Wed 30-Nov-22 02:47 by mcpre",
                "",
                "",
                "Cisco IOS-XE software, Copyright (c) 2005-2022 by cisco Systems, Inc.",
                "All rights reserved.  Certain components of Cisco IOS-XE software are",
                "licensed under the GNU General Public License (\"GPL\") Version 2.0.  The",
                "software code licensed under GPL Version 2.0 is free software that comes",
                "with ABSOLUTELY NO WARRANTY.  You can redistribute and/or modify such",
                "GPL code under the terms of GPL Version 2.0.  For more details, see the",
                "documentation or \"License Notice\" file accompanying the IOS-XE software,",
                "or the applicable URL provided on the flyer accompanying the IOS-XE",
                "software.",
                "",
                "",
                "ROM: IOS-XE ROMMON",
                "Cat8000V uptime is 14 hours, 40 minutes",
                "Uptime for this control processor is 14 hours, 41 minutes",
                "System returned to ROM by reload",
                "System image file is \"bootflash:packages.conf\"",
                "Last reload reason: reload",
                "",
                "",
                "",
                "This product contains cryptographic features and is subject to United",
                "States and local country laws governing import, export, transfer and",
                "use. Delivery of Cisco cryptographic products does not imply",
                "third-party authority to import, export, distribute or use encryption.",
                "Importers, exporters, distributors and users are responsible for",
                "compliance with U.S. and local country laws. By using this product you",
                "agree to comply with applicable laws and regulations. If you are unable",
                "to comply with U.S. and local laws, return this product immediately.",
                "",
                "A summary of U.S. laws governing Cisco cryptographic products may be found at:",
                "http://www.cisco.com/wwl/export/crypto/tool/stqrg.html",
                "",
                "If you require further assistance please contact us by sending email to",
                "export@cisco.com.",
                "",
                "License Level: ",
                "License Type: Perpetual",
                "Next reload license Level: ",
                "",
                "Addon License Level: ",
                "Addon License Type: Subscription",
                "Next reload addon license Level: ",
                "",
                "The current throughput level is 20000 kbps ",
                "",
                "",
                "Smart Licensing Status: Smart Licensing Using Policy",
                "",
                "cisco C8000V (VXE) processor (revision VXE) with 1980715K/3075K bytes of memory.",
                "Processor board ID 9UWS2FADP45",
                "Router operating mode: Autonomous",
                "3 Gigabit Ethernet interfaces",
                "32768K bytes of non-volatile configuration memory.",
                "3965344K bytes of physical memory.",
                "5234688K bytes of virtual hard disk at bootflash:.",
                "",
                "Configuration register is 0x2102"
            ]
        ]
    }
}

PLAY RECAP *****************************************************************************************************************************************************************************************************
router1                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
router2                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```
