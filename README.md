# Mod Authoring
## Prefer to watch?
- VIDEO TO BE PLACED HERE


## Prefer to read?


- Install [Animonculory Dev Tools](https://github.com/The-Animonculory/ADT/blob/main/README.md), which has pre-installation requirements.
- Please read the instructions completely, in that link. 
- If you are encountering issues (ex: installation failed), please join the [Animonculory Discord](https://discord.gg/DffHKcszfg).
- When the installation is complete, let's proceed below.


### Making the Game Root and Copying across the files

- Make a folder inside of your ADT folder, called **Game Root**.
- Open that folder and then open a new explorer window.
- Navigate to where your original Skyrim is installed. It is typically nested similar to `\steam\steamapps\common\Skyrim Special Edition`.
Select everything in the folder EXCEPT gpu.txt and copy it into the folder you just created. **DO NOT MOVE IT.**
![img](https://raw.githubusercontent.com/The-Animonculory/Modding-Resources/main/Images/Stock%20Game/CopyThis.webp)
- If you have Creation Club content, check this: [Stock Game guide - Cleaning up the CC content](https://github.com/The-Animonculory/Modding-Resources/blob/main/Stock%20Game%20Setup.md#cleaning-up-the-cc-content).
- Download **SKSE**. Get the one for whichever Skyrim version you have https://skse.silverlock.org/ and add to a folder you create (NOT in your ADT folder), perhaps call it **SkyrimFresh**. Extract it in there. 
- Drag the `skse dll, skse loader.exe` into the Game Root folder.
- Download **Skyrim Special Edition: Creation Kit** on Steam. 
- Open Creation Kit. Say NO to unpacking Scripts. Exit Creation Kit. 
- Run the **UCKP Patcher** tool in your `ADT > Tools > Creation Kit Patches` folder. Don't change anything, and just Extract.
- Copy everything in the Creation Kit Patches folder and paste the contents into your new `ADT > Game Root` folder.
- Go to your Skyrim directory/Data: `steam\steamapps\common\Skyrim Special Edition\Data`. Copy that **Scripts.zip** file. 
- Go to your **SkyrimFresh** folder. Paste and unpack **Scripts.zip** there. 
- Delete **Scripts.zip** in that **SkyrimFresh** folder.
- In the unpacked Scripts folder, you'll now see **DialogueViews** and **Source**.
- Rename ``Source`` to ``Scripts``. Open that folder. Rename ``Scripts`` to ``Source``. So it has to be `Scripts > Source`. *NOT Source > Scripts*.
- Go back to where you see **DialogueViews** and **Scripts**.
- Add both **DialogueViews** and **Scripts** into a .zip file. You can name it ``CKScripts.zip`` (or 7z). You can delete both the **DialogueViews** and **Scripts** folders after successfully placing them into a .zip file.
- Open Mod Organizer (MO2) in your ADT folder.
- Drag **CKScripts.zip** into your MO2 window, and place it before SKSE on the lefthand pane. **Enable it.**
- Create a separator and name it whatever you'd like. This is where you can place your created/edited mods. Order-wise, it should be fine to place it under the *Plugin Dev Libraries* separator.
- ![img](https://imgur.com/DJD2Bu1.png)
- ![img](https://imgur.com/Ufe8Uqq.png)
- In Mod Organizer, click on SKSE and press `<Edit...>`
- ![img](https://imgur.com/ceG5cO7.png)
- Scroll until you see Creation Kit.
- ![img](https://imgur.com/s619kip.png)
- In the** Binary** field, you'll want to select CreationKit.exe in your Game Root folder:
`ADT > Game Root > CreationKit.exe`
- In the **Start In** field, it should say: `ADT > Game Root`. 
- In the **Overwrite Steam AppID** field, enter `1946180`.
- ![img](https://imgur.com/Vou1sVI.png)
- Now scroll up back to see SKSE on the list. 
- ![img](https://imgur.com/TFmorzN.png)
- You will also need to switch the **Binary** and **Start In** fields, as shown above.
- Press OK.
- Look for the **SSE Engine Fixes (PreLoader)** folder (it came with ADT, in `ADT > mods`), go into **Root**, and then copy all 3 files. Paste that into your Game Root folder.
- Now, go into Mod Organizer's settings. Change the **Managed Game** to lead to  `Game Root > SkyrimSE.exe`.
- ![img](https://imgur.com/OVQOGNh.png)
- Again, in your ORIGINAL Skyrim directory, copy the **Papyrus Compiler** folder.
- Paste it into your new Game Root folder.
- In the newly copied Papyrus Compiler folder, edit **ScriptCompile.bat** (right-click > Edit)
- Replace what's in there with: `cd %2 "%~dp0PapyrusCompiler" %1 -f="TESV_Papyrus_Flags.flg" -i="%~dp0..\Data\Scripts\Source" -o="%~dp0..\Data\Scripts" pause`. Save.

## Scripting for Mod Authoring
### Visual Studio Code
- Download here: https://code.visualstudio.com/
- You can choose a different directory to install it in.
- Setup: Check all boxes under *Other*.
- Open VS Code. Go to File > Preferences > Extensions `CTRL+SHIFT+X`.
- Look up `Papyrus` by Joel Day. Install. **Switch to the pre-release version**.
- Look up `Workspace Explorer` by Tom Saunders. Install.
- Now, go to File > Preferences > Settings `CTRL+,`.
- Look up `papyrus skyrim`. Scroll down to Special Edition's *Mod Directory Path*. Add your `ADT > mods` path to the field. Do the same for the Install Path, but go to Game Root.
- ![img](https://imgur.com/CELVs0D.png)
- You will paste that line into another field. Now, look up `explorer` and scroll down to *Workspace Storage Directory*. Paste there. Saving is automatic.
- ![img](https://imgur.com/FOL0iN3.png)
- Now, look up `creation kit` in the settings. 
- Remove `CreationKitCustom.ini` and add `CreationKitPrefs.ini`.
- ![img](https://imgur.com/puZJfgt.png)
- Close VS Code. We have to replace template files.
- Go to ``C:\Users\USERNAME\.vscode\extensions``. 

<!-- HOLD ON 
- Install the latest Pyro release. https://github.com/fireundubh/pyro/releases Not the Source code.
- Back to that .vscode\extensions folder, open `joelday.papyrus-lang-vscode-VERSIONNUMBER` Open the *pyro* folder. Delete everything in there. Open the latest pyro release you just downloaded. Copy everything and paste them into your pyro folder.
-->

- Now, go into ``C:\Users\Anna\.vscode\extensions\joelday.papyrus-lang-vscode-VERSIONNUMBER\resources\sse``.
- Open `skyrimse.ppj` with VS Code. 
- If you see a message in a blue bar that mentions Restricted Mode, click *Manage*. Scroll down to *Trusted Folders & Workspaces*. Click *Add Folder*. You can just add the drive where all of your Skyrim + modding files are saved. If they're all in D: Drive, for example, you select that. And then press *Trust*.
- TIP: If your Visual Studio Code's text in the scripts don't have any color, that means your configurations mentioned here aren't set up correctly.
- Back to `skyrimse.ppj`: Delete all the text in that file.
- Copy the text in the wonderful mrowrpurr's ppj file: 
```
<?xml version='1.0'?>
<PapyrusProject xmlns="PapyrusProject.xsd" 
    Flags="TESV_Papyrus_Flags.flg" 
    Game="sse"
    Anonymize="true" 
    Output="Scripts" 
    Optimize="false" 
    Release="false" 
    Zip="false"
    Package="false"
    Final="false">
    <Variables>
        <!-- Set the name of your mod: -->
        <Variable Name="ModName" Value="CHANGE THE MOD NAME HERE" />
        <!-- The folder where you store all of your mods -->
        <Variable Name="ModsFolder" Value="C:\[YOUR MODS FOLDER]" />
    </Variables>
    <Imports>
        <!-- <Import>@ModsFolder\SKSE64\Scripts\Source</Import> -->
        <Import>C:\Program Files (x86)\Steam\steamapps\common\Skyrim Special Edition\Data\Scripts\Source</Import>
    </Imports>
    <Folders>
        <!-- Relative path to folder containing .psc Papyrus source code files for this project -->
        <Folder>./Scripts/Source</Folder>
    </Folders>
    <!-- The following section is for .bsa archives. You can enable it by setting Package="true" in the PapyrusProject -->
    <Packages Output=".">
        <Package Name="@ModName" RootDir=".">
            <Match In="Scripts">*.pex</Match>
            <!-- <Match In="interface\translations">*.txt</Match> -->
        </Package>
        <!-- If you have any texture files, uncomment the following to create a Textures .bsa archive with texture files -->
        <!-- <Package Name="@ModName - Textures" RootDir=".">
            <Include>*.dds</Include>
        </Package> -->
    </Packages>
    <!-- The following section is for .zip archive. You can enable it by setting Zip="true" in the PapyrusProject -->
    <ZipFiles Output="Build">
        <ZipFile Name="@ModName" RootDir="." Compression="deflate">
            <Include>@ModName.esp</Include>
            <Include NoRecurse="true">*.bsa</Include>
            <Match In="Scripts\Source">*.psc</Match>
        </ZipFile>
    </ZipFiles>
    <!-- This will remove any *.bsa files in this directory *after* the build, if there are any. Set UseInBuild="false" to disable. -->
    <PostBuildEvent Description="Post-Build Remove BSA Files" UseInBuild="true">
        <Command>del /s /q /f *.bsa</Command>
    </PostBuildEvent>
</PapyrusProject>
```
- Paste that into your `skyrimse.ppj`, you will need to change the directory under: `` <!-- <Import>@ModsFolder\SKSE64\Scripts\Source</Import> -->`` and SAVE. Mine says:
 ``<Import>D:\ADT\mods\CKScripts\Scripts\Source</Import>
 <Import>D:\ADT\mods\SKSE\Scripts\Source</Import>``
- Now, open `tasks.json` in that same folder.
- Delete all text again.
- Copy mrowrpurr's tasks.json: 
```
{
    "version": "2.0.0",
    "tasks": [
        {
            "type": "pyro",
            "projectFile": "skyrimse.ppj",
            "gamePath": "C:\\Program Files (x86)\\Steam\\steamapps\\common\\Skyrim Special Edition\\",
            "problemMatcher": [
                "$PapyrusCompiler"
            ],
            "label": "pyro: Compile Project (skyrimse.ppj)",
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
```
- Paste that text into your `tasks.json`, change the game path directory to reflect ADT's, and SAVE. For me, it's `"gamePath": "D:\\ADT\\Game Root\\",`.
- With VS Code open, click on what looks like a scroll on your VS Code toolbar: 
![Papyrus](https://cdn.discordapp.com/attachments/803257955029352518/931558126891720815/14598224c7cb9384de2fc3c9b1402908.png).
- Click on the three dots here: ![Papyrus](https://cdn.discordapp.com/attachments/803257955029352518/931558480328949760/62279b5a23636b5787500448e713ad1b.png).
- Select *Generate Skyrim Special Edition Project Files*.
- Go to the main directory of the mod you are working on. Ex: Mod123's folder, where you typically see *meshes, scripts, textures, seq* in mods. A workspace has now been created for you. You should see a notification in the lower-right, like this: 
  - ![img](https://imgur.com/MVj1sIk.png)
- To change which workspace you are in, press `CTRL+SHIFT+E` and if you look below, there's a *WORKSPACES* tab. You can move this tab to the top.

## Visual Studio Code Notes
- How to compile: `Terminal > Build Task`.
- When you want to pack your bsa (I have not done this yet, and I do not think I will), you WILL need to return to your mod's skyrimse.ppj to change some values. Thanks to mrowrpurr, they're pretty straightforward:" CHANGE THE MOD NAME HERE".

### Debugging in VS Code
- Go to `MO2 > INI Editor`. In skyrim.ini, look for *papyrus*. Change the settings to reflect the following:
 ``bEnableLogging = 1, bEnableTrace = 1, bLoadDebugInformation = 1`` and hit Save.
- Set up your debugging: when you have one of your mod's scripts open, click on ![Papyrus](https://cdn.discordapp.com/attachments/803257955029352518/931574029217828884/6b41099efb62089166a1ca330feea893.png). And then the play button ![Papyrus](https://cdn.discordapp.com/attachments/803257955029352518/931574329651654757/5abfe5c1dd4544dad433ba9ce44157cb.png). Select `Install SKSE Plugin`. Go to MO2, refresh, and enable `Papyrus Debug Extension`.
- When you test things in-game, it's SKSE you need to choose. 
- If you are in-game and want to see debug logs, you will need to press that play button. 
- An indication of a successful connection looks like this: ![Papyrus](https://cdn.discordapp.com/attachments/803257955029352518/931575185218367588/38573e2b0313caf79bceae9a624252cd.png). 
- If you don't see your real-time logs, hit `View > Debug Console`.


## Credits
- [Stock Game Info and ADT - The Animonculory](](https://github.com/The-Animonculory/))
- [Mrowrpurr](https://github.com/mrowrpurr)
