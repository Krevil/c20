**Fog** tags describe the colour and density properties of fog which can be applied to BSP [_fog planes_][scenario_structure_bsp#fog-planes] using [Sapien][].

Non-planar atmospheric fog does _not_ use a fog tag, and is instead controlled by the [sky][] tag.

# Known issues
Due to a [renderer regression][renderer#gearbox-regressions], the _screen layers_ effect of these tags does not render on H1CE or H1PC, nor does it draw over the skybox unless [_atmosphere dominant_](#tag-field-flags-atmosphere-dominant) is set. This tag renders correctly in H1X and H1A.

As of MCC season 7, there is a new issue where fog does not render at the right density over models and causes them to stand out especially in areas of high fog density.
