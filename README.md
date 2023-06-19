![openarm banner](/img/banner_openArm.png)

# OpenArm
_An open-source robot arm_

> **PURPOSE: to design a robot arm using bio-inspiration for higher modularity and higher loads than leading commercial designs in 2023.**

| [Github Repo](https://github.com/dmalawey/OpenArm ':class=button') 
| [Website](https://docsify-this.net/?basePath=https://raw.githubusercontent.com/dmalawey/OpenArm/main&sidebar=true#/?show-page-options=true ':class=button')
| 

June 17: I am beginning design for a robot arm and invite the open community to collaborate.  Researchers, Makers, & Hackers Invited. 


| Bearing, affordable & printable   | Collar cross-section | Early conceptual sketch |
| --------------------------------- | -------------------- | ----------------------- |
| ![img1](https://d2t1xqejof9utc.cloudfront.net/screenshots/pics/42bde2079c49b20d65c9337484c22407/large.PNG) | ![img2](https://d2t1xqejof9utc.cloudfront.net/screenshots/pics/66d2971d7f5fd3bfa806faa31e257edc/large.png) | ![img3](https://d2t1xqejof9utc.cloudfront.net/screenshots/pics/97336228ee94392cfc37916c0e548c0c/large.jpg) |


## Characteristics:

* 3D Printable + OTS
* VERY affordable
* Using DC motors, M2 Belts, and M2 pulleys like those of 3D printers
* having no encoders required *️⃣
* bio-inspired - having damping forces and torque stack additively along joints. 
* Digital-Twin oriented - the simulated design shall represent the real implementation sufficiently to simulate motion.
* interchangeable motors & pulleys - the joint geometry leaves space internally for changes.

### Mechanical
* Payload Target = 1kg
* Derived from SCARA configuration to enhance payload
* Hope to derive encoder-like function of Motor "n" from measurement of reaction torque at motor "n-1"
* All motor assemblies to be backdrivable
* Modular - multi-DOF, selectable
* Parametric - change the size as you wish
* Rigid frame - components will not have intentional compliance or antagonistic actuators

## AI Intentions
Instead of encoders and highly precise motion at every joint, this arm is intended to control the end-effector like a person controls their hands.  We have a general sense of our elbow location but we don't perform fine control of the elbow to position the hands finely.  

Kinematics will not be easy as the motors, back-EMF, etc will cross-influence one joint to another.  Instead, the bot is intended to evolve its performance through AI training (simulated and real-world).

*️⃣ As noted above, no encoders required but some measurement of torque or current or derivatives thereof will become part of the control loop in time.

| State of the Art   | Benchtop Arm      | How the Robot Feels |
| ------------------ | ----------------- | ------------------- |
| ![UR3_setup](https://i.imgur.com/CmJoOIh.png) | ![UR3_benchtop](https://i.imgur.com/r9iqdeW.png) | ![snowboarder](https://i.imgur.com/ItancgQ.png) |
| Privileged human with mobile power & two arms, sets robot with fixed power & one arm. 🎓7 | Rigid benchtop to counteract reaction forces. | Human withone arm, and feet strapped down. |

_If you search high and low for mobile manipulators, the arms can lift only a fraction of the base's capability_

| State of the art | How the Robot Feels |
| ---------------- | ------------------- |
| ![mobile manipulator](https://i.imgur.com/XRKMbMa.jpg) | ![atlas_stones_competition](https://i.imgur.com/Kehy5rB.png) | 
| mobile base capable of 15kg payload, with arm of 2.2kg payload 🎓8 | Competitor in Atlas Stones bodybuilding with a yoga ball |

## How it started
Ten years of pondering and working with robot arms, and CLICK! We can make them much better, and vastly less expensive.  Less rigid materials, less torque-intensive motors, and less fine control.  Here are some thoughts that came before the sketches.

<iframe width="640" height="360" src="https://www.youtube.com/embed/5sXRnYCKep4" title="Human-inspired &amp; Bio-inspired concepts NOT found in state of the art Robots" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


# Build & Design Log

## Getting Started
This deisgn will take a long time as it's not my priority project.  Collaboration is welcome.  Editing this repository is welcome.  Sharing comments & intellectual additions are encouraged by all.

Here's a grabCAD model of the first parts of the collar.
[GrabCAD OpenArm](https://grabcad.com/library/openarm-2 ':class=button')


Soon I'll Post a video of the initial bearing assembly.

A photo album to begin sharing photos
[Google Photo Album](https://photos.app.goo.gl/zSo8spTBcs2SwBfr6 ':class=button')

Let's see if I can post an image of an early sketch:
![sketch 1](https://photos.app.goo.gl/fd8ezmeAaVzynse1A)

# How You Can Help

| [Github Repo](https://github.com/dmalawey/OpenArm ':class=button') 
| [Website](https://docsify-this.net/?basePath=https://raw.githubusercontent.com/dmalawey/OpenArm/main&sidebar=true#/?show-page-options=true ':class=button')
| 

## Why you should help:

Most robot arms have missed the point of arms, and we should improve on this.

| Key Point | Our current robot arms:                                      | How God Designs arms:                                                    |
| --------- | ------------------------------------------------------------ | ------------------------------------------------------------------------ |
| 1         | One design = one product                                     | Make one design with many derivative instantiations                      |
| 2         | Energy is unlimited, and plugged in                          | Energy is portable, arms are portable                                    |
| 3         | Base receives high reaction forces.                          | Base sees no reaction forces OR reaction force contributes to the motion |
|           | Base must be rigidly secured.                                | Base may move.                                                           |
| 4         | Has rare materials like aircraft-aluminum                    | Has common materials like hydrocarbons.  :mortar_board: 3                |
| 5         | Components cost is imbalanced:<br>Muscles > Joints > members | Components cost is balanced:<br>muscles = joints = members               |
| 6         | Each joint receives independent control.                     | Joints are controlled together.                                          |


## Mechanical Needs
* Building: I could use builders in parallel or in series - plenty of mistakes will need resolutions.  You may build an early revision that becomes overwritten but I guarantee you won't build anything without learning.  I will be building this project one module at a time.  Then we will need to resize it for various budgets or tasks.
* Design decisions: how much counterweight to add behind each joint?  where to place the counterweight?  Which parameters to build into the components vs build into the assemblies?  (does a long arm need just a longer member or a whole configuration of the assembly?  How can we input materials to keep the local center of gravity in the centerline of each joint?
* Modeling:  Lots of modeling to do. We can collaborate in solidworks or begin the equivalent designs in Fusion360 or other popular software.  We want this design to be as open and repeatable as possible so multiple formats are desired.
* Which nominal belts and pulleys are best suited, to leave space for increasing and decreasing the scale of the arm?  Are there kits to be bought in sets that have a high value, such as 3D printer actuators?

## Electronics Needs
* Our starting point is a 12v dc motor from the SCUTTLE robot.  It's a gearmotor - but which is the best choice for a base publication?  How will we route the wires through each member?  Should we make a variation of the bearings that have a slip ring?  can we prototype a bearing that has a slip ring functioning?
* Are there some off-the-shelf motor driver arrays from another application (like 3d printers, but for DC motors) that have a low-low cost?
* Is it possible to plan for both DC and Stepper motors simultaneously?  How big of an electrical mess is made if we backdrive the stepper motors?
* What standard OTS boards should the mechanical team make space for interior to the joints and members?
* Can the whole robot communicate with i2c?  Do we need somethign more robust like CAN-bus?
* We wish to recapture energy (even tiny amounts) when the small arm swings and backdrives the larger member.  how can we switch responsively between motor driving, motor breaking, and energy recap?
* Note: the purpose of energy recapture isn't to try to conserve all energy, it's to maintain in our models that the consumption will vary based on this - and gain understanding of the interactions so they can be modeled.

## Software Needs
* which are the first models necessary to begin simulation?  what parameters do we need to output to help the simulation team operate effectively?  Are there some university or research courses currently operating on digital plans that we could offer this design to?  That's a win-win, then they could align their digital simulations with our design to give more meaning to their exercises.
* What measurements should be taken at what frequency?  Can we get away with no encoders at all?  Perhaps with a top-down camera the whole system could be tested under machine-vision learning.
* How should we assign variables and capture the performance metrics that come from software simulation?  What is the software control system, minimal-viable, that must be implemented to get a rough control scenario working on a real model?  Can we get away with something as cheap as an arduino?

## Documentation Needs
* This project will be highly multidisciplinary in order to be successful.  To attract great talent, we need to make the physics & data very clear.  And to provide native design files for each element, as well as a clear BOM. 
* My recommendations
  1. BOM itemS - directly here in the readme.md, in a markdown table
  2. CAD data - grabCAD is preferred, using subdirectories for IMG, STEP, SOLIDWORKS
  3. Version numbers - add a version to each item and collection of items that may need repeating.  Use vX.XX please.
  4. Videos - Let's post on youTube and link here in markdown.  I can build a playlist as it grows.
  5. Discussion - best place to discuss this, TBD.  Feel free to comment on any of our postings to begin.

## References

| [Github Repo](https://github.com/dmalawey/OpenArm ':class=button') 
| [Website](https://docsify-this.net/?basePath=https://raw.githubusercontent.com/dmalawey/OpenArm/main&sidebar=true#/?show-page-options=true ':class=button')
| 

### Credits

> _giving credit to prior works of art in this project_
> 
> * I collected the first parametric bearing part from Daniel Amuendo's design - his channel is [Dangineering](https://www.youtube.com/@Dangineering) on youtube.  I revised his [original solidworks model](https://www.printables.com/model/263264-200mm-bore-5mm-bore-cheap-ultra-thin-parametric-ba/filess) to get my bearing to print nicely, then further changed it to become part of a collar joint.  Thanks Daniel!
>

### Sources

> _Sources used to produce this documentation and project_
>
> 1. Markdown icons list [on github](https://gist.github.com/rxaviers/7360908#file-gistfile1-md)
> 2. Enhance image resolution online [cutout.pro](https://www.cutout.pro/photo-enhancer-sharpener-upscaler/upload)
> 3. Fonts from [Google Fonts](https://fonts.google.com/?query=robo)

### References :mortar_board:

> _References are referred above using icon and number such as :mortar_board: 1
>
> 1. GummiArm Project: A Replicable & Variable-stiffness Robot Arm [PDF Journal article](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8963345/pdf/fnbot-16-836772.pdf), [Youtube demo](https://youtu.be/ytCcpD84Jt0), and [Github Repository](https://github.com/mstoelen/GummiArm)
> 2. SCARA Arm example, Pybot, opensource, [Hackaday writeup](https://hackaday.io/project/175419-pybot-scara-robotic-arm-3d-printed-python)
> 3. What Bones are made of: NIH [webpage](https://www.niams.nih.gov/health-topics/what-bone#:~:text=Bone%20is%20made%20of%20protein,the%20bone%20can%20resist%20breaking.)
> 4. What Robot Arms are made of: Makeitfrom [Aluminums](https://www.makeitfrom.com/material-properties/6061-AlMg1SiCu-3.3214-H20-A96061-Aluminum)
> 5. Setup of UR Robot Arm: [universal robots video](https://video.universal-robots.com/ur-3-unboxing-video)
> 6. Fixtures for UR Robot: [Vention.io](https://vention.io/designs/ur5-robot-tending-bench-35492)
> 7. UR3e robot manual [PDF](https://s3-eu-west-1.amazonaws.com/ur-support-site/105370/99202_UR5_User_Manual_en_Global.pdf)
> 8. Kinova Robot Arm Manual [PDF](https://drive.google.com/file/d/1xQbkx1-v3SfAentKR9f3p3c2SVdViyQl/view)
