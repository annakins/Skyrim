# Streaming Wabbajack Lists (Skyrim) onto Steam Deck with Sunshine and Moonlight
- Download Sunshine (.exe) on your PC: https://github.com/LizardByte/Sunshine/releases
- You may get a warning when you install (`Windows protected your PC`). Run anyway as it isn't malicious. Go with default settings, but the installation location can be different.
- Open Sunshine. You will be prompted again (`Your connection isn't private`), but continue anyway.
- Create an account.
- On your Steam Deck, switch to desktop mode.
- Open Discover.
- Search Moonlight and install.
- Open Steam.
- Add a Non-Steam game, look for Moonlight, and add that.
- Switch to gaming mode. 
- Check the Non-Steam tab and launch Moonlight.
- Select your gaming PC, which will bring up a prompt of a PIN.
- On your PC, on Sunshine, go to the PIN tab and enter it there.
- On your Steam Deck, change the resolution to Native (1280x800).
- Under Host Settings, check the box for **Quit app on host PC after ending stream**.
- If needed, change the bitrate. Mine is currently set to 11 Mbps.
- I do not have V-sync and frame pacing on.
- My GUI display mode is set to Windowed, but up to you to see what works for you.
- Download Resolution Change on your PC: https://github.com/designer-living/sunshine_utils/releases - You do not have to run this.
- Move it to a folder that's easy for you to find, ex: `D:\ChangeScreenResolution`.
- On your PC, on Sunshine, go to Applications.
- Add a new application, call it Wabbajack or whatever you want.
- In Do Command, enter the following: `D:\ChangeScreenResolution\resolution_change.exe -p 800p`.
- In Undo Command: `D:\ChangeScreenResolution\resolution_change.exe -r`.
- All this does is make sure that when you exit Moonlight on your Steam Deck, your original resolution is restored. **Save**.
- On the modlist of your choice, change the resolution. For Lorerim, head to the INI editor. In skyrimprefs.ini, look up size, and switch the height to 800 and width to 1280. Save.

![Lorerim](https://imgur.com/7GgysM6.png)
- You're all set. You should be able to run the modlist of your choice on your Steam Deck now.
