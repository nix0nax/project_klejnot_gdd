
How to immersive sim design (from reddit):
```
The other guy in this thread is wrong. There actually is a fairly standard method for designing immersive sims (and it doesn't mean a stealth game with physics gimmicks either.) However I'm not much of a programmer so maybe take my advice with a grain of salt, and if I get any basic programming terminology wrong feel free to laugh.

Generally you're gonna want to start with your object system. One of the first things you're gonna want to create is a Stimulus class because your game's going to be using Stimulus/Response for object interactions. So instead of defining object relationships via inheritance you're going to instead boil all (or close to all) of your object interactions down to a list of generic stimuli. I'd try to make the list as short as you possibly can, try to have a limit of, like, I dunno 20 or 25 stims total. You're gonna want to make them as generic and universal as possible too so if you want fire in your game you're gonna create a Fire Stimuli (FireStim) and that's gonna apply to every single fire source in your game.

This is why you need to make this class as soon as possible, otherwise you might start defining object interactions via inheritance or a case-by-case basis or however else and it's the wrong way to go about making an immersive sim and you're gonna start running into problems eventually. With the stimuli method every single object interaction is on a nice, short list, right near the top of your object hierarchy, and if you need to create an entirely new type of object interaction halfway through development all you have to do is just add a new stim to your list.

Why are you programming object interactions this way, you ask? I'll give you an example using Thief: The Dark Project. In Thief there's an enemy called Fire Elementals, big, floating balls of fire that shoot smaller fireballs at you. Now, this is very unlikely to happen in the base game (simply because they're almost all exclusively in the tomb raiding missions) but in certain FMs they can create absolute chaos because they can destroy crates (thereby creating tons of noise,) blow open locked wooden doors, damage and kill other enemies (which under the right circumstances can cause a massive battle which the fire elemental will usually win,) and relight doused torches. And all of this is unscripted, emergent behavior - not necessarily intended by the devs.

So what's going on? Well, since Thief uses Stimulus/Response the fire elemental is tagged with a Source: FireStim property (since it's on fire, duh.) And everything that should react to fire, like objects made out of wood (objects tagged with MetaProperty: MatWood,) creatures made out of flesh (MetaProperty: fleshy) and torches (Object: torches) all already react to fire since they've all got a Receptron: FireStim property in them. Or to put it another way: Thief's world understands fire and every object that should react to fire already does.

Take that logic, apply it to literally every single object interaction and... you've pretty much got, like, maybe 30% of an immersive sim. You've still got to develop a bunch of other systems as well like physics and AI and so on but it's a decent starting point. Note: not all immersive sims use this/a similar system it's just that most do. Thief and System Shock 2 use this and Dishonored and Prey use a really similar system (also: Breath of the Wild since that's basically what the Chemistry engine is, so when people ask whether BoTW's an immersive sim I kinda shrug and say, "Sorta, kinda. Maybe. Not really, the quest designs completely wrong but on the other hand the Chemistry engine's literally just the Act/React system from Thief.") It's a sure-fire way of getting consistent emergent behavior and to allow for realistic, unplanned player agency and all that other immersive sim stuff you're gonna want in your game.
```

This approach seems super smart. Every item, npc, object or just THING should be a stimulus and then we can make a table of stimulus interactions. This would be epic.

https://www.systemshock.org/index.php?topic=5798.0
https://www.ttlg.com/Forums/showthread.php?t=47822
https://dromed.whoopdedo.org/dromed/s_and_r_basics


## game design template thingy
https://davidmullich.com/2018/06/25/an-actionable-game-design-document-template/
It splits systems, mechanics, resources and elements. This makes sense I think.

# General gameplay loop idea

# Main systems
## Health system
When you run out you die. You take damage from various obstacles, but it can also be sacrificed for "worse" solutions (e.g. just tank a hit and rely on healing items instead of finding a soultion to something).
## Crafting system
Player can use things directly around them (including parts of the environment e.g. environmental water, fire....) to craft new items.
### Recipe ideas
- rope
- fishing rod
- pickaxe
- potions? - at least funky consumables
- molotov :3
- pots/containers with mud (need to be placed near fire to actually work)
- different recipes maybe?
- bounce pad
- zipline
- cannon
- something that let's you "scout" 
### Recipe book
We need a way to tell the player what they can craft. Recipe book does not have to be full from the start, things should be discovered either organically or via various notes.
## Movement
Big question of verticality here. I think it allows for a lot more interesting design so I'm leaning towards some level of verticality.
Regular top down movement. If something is on top of something else and the bottom thing moves it should move the top one too.
Ledges can be a bit of an issue here with platforms. Probably needs some kind of weight system, this could be unnecessarily complex to implement. Discuss with Shiloh.
Since movement challenges are gonna be a large part of the first thing it should have plenty of options (like ziplines, bounce pads, making platform paths, sliding with oil/ice...).
### Limited movement
Ropes/ladders... only allow movement on one axis.
### Cannon/bounce pad
Forces you to move forward and ignores any low obstacles (ig maybe just all obstacles that aren't literally walls).
### Teleport
Just an idea but teleportation as movement could provide some more options.
## The Cart
The cart can contain a lot of items, limited by volume and weight tho. Gonna act as a pseudo-inventory you have to push around. Crucially you ALSO have to get the cart around not just yourself. You need to get it to the end.
## Moving/throwing things
You can move and throw things depending on their weight and your current "strength" (not a stat per-se but something that can increase/decrease based on buffs. Could also be a binary "can lift heavy things now" flag). Pick up and drop stuff with e. Throw stuff with mouse if carrying something. Moving big things by pushing them with e. Same as carrying but you can't throw it.
### Stimuli/reactor
Everything has reactors. Some things emit stimuli. When a reactor gets triggered by a stimulus (usually if it's in range or on collision but can also be other things like getting consumed) it has some kind of effect on the thing with the reactor. This is the primary way of crafting world interactions.
## (De)buffs
Consumables and the environment can give you buffs/debuffs (slowed when freezing and maybe some wacky ones with potions/food).
## Map
Probably should fill in as the player explores, allows for more interesting interactions.
## Gathering Materials
Sometimes sources can have materials and if you interact with them they spawn a material. This can have requirements (e.g. certain buff or item)
## Notes
There should be notes for lore (and also crafting recipes and maybe buffs and things like that). Ideally we do a lot of environmental storytelling tho
## Lighting
Lighting is a pretty big deal. You can't see when it's dark! Could also reveal some hidden stuff for observant players (light shining suspiciously through a rock)
## Basic enemies?
a basic enemy that one shots could be a good way to add an obstacle that has many solutions

# Resources
- health
- biomass
# Elements
- the cart!
- rope (like zipline)
- spilled liquids
- mud
- fire
- traps
- planks/platforms
- big rocks
- lake
- doors
- destroyable wall
- cannon ("jump over" stuff)
- jump pad ("jump over" stuff)
- switches
- Keys
- portal type thing?
- Pressure plates
## Crafting
- biomass (mostly acts as resource)
- food
- rock
- stick
- mud
- containers
- water
- oil
- rocks (different kinds?)
- rope
- fishing rod
- pickaxe
- ore? (don't really know what you would craft with metal yet, but it fits the theme)
- coal
# Goals
Get from point A to point B (WITH your cart). You probably don't know the exact path to point B, this encourages exploration, which fits with the theme very nicely. We do need to provide at least a general direction though.
# Level Design
levels should probably be very very expansive. Big reusable areas with a ton of branching paths, not one corridor from A to B. Part of the challenge can also be navigation?
# ideas for stimuli and reactors
## Stimuli
- food
- fire
- biomass
- kinetic energy
- explosion
- water
- electricity (or other form of power)
- poison
- cold
- noise
- glue type thing
- acid
## reactors
- burn (start emitting fire stimulus)
- eat food (creatures want to eat food, they can reward you or just be distracted)
- explode (become explosion stimulus)
- take damage
- cook (food gets cooked or eventually burned)
- wet (thing gets wet - gains new properties)
- become poisoned (damage over time)
- become poisonous (added poison stimulus that activates upon consumption)
- become lit (eg torches and shit)
- get powered on (if machinery plus electricity)
- melt (instead of burning, become liquid of some kind)
- freeze
- run away (spooky)
- make noise (emit noise stimulus)
- fill up container
- break container (releases contents)
- harden (mud near fire)
- flatten dough into tortilla lol