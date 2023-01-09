## Summary

##### **IKEA Lillabo- & BRIO- & others- compatible train tracks generator**

Read this summary till the end before you print any part generated by this generator!

This library can be used in two ways:
-> just download, slice and 3D print provided STL files,
-> generate your own models using provided OpenSCAD file (train_tracks_generator.scad), you can easily modify properties of your models as well as change common dimensions used by the generator (track width, height, plug & nest radius etc.).

The library can so far be used to generate the following types of train tracks:
-> short, low profile test track,
-> straight tracks,
-> arcs (track curves),
-> bridges,
-> switches,
-> intersections,
-> "snake" tracks,
-> dog-bones (nest-to-nest connection),
-> adapters between various train track systems (e.g., IKEA<>BRIO).

Dimensions of the inter-connectors (plugs & nests) are defined based on my own measurements and experiments. They are chosen in a way that connecting a wooden track with a 3D printed one creates a connection which is a little bit tighter than a standard wood-to-wood connection is. Connecting two 3D-printed parts should give a snug and sturdy connection (maintaining a minimal play to ease disconnecting). A play between the parts (wooden vs 3D printed) could be reduced even more but then connecting two 3D-printed parts together would not be possible anymore. Keep it in mind if you decide to play with the configuration parameters.


**Are various train track systems compatible with each other?**

It depends on how much force you are willing to apply :) In general, the answer is: NOT, the most popular systems are incompatible. For instance, tracks from IKEA and BRIO do not fit to each other well. The general dimensions of the parts are similar but - for instance - fitting IKEA track plug (shorter) to BRIO track nest (longer) may be impossible without braking or damaging one of the parts. Even if you will manage to connect two incompatible parts, it may be very difficult to disconnect them.
There may be of course exceptions. I found out that J'adore system (sourced from Rossmann) is pretty compatible with BRIO.

Do you posses two or more various systems and want to connect them? With use of my generator, you can easily generate an adapter which will allow to connect two different systems together.

**IMPORTANT - my strong advice - print the tester at first!**

Before printing any "bigger" part generated by this generator, I highly recommend to print a tester-track relevant to the system you use:

-> file "train_tracks_ikea_tester.stl" (for IKEA Lillabo),
-> file "train_tracks_brio_tester.stl" (for BRIO).

This is a short, 20mm-long, low-profile railway track which takes maximum a dozen minutes to print and requires only ~2g of filament. Test the printed part with your train tracks system. It will help to you asses if the dimensions of the parts (including track plug and nest) used by the generator fit dimensions of the tracks you own. If you posses genuine IKEA Lillabo or/and BRIO railway system/s, the generator default dimensions should be fine, nevertheless, when reading various comments for the similar projects on Internet, I found out that in some countries, dimensions of the tracks may differ a little bit from the commonly known. Default dimensions used in this library are tested on tracks available from IKEA (sourced from Germany & Poland), BRIO and J'adore (Rossmann). Please let me know about your test results in the comments and I will add more information to this description if necessary.  


Printed tester does not fit?
I tested multiple combinations of inter-connectors dimensions, so you should not experience any issues but if you do, do not worry, you can easily experiment and customize dimensions used by the generator to fit your system.

(image)

This is what I call a nest and a plug:

(image)

If you want to change dimensions of a plug or a nest, locate these variables in the library and modify according to your needs (example values below are relevant for IKEA Lillabo):


>// Track Plug
>track_plug_radius = 6.25;
>track_plug_radius_ext = 6.5; // for a dog-bone with a springy plug
>track_plug_neck_width = 6.1;
>track_plug_neck_length = 11;

>// Track Nest
>track_nest_radius = 6.4;
track_nest_neck_width = 6.3;
>track_nest_neck_length = 11;

(image)
