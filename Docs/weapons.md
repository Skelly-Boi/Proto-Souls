Weapons have 2 main statistics:
The damage type, Edge, Pierce and Blunt (.cls)
The element, physical, air, earth, fire, water, light, dark (aff), affecting damage for weapons and defense for equips, altho that can be changed with

sld.stksld.oneq=function(){you.aff[0]+=x};
sld.stksld.onuneq=function(){you.aff[0]-=x};

to add damage, and -caff to reduce damage. Lower caff reduces it, yes.

cmaff is monster type defense, works just fine.
maff is monster type offense, works fine
