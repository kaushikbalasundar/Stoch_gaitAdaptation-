# Stoch Gait Adaptation: Literature Review

We explore previous works that elucidate terrain identification and adaptation 

## Paper 1: Using Gait Change for Terrain Sensing by Robots

### What I understood: 

#### Abstract:

- They are using changes in the walking speed to adapt to walk optimally in different terrains
- The terrain is identified by monitoring various parameters and using unsupervised classification algorithm, kNN.

#### Deliberation in chronological sequence: 

- The reason why gait transition occurs in biological systems is either due to mechanical limitations of the legs or due to the fact that in  the current gait the system cannot travel any faster. Another reason is to minimize energy expenditure.

- If travelling from point A to B becomes more energy efficient by one  gait than by the other, transition of gaits will occur. 

- The issue with reaction-based terrain classification (i.e., determining terrain based on the reaction forces) is that the data-sets involved is very large. 

- Cycle period (tc): Time taken for completion of one gait cycle (fc = 1/tc). 

- Duty factor = single stance period / cycle period

- The problem of classifying the terrain and optimizing the speed & efficiency is divided into two sub-problems: 1) Find the optimal cycle frequency for a terrain at which the robot obtains highest physical speed or maximum power efficiency or a combination of both 2) Seperation between terrain classes within a chosen set of features: 

	1.  Electric current
	2.  Torque at each leg
	3. Actual leg angle
	4. Leg point of contact to the ground
	5. Acceleration of the robot and other IMU measurements

- Vertical acceleration of the robot and current are two important parameters that change between terrains (Robot legs provide different push based on the terrain involved)

- Optimal cycle frequency is used as a feature to enhance the accuracy of classification. 

- Experiment & data collection:

	1. 4 different terrains were used (dry sand, wet sand, grass, concrete)
	2. 5 different cycle frequences(fc) used on each terrain. Different fc is obtained by changing the input speed control settings of robot
	3. Relative leg rotations are  measured using optical encoders
	4. Leg motor electrical current is measured
	5. 3 axis IMU sensor (3 gyroscopes & 3 magnetometers)
	6. Video of all trials was used to measure the time taken as this method is more accurate than using a stopwatch & also serves as documentation. 
	7. Sampling rate: 30 samples/ revolution of leg

-  Observations: 

	1. As fc increases, physical speed increases for soft terrains like dry & wet sand. However, for hard surfaces, physical speed decreases after increasing the fc beyond a certain point. This is probably due to slip. An optimal fc is necessary in hard terrains for maximum speed. 

	2. Motor current (I) & vertical acceleration of the robot (Az) are the most affected by changes in the terrains.

	3. IMPORTANT: The dimensionality of the feature-set was reduced by sampling the data only at a particular angle in the leg rotation cycle at which there was maximum deviation or 'class separation' in readings for the different terrains. 

	4. The robot walks initially at  fc =0.1 and identify the terrain. Then it switches to fc = 0.8 and re-evaluates it to be absolutely sure  of its terrain. Once it is certain about a given terrain, the optimal fc for that terrain is adopted. 

	5. kNN unsupervised learning algorithm takes the sequence of time-dependent real-time sensor readings from the robot for classification as it traverses the terrain.  
	
- Results: 

	1. IMPORTANT: There are specific values of fc at which the terrain classification is most accurate. We need to experimentally identify this value of fc. Do this by looking at the success rate of correct identification of the terrain. 

	2. Small data set and unlabelled data provided upto 90% accuracy of terrain differentiation. 

### What I didn't understand / need to explore: 


- What is singular value decomposition interpolation (SVDI) ?
- Working of kNN
- Why does reaction based terrain classification consume a lot of data? 
- '... speed dependencies to increase the classification accuracy' How does it increase accuracy? 
- What is Buehler clock and central pattern generator (CPG)?
- What is single stance period?
- How do we change fc/input speed levels in Stoch? 
- What is single stage batch nature of kNN? 
- What is a Markovian process?  

## Paper 2: Terrain-Adaptive Gait for Walking Machines

### What I understood: 

#### Abstract: 

- The advantage of walking machines is their ability to move across different terrains. However, we need gait modification based on operational terrain to reap maximum benefits. 

- The article proposes a strategy to adapt gait on irregular terrain in real time based on variations in parameters of a periodic gait. 

- It doesn't require prior knowledge of footholds. The gait adaptation is demonstrated for wave-crab gaits, but can also be applied to other periodic gaits. 

#### Deliberation in chronological sequence: 

- Periodic gaits having constant cycle times are preffered over aperiodic gaits as they are simpler and easier to implement.  

- Non periodic gaits can be used to place the legs at pre-planned footholds. However, this is more computationally expensive and complex to deisgn. 

- The  objective is to achieve terrain adaptability using periodic gatis. 

- Hirose(1984) proposed a system assuming horizontal terrain, constant speed and characterized certain regions in the working space to be forbidden which uses free gait (non-periodic), but maintains wave gait for crab walking. Kumar and Waldron proposed the modified wave gait, where parameters like duty factor and leg phase induced the changes in gait. Both don't have experimental proof. 

- When a blind quadruped walks over uneven terrain, two sitations can arise: 

	1. Leg finishes one gait cycle before touching ground. 
	2. Leg contacts ground before expected. 

- Objectives for this paper: Deal with situations described above, using a cyclic periodic wave-crab gait and constant velocity as this provides maximum static stability. 

- Supporting leg moves between the front limit position (FLP) and rear limit position (RLP). 

- Types of irregular terrains: 

	1. O-Type: Crests and troughs
	2. OH-Type: Only Troughs
	3. OP-Type: Only Crests

- Terrain adaptation: 

	1. When a leg is placed on a crest  (OP terrain), its support time is increased 
	2. When a leg is inside a trough (OH terrain), its return time is increased to prevent the gait cycle from completing before the leg makes contact with the ground.
	3. Initial stroke R is changed to R1 to facilitate the above changes while maintaining a constant velocity. 
	4. The original stroke Ro needs to be restored ideally to ensure that the adaptive gait control is performed multiple times. 
	5. The extra time for which the  leg remains in the air after the completion of the gait is called extra-transfer phase. 
	
	
### What I didn't understand / need to explore:

- Explore Kumar and Waldron's modified wave gait
- Mathematical formulations of leg trajectory in support phase
- Description of the transfer phase 
- What is the relationship between support time, return time, and time period? (pg. 326)
- How do you measure the latency between the end of gait and time of contact of leg on ground? 
