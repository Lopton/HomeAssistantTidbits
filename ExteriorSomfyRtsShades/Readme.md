# Background:
I have purchased 2 different SunSetter exterior motorized shades to prevent the sun from hitting the south wall of my house in the summer. Each shade comes with a remote and communicates via the proprietary Somfy RTS protocol. I elected to use the Somfy ZRTSI to act as an interface between the shades and z-wave controls. 

The downsides of the Somy ZRTSI is that there is no bi-directional communication so your automation will not know the true state (up or down) of the shades. Also the ZRTSI has poor range on the RTS side, so it needs to be within 20-30 feet of the shades you want to operate.

The ZRTSI itself is super easy to use and program. Essentially to link each shade to the ZRTSI by pushing a small button on the back of the remote and then clicking a button the ZRTSI. I programmed all of the shades to the ZRTSI then did the zwave stuff. Zwave stuff is easy enough, first you add the main unit, then add one virtual unit for each set of shades. Overall it was easy to do.

# Concept:
The Home Assistant automation that I wanted to do was automatically lower 2 of my shades when the sun starts hitting the wall these shades cover. Some considerations that I wanted to be aware of were: 

  1.)	Sun position varies throughout the year
  
   a.	I didn’t want to install a sensor, instead I wanted to use the sun position in the sky to determine when it could be hitting the wall.
    
   b.	Sun position is already baked in to the default Home Assistant, but I didn’t want just above horizon or below, I wanted the precise time that the sun would start hitting the walls. I found this NOAA site (https://www.esrl.noaa.gov/gmd/grad/solcalc/) and inputted my lat/long, then played with the date and time to get the azimuth which the sun would be hitting the south face of my house. (click show azimuth to see a line). It worked out to between solar azimuth of 120 and 295. Also elevation of >5 worked out pretty well.  
    
  2.)	high winds could damage the shades 
  
   a.	At this time I don’t have a wind sensor, so I choose to use the YR sensor that comes default with Home Assistant
    
  3.)	clouds may make the shades not needed
  
   a.	Still haven’t found the best solution for this. The YR sensor clouds is not accurate enough for me to make use of.
    
  4.)	shades should close when the heat on the wall may be beneficial 
  
   a.	Currently going to base this on a temperature sensor I have in my non-conditioned garage. I figure heat load in the garage is a reasonable model for the house.
    
   b.	In the future I may also include ties from my heat pumps, basically if any heater is running the shades should be up.
    
# Home Assistant Automation:
  1.)	Create a Binary Template Sensor for if the shades should be open or closed
  
   a.	See HouseExterior.yaml
    
  2.)	Create automations
  
   a.	See Exterior_shades.yaml

