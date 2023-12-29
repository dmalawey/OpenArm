![openarm banner](/img/banner_openArm.png)

# OpenArm
_An open-source robot arm_

> **PURPOSE: to design a robot arm using bio-inspiration for higher modularity and higher loads than leading commercial designs in 2023.**

| [Github Repo](https://github.com/dmalawey/OpenArm ':class=button') 
| [Website](https://qr.page/g/2wY5JrxcciD ':class=button')
| 

## Characteristics

Version 1
* Comprised of 3D Printable + OTS parts
* Less than $150 in components
* Using DC motors, M2 Belts, and M2 pulleys like those of 3D printers
* Having no encoders required *️⃣
* Bio-inspired - having damping forces and torque relationships similar to a human arm. 
* Digital-twin oriented - the simulated design shall represent the real implementation sufficiently to simulate motion.
* Parametric design - the geometry leaves space for variations and modifications of internals & frame.

| Biological Sketch   | Biological sketch with motors identified | Robot Arm concept with motors |
| --------------------------------- | -------------------- | ----------------------- |
| ![davinci1](https://i.imgur.com/8pUq4JF.jpg) | ![davinci_markup](https://i.imgur.com/iho4c2z.jpg) | ![vitruvian_robot_arm](https://i.imgur.com/e5CzMqP.jpg) |

### Mechanical
* Payload Target = 1kg
* Derived from SCARA configuration to enhance payload
* Hope to derive encoder-like function of Motor "n" from measurement of reaction torque at motor "n-1"
* All motor assemblies to be backdrivable
* Modular - multi-DOF, selectable
* Parametric - change the size as you wish
* Rigid frame - components will not have intentional compliance or antagonistic actuators

## Rules
The rules of a bio-inspired robot arm design:

> 1. No arm is fixed to the ground.
> 2. Every arm has a power supply.
> 3. Everything which has an arm, has learning.
> 4. Arms function without knowing the position of the feet.
> 5. Joints have limited rotation angles.
> 7. Every mass in an arm can contribute to a counterbalancing effort for motion.
> 8. Linear motion takes place in pairs of links.
> 9. The actuator of a joint is located in a superior link.
> 10. Structure supports static loads. Actuators support dynamic loads.
> 11. Force is never exerted with just one actuator.
>
> 5.1) * Rotation limit is set by tendons, which add strength & spring behavior.


### Rule for Precision
2023.11.14

Extreme precision will be engineered at low cost.

![laser pointer](https://m.media-amazon.com/images/I/61X6oZhH-YL._AC_SL1500_.jpg ':class=image-40')

Extreme precision at low cost:  Expensive modern arms range have a massive waste in design effort. The goal of precision is at the end-effector, nowhere else.  Modern industrial robots cost so much because they mechanically solve a problem that should be solved computationally.  Each joint is built with extremely fine tolerances, which stack up so that the 1mm movement at the wrist requires a 0.01mm precision at the shoulder.  In contrast, a human being peeling tying a fishing knot requires sub-milimeter precision while the elbow is free to move about.  This is the way.  

As Elon once said "Engineers are extremely good at optimizing solutions that shouldn't exist in the first place.  Designers have already solved 1mm accuracy at 100 meters lever arm length, for 20 USD. You'll find in a product such as a firearm [laser pointer](https://www.amazon.com/gp/product/B019Q05CNY), small knobs that make such a fine adjustment.  A $5 servo is capable of controlling these knobs.  Combining them is not difficult.  The rule here is that OpenArm elements will not be given precision and high-effort engineering in achieving what is already designed and available for purchase. At each moment that we stumble on a goal requiring very high effort, we will ask if that goal serves the robot function or if it simply serves to help with another goal.  By this question, we can biforcate between the useful from the useless targets, and design only useful modules.


# Machine Learning (AI)

This arm is intended for learning & feedback.  Instead of encoders and highly precise motion at every joint, the end-effector works like a person controls her hands.  We have a general sense of our elbow location but we don't perform fine control of the elbow to position the hands finely.

Kinematics will not drive the design. Rather, the motors, back-EMF, counterbalances, will cross-influence each joint. The bot is intended to evolve its performance through AI training (simulated and real-world).

The rigidity will be sufficient to perform simulations and learning without physical prototype, but less rigid than modern COTS arms.  Modern COTS designs always have a rigidity intended to meet the resolution of the kinematics equations.  Instead, low-force motion planning will be kinematically true but high-force or high-acceleration motion will be controlled through learning, and will not be possible without learning.

*️⃣ As noted above, no encoders required but some measurement of torque or current or derivatives thereof will become part of the control loop in time.


| State of the Art   | Benchtop Arm      | How the Robot Feels |
| ------------------ | ----------------- | ------------------- |
| ![UR3_setup](https://i.imgur.com/QSIwgy6.png) | ![UR3_benchtop](https://i.imgur.com/r9iqdeW.png) | ![snowboarder](https://i.imgur.com/kWtVqm7.jpg) |
| Privileged human (with 2 arms & mobile power-supply), sets robot (one arm and fixed power supply). 🎓7 | Heavy Rigid fixture is required to counteract reaction forces. | A human with one arm and feet strapped down. |

_If you search high and low for mobile manipulators, the arms can lift only a fraction of the base's capability_

| State of the art | How the Robot Feels |
| ---------------- | ------------------- |
| ![mobile manipulator](https://i.imgur.com/0HHbPZ1.jpg) | ![atlas_stones_competition](https://i.imgur.com/Kehy5rB.png) | 
| mobile base capable of 15kg payload, with arm of 2.2kg payload 🎓8 | Competitor in Atlas Stones bodybuilding with a yoga ball |

## Learning input/output

### Draft of machine learning scenario (2023.07)

A concept for method of achieving motion control without encoders or extreme rigidity:
* Stage 1) overhead camera captures fine motion resolution while all actuators sweep all command states + responses. (Encoders could be implemented or not) Dump all data into a model. Derive relationships between control inputs and motion outputs.
* Stage 1 step 2) Also derive a set of relationships between the wrist motion and current generated by elbow being back-driven by reaction torque.
* Stage 1 step 3)Derive it again for all 360 degrees of starting positions. Repeat for all joints relative to all other joints. (Note: this is also what an infant human baby does).
* Stage 2) use the math relationships from stage 1 on a robot with no encoders and no overhead camera to command actuators. Moving from “home” to any fixed position could be achieved within 5 degrees for each joint. With this method, move the wrist near a flower of known position relative to “home.”
* Stage 2 step 2) activate a low resolution wrist-mounted camera to adjust wrist and fingers, along with simple kinematics and known models, to pluck a pedal.

## Learning for Self-Design

(2023.10.18)

What if the robot can design itself for each application? I almost forgot to disclose this part of the discussion:  **Multidisciplinary Design Optimization,** or MDO for short, is a recent field in engineering that leverages computational power to co-optimize systems with interacting subsystems.  In a robot, some systems are power, mass, articulation, rigidity, among other aspects that can have severe tradeoffs when optimized independently.  For complex systems, an expert may find a great solution to optimize one aspect but is not fully aware of it's cross-interactions on other aspects.  One solution is to create a computer model which combines other models.  

In 2015 I took an amazing MDO course in the mechanical engineering department taught by Dr. Douglas Allaire at Texas A&M.  This subject was so inspiring that it became core to my [masters' thesis](https://oaktrust.library.tamu.edu/handle/1969.1/174238).  The approach of mathematically optimizing a system of systems takes a great deal of pre-calculation but there is one magical outcome:  After building the optimizer, we can adjust the constraints or the application for which our system is intended, and it will re-compute the optimal design.  Imagine selecting the best components for your new gaming PC build, for the overall best price and best metrics that you ask for.  Then, use the same optimizer to re-select parts for your colleagues CAD workstation.  This approach is a perfect pairing for a design like OpenArm and [SCUTTLE](https://www.scuttlerobot.org) which are highly modular and intended for broad applications.

After some progress is made, it will make sense to build an MDO solver around the OpenArm, and [SCUTTLE](https://scuttlerobot.org), and perhaps the combination of the two.

# Research Phase

## How it started

Ten years of pondering and working with robot arms, and CLICK! We can make them much better, and vastly less expensive.  Less rigid materials, less torque-intensive motors, and less fine control.  Here are some thoughts that came before the sketches.

<iframe width="640" height="360" src="https://www.youtube.com/embed/5sXRnYCKep4" title="Human-inspired &amp; Bio-inspired concepts NOT found in state of the art Robots" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Energy Regen

Energy regeneration is possible if we use DC motors rather than stepper motors.  A DC motor design is quite unique for a robot arm.  Usually stepper motors are used, except for extremely expensive encoded servos motors.

**The main purpose is NOT to recharge the battery! It is to A) make voltage and current available during transient states while motors work in tandem. B) to generate current in each actuator while other actuators move, giving a measurable parameter for realtime feedback.**

Elaborating on realtime feedback: when we move the elbow, the shoulder feels a reaction.  We generate a current in the shoulder motor that communicates the elbow motion, and it also dampens the elbow motion.  Taking control of the "braking" force as a variable, we can adjust the damping and control the power returned for a given elbow motion. When the hand grips a mass, we can recompute the desired damping in realtime and maintain the dynamic response of the whole system, or manipulate it.  When a tennis plater strikes a backhand, the right (forward arm) tricep transitions from pulling to releasing, allowing the arm to swing behind the shoulder (no braking).  When you shift a transmition lever into park, the tricep behavior is much differnt although the wrist is controlling the kinematics.  These different dynamics can be implemented through full control of reaction forces.  Poewr generation will naturally be a function of  reaction forces.

My first question: can energy regeneration be implemented with affordable OTS brushless motors?  If so, brushless outperforms brushed DC motors and is the way to go.

On Youtube, Oren made a detailed analysis of recharging batteries on a brushless powered skateboard (📖5) .  The [video is here](https://youtu.be/HmUrjAJ5_jA).   From my calculations, the best-case recharging trial recovered nearly 30% of spent energy.  Power was spent during an uphill drive and recovered by braking during during the downhill return.

| Data for Analysis | Chart: Key Takeaway |
| ----------------- | ------------------- |
| ![data](https://i.imgur.com/ShzraEz.png) | ![chart](https://i.imgur.com/NLUdTKq.jpg) |  

## Tendons & Ligaments

In biology, ligaments attach bone to bone, and tendons attach bone to muscle or otherwise serve mobility 🎓8. As of 2023.07, it's undecided whether to design with rigidity for attachments of motors and joints to the structure.  If the robot is given hard mechanical stops, it creates discrete discontinuities in the mobility and would be nonoptimal for machine learning.  If we introduce endstops that are elastic, then two benefits arrive: First, the end-stop behavior is continuous, and second, extra strength can assist the actuators near the limits.  (If you spread your arms and walk through a doorway, you can put a force on the door frame without using your pectoral muscles - that's the tendons helping you exert force for free - instead of using your own energy, you use a "spring force" which simply conservation of energy.  You recover your energy from the walking motion and load that into the spring which is in your shoulder.   

Implementation of rubber, silicone, or actual springs are worth considering throughout the design.  Muscle/bone attachment may manifest in the form of rubber pulleys instead of gears in the geartrain.  Rotation-limiting elastic would do a similar job to tendons at the end-stop configurations.

**Analysis 06.26:**

This analysis compares a battery-recharging test with my data from a Li-ion cell (similar curves) to estimate percentages.  Data from a discharge of Li-ion cell from 4.12v starting, no-load voltage is compared with Oren's data from a LiPo cell from 4.18v starting, no-load voltage.  Oren's batteries lost 5% of 4.12v at hilltop, giving 3.98v.  To gather energy data, I found the corresponding 95% of my Li-ion cell starting voltage, giving 0.95 * 4.12 = 3.91v.  At this voltage, my cell's energy consumption was 27% of capacity.  (capacity, assuming 3.0v equals 0% capacity and 4.12v = 100% capacity, taken from true samples of mWh discharged). The energy level in WH was noted from the corresponding sample, giving 27% energy reduction.The same method was used to trace Oren's 96% voltage value back to it's coresponding energy level and we see the difference between these samples show 72% energy recovery.   72% of the lost energy was still available at the recovery voltage. The energy loss from 95 to 94% voltage represents more than 70% of the energy loss from 100 to 94% voltage, due to nonlinearity of the Li-ion and LiPo chemistry.

## Slip Ring

I found a benchmark on-hand so I went ahead and disassembled my Craftsman utility jack which contains a slip ring.  They don't make it anymore but this design has LED's that spin with the plate where the jack lifts the car (crazy, right?)

| Slip Ring Base | LED Panel | Contacts | Insulating Polymer | Working LED's |
| -------------- | --------- | -------- | ------------------ | -------------- |
| ![slipring](https://i.imgur.com/nkjqnX5.jpg) | ![slipring](https://i.imgur.com/ug5mMmN.jpg) | ![slipring](https://i.imgur.com/k0VWEd7.jpg) | ![slipring](https://i.imgur.com/9PMD6mu.jpg) | ![slipring](https://i.imgur.com/im79b1v.jpg) |

**Takeaways 06.30**
1. This system lasted for 10 years!  I think that's a successful design to benchmark.
2. The slip ring probably only carries a few miliamps.  It's unclear if the same setup could be used to power motors with 5-10 amps.
3. The gaps are maintained fairly tightly (probably +/- 0.2mm) under operation, and the spring-backed contacts do a fine job of maintaining contact when the ring is spun.
4. The threaded cap is made from copper or brass, coated with chrome.  It carries the ground path back to the jack from the LED panel.  The chrome was delaminating, but the copper worked fine after.
5. This system carries up to 1 ton and can still rotate under load. However, there's a lot of friction: sliding action between the plastic film and the steel is the only way it spins.
6. The electrical contacts consist of steel-on-steel or steel pins on whatever material is shown in the 2nd image.  Again there's a tradeoff of wear-resistance versus conductivity.

 
# Build & Design Log

## December 2023

### Dec 29, 2023

Yesterday I had the pleasure of meeting Dr. David Surovik, employee 11 of Boston Dynamics' AI Institute.  He's actually a family member of a Texan friend of mine. This type of interaction (frequent, short meetings with deep experts) is critical, as robotics evolves so quickly.  Sometimes it evolves backwards, so we need to interact to avoid local minima.

My key "download" was basically the state of the art for robotics AI - there are some very ethical, good, hardworking people in the leading companies and the biggest question is regarding direction (what do we work on for the 5-year goal?) but everyone is doing their best.  I'm pleased to say there's nothing I learned that refutes the direction I'm establishing with OpenArm and SCUTTLE - that's great news.

### Dec 26, 2023

I've unburied my 2016 masters' thesis on Multidisciplinary Design Optimization of a Cubesat - an essential step in my understanding of how we will make robotics that evolve over time, and advance towards optimality.

You can find the video and a thoughtful description here in the youtube video:

[VIDEO LINK](https://youtu.be/XbSdwpLa4j4)

## June 2023

**Getting Started**

This deisgn will take a long time unless it becomes funded. Collaboration is encouraged.  Editing this repository is welcome.  Sharing comments & intellectual additions are encouraged by all.

Here are some early open design files.
| GrabCAD model of the first parts of the collar | [GrabCAD OpenArm](https://grabcad.com/library/openarm-2 ':class=button') |
| ---------------------------------------------- | ------------------------------------------------------------------------ |
| Photo album to share & collaborate | [Google Photo Album](https://photos.app.goo.gl/zSo8spTBcs2SwBfr6 ':class=button') |

**June 2023**

June 20

| Bearing loading with bb's, 4.5mm | Bearing on PVC, 60mm | Building Collars |
| -------------------------------- | -------------------- | ---------------- |
| ![Bearing 60mm on PVC](https://i.imgur.com/LxD7FG8.jpg) | ![bearing on pvc 60mm](https://i.imgur.com/3ticoLs.jpg) | ![img](https://i.imgur.com/GXAsp22.jpg) |

June 24

| early CAD model | gluing with PVC/ABS glue | Bearing tests 60mm & 89mm |
| --------------- | ------------------------ | ------------------------- |
| ![cad model](https://i.imgur.com/DGTnTfW.png) | ![PVC glue](https://i.imgur.com/uGdo5Hi.jpg) | ![5 bearings printed](https://i.imgur.com/ZZhuT2S.jpg)


June 25

| Steel balls, 9.5mm | Nylong Balls, 11.6mm | New CAD model - better parametrics |
| ------------------ | -------------------- | ---------------------------------- |
| ![cad model](https://i.imgur.com/2KZN6c2.jpg) | ![cad model](https://i.imgur.com/QbB7Jv3.png) | ![cad model](https://i.imgur.com/uohBkZG.png) |


The latest bearing uses these nylon balls from Amazon.com [link here](https://www.amazon.com/dp/B09WV4BZPC)

Here's a video testing out the bearing after printing:

<iframe width="640" height="360" src="https://www.youtube.com/embed/g5g48a-ZDeI" title="3D Printed Bearing with Nylon Balls" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

June 17: I am beginning modular design elements according with our "rules" and inviting the open community to collaborate.  Researchers, Makers, & Hackers Invited. 


| Bearing, affordable & printable   | Collar cross-section | Early conceptual sketch |
| --------------------------------- | -------------------- | ----------------------- |
| ![img1](https://d2t1xqejof9utc.cloudfront.net/screenshots/pics/42bde2079c49b20d65c9337484c22407/large.PNG) | ![img2](https://d2t1xqejof9utc.cloudfront.net/screenshots/pics/66d2971d7f5fd3bfa806faa31e257edc/large.png) | ![img3](https://d2t1xqejof9utc.cloudfront.net/screenshots/pics/97336228ee94392cfc37916c0e548c0c/large.jpg) |

## October 2023

October 15

| Prototype 2DOF | Prototype 2DOF |
| -------------- | -------------- |
| ![proto](https://i.imgur.com/8lMNrTj.jpg)) | ![proto2DOF](https://i.imgur.com/oqLZyIe.jpg) | 

This assembly moves nicely - now, deciding on the bearings and the motors will depend on the lifting task we wish to perform.  We can give more diameter to the members for greater rigidity, or make it light and fast.

October 20

| Quick Render| Motor Dimensions |
| ----------- | ---------------- |
| ![motor model](https://i.imgur.com/mhCejSM.png) | ![dimensions](https://i.imgur.com/8lfM9Xy.png) | 

Myself and collaborators went ahead and ordered a brushless motor to test integration.  This does not preclude us from using steppers or DC brushed motors later.   This month's challenge will be to look for the most elegant integration that leaves us with a parametric assembly.  Let's tie in these motors in such a way that changing motors will not pin down the design to one geometry.

**Unidirectional** By accident, we picked a controller (usually for RC planes) which spins only one direction.  At first it was a mistake - now I am on a thinking path about keeping it.  Your bicep only actuates in one direction.  Maybe that's a clever way to design a robot as well!  Later I can discuss how this could be an advantage.


# How You Can Help

| [Github Repo](https://github.com/dmalawey/OpenArm ':class=button') 
| [Website](https://docsify-this.net/?basePath=https://raw.githubusercontent.com/dmalawey/OpenArm/main&sidebar=true#/?show-page-options=true ':class=button')
| 

## Why help?:

Most robot arms have missed the point of arms, and we should improve on this.

| Key Point | Our current robot arms:                                      | How God Designs arms:                                                    |
| --------- | ------------------------------------------------------------ | ------------------------------------------------------------------------ |
| 1         | One design = one product                                     | Make one design with many derivative instantiations                      |
| 2         | Energy is unlimited, and plugged in                          | Energy is portable, arms are portable                                    |
| 3         | Base receives high reaction forces.                          | Base sees no reaction forces OR reaction force contributes to the motion |
| 4         | Base must be rigidly secured.                                | Base may move.                                                           |
| 5         | Has rare materials like aircraft-aluminum                    | Has common materials like hydrocarbons.  :mortar_board: 3                |
| 6         | Components cost is imbalanced:<br>Muscles > Joints > members | Components cost is balanced:<br>muscles = joints = members               |
| 7         | Each joint receives independent control.                     | Joints are controlled together.                                          |


## Mechanical
* Building: I could use builders in parallel or in series - plenty of mistakes will need resolutions.  You may build an early revision that becomes overwritten but I guarantee you won't build anything without learning.  I will be building this project one module at a time.  Then we will need to resize it for various budgets or tasks.
* Design decisions: how much counterweight to add behind each joint?  where to place the counterweight?  Which parameters to build into the components vs build into the assemblies?  (does a long arm need just a longer member or a whole configuration of the assembly?  How can we input materials to keep the local center of gravity in the centerline of each joint?
* Modeling:  Lots of modeling to do. We can collaborate in solidworks or begin the equivalent designs in Fusion360 or other popular software.  We want this design to be as open and repeatable as possible so multiple formats are desired.
* Which nominal belts and pulleys are best suited, to leave space for increasing and decreasing the scale of the arm?  Are there kits to be bought in sets that have a high value, such as 3D printer actuators?
* Energy regeneration is important.  How can we select a motor type which balances high performance with useful regeneration?  This video from [Oren's Projects on youtube](https://youtu.be/HmUrjAJ5_jA?t=389) shows that energy regeneration for common brushless motors is negligible when measured in voltage.  But, we need to measure in energy.  Do we need to stay with bipolar DC motors in order for energy to return during backdriving?

## Electronics
* Our starting point is a 12v dc motor from the SCUTTLE robot.  It's a gearmotor - but which is the best choice for a base publication?  How will we route the wires through each member?  Should we make a variation of the bearings that have a slip ring?  can we prototype a bearing that has a slip ring functioning?
* Are there some off-the-shelf motor driver arrays from another application (like 3d printers, but for DC motors) that have a low-low cost?
* Is it possible to plan for both DC and Stepper motors simultaneously?  How big of an electrical mess is made if we backdrive the stepper motors?
* What standard OTS boards should the mechanical team make space for interior to the joints and members?
* Can the whole robot communicate with i2c?  Do we need somethign more robust like CAN-bus?
* We wish to recapture energy (even tiny amounts) when the small arm swings and backdrives the larger member.  how can we switch responsively between motor driving, motor breaking, and energy recap?
* Note: the purpose of energy recapture isn't to try to conserve all energy, it's to maintain in our models that the consumption will vary based on this - and gain understanding of the interactions so they can be modeled.

## Software
* which are the first models necessary to begin simulation?  what parameters do we need to output to help the simulation team operate effectively?  Are there some university or research courses currently operating on digital plans that we could offer this design to?  That's a win-win, then they could align their digital simulations with our design to give more meaning to their exercises.
* What measurements should be taken at what frequency?  Can we get away with no encoders at all?  Perhaps with a top-down camera the whole system could be tested under machine-vision learning.
* How should we assign variables and capture the performance metrics that come from software simulation?  What is the software control system, minimal-viable, that must be implemented to get a rough control scenario working on a real model?  Can we get away with something as cheap as an arduino?

## Documentation
* This project will be highly multidisciplinary in order to be successful.  To attract great talent, we need to make the physics & data very clear.  And to provide native design files for each element, as well as a clear BOM. 
* My recommendations
  1. BOM itemS - directly here in the readme.md, in a markdown table
  2. CAD data - grabCAD is preferred, using subdirectories for IMG, STEP, SOLIDWORKS
  3. Version numbers - add a version to each item and collection of items that may need repeating.  Use vX.XX please.
  4. Videos - Let's post on youTube and link here in markdown.  I can build a playlist as it grows.
  5. Discussion - best place to discuss this, TBD.  Feel free to comment on any of our postings to begin.

# References

| [Github Repo](https://github.com/dmalawey/OpenArm ':class=button') 
| [Website](https://qr.page/g/2wY5JrxcciD ':class=button')
|

## Credits 👍

> _giving credit to prior works and contributions_
> 
> 1. Daniel Amuedo's design of the first parametric bearing, adapted for joints. His youtube channel is [Dangineering](https://www.youtube.com/@Dangineering).  I revised his [original solidworks model](https://www.printables.com/model/263264-200mm-bore-5mm-bore-cheap-ultra-thin-parametric-ba/filess) to get my bearing to print nicely, then further changed it to become part of a collar joint.  Thanks Daniel!
> 2. Oren's review on E-skateboard regenerative braking.  This data helps steer us to the right type of motor.  [Oren's Projects](https://youtu.be/HmUrjAJ5_jA?t=389)

## Sources 📖

> _Sources used in producing the project & documentation_
>
> 1. Markdown icons list [on github](https://gist.github.com/rxaviers/7360908#file-gistfile1-md)
> 2. Enhance image resolution online [cutout.pro](https://www.cutout.pro/photo-enhancer-sharpener-upscaler/upload)
> 3. Fonts from [Google Fonts](https://fonts.google.com/?query=robo)
> 4. Human Sketches from [Royal Collection Trust](https://www.rct.uk/collection/919013/the-muscles-of-the-shoulder-and-arm-recto-the-muscles-of-the-shoulder-and-arm-and)
> 5. Energy Regeneration trials from youtube [Oren's Projects](https://youtu.be/HmUrjAJ5_jA)
> 6. Icon Generator online [ICO-convert](https://icoconvert.com/)

## References 🎓

> _References in the discussion_
> These are referred above using icon and number such as :mortar_board: 1
>
> 1. GummiArm Project: A Replicable & Variable-stiffness Robot Arm [PDF Journal article](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8963345/pdf/fnbot-16-836772.pdf), [Youtube demo](https://youtu.be/ytCcpD84Jt0), and [Github Repository](https://github.com/mstoelen/GummiArm)
> 2. SCARA Arm example, Pybot, opensource, [Hackaday writeup](https://hackaday.io/project/175419-pybot-scara-robotic-arm-3d-printed-python)
> 3. What Bones are made of: NIH [webpage](https://www.niams.nih.gov/health-topics/what-bone#:~:text=Bone%20is%20made%20of%20protein,the%20bone%20can%20resist%20breaking.)
> 4. What Robot Arms are made of: Makeitfrom [Aluminums](https://www.makeitfrom.com/material-properties/6061-AlMg1SiCu-3.3214-H20-A96061-Aluminum)
> 5. Setup of UR Robot Arm: [universal robots video](https://video.universal-robots.com/ur-3-unboxing-video)
> 6. Fixtures for UR Robot: [Vention.io](https://vention.io/designs/ur5-robot-tending-bench-35492)
> 7. UR3e robot manual [PDF](https://s3-eu-west-1.amazonaws.com/ur-support-site/105370/99202_UR5_User_Manual_en_Global.pdf)
> 8. Chicken wing dissection [PDF guide](https://assist.asta.edu.au/sites/assist.asta.edu.au/files/SOP%20Performing%20a%20chicken%20wing%20dissection.pdf)
> 9. Kinova Robot Arm Manual [PDF](https://drive.google.com/file/d/1xQbkx1-v3SfAentKR9f3p3c2SVdViyQl/view)
> 10. Leonardo Da Vinci, 1452 [Repository by RCT](https://www.rct.uk/collection/919013/the-muscles-of-the-shoulder-and-arm-recto-the-muscles-of-the-shoulder-and-arm-and)
