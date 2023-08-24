# This applies fixes I found to a GitHub repo for simplicity. I claim none of this code.
 **This is simply a bandaid fix of the main repo, it is not meant to be a replacement for it. I'm not a maintainer, I can barely code. This is just what I know some of it may be incorrect.**
 **Fixes applied [Restore Last Played date](https://github.com/FriendsOfGalaxy/galaxy-integration-psn/pull/39) using info from [this comment](https://github.com/FriendsOfGalaxy/galaxy-integration-psn/pull/39#issuecomment-1146746932) & [a switch from web-based OAuth to using NPSSO token](https://github.com/FriendsOfGalaxy/galaxy-integration-psn/issues/40#issuecomment-1251114176).**
 **These fixes aren't always guaranteed to work. Sony is basically constantly changing the PSN private internal API from which most things are reverse-engineered. Things may change.**

Supports PSN-owned game list & last played date. PSN API has changed several times over the last few years when this code was initially first created. [Several](https://github.com/andshrew/PlayStation-Trophies/blob/master/docs/APIv2.md) [trophy APIs](https://github.com/achievements-app/psn-api) have been created since then but they'd likely require nearly a full rewrite to be integrated into the GOG Galaxy integration.

## Authenticating with NPSSO token
1. Close GOG Galaxy 2.0 if it is opened.
2. Replace what is currently within your GOG PSN folder with the files in this repo. More specifically the `src` folder.
 Windows: `%localappdata%\GOG.com\Galaxy\plugins\installed`
 MacOS: `~/Library/Application Support/GOG.com/Galaxy/plugins/installed`
3. Sign in to a PlayStation site such as the [PlayStation home page](https://playstation.com) or the [PlayStation Store](https://store.playstation.com).
4. Go to [https://ca.account.sony.com/api/v1/ssocookie](https://ca.account.sony.com/api/v1/ssocookie) and copy the code contained within `{"npsso":"12345678901234567890"}`, so for an example `12345678901234567890`.
5. Open plugin.py with a code editor of your choice. I personally prefer [Visual Studio Code](https://code.visualstudio.com)
6. Go to line 43 and insert your token within `{"npsso":""`
7. Restart/reopen GOG Galaxy 2.0 and connect PSN again. It should automatically log into your PSN account via your NPSSO token.
8. Enjoy having PSN somewhat returned to GOG Galaxy 2.0.
**Note: NPSSO tokens do eventually expire, you will have to eventually repeat steps 4 to 7 again. Sadly no way around it.**

## GOG Integration Levels
Built-in Search: Yes, main repo only.
Install & Launch: No, may be able to be reverse-engineered eventually via Remote Play API.
Achievements: No, ever since the [discontinuation of My PlayStation](https://www.playstationlifestyle.net/2021/06/02/myplaystation-ps-vita-messaging-service-end/) back in 2021 achievements have been unsupported. Hopefully, they'll return one day.
Game Time: Yes, only time last played.
Friend Recommendation: No.
Friend Presence: No.

## Credits

I've based this partially on work done by others:
* https://github.com/jhewt/gumer-psn
* https://github.com/Tustin/psn-php
* https://github.com/mgp25/psn-api
* https://github.com/adrianzhang/wechat-psn-backend
