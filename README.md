# Stoch Gait Adaptation: Literature Review

We explore previous works that elucidate terrain identification and adaptation 

## Paper 1: Using Gait Change for Terrain Sensing by Robots

### What I understood: 

#### Abstract:

- They are using changes in the walking speed to adapt to walk optimally in different terrains
- The terrain is identified by monitoring various parameters and using unsupervised classification algorithm, kNN.

#### Deliberation in chronological sequence: 

- The reason why gait transition occurs in biological systems is either due to mechanical limitations of the legs or due to the fact that in the current gait the system cannot travel any faster. Another reason is to minimize energy expenditure.

- If travelling from point A to B becomes more energy efficient by one gait than by the other, transition of gaits will occur. 

- The issue with reaction-based terrain classification (i.e., determining terrain based on the reaction forces) is that the data-sets involved is very large. 

- Cycle period (tc): Time taken for completion of one gait cycle (fc = 1/tc). 


- The problem of classifying the terrain and optimizing the speed & efficiency is divided into two sub-problems:

 1) Find the optimal cycle frequency for a terrain at which the robot obtains highest physical speed or maximum power efficiency or a combination of both 

 2) Seperation between terrain classes within a chosen set of features: 

	1. Electric current
	2. Torque at each leg
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
- What is single stance period? (
- Duty factor = single stance period / cycle period)
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

## Paper 3: Biologically Inspired Dynamic Walking of a Quadruped Robot on Irregular Terrain- Adaptation at Spinal Cord and Brain stem

### What I understood: 

#### Abstract:

- The authors employ a Neural System Model, which integrates several reflxes such as the stretch reflex, vestibulospinal reflex, extensor and flexor reflex into CPG (Central Pattern Generator)


#### Deliberation in chronological sequence:

##### Introduction

- Animals can easily adapt their gait in any walking environment. 
- Previous studies by the same authors achieved dynamic walking on slopoes with only minimal irregularity. The walking was not smooth. Reflexes were independent of CPGs. 
- This study combines CPGs and reflexes and has been proven to be more effective compared to using both independently. 
- Testing done on quadruped robot 'Patrush'

##### Specifications of Patrush 

	1. Each leg has three joints
	2. Three joints are hip, knee and ankle (passive)
	3. Length=36cm ; width=24cm ; height=33cm ; weight=5.2kg 
	4. For reflex mechanism, 6 axis force sensor is attached on a lower link beneath the knee joint. 
	5. A rate gyro as an angular velocity sensor is mounted on a body as a vestibule. 
	6. All control programs written in C and executed on RT-Linux. 
	7. Notations used: R(right), F(fore), H(hind), S(hip), x(joint angle),fx and fz(force sensor value in x and z direction). For example, LFS means the hip joint of the left foreleg, and LFS.x and LF.fx mean the angle at this joint and force sensor value at this leg.

##### Walking on flat terrain using CPGs

- CPG like models have the capability to generate and modulate walking patterns along with rhythmic joint motion. 

- The model of CPG used is called 'Neural oscillator' (NO) proposed by Matsuoka. 

- Single NO consists of two mutually inhibiting neurons. Each neuron is represented by a non-linear differential equation. 

-  By connecting the NO of a hip joint of each leg, the NOs are mutually entrained and thus oscillate with  the same period and phase difference, thus resulting in the formation of a gait. 

- In animals we consider two kinds of reflexes: 
	1. Short term reflex or 'Phasic stretch reflex'
	2. Long term reflex or 'Tonic stretch reflex'

-By experiment using only CPGs and tonic stretch reflexes, it was confirmed that Patrush could walk on Flat terrain. 

##### Walking on irregular terrain using CPGs and Reflexes: 

- Adjustment of CPG and reflexes is based on somatic sensation such as contact with floor and tension of muscle of supporting legs, and vestibular sensation to achieve adaptive walking. 

- Three types of models are considered for adaptation: 

	1. a CPG only involving a tonic stretch reflex
	2. a CPG and reflexes independent of CPG 
	3. a CPG and reflexes via a CPG 

- Type 1. did not result in Patrush walking over obstacles 3 cm in height, or slope more than 7 degrees.

- Type 2. reflexes are independent of CPG and sum of CPG torque and reflexes torque is output to a motor. This was more efficient and walked over obstacles of 3cm height and 12 degrees of slope. The problems were as follows: 

	1. Delay in joint motion from the phase of CPG in walking up a slope resulted in slipping and stamping with no progress. 

	2. Sensor based adjustments to solve such problems increased number of paramters and made control system complicated. 

	3. Falling of quadruped as there was no sync in signals from the CPG and flexor reflex. 

- Type 3.


	1. Problem 1 of Type 2. was solved using this approach because excitatory feedback signal to the extensor neuron of a CPG in walking up a slope makes the active period of the extensor neuron of a CPG become longer, and difference between phases of a CPG and joint motion becomes small.



### What I didn't understand / need to explore:

- What is a CPG and how are reflexes generated? 

Ans: 
Central pattern generators (CPGs) are biological neural circuits that produce rhythmic outputs in the absence of rhythmic input. They are the source of the tightly-coupled patterns of neural activity that drive rhythmic motions like walking, breathing, or chewing. 

- Not fully understood: 'The body motion of the robot is constrained on the pitch plane by two poles since the robot has no joint around the roll axis'

- What is the describing functions method for analyzing and tuning a NO? 


## Paper  4: Design, Development and Experimental Realization of a Quadrupedal
Research Platform: Stoch

### What I understood: 

#### Abstract: 

- 'Stoch' is a quadruped robot built to explore different research problems in legged locomotion, using traditional and learning based techniques. 

- What is covered: hardware design, control architechture, merits & demerits of the quadruped platform on which Stoch is built upon, trotting, bounding, turning, and gait various gait transitions. 

##### Introduction

- Software consists of a real-time trajectory, which are passed as commands. 

- CPG based trajectory generator also enables the realization of gaits like bound, walk, gallop and turning in hardware with no additional training and provides smooth transition from one gait to another. 


Since the emphasis of my study is on controls, it will be dealt with in more detail. 

#### Electronic System Architecture: 

- Objectives: 

	1.  Tele-operation is implemented using SSH over wireless communication. 

	2. Low level implementation of walking controller that gives the desired joint configuration to the actuators. 

	3. Integrating sensory feedback with walking controller. 

- Tele-operator: The walking controller changes by changing the internal parameters of the  CPG such as frequency, phase difference, and amplitude during process execution via SSH.

- Motor actuation: PWM enabled motors coupled with Adafruit PWM drivers communicating via I2C. 

- Sensory feedback: The sensory elements are: 
	1. Joint encoders (angular position of shaft read using multi-duplex SPI bus)
	2. IMU (measures RPY using sensor fusion)
	3. Limit switches (self-calibration and failure prevention at joints)

- Walking controller: 
	
	* The controller is based on non-linear coupled oscillator called central pattern generator (CPG)

	* A CPG mimics what a network of neurons in our brains do to generate rhythmic signals. CPGs constitute non linear differential equations to mimic this. 

	* CPG produces predetermined rhythmic patterns, and the difference in phase offset results in different types of gaits. This phase offset can be produced on the fly by passing the desired phase offset through a low pass filter. 

	* Low pass filters in the time domain ensures that there is no discontinuous changes in the variables (i.e., periodic changes are allowed but no high frequency changes)

	* The coordinates obtained in the cartesian or polar coordinates (positions measured from the hip joint), is then converted into the corresponding joint angles using inverse kinematics. 

#### Experimental Results: 

- 6 different gaits are realized on flat ground which are trot, gallop, bound, walk, modified trot 1 and modified trot 2. 

- Weight matrix contains basis function generated values about the various trajectories. 

- 

### What I didn't understand / need to explore:

- On what basis is this pre-determined pattern of rhythmic signals generated by the CPG?
- "Oscillation frequency updates the phases and coupling ensure the phase offsets between the  oscillators" 
- What is the significance of multi-duplex?
- How is self calibration possible using limit switches? 
- Working of low pass filters 
- How is the desired phase offset determined for a particular gait? 
- Basis function based approach 
	Ans: It is a method of linear regression

## Paper 5: Realizing Learned Quadruped Locomotion Behaviors through Kinematic Motion Primitives


### What I understood: 


#### Abstract: 

- Kinematic motion primitives (kMPs) are a set of basic patterns used by humans and other animals to realize periodic (walking, running) and discrete tasks

- These basic motions are learned using 'Deep Reinforcement Learning' (D-RL), as opposed to traditional controllers. 

- The objective is to realize basic walking patters namely trot, gallop, walk and bound using these kMPs. 

- kMPs can effectively embody the walking pattern and using this we can derive other behaviour. 

- The kMPs are invariant waveforms, and it will be shown that a small set of kMPs is sufficient to explain a wide variety of complex coordinated motions, both periodic (e.g., walking and running), and discrete (e.g., reaching for a target with one hand). 

- D-RL uses policy gradient based approaches. The resulting walking is analyzed using principle component analysis.

- KMPs extracted from PCA followed a similar pattern irrespective of the type of gaits generated.

#### Introduction

- Proximal policy optimization (PPO) was used by Minitaur

- KMPs are basis functions from which the trajectories for each of the joints were reconstructed.

- A small number of basic trajectories are sufficient to realize periodic trajectories

- Using RL and D-RL to derive robust locomotion behaviours in both bipeds and quadrupeds eliminates the need to model the robot and also allows the computer to adapt to changing environments

- Controller learned is model free and done in simulation which is often not realistic for implementation. 

- D-RL techniques are used as a optimization methodology to generate the trajectories and the gaits associated with


### What I didn't understand / need to explore:

- Similar patterns of different gaits in terms of what? 

- How does using KMPs improve transferrability to the real hardware?

- How do KMPs point to the fact that high freqency modulations aren't present in joint angle trajectories? 

