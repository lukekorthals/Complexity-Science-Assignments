# Complexity-Science-Assignments
Some Assignments from the complexity science course at the University of Amsterdam.
During the course we learned to run basic simulations in netlogo, work with the cusp catastrophe model in R and use networks in JASP. 

# Netlogo Simulations
The Netlogo folder contains three simulations. 
You can run them with basic settings by clicking setup and go and play around with the sliders, buttons and switches. 
Sometimes it makes sense to play around with the speed slider at the top to make the simulation run faster or slower.

## 1. Dancing Simulation
We were supposed to create a simulation that represents what is happening in this youtube vide: https://www.youtube.com/watch?v=GA8z7f7a2Pk

### Short Video Description: 
- First only one person dances.
- Then a couple more join them.
- More and more people join until finally a large crowd emerges.
- Initially people are hesitant to join. With the growing crowd, more people join quicker. 

### My Solution:
- On every tick each turtle (person) evaluates whether to join the dancers according to a decisiveness score. If the score is above 100, they join. 
- The decisiveness score is the sum of their current adventurousness and comfort level. 
- Their adventurousness is determined at each tick as a random float between 0 and 100.
- Their current comfort level is determined by the number of dancers and the minimum number of dancers they require to be comfortable.
- The individual minimum number of dancers each turtle requires to be comfortable is determined at random upon creation according to a user specified normal distribution.
- This simple formula ensures that turtles are very unlikely to join when there are few dancers (pretty much only according to adventurousness) and very likely to join when there are many dancers (according to comfort level).
- Apart from this turtles have different behaviour according to their state (sit, walk, join, dance) and the sliders allow to play around with multiple groups different threshholds etc. 

### The Math:
- $minimumdancers \in \mathbb{R}, minimumdancers \in [0,100]$ # determined upon creation
- $comfort = (dancers / minimumdancers)^2$ # more dancers exponentially higher comfort
- $adventurousness \in \mathbb{R}, adventurousness \in [0,100]$ # determined every tick
- $decisiveness = adventurousness + comfort$ # if > 100, turtle joins the dancers

## 2. Flocking Simulation
We were supposed to create a basic flocking simulation using the alignment rule. I took it a few steps further by adding cohesion and seperation to the flocking behaviour and introducing predators. 

You can run this by clicking Setup, Spawning some fish and clicking go. Play around with the sliders and introduce some predators to see what happens. 

### Short Description: 
- Animals like birds, insects and fish show flocking behaviour in groups. 
- This seemingly complex behaviour is largely determined by three simple rules. 
    - Alignment - individuals align their direction to their neighbours. 
    - Cohesion - individuals stay close to their neighbours. 
    - Seperation - individuals keep a minimum distance from their neoghbours. 

### Interface
- **Fish Behaviour** - Enable or disable basic behaviour of the fish.
- **Predator Behaviour** - Enable or disable basic behaviour of the predators. 
- **General** - Determine random heading of fish and predators and birth rate of fish. 
- **Alignment**, **Seperation** **&** **Cohesion** - Finetune flocking behaviour of fish. 
    - Example: a smaller field of view leads to smaller swarms. 
    - Example: a larger/ smaller minimum and maximum distance lead to more/ less distributed swarms.
- **Add Agents** - Spawn fish and predators. 
- **Color Coded Behaviour** - Different colors show what affects the turtles (fish and predators). Turn switches off and on to figure out which color demarcates what. 

## 3. Ising Model
We were supposed to add an external field to the basic Ising Model from the netlogo model library. Additionally we were supposed to show the hysteresis and pitchfork effects using this simulation.

You can play around in the free simulation (select at the top right) or run simulations for hysteresis or the pitchfork. If you want to rung the latter, just select them, click setup and press run. Check out the plot and don't play around with the sliders as they are automated.

### Short Description: 
- The Ising model is a classical simple model to describe the magnetism of crystals on the atom level. 
- Atoms can have a positive or negative spin (+-1). 
- This spin can be influenced by their neighbours and an external field. 
- Atoms allign their flips to their neighbours and an external field.  
- They are also affected by the surrounding temperature, with colder temperatures resulting in fewer flips. 
 
### Hysteresis
- Hysteresis is a property of complex (chaotic systems). 
- It describes the phenomenon that the change in an effect lags behind the change in its cause. 
- This means that a system stuck in a stable state may require a disproportionally large pertubation before it transitions into another state.
- Once the perubation is large enough, the change in the system is sudden and catastrophic.  

### Pitchfork
- A complex (chaotic) system has distinct stable states. 
- According to variables that affect the system, it may be attracted to one state or another. 
- It is often dificult (or impossible) to predict the next state of a system. This is illustrated by the pitchfork which represents the different states a system may fall in to. 

### Interface
- **Free Simulation** - Play around with the sliders to see how they affect the spins.
    - Start with a flipping probability of 50%, a temperature of 5, and the external field at 0 to see random flips and an average around zero. 
    - Move the sliders for temperature and the external field to see how they affect the spin. 
- **Simulate Hysteresis** - Click Setup and Go and watch the plots. Don't play with the sliders. 
    - The slider for the external field is automated. 
    - By looking at the plot, you can see a clear hysteresis effect: The change in spin lags behind the change in the external field. 
- **Simulate Pitchfork** - Click Setup and Go and watch the plots. Don't play with the sliders. You might want to increase the speed. 
    - The slider for the temperature is automated. 
    - The simulation starts with a high temperature which results in random spins and an average around zero. 
    - After 50000 ticks the temperature sliders is set to 4.4 which results in the system collapsing to either a positive or negative state (positive or negative average spin). 
    - This illustrates how a chaotic system can be attracted to different states.  
- **Simulate Hysteresis Temp 1** - This is simply the hysteresis simulation but with the temperature at 1. 

# R Final Project
As the smaller R assignments were not as interesting, I only included the final project in this repository. 
I conducted this final project together with Laura Groot and Roy Moore. Specifically, we investigated the parameter recovery of the cusp model in R using simulations. We implemented the cusp with the cusp package by Grasman et al. (2009). 

Grasman, R., van der Maas, H. L., & Wagenmakers, E.-J. (2009). Fitting the Cusp Catastrophe in R: A cusp Package Primer. Journal of Statistical Software, 32(8), 1–27. https://doi.org/10.18637/jss.v032.i08

## The Cusp
- The cusp is a very simple catastrophe model. It essentially models a dependent variable according to two axes representing an independent variable and a splitting variable. 
- The independent variable affects the dependent variable directly, while the splitting variable moderates this relationship. 
- The relationship is either linear or s-shaped according to the splitting variable axis.
- If the relationship is s-shaped, the dependent variable can fall in one of two states according to the independent variable.
- This attraction to one of two stable states represents a pitchfork bifurcation. 

## Our Study
- The cusp can be used to model psychological phenomena and sometimes fits better than linear models. 
- However, psychological experimentation often suffers from poor sampling, or test methods. Therefore, we tested the parameter recovery of the cusp under suboptimal conditions.
- We ran three simulations, manipulating sample size (simulation 1), granularity of the dependent variable (simulation 2), and the sampling range (simulation 3) 
- We investigated accuracy using mean absolute error (MAE) and systematic bias using ean bias error (MBE).
- In Simulation 1, we found that accuracy suffers from small sample sizes (<100) but could detect no systematic over- or underestimation.
- In Simulation 2, we found that accuracy suffers from measures with low granularity (e.g., 7-point scales). Additionally, we found that some parameters are systematically underestimated and others are systematically overestimated.
- In Simulation 3, we found similar results to simulation 2, with accuracy suffering under a restricted sampling range and some parameters getting systematically over- or are underestimated.
