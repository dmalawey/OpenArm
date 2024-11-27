## Characteristics

Version 1
* Bio-inspired - having damping forces and torque relationships similar to a human arm. 
* Digital-twin oriented - the simulated design shall represent the real implementation sufficiently to simulate motion.
* Parametric design - the geometry leaves space for variations and modifications of internals & frame.
* Having no encoders required *️⃣

An initial builds should aim for low cost, usually achieved with 3D Printable + OTS parts.  It should serve to validate dynamics models, test feedback control functions, establish parameters for further development. Ie, instead of aiming for a torque at a joint, we derive a dynamic function that better relates to the capability of end-effector.  A system using DC motors, M2 Belts, and M2 pulleys like those of 3D printers is likely to serve the purpose of a first build.  A 1-kg payload target is well-matched to this hardware.


| Biological Sketch   | Biological sketch with motors identified | Robot Arm concept with motors |
| --------------------------------- | -------------------- | ----------------------- |
| ![davinci1](https://i.imgur.com/8pUq4JF.jpg) | ![davinci_markup](https://i.imgur.com/iho4c2z.jpg) | ![vitruvian_robot_arm](https://i.imgur.com/e5CzMqP.jpg) |

### Mechanical
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

Extreme precision will be engineered at low cost.  How?

![laser pointer](https://m.media-amazon.com/images/I/61X6oZhH-YL._AC_SL1500_.jpg ':class=image-40')

Extreme precision at low cost:  Expensive modern arms range have a massive waste in design effort, demanding intensive precision from a mechanical team and only subsequently passing the system to a software team. The goal of precision is at the end-effector, nowhere else. Modern industrial robots cost so much because they mechanically solve a problem that should be solved computationally.  Each joint is built with extremely fine tolerances, which stack up so that the 1mm movement at the wrist requires a 0.01mm precision at the shoulder.  In contrast, a human being tying a fishing knot requires sub-milimeter precision while the elbow is free to deviate broadly.  This is the right way.  

As Elon once said "Engineers are extremely good at optimizing solutions that shouldn't exist in the first place."  Designers have already solved 1mm accuracy at 100 meters lever arm length, for 20 USD. You'll find in a product such as a firearm [laser pointer](https://www.amazon.com/gp/product/B019Q05CNY), small knobs that make such a fine adjustment.  A $5 servo is capable of controlling these knobs.  Combining them is not difficult.  The rule here is that OpenArm elements will not be given precision and high-effort engineering in achieving what is already designed and available for purchase. At each moment that we stumble on a goal requiring very high effort, we will ask if that goal serves the robot function or if it simply serves to help with another goal.  By this question, we can biforcate between the useful from the useless targets, and design only useful modules.


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

## Self-Design

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

Elaborating on realtime feedback: when we move the elbow, the shoulder feels* a reaction.  We can (in robot) generate a current in the shoulder motor that communicates the elbow motion, and it also dampens the elbow motion.  Taking control of the "braking" force as a variable, we can adjust the damping and control the power returned for a given elbow motion. When the hand grips a mass, we can recompute the desired damping in realtime and maintain the dynamic response of the whole system, or manipulate it.  When a tennis plater strikes a backhand, the right (forward arm) tricep transitions from pulling to releasing, allowing the arm to swing behind the shoulder (no braking).  When you shift a transmition lever into park, the tricep behavior is much differnt although the wrist is controlling the kinematics.  These different dynamics can be implemented through full control of reaction forces.  Poewr generation will naturally be a function of  reaction forces.

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
