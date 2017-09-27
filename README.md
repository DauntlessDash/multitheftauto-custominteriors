# Multi Theft Auto Custom Interiors


## Synopsis

This project serves as a demonstration of the best method I have discovered for constructing custom interior spaces in servers for Multi Theft Auto. [Multi Theft Auto](http://www.multitheftauto.com/) (MTA) is a software project that adds network play functionality to Rockstar North's Grand Theft Auto game series, in which this functionality is not originally found. Custom interiors allow servers to turn buildings that cannot me entered in the exterior world of San Andreas into buildings that their players can go inside of and utilize. 

## Motivation

Because Multi Theft Auto is based on code injection and hooking techniques whereby the game is manipulated without altering any original files supplied with the game it is inefficient for servers to use custom models, and by extension custom interiors, in MTA. In order for servers to operate reliably custom levels must be created from existing models in the original game that have been manipulated in different ways. These limitations are not so restricting for most servers/gamemodes which only require the addition of small objects to the exterior world of San Andreas. However, some servers (mostly RPG game modes) also want additional custom interiors added to the game so that their players can enter into buildings. I have seen many different methods of constructing interiors for this purpose, but many implementations fail to operate correctly when put into high stress servers. I wanted to create a collection of custom interiors that could be used as a demonstration on how to properly implement custom interiors for servers of this type. However, in addition to their application as an example of methodology all maps contained in this library have also been used for their designed purpose within various servers across MTA.

## Installation

Each folder is its own custom interior and can be added to any server and not be dependent on one another. Some interiors are separated into several parts (in order to prevent lag) and are marked accordingly.

1. Add the desired interior directory into your server at the location MTA/server/mods/deathmatch/resources. 

2. Open the _interiorname_.map file within the interior's folder and change all dimension values to desired [dimension](https://wiki.multitheftauto.com/wiki/Dimension).

3. Start your server and run the resource from the resource manager.

4. Use the coordinates contained within the _interiorname_.map to teleport players to the location of the interior using your desired method.


## How These Interiors Prevent Falling and Trapped Player Errors

On high population servers when you enter a new interior it is loaded for you at that time, but players with slow internet connections can fall down before those objects have time to load and can become be trapped inside the void of the interior dimension. This was so prevalent that it was starting to become a major problem and many of our players were vocally complaining. To solve this issue I looked into how the original game handled their interiors. 

In MTA all objects are defined by a set of parameters which include a value called _interior world_. This value from 0-24 defines what world you are in, with 0 being the exterior world. Worlds 1-24 are empty voids that contained the interiors that came with the base game. However, after some experimenting I noticed that the collision files for all of the original GTA objects in their original placement transcended across all of the interior worlds. For example, if you were in the exterior world 0 and were teleported to those same coordinates in interior world 1 you wouldn't be able to see anything but you'd still be able to collide with the ground, road, and all other nearby static objects. However, the collision for objects added in custom maps do not transcend through all interior worlds. So how does this help prevent players from falling through not-yet-loaded objects? 

Say you make an interior in world 0, the exterior world, with the floor of the interior touching the ground and then change the _interior world_ value of all objects to 1. So now say a player doesn't load all the objects quickly enough: instead of falling down and past these objects the player will now just collide with the "ground" that is actually apart of interior world 0 despite the player being located in interior 1. The collision files for the exterior world are always loaded, when making maps you should utilize them to completely remove the possibility of any players falling through a map.  


## License

Feel free to use these interiors for any MTA server or gamemode.
