# tauceti

Does a planet transit tau Ceti in TESS Sector 3?

###  Comments

There is a deep dip in the light curve of tau Ceti at TJD 1394.3, as revealed separately by halo photometry and Planet Hunters.

What is happening?!

Some comments:
* If you take the pipeline 2-min cadence TPF and run halophot, excluding the centre portion but keeping basically the rest of the field, it aggressively up-weights a few background stars and something that looks rather like the deep TESS PSF. It doesn't do the pathological thing you sometimes get of eg focusing exclusively on a few hot or partially saturated pixels or on weird non-contiguous blocks. The light curve you get from this has a deep and clean transit, which is maybe a bit long and deep, but looks ok.
* If you compare this to the CBVs, the only one it really looks like is on camera-CCD 1-2, ie the CCD on which tau Ceti itself lies. This is maybe a mild mark in its favour: I can easily imagine such a bright star dominating a component of the CBVs and you don't see this effect in other detectors.
* The FFI cutout tool doesn't have a background calibration, and the flux in every pixel rises sharply towards perigee. We see the same in the pipeline 2-min TPF background lightcurve. Just before perigee, at TJD 1394.3, there is a dip superimposed on the otherwise smooth rise. In the other stars I've looked at I haven't noticed this, though I haven't been exhaustive about it, and it could just be a feature of the Earthlight that I haven't seen before. At a timescale of half a day or so I can imagine this being an ocean glint or something weird like that. Who knows! 
* If you use lightkurve.interact() and look at the individual pixel time series in the FFI TPF, they all show this dip. But in the pipeline TPF this is different: above the mid-axis of the star, they go up during 'transit' and below they go down. You can actually see this at a global level if you use the slider and the right scalings: it seems that as a whole the background flux shifts upward on the detector for a few hours and then shifts back down. 
* I think with the field dependent thing happening we could be seeing some kind of crosstalk. Depending on how this happens it could either mean that the field dependent background is crosstalk from tau Ceti itself and it is shifting thanks to the transit - so the transit is real - or that the background is dominated by something else and the transit isn't.
* Are there other astrophysical events happening at this time? I haven't looked at μany other Sector 3 lightcurves yet really, but from what I can tell they don't seem to do this (see notebooks/random.ipynb for a lightkurve interface - I just picked a fifth mag star as an example - look in data for the list of all targets in Sector 3).
* I think the key issue is to figure out what is the field-dependent background calibration the TESS team pipeline applied. We won't figure this out unless we know what processing gave us the pipeline TPF and whether there are known effects that do this!

I have done a comparison to zeta Ceti using halo - we get overall very poor halo results (but surprisingly very good pipeline results) on zeta Ceti, which shows the same background dip. In the halo light curve you can kind of see a very weak dip at the epoch. I am not sure what this tells us.

### Dependencies

The main dependencies are

	pip install astropy lightkurve halophot

and generic Python stuff.

I haven't included the CBVs because these are large but you can download them yourself if necessary. They don't seem to have much interesting bearing on the problem though.