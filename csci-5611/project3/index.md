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
skeleton.

### Inverse Kinematics Scenario

The first IK solver I implemented used the cyclic coordinate descent approach to
animate the arms of a spider reaching toward a goal. The goal here was the
current coordinates of the mouse to allow for user interaction with the scene. I
consider this the primary IK solver I implemented since I found it looked the
most natural.

### Comparative analysis

Placeholder text

### Reflection

Placeholder text

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

* Algorithm for Jacobian IK: https://medium.com/unity3danimation/overview-of-jacobian-ik-a33939639ab2