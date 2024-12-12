The map is separated in 2 parts: Areas and Zones. 

Areas are simple.

function Area(){
  this.name='Nowhere';
  this.id=0;
  this.pop=[];
  this.size=10
  this.drop=[];
  this.onEnd=function(){};
  this.onDeath=function(){};
}

Pop determines the monsters that spawn. An example is: {crt:creature.default,lvlmin:1,lvlmax:1,c:1}, with lvlmin and max being the level range, and c:1 the chance of it spawning.
Size is how many monsters, and drop what drops the zone should give on beating a monster. you can add multiple chances by adding a , between each chance: .4,.7,.8 etc.
onEnd is for a function that runs when finishing the zone, a common one is going to the next zone in line, with an {smove(chss.nextzone,false), activating flags, and item drops; A this.size=rand(40)+30; can be used to make the area pop varry.
onDeath is used to add functions, activating flags, such as during the initial training to get herbs. Can also be used with a this.size=rand(x)+y; to increase the pop size, such that the player has to take every enemy on at the same time. Could also be used to send the player someone else upon death. no idea. If not/don't know how, simply use other ways to move. (perhaps try putting the death move on the onDeath killer function on a variable thing, so you can modify it, depending on what kills you/where you sleep). Very rare. Most common will be requiring the player to manually travel between minor areas (including the elemental lands) and expensive transport stones (as they don't require the player spending lots of healing/consumables to travel). Permanent save spots will only be between very large central areas.

## Areas are more complex

### how to make a basic zone.
chss.area5 = new Chs(); chss.area5.id = 888; addtosector(sector.vcent,chss.area5); addtosector(sector.vmain1,chss.area5)
chss.area5.sl=()=>{global.flags.inside=false; d_loc('Shadow Realm'); global.lst_loc = 888;
chss.area5.onEnter=function(){
  area_init(area.area5c);
};
chs('"=> Go back"',false).addEventListener('click',()=>{  
   smove(chss.lsmain1,false);
/ });

### how to make a basic area, where combat takes place
area.area5c = new Area(); area.area5c.id = 119;
area.area5c.name = 'Training Grounds';
area.area5c.pop = [{crt:creature.frostpixie,lvlmin:1,lvlmax:3,c:1}];
area.area5c.size = 10; z_bake(area.area5c);
area.area5c.onEnd = function(){ smove(chss.area5,false)}

### adding items drops
area.frstn9a1.onEnd = function(){
  roll(item.acrn,.2,1,5);  roll(item.mshr,.35,1,3);
  roll(wpn.stk1,.15); roll(item.sbone,.3,1,3);  roll(item.wdc,1,5,17); roll(item.appl,.25,2,5); roll(wpn.axer,1); roll(item.pcn,.5,1,3); 
  this.size=rand(20)+40; smove(chss.frstn3main)
}; area.frstn9a1.drop=[{item:item.hrb1,c:.03},{item:item.wdc,c:.06}]
or
area.frstn1a4.drop=[{item:item.cp,c:.006},{item:wpn.stk1,c:.0009},{item:wpn.axer,c:.001},{item:item.sbone,c:.0005}]

### And this for scouting

chss.bsmnthm1.data={scoutm:900,scout:0,scoutf:false,gets:[false,false],gotmod:0}
chss.bsmnthm1.scout=[
  {c:.01,f:()=>{msg('You found a pouch with some coins!','lime');giveItem(item.cp,rand(1,5));giveItem(item.cn,rand(1,5));giveItem(item.cq,rand(1,5));chss.bsmnthm1.data.gets[0]=true;},exp:40},
  {c:.03,f:()=>{msg('You found a pile of scattered firewood, some logs seem useful but others have rotted completely. You decide to grab them anyway');giveItem(item.fwd1,rand(2,4));giveItem(item.wdc,(45,90));chss.bsmnthm1.data.gets[1]=true;},exp:10},
  {c:.03,f:()=>{
    chs('Among the rabble and remains of collapsed bookshelves you decide to confirm if anything survived. Rotten and soaked in basement juices books seems unsalvagable, bookshelves as well, you can\'t even tell if they are made of wood anymore. One of the books was incased into a small mound formed by rocks and sand, it seems surprisingly fine',true);
    chs('"<= I\'m taking this"',false).addEventListener('click',()=>{chss.bsmnthm1.data.gets[2]=true;giveItem(item.jnlbk);deactivateAct(global.current_a);smove(chss.bsmnthm1,false)})
  },exp:15},
]; 
chss.bsmnthm1.onScout=function(){scoutGeneric(this)}

Uhh, figure out the rest.