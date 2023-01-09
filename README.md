# **IKEA Lillabo- & BRIO- & others- compatible train tracks generator**

![Train tracks loops](img/train_tracks_lib_example_loops_600px.jpg?raw=true)

# Summary

Read this summary till the end before you print any part generated by this generator!

This library can be used in two ways:
- just download, slice and 3D print provided STL files,
- generate your own models using provided OpenSCAD file (src/train_tracks_generator.scad), you can easily modify properties of your models as well as change common dimensions used by the generator (track width, height, plug & nest radius etc.).

The library can so far be used to generate the following types of train tracks:
- short, low profile test track,
- straight tracks,
- arcs (track curves),
- bridges,
- switches,
- intersections,
- "snake" tracks,
- dog-bones (nest-to-nest connection),
- adapters between various train track systems (e.g., IKEA<>BRIO).

Dimensions of the inter-connectors (plugs & nests) are defined based on my own measurements and experiments. They are chosen in a way that connecting a wooden track with a 3D printed one creates a connection which is a little bit tighter than a standard wood-to-wood connection is. Connecting two 3D-printed parts should give a snug and sturdy connection (maintaining a minimal play to ease disconnecting). A play between the parts (wooden vs 3D printed) could be reduced even more but then connecting two 3D-printed parts together would not be possible anymore. Keep it in mind if you decide to play with the configuration parameters.

**Are various train track systems compatible with each other?**

It depends on how much force you are willing to apply :) In general, the answer is: NOT, the most popular systems are incompatible. For instance, tracks from IKEA and BRIO do not fit to each other well. The general dimensions of the parts are similar but - for instance - fitting IKEA track plug (shorter) to BRIO track nest (longer) may be impossible without braking or damaging one of the parts. Even if you will manage to connect two incompatible parts, it may be very difficult to disconnect them.
There may be of course exceptions. I found out that J'adore system (sourced from Rossmann) is pretty compatible with BRIO.

Do you posses two or more various systems and want to connect them? With use of my generator, you can easily generate an adapter which will allow to connect two different systems together.

**IMPORTANT - my strong advice - print the tester at first!**

Before printing any "bigger" part generated by this generator, I highly recommend to print a tester-track relevant to the system you use:

- file "train_tracks_ikea_tester.stl" (for IKEA Lillabo),
- file "train_tracks_brio_tester.stl" (for BRIO).

This is a short, 20mm-long, low-profile railway track which takes maximum a dozen minutes to print and requires only ~2g of filament. Test the printed part with your train tracks system. It will help to you asses if the dimensions of the parts (including track plug and nest) used by the generator fit dimensions of the tracks you own. If you posses genuine IKEA Lillabo or/and BRIO railway system/s, the generator default dimensions should be fine, nevertheless, when reading various comments for the similar projects on Internet, I found out that in some countries, dimensions of the tracks may differ a little bit from the commonly known. Default dimensions used in this library are tested on tracks available from IKEA (sourced from Germany & Poland), BRIO and J'adore (Rossmann). Please let me know about your test results in the comments and I will add more information to this description if necessary.  

Printed tester does not fit?
I tested multiple combinations of inter-connectors dimensions, so you should not experience any issues but if you do, do not worry, you can easily experiment and customize dimensions used by the generator to fit your system.

![Plug & nest tests](img/plug_nest_tests_600px.jpg?raw=true)

This is what I call a nest and a plug:

![Plug & nest](img/nest_plug_600px.png?raw=true)

If you want to change dimensions of a plug or a nest, locate these variables in the library and modify according to your needs (example values below are relevant for IKEA Lillabo):


	// Track Plug
	track_plug_radius = 6.25;
	track_plug_radius_ext = 6.5; // for a dog-bone with a springy plug
	track_plug_neck_width = 6.1;
	track_plug_neck_length = 11;
	
	// Track Nest
	track_nest_radius = 6.4;
	rack_nest_neck_width = 6.3;
	track_nest_neck_length = 11;

![Plug dimensions](img/plug_dims_600px.jpg?raw=true)

# "We want a bridge!" -> module generate_bridge(); 

This is actually how this story began. We had some IKEA Lillabo and J'adore wooden railway tracks at home but these were only basic parts which were useful for building nothing more than two traditional "2D" loops. One day I heard "We want a bridge!". IKEA is maybe not far away from us but when we want to go there, it's already a kind of trip to organize. And the "bridges" offer is not too impressive in IKEA, and our 3D printer stands in the next room, and there was willingness to improve OpenSCAD skills, so...the project was born.

![Example bridge](img/bridge_example_600px.jpg?raw=true)

To build a full bridge, you will need minimum five parts: two "ground" and two "slope" parts,  plus so called a "dog-bone" when you are going to use straight connecting tracks in plug-nest configuration. The ground and slope parts have to be connected by a straight track of your choice. I highly recommend to use one of the standard straight tracks from an original IKEA Lillabo main or expansion set. I think it makes no sense really to print the simplest, commonly available parts.
You can easily extend the total length of the bridge by adding one or more "pillar" track parts.

OpenSCAD module to build a bridge is called "**generate_bridge();**" It takes a few parameters but the most important one is called *what_to_generate". It controls what the module generates. These are the possible values:
- 0 - generates a bridge overview and calculates what will be the height of the bridge,
- 1 - generates only a "ground" part,
- 2 - generates only a "slope" part,
- 3 - generates only a "pillar" part.

This is an example of a bridge overview:

![Example bridge overview](img/bridge_example_desc_600px.png?raw=true)

You can generate a bridge without providing any further parameters. In such a case default values will be used:

	**module generate_bridge**(what_to_generate = 0,
	bridge_angle = 14,
	slope_radius = 100',
	straight_part_l = 205,
	pillar_l = 50,
	cutout = true);

The picture below explains the bridge module parameters:

![Bridge parameters](img/bridge_example_params_600px.png?raw=true)

![Bridge part cutout description](img/bridge_example_cutout_desc_500px.png?raw=true)

To speed up printing of the bridge parts and to reduce amount of filament which has to be used for supports, I recommend to slice the parts in the following position (laying on a sidewall):

![Bridge parts - how to print](img/bridge_parts_how_to_print_540px.jpg?raw=true)


# Straight railway track -> module track();

Straight railway track is the simplest to generate. Just use **track();** module. You will find explanation of the available parameters on the pictures below:

![Straight railway track - Example 1](img/straight_20mm_desc_600px.png?raw=true)
![Straight railway track - Example 2](img/straight_100mm_desc_600px.png?raw=true)


# Arcs -> module track_arc(); 

![Arcs examples](img/arcs_switch_dogbone_examples_600px.jpg?raw=true)

To generate an arc, use **track_arc()** module. You can define an ark angle, radius and configuration of its endings (plugs/nests). Positive angles will cause generating an arc which turns to the left and negative angles will force generation of an arc turning right. In addition, you can control if a part will be generated with a material-saving **cutout** or without it. Parameter **both_sides** allows to control if the part will have groves on both sides or only on the top side. This is important if you want to keep the part the most universal (flip it up -side-down and it will turn to the opposite side). 

![Arc description](img/arcs_desc_600px.png?raw=true)

# Intersections -> module intersection(); 

![Intersection description](img/intersection_desc_600px.png?raw=true)

# Switches -> module switch();

![Switch description](img/switch_desc_600px.png?raw=true)

# "Snake" track -> module snake_track();

![Snake track description 1](img/snake_desc1_600px.png?raw=true)
![Snake track description 2](img/snake_desc2_600px.png?raw=true)

# Dog-bone -> module track_dogbone(); 

A dog-bone is a part generated using additional parameter called **track_plug_radius_ext**. It should be always set to a little larger value than standard plug radius. When connecting two track parts facing each other with nests, you are interested in reducing lateral play. This is exactly why the dog-bone has slightly oversized "heads". Deep cutouts allow such plugs to be flexible and tightly fit to slightly "undersized" for them nests.

![Dog-bone](img/example_dogbone.png?raw=true)

# Adapters -> module tracks_adapter();

As mentioned in the summary above, some systems are just incompatible with each other (like IKEA and BRIO). This does not mean that you cannot use them together. I guess this incompatibility is just a standard method of locking us - customers - to a specific system. You can easily escape this game played by train tracks manufacturers by using dedicated adapters. Adaptation takes place only in the plug/nest areas (body of a whole adapter is always "common").

Generating an adapter is as easy as calling **tracks_adapter();** module with appropriate parameters (default values in the brackets):

	tracks_adapter(length = 30, nest = "B", plug = "I");

- length - total adapter length (without a plug), I recommend 30mm minimum,
- nest - here you have to define what is the "nest" system,
- plug - here you have to define what is the "plug" system.

So far, dimensions for two plug/nest systems are defined:
- IKEA Lillabo represented by the letter "I",
- BRIO represented by the letter "B".

Below you can find two examples of parts generated to connect IKEA and BRIO systems:

![Adapters description](img/train_tracks_adapter_ikea_brio_desc_600px.png?raw=true)
![Example adapters](img/train_tracks_adapters_brio_ikea_examples_600px.jpg?raw=true)

---
Shield: [![CC BY-NC-SA 4.0][cc-by-nc-sa-shield]][cc-by-nc-sa]

This work is licensed under a
[Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License][cc-by-nc-sa].

[![CC BY-NC-SA 4.0][cc-by-nc-sa-image]][cc-by-nc-sa]

[cc-by-nc-sa]: http://creativecommons.org/licenses/by-nc-sa/4.0/
[cc-by-nc-sa-image]: https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png
[cc-by-nc-sa-shield]: https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg
