# The OriginalSoundTrack Plugin

This mod allows you to play Risk of Rain 1 (or any) music along side of the normal soundtrack.

You must supply your own music files though.

Place the DLLs and settings.xml in:
Risk of Rain 2\BepInEx\plugins\OriginalSoundTrack

Your music files can either go in the same directory or you can specifiy a directory
in settings.xml (using the `<music-path>` tag).

Music files can be in .mp3 or .wav format (with those exact extensions).

Make sure the filenames match what's in settings.xml (or edit settings.xml to match your files.)

If you delete settings.xml, don't match your filenames with `<song>` tags, or delete all `<song>` tags, then the
plugin will just choose random music it found, or, if the property `<pool>` is set, the plugin will include the normal
music from the game. There is a 66% chance for custom music to be played. 33% chance that normal music from the game will play.
I may add the ability to change these chances later and maybe even song probablilty. The former being more likely cause its easy.

## settings.xml

If your files match all the song "names", then you don't need to do anything else, but feel free to customize.

If the plugin fails to match a song for a scene, it will just choose a random one it found in the plugin directory or music from the game.

Put scene IDs in the "scenes" attribute to have audio play on that scene in settings.xml.
The scenes attribute is comma separated. A scene only has to be "contained" in the real scene ID for it to match:
("golemplains" in the scene attr will match for the golemplains2 scene id.)

Example for playing MyFile.mp3 on the title screen and main menus:
```
<song
    name="MyFile.mp3"
    scenes="title,lobby,logbook,crystalworld,eclipseworld"
    boss="false"
    volume="1"
/>
```

Setting boss to "true" means that music can only play when the player activates the teleport on a level (or on the final boss fight).
Otherwise music can only play elsewhere (non teleport events).
"volume" is a decimal between 0 and 1.

It's ok to have multiple `<song>` definitions with the same name or scenes. The plugin will choose a song randomly
among the matching songs.

The top level `<volume>` tag is the master volume for all this plugin's music. Again, a decimal between 0 and 1.

The top level `<loop>` tag determines if music should loop or pick another song (from matching songs) after a song ends.

The top level `<pool>` tag determines if music should be pooled with the game's own music

The top level `<music-path>` tag specifies where the plugin should scan for music. It does not traverse down directories.
The default path it scans for music is: `Risk of Rain 2\BepInEx\plugins\OriginalSoundTrack`

Currently there is a bug with playing music on the splash screen, if the song currently playing on the splash screen
is the same song chosen for the any following scene changes, like the menu, it will fail to play.

## Scene IDs (level IDs).

(As of the SoV update)

See here for pictures of the level scenes:
https://risk-of-thunder.github.io/R2Wiki/Mod-Creation/Developer-Reference/Scene-Names/#main-stages-stage
https://riskofrain2.fandom.com/wiki/Soundtrack#Integration
https://riskofrain2.fandom.com/wiki/Environments

```
Non Levels:
ID					Description
===============================================
splash              -   "hopoo games" image
intro               -   intro cutscene
outro               -   outro cutscene
title               -   the title screen
lobby               -   the select character screen.
logbook             -   view logs screen.
crystalworld        -   prismatic trials menu (not normally reachable in modded RoR2)
eclipseworld        -   eclipse menu
infinitetowerworld  - Simulacrum menu

Levels:
ID					Level Name / Description
===============================================

*First Stages**********************************
blackbeach		-	Distant Roost
blackbeach2		-	Distant Roost Variant
golemplains		-	Titanic Plains
golemplains2	        -	Titanic Plains Variant
snowyforest		-	Siphoned Forest

*Second Stages*********************************
foggyswamp		-	Wetland Aspect
goolake			-	Abandoned Aqueduct
ancientloft		-	Aphelian Sanctuary

*Third Stages**********************************
frozenwall		-	Rallypoint Delta
wispgraveyard   	-	Scorched Acres
sulfurpools		-	Sulfur Pools

*Fourth Stages*********************************
dampcavesimple  	-	Abyssal Depths
shipgraveyard   	-	Siren's Call
rootjungle		-	Sundered Grove

*Fith Stage************************************
skymeadow		-	Sky Meadow

*Finial Levels*********************************
moon			-	Commencement (Orginal Final Level(Accessible with Commands))
moon2                   -	Commencement (Revised Final Level(Currently Used))

*The Simulacrum********************************
itancientloft	        -	The Simulacrum Aphelian Sanctuary
itdampcave		-	The Simulacrum Abyssal Depths
itfrozenwall    	-	The Simulacrum Rallypoint Delta
itgolemplains   	-	The Simulacrum Titanic Plains
itgoolake		-	The Simulacrum Abandoned Aqueduct
itmoon			-	The Simulacrum Commencement
itskymeadow		-	The Simulacrum Sky Meadow

*Other*****************************************
voidstage		-	Void Locus
voidraid		-	Planetarium (Purple portal after void field event)
bazaar			-	Bazaar Between Time (The Shop)
artifactworld	        -   Bulwark's Ambry (Artifact Challenge arena where you unlock the artifacts with keys.)
arena			-   Void Fields (poison area with lots of "teleport" events.)
mysteryspace	        -   A Moment, Fractured (the place where you can obliterate yourself.)
limbo			-   A Moment, Whole (the mega scavenger boss)
goldshores		-   Glided Coast (the place where you fight Aurelionite(Gold Stone Titan))
***********************************************
```
## Other Info
Forked from https://github.com/davidstevenrose/RoR2-Original-Sound-Track
Which is a fork from https://github.com/kylepaulsen/RoR2-Original-Sound-Track

This plugin uses NAudio.dll https://github.com/naudio/NAudio to help load and play music at runtime.
This is done to make it very easy for players to supply their own music. The downside is that the normal in game
music isn't disabled (Maybe there is a way to do that, I dunno). To get around this, this plugin sets your in game
music volume setting to 0. It tries to set it back to where it was when the game closes but I'm not sure if this works.
Anyway you have been warned.

## Licence

When applicable, assume stuff is under the MIT licence ( https://opensource.org/licenses/MIT )
I am not liable for any damages and there is no warranty etc...
