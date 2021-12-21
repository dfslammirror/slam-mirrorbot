```diff 
- [ DEAD REPO AND NO MORE UPDATE ]
```
[![SlamDevs](https://telegra.ph/file/143032e96542e7534f073.jpg)](https://t.me/SlamDevs)

# Slam Mirror Bot
![GitHub Repo stars](https://img.shields.io/github/stars/breakdowns/slam-mirrorbot?color=blue&style=flat)
![GitHub forks](https://img.shields.io/github/forks/breakdowns/slam-mirrorbot?color=green&style=flat)
![GitHub contributors](https://img.shields.io/github/contributors/breakdowns/slam-mirrorbot?style=flat)
![GitHub watchers](https://img.shields.io/github/watchers/breakdowns/slam-mirrorbot)
![Docker Pulls](https://img.shields.io/docker/pulls/breakdowns/mega-sdk-python?label=Docker%20Pull)

**Slam Mirror Bot** is a _multipurpose_ Telegram Bot written in Python for mirroring files on the Internet to our beloved Google Drive. Based on [python-aria-mirror-bot](https://github.com/lzzy12/python-aria-mirror-bot)

## Installing requirements

- Clone this repo:
```
git clone https://github.com/mrsammaus/slam-mirrorbot/
cd slam-mirrorbot
```

- Install requirements
For Debian based distros
```
sudo apt install python3
```
- Install dependencies for running setup scripts:
```
pip3 install -r requirements-cli.txt
```

## Getting Google OAuth API credential file
- Move that file to the root of mirrorbot, and rename it to **credentials.json**
- Finally, run the script to generate **token.pickle** file for Google Drive:
```
pip install google-api-python-client google-auth-httplib2 google-auth-oauthlib
python3 generate_drive_token.py
```

## Deploying on Heroku
- Deploying on Heroku with heroku-cli and Goorm IDE
<p><a href="https://telegra.ph/How-to-Deploy-a-Mirror-Bot-to-Heroku-with-CLI-05-06"> <img src="https://img.shields.io/badge/Deploy%20Guide-grey?style=for-the-badge&logo=telegraph" width="170""/></a></p>

# Using Service Accounts for uploading to avoid user rate limit
For Service Account to work, you must set `USE_SERVICE_ACCOUNTS` = "True" in config file or environment variables.
**NOTE**: Using Service Accounts is only recommended while uploading to a Team Drive.

## Generate Service Accounts. [What is Service Account](https://cloud.google.com/iam/docs/service-accounts)
Let us create only the Service Accounts that we need. 
- List your projects ids
```
python3 gen_sa_accounts.py --list-projects
```
- Enable services automatically by this command
```
python3 gen_sa_accounts.py --enable-services $PROJECTID
```
- Create Sevice Accounts to current project
```
python3 gen_sa_accounts.py --create-sas $PROJECTID
```
- Download Sevice Accounts as accounts folder
```
python3 gen_sa_accounts.py --download-keys $PROJECTID
```
If you want to add Service Accounts to Google Group, follow these steps

- Mount accounts folder
```
cd accounts
```
- Grab emails form all accounts to emails.txt file that would be created in accounts folder
```
grep -oPh '"client_email": "\K[^"]+' *.json > emails.txt
```
- Unmount acounts folder
```
cd -
```
Then add emails from emails.txt to Google Group, after that add Google Group to your Shared Drive and promote it to manager.

**NOTE**: If you have created SAs in past from this script, you can also just re download the keys by running:
```
python3 gen_sa_accounts.py --download-keys project_id
```

## Add all the Service Accounts to the Team Drive
- Run:
```
python3 add_to_team_drive.py -d SharedTeamDriveSrcID
```

# Credits

Thanks to:
- [`out386`](https://github.com/out386) heavily inspired from his Telegram Bot written in Typescript
- [`Izzy12`](https://github.com/lzzy12) for build up of this bot from scratch
- [`jaskaranSM`](https://github.com/jaskaranSM) for build up of this bot from scratch
- [`Dank-del`](https://github.com/Dank-del) for base repo
- [`magneto261290`](https://github.com/magneto261290) for some features
- [`SVR666`](https://github.com/SVR666) for some features & fixes
- [`breakdowns`](https://github.com/breakdowns) for slam-mirrorbot
- [`zevtyardt`](https://github.com/zevtyardt) for some direct links
- [`yash-dk`](https://github.com/yash-dk) for implementation of qBittorrent on Python
- [`xyou365`](https://github.com/xyou365) for Service Accounts script

And many more people who aren't mentioned here, but can be found in [Contributors](https://github.com/breakdowns/slam-mirrorbot/graphs/contributors).
