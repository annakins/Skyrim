## Before you proceed
This guide is meant for existing actors that already have a FaceGen. It's also mostly for me so I can easily remember the next time I do this. :P

## Hair
- Let's use KS Hairs as an example. 
- Open up the KSHairdos.esp in Creation Kit just to see what hairline the hair you want used.
- Check the box for `Show only active (*) forms`. In the Filter field, look up the hair.
- Check the Extra Parts section to see if you need to change the scalp.
- Close Creation Kit.
- Copy the new hair files. 
  - KS Hairs folder > meshes > KS Hairdo's > Synthesis.nif, Synthesis.tri, SynthesisHl.nif.
  - KS Hairs folder > textures > KS Hairdo's > Synthesis.dds, Synthesis_n.dds
- Paste them into your mod's folder.
  - Follower folder > meshes > actors > character > Follower > hair
  - Follower folder > textures > actors > character > Follower > hair
- Open Creation Kit. Load your follower.esp.
- Go to the hair headpart. 
- Replace the .nif and .tri associated with that hair.
- Do the same for the hairline.
- Go to the TextureSet section.
- Change the .dds files associated with the hair (remember to include the `_n.dds` file also).
- Save your file and close the Creation Kit.
- Go to follower.esp > meshes > actors > character > FaceGenData > FaceGeom > follower.esp > XXXXXXX.NIF (Open NifSkope).
- Also open Synthesis.nif (whatever hair you chose) using NifSkope.
- Copy the BSDynamicTriShape in Synthesis.nif.
- Paste that into the FaceGen NIF's NiNode named BSFaceGenNiNodeSkinned.
- Paste again so there's two.
- Name one of them as the hair. The other is a hairline.
- Delete your original hair and hairlines trishapes. Make sure to use `Remove Branch`.
- For the hair: Click on BSDynamicTriShape > BSLightingShaderProperty > BSShaderTextureSet
  - Change the texture paths so they say `textures\actors\character\follower\hair\synthesis.dds` and `...synthesis_n.dds`.
  - Do this for the hairline as well.
- For the hair, click NiAlphaProperty and make sure the Flags say 4845. And the threshold should be 40.
- For the hairline, click on NiAlphaProperty also and now the Flags should say 4844. Threshold is 128.
