# Ethernet Cabling Maximum length

Cat 5,Cat 6, Cat 7 & Cat 8 maximum length is specificed at 100m. [See here](https://blog.tripplite.com/what-is-cat8-cable). Also see [Cable academy max length](https://www.truecable.com/blogs/cable-academy/maximum-ethernet-cable-length)

This feeds into POE where also it's max length is specified at 100m (328ft). See [[2022-03-07_1908_power_over_ethernet]]

This length is normally fine for domestic requirements. Also note that the gauge of the copper matters, as the maximum distance assumes

> you are using solid copper Ethernet cable with a conductor gauge of 22 to 24 AWG.

Whenever you combine patch panels with patch cables to connect equipment, note:

> Permanent links are typically used in commercial installations, or installations done by savvy DIYers desiring flexibility and clean looking installs. You see, permanent links are typically **solid copper** “structure” cable that runs inside walls, below floors, in your basement, and typically out of sight. The only thing you see is a wall mounted keystone jack at one or both ends.

then...

> The permanent link maximum is limited to 295 (90m) feet at 68 degrees F. This length gets shorter as ambient temperatures rise, and can be offset by using shielded cable to some extent. See [Temperature's Effect on Ethernet Cable Length
(https://www.truecable.com/blogs/cable-academy/temperatures-effect-on-ethernet-cable-length).  The maximum of 295 (90m) feet is also assuming you are using patch cables with 24 AWG conductors.  Again, permitted length gets shorter if you do something different. 
You should not use stranded patch cables longer than 75 feet (23m), and you can read more here about why: [Solid vs Stranded Ethernet Cable](https://www.truecable.com/blogs/cable-academy/solid-vs-stranded-ethernet-cable).  In the case of stranded patch cable that makes use of 28 AWG conductors (ultra thin patch cable), you should not exceed 49 feet, even if the patch cable is serving as the entire channel

Quotes from [Cable academy max length](https://www.truecable.com/blogs/cable-academy/maximum-ethernet-cable-length)

## Overall

So, you need to be careful that if you run a long distance, use solid-core cables at 22 to 24 AWG.

If you're combining this with [[patch panels|2022-03-08_1015_ethernet_patch_panel]] and patch cables, then it drops to 295 ft (90m).

Stranded patch cables should not exceed 75 ft (23m). It drops to 49ft if using 28 AWG stranded cable.

Total distance cannot exceed 100m (328ft).

See [[2022-03-08_1030_ethernet-solid-core-v-stranded-cable]]

#ethernet
#cable
#network
#poe
#cat
