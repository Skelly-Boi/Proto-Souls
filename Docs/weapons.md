Weapons have 2 main statistics:
The damage type, Edge, Pierce and Blunt (.cls)
The element, physical, air, earth, fire, water, light, dark (aff), affecting damage for weapons and defense for equips, altho that can be changed with

sld.stksld.oneq=function(){you.aff[0]+=x};
sld.stksld.onuneq=function(){you.aff[0]-=x};

to add damage, and -caff to reduce damage. Lower caff reduces it, yes.

cmaff is monster type defense, works just fine.
maff is monster type offense, works fine

To deal damage, your weapon cls has to approach the enemy's cls, with a [0,0,10] weapon dealing full damage against a [999,999,0] enemy, while a [3,3,3] while have 2/3 of the damage blocked. A [900,0,0] weapon will still deal damage, although slightly reduced by the resistance.
Cls on a weapon, as with aff, also increases teh damage it does, 999 being almost 300 extra damage.
