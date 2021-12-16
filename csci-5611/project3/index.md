# CSCI 5611: Project 3 -- Optimization-Based Animation

## Group

* Alexandra Hanson (hans7203)

## Attempted features

I have completed the following features:

* Multi-arm IK (at least 2D)
* Moving IK (at least 2D)
* Joint limits
* User Interaction
* Alternative IK Solver

## About (& some reflection)

This is a project for CSCI 5611: Animation and Planning in Games that uses 
optimization based approaches to implement inverse kinemantics for a basic
skeleton. (I apologize that my simulation is very simple!)

### Inverse Kinematics Scenario

The first IK solver I implemented used the cyclic coordinate descent approach to
animate the arms of a spider skeleton reaching toward a goal. The goal here was 
the current coordinates of the mouse to allow for user interaction with the scene. I
consider this the primary IK solver I implemented since I found it looked the
most natural.

For the spider animation, I created an "Arm" library which stores as floats the 
lengths, angles, and joint speeds of each component making up the arm. 
Additionally, I used Vec2s as positions for where the arm is rooted in place, 
the starting places of each arm component, and the endpoint. I also have an 
array of Vec2s that represent the joint limits of each arm component, where the
"x" is a minimum and the "y" is a maximum degree (in radians) around the unit
circle. Deciding these minimums and maximums was actually quite difficult -- I
was constantly referencing a unit circle and thinking about the angle at which
each component was resting in order to debug and tune my parameters.

In the Arm library, I have my CCD IK solver (as well as the Jacobian solver),
along with methods to check the joint limits, draw the arm, and do the actually
forward kinemantic computation.

In addition to the spider skeleton, I also created an animation "walk" that
implements a moving IK system. The movement produced does not really look like
walking because I was not able to figure out how to use joint limits to restrict
the skeleton's movement; however, it does successfully move across the screen by 
changing the root of the skeleton. I give it a number of a goal points along the
floor and each time a goal is reached, the root of the skeleton changes and I
reverse the skeleton data so that the movement appears seemless and connected.

The computation here uses a CCD solver within a library called "Legs" which is
very similar to the library for the Arm in my spider simulation. In this 
library, I add an array of goal positions and iterate through it to move the 
skeleton across the screen.

### Comparative analysis

The alternative IK solver I chose to implement was the Jacobian matrix method.
This thing was a doozy! But I was finally able to get it working. I initially
tried to do so for 2-dimensions and became confused by the axis of rotation
(there is not really one in 2d) so my workaround was to translate my endPoint
into 3d and use a 3 vector (0, 0, 1) for my axis of rotation. This was probably
silly of me but I was able to compute the Jacobian matrix this way.

The Jacobian solver uses the same angle limits, joint speeds, etc. as the 
CCD-solver, so they should be quite similar. However, you can see in the video 
of the spider with the Jacobian solver that it looks much less natural and is
quite jittery. This could be because I may not have implemented it perfectly.
In any case, comparing the two, I found that

1. The movement produced by my CCD looked much more natural than that of my
Jacobian solver.
2. The Jacobian matrix method was way harder to implement! It took me a lot of
time and reading to figure out exactly what was going on. I generally found it
less intuitive.

## Code

I have a private repository that contains my work for the course. It should be 
shared with Prof. Guy and Dan. The code for the "spider" animation should be
linked at 
[csci-5611-animation-and-planning-in-games/assignments/project3/spider/](https://github.com/alexandra-hanson/csci-5611-animation-and-planning-in-games/tree/main/assignments/project3/spider)
and the code for the "walking" animation should be linked at
[csci-5611-animation-and-planning-in-games/assignments/project3/walk/](https://github.com/alexandra-hanson/csci-5611-animation-and-planning-in-games/tree/main/assignments/project3/walk).

## Media

I implemented the following features, which you can see in the different videos 
below.

### Simulation : Spider

**CCD SOLVER**

This first video I consider my "baseline." I used a CCD solver with joint limits
to create the animation below:

<iframe width="560" height="315" src="https://www.youtube.com/embed/uQrM6lJb8wY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

| **Component**      | **Timestamps** |
| ----------- | ----------- |
| Multi-arm IK (CCD approach) | Whole video |
| Joint limits | Whole video |
| User interaction | Whole video |

In contrast, you can see the same solver without joint limits below. The legs
bunch together and move extremely quickly -- not very natural looking at all!

<iframe width="560" height="315" src="https://www.youtube.com/embed/cGfC8nlMPw0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

**JACOBIAN MATRIX METHOD**

I implemented a Jacobian IK solver for my alternative approach. This next video
shows this approach with the same features as the first CCD solver above (i.e.
multi-arm IK, joint limits, and user interaction).

<iframe width="560" height="315" src="https://www.youtube.com/embed/07DZA5a7B90" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

| **Component**      | **Timestamps** |
| ----------- | ----------- |
| Multi-arm IK | Whole video |
| Joint limits | Whole video |
| User interaction | Whole video |
| Alternative IK Solver (Jacobian matrix method) | Whole video |

### Simulation : "Walking"

I hesitate to call this walking since I wasn't able to get this work with joint
limits. However, my IK system does move across the screen by changing the root
of the skeleton based on which node is currently touching the floor, so this
should be considered moving IK.

<iframe width="560" height="315" src="https://www.youtube.com/embed/jknES7rTzv4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

| **Component**      | **Timestamps** |
| ----------- | ----------- |
| Moving IK | Whole video |

## Credit

* I largely followed this [Overview of Jacobian IK](https://medium.com/unity3danimation/overview-of-jacobian-ik-a33939639ab2)
   * This helped me a great deal in understanding and implementing the algorithm
     in Processing
* I again used the Vec2 library provided in the first homework assignment and 
modified it for 3d to use for the Jacobian IK solver