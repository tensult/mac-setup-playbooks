# mac-setup-playbooks
Ansible playbooks for setting up mac

```git clone https://github.com/tensult/mac-setup-playbooks.git```

Copy the folder and paste it to the Desktop.

Open the terminal and type in the following commands:
1) $ cd mac-setup-playbooks
2) $ ./install.sh
Enter password when prompted.

The [shell script](https://github.com/tensult/mac-setup-playbooks/blob/master/install.sh) will install [Homebrew](https://brew.sh/), [Git](https://git-scm.com/), [Pip](https://pip.pypa.io/en/stable/), [Ansible](https://www.ansible.com/) and [AWS CLI](https://aws.amazon.com/cli/?sc_channel=PS&sc_campaign=acquisition_IN&sc_publisher=google&sc_medium=command_line_b&sc_content=aws_cli_e&sc_detail=aws%20cli&sc_category=command_line&sc_segment=159807028003&sc_matchtype=e&sc_country=IN&s_kwcid=AL!4422!3!159807028003!e!!g!!aws%20cli&ef_id=WsIXuQAAAaLautiZ:20180419092918:s) with it's commands. Then it'll run the ansible playbook called [mainplaybook](https://github.com/tensult/mac-setup-playbooks/blob/master/mainplaybook.yml) which will install [Firefox](https://github.com/tensult/mac-setup-playbooks/blob/master/playbooks/firefox.yml), [Google Chrome](https://github.com/tensult/mac-setup-playbooks/blob/master/playbooks/google_chrome.yml), [Postman](https://github.com/tensult/mac-setup-playbooks/blob/master/playbooks/postman.yml), [Slack](https://github.com/tensult/mac-setup-playbooks/blob/master/playbooks/slack.yml) and [Visual Code Studio](https://github.com/tensult/mac-setup-playbooks/blob/master/playbooks/visual_studio_code.yml). The playbook will download the application installer from the website and depending on the type of file it will carry out the required installation steps.

You can reconfigure the code to install other apps based on your needs by editing the following:-

1) Go the playbooks folder. Create a new YAML file with the following details
```
---
- hosts: local
  become: yes
  vars:
    app_name: <Enter app nam here>
    app_url: <Enter app download URL here>
    installer_type: app
    install_method: 
    download_file_type: 
  roles:
    - setup
    - installer
    - cleanup
```
Depending on the type of file being downloaded enter the download_file_type as "app", "dmg" or "zip"
Depening on the file obtained after unzipping, enter the install_method as "dmg", "app" or "pkg".

2) Save the YAML file and insert the following line into the [mainplaybook](https://github.com/tensult/mac-setup-playbooks/blob/master/mainplaybook.yml) YAML file

```- import_playbook : playbooks/<app-playbook>.yml```

3) Run the [install shell script](https://github.com/tensult/mac-setup-playbooks/blob/master/install.sh) in the terminal to run the ansible code.

$ ./install.sh