## ENB Tips
*Feel free to make suggestions or contribute.*

### Quick Notes
- Not everything here will apply to your ENB, but hey, just trying to help. ;)
- First off, to tweak your ENB settings in-game, the key(s) to open up the UI will vary per ENB. By default, it's `SHIFT + ENTER`. If you've tried several combinations and still haven't opened up the UI, look for your enblocal.ini and edit what it says in KeyEditor. To check values, go here: https://css-tricks.com/snippets/javascript/javascript-keycodes/#aa-tester-tool
<img src="https://imgur.com/eRVASB5.png" width=50%></img>
- Also, please calibrate your monitor. http://www.lagom.nl/lcd-test/

### Tweaks

#### Why does hair look funny? 
- Try to turn off/tweak `DetailedShadow` and `WETSURFACES`. Look for `ReflectionAmount` in `WETSURFACES`, if you decide not to turn it off.

![image](https://user-images.githubusercontent.com/92814468/167032260-00ce0b1b-ff71-445b-865d-14a4f84bf73e.png)

#### Why does the water look green?
- Change the brightness. Or your water mod.
#### So much water reflection. Doesn't matter what I do.
- There are mods like this, to help: https://www.nexusmods.com/skyrimspecialedition/mods/64736
- Really depends on what mods you have. There are other brightness and reflection fixes. 
- Also tweak the `WATER` section, evidently.

#### My candles look like they're vanilla candles. The "twinkle" look is there.
- Edit your `LIGHTSPRITE` settings.

#### Why is there a gigantic glow around candles and things like nirnroots?
- Edit your `LIGHTSPRITE` settings.

#### How do I disable/adjust Depth of Field and Film Grain?
- 
#### Which settings are relevant to adjust to help darken/lighten lights?
- Torches, lanterns: Go to `ENVIRONMENT` and tweak `PointLighting` (Intensity, Curve).

#### How can one tweak the brightness?
- So many ways. I personally tweak what's in `ENBEFFECT` and `ENBEFFECTPOSTPASS` first, before anything else. These sections vary so much per ENB, but you have your usual clues, like Brightness, Gamma correction, and you might as well modify Saturation and Contrast if they look incorrect. "Correct" values are typically 1 or 0. Additionally, many ENBs also come with Fake HDR. 
#### How can I improve performance?
- Uncheck `EnableLens`.
- Uncheck `Bloom`.
- Uncheck `DepthofField`.
- Uncheck `ComplexFireLights` and `ComplexFireLights` OR
  - Uncheck `EnableBigRange`. in these two settings.
 - 

#### Why is skin so saturated?
- Tweak `SUBSURFACESCATTERING`.

#### Fog coming from windows looks weird.
- First, you might have some sort of mod conflict. If not the case, try tweaking the `PARTICLE` section.

#### Why does hair look weird/yellow/glowy/orange in different angles?
- Disable or tweak `CLOUDSHADOWS`.

#### What's affecting skin + environment glossiness?
- Tweak `WETSURFACES`. 

#### How do I get that foggy look? But not in the mountains.
- Tweak `GAMEVOLUMETRICRAYS`.
