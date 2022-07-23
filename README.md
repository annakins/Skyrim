# Mod Authoring
- Install [Animonculory Dev Tools](https://github.com/The-Animonculory/ADT/blob/main/README.md).
- Please read the guide in that link. When the installation is complete, let's proceed.

## Instructions
- Go to ADT/GameRoot/CreationKitCustom.ini.
- Find `sScriptSourceFolder` and ensure the value for that is `"Data\Scripts\Source"`.
- Go to your original Skyrim directory. 
- Copy the Papyrus Compiler folder.
- Go to ADT/GameRoot and paste it there.
- Within that folder, edit ScriptCompile.bat.
- Replace what's in there with: `cd %2 "%~dp0PapyrusCompiler" %1 -f="TESV_Papyrus_Flags.flg" -i="%~dp0..\Data\Scripts\Source" -o="%~dp0..\Data\Scripts" pause`.
- Go to your original Skyrim directory/Data.
- Copy Scripts.zip to the desktop (temporarily). Unpack/Extract there.
- Rename `Source` to `Scripts`. Open that folder you just renamed. Now name `Scripts` to `Source`. Go back to desktop.
- Zip `DialogueViews` and `Scripts` together and name that `CKScripts.zip`. 
- Open ADT's MO2.
- Install `CKScripts` as a mod, and place it before SKSE on the lefthand pane. Enable it.
- You can delete both the `DialogueViews` and `Scripts` folders on your desktop now.
- Download FaceFXwrapper https://www.nexusmods.com/skyrimspecialedition/mods/20061.
- Open the `FaceFXWrapper` folder. Drag `Tools` into `Game Root`.
- If Creation Kit's render window is flickering for you, downgrade your NVIDIA card to 512.77.
- Open Command Prompt in Administrator Mode. Enter this: `%windir%\System32\regsvr32.exe "D:\ADT\Game Root\flowchartx64.dll"`

## Scripting for Mod Authoring
### Visual Studio Code
- Download here: https://code.visualstudio.com/
- You can choose a different directory to install it in.
- Setup: Check all boxes under *Other:* in *Select Additional Tasks*. 
- Open VS Code. Go to File > Preferences > Extensions (CTRL+SHIFT+X).
- Look up `Papyrus` by Joel Day. Install.
- Look up `Workspace Explorer` by Tom Saunders. Install.
- Now, go to File > Preferences > Settings (CTRL+,).
- Look up `papyrus skyrim`. Scroll down to Special Edition's *Mod Directory Path*. Based on this guide, it's `X:\ADT\mods`. Add that path to the field.
- You will paste that line into another field. Now, look up `explorer` and scroll down to *Workspace Storage Directory*. Paste there. Saving is automatic.
- Close VS Code. We have to replace template files.
- Go to ``C:\Users\USERNAME\.vscode\extensions``. 
- Install the latest Pyro release. https://github.com/fireundubh/pyro/releases Not the Source code.
- Back to that .vscode\extensions folder, open `joelday.papyrus-lang-vscode-2.23.1` Open the *pyro* folder. Delete everything in there. Open the latest pyro release you just downloaded. Copy everything and paste them into your pyro folder.
- Now, go into ``C:\Users\Anna\.vscode\extensions\joelday.papyrus-lang-vscode-2.23.1\resources\sse``.
- Open `skyrimse.ppj` with VS Code. 
- If you see a message in a blue bar that mentions Restricted Mode, click *Manage*. Scroll down to *Trusted Folders & Workspaces*. Click *Add Folder*. You can just add the drive where all of your Skyrim + modding files are saved. If they're all in D: Drive, for example, you select that. And then press *Trust*.
- TIP: If your Visual Studio Code's text in the scripts don't have any color, that means your configurations mentioned here aren't set up correctly.
- Back to `skyrimse.ppj`: Delete all the text in that file.
- Copy the text in the wonderful mrowrpurr's ppj file: https://gist.githubusercontent.com/mrowrpurr/e164735e14ee6d07daf4f4217caf3714/raw/40a0684d55e139d4c1437b1a7e2ac0997bf36c0b/skyrimse.ppj
- Paste that into your `skyrimse.ppj`, you will need to change the directory under: `` <!-- <Import>@ModsFolder\SKSE64\Scripts\Source</Import> -->`` and SAVE. Mine says:
 ``<Import>D:\ADT\mods\CKScripts\Scripts\Source</Import>
 <Import>D:\ADT\mods\SKSE\Scripts\Source</Import>``
- Now, open `tasks.json` in that same folder.
- Delete all text again.
- Copy mrowrpurr's tasks.json: https://gist.githubusercontent.com/mrowrpurr/e164735e14ee6d07daf4f4217caf3714/raw/40a0684d55e139d4c1437b1a7e2ac0997bf36c0b/tasks.json
- Paste that text into your `tasks.json`, change the game path directory to reflect ADT's, and SAVE. For me, it's `"gamePath": "D:\\ADT\\Game Root\\",`.
- With VS Code open, click on what looks like a scroll on your VS Code toolbar: 
![Papyrus](https://cdn.discordapp.com/attachments/803257955029352518/931558126891720815/14598224c7cb9384de2fc3c9b1402908.png).
- Click on the three dots here: ![Papyrus](https://cdn.discordapp.com/attachments/803257955029352518/931558480328949760/62279b5a23636b5787500448e713ad1b.png).
- Select *Generate Skyrim Special Edition Project Files*.
- Go to the main directory of the mod you are working on. Ex: Mod123's folder, where you typically see *meshes, scripts, textures, seq* in mods. A workspace has now been created for you. You should see a notification in the lower-right, like this: 
  - ![img](https://imgur.com/MVj1sIk.png)
- To change which workspace you are in, press `CTRL+SHIFT+E` and if you look below, there's a *WORKSPACES* tab. You can move this tab to the top.

## Visual Studio Code Notes
- How to compile: Run > Build Task.
- When you want to pack your bsa (I have not done this yet), you WILL need to return to your mod's skyrimse.ppj to change some values. Thanks to mrowrpurr, they're pretty straightforward:" CHANGE THE MOD NAME HERE".

### Debugging for VS Code - WIP
- Go to MO2 > Tools > INI Editor. In skyrim.ini, look for *papyrus*. Change the settings to reflect the following:
 ``bEnableLogging = 1, bEnableTrace = 1, bLoadDebugInformation = 1`` and hit Save.
- Set up your debugging: when you have one of your mod's scripts open, click on ![Papyrus](https://cdn.discordapp.com/attachments/803257955029352518/931574029217828884/6b41099efb62089166a1ca330feea893.png). And then the play button ![Papyrus](https://cdn.discordapp.com/attachments/803257955029352518/931574329651654757/5abfe5c1dd4544dad433ba9ce44157cb.png). Select Install SKSE Plugin. Go to MO2, refresh, and enable Papyrus Debug Extension.
- When you test things in-game, it's SKSE you need to choose. 
- If you are in-game and want to see debug logs, you will need to press that play button. An indication of a successful connection looks like this: ![Papyrus](https://cdn.discordapp.com/attachments/803257955029352518/931575185218367588/38573e2b0313caf79bceae9a624252cd.png). If you don't see your debug console, hit View > Debug Console.


