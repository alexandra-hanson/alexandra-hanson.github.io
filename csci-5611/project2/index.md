# CSCI 5611: Project 2 -- Physically-Based Animation with PDEs

## Group

* Alexandra Hanson (hans7203)

## Attempted features

I have completed the following features:

* Multiple Ropes (at least 2D)*
* Cloth Simulation
* 3D Simulation & Rendering
* User Interaction
* SPH Fluid Simulation

## About (& some reflection)

This is a project for CSCI 5611: Animation and Planning in Games that uses numerical integration to simulate 1) cloth and 2) water.

### Cloth Simulation

My cloth simulation uses an abstract mass spring representation of particles connected by spring dampers. I use 2D arrays to track the particle positions and velocities. In my `update` function, I use two nested for-loops to seperately compute the "horizontal" and "vertical" forces on a given particle before using these to update the velocity and position of the particle. I also use a simple approach of computing distance to detect if a particle is colliding with the sphere; I then bounce the particles upon collision using a small COR. To simulate the cloth's surface, I use a triangle mesh to connect adjacent particles.

I implemented simple user interaction with the scene by allowing the user to move the mint-colored sphere along the x- and y-axis. The relevant keys for this are: `o` to go up, `k` to go left, `;` to go right, and`k` to go down. I used the provided example camera code to navigate perspective in the scene -- the key mappings for this did not change from the original code.  

### SPH Fluid Simulation

To simulate water, I use an SPH fluid simulation. Here, I use an array to keep track of the current particle positions, the "old" particle positions, velocities, pressures, and densities. For each pair of particles that are within some distance -- i.e. within the smoothing radius -- I compute separation and cohesion forces based on the target densities of each given particle. I created a `Pair` class to store my `q`, `q2`, and `q3` values that are used in the computation of the pressure and displacement for a given particle.

For the fluid simulation, I generate particles above that drip down into the pool of water to create ripple effects. As particles are generated, their relevant information is added to my particle arrays.

### Reflection

I think both of these simulations turned out decently. What took the most time was tuning parameters to create the most effective scene. If I'd had more time, I would have liked to 1) For the cloth simulation, add a check to see if any part of my triangle mesh was colliding with the sphere rather than just the particle positions; and 2) Figure out how to make my fluid simulation look more like water rather than jittery particles.

## Code

I have a private repository that contains my work for the course. It should be shared with Prof. Guy and Dan. The cloth simulation should be linked at [csci-5611-animation-and-planning-in-games/assignments/project2/cloth/](https://github.com/alexandra-hanson/csci-5611-animation-and-planning-in-games/tree/main/assignments/project2/cloth) and the sph fluid simulation should be linked at [csci-5611-animation-and-planning-in-games/assignments/project2/water/](https://github.com/alexandra-hanson/csci-5611-animation-and-planning-in-games/tree/main/assignments/project2/water).

## Media

I implemented the following features, which you can see in the two videos below.

### Cloth Simulation

<iframe width="560" height="315" src="https://www.youtube.com/embed/dMBGsU7PwBU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

| **Component**      | **Timestamps** |
| ----------- | ----------- |
| Multiple Ropes (at least 2D)* & Cloth Simulation | 0:03, (and whole video) |
| User Interaction | 0:33, user controls mint sphere by keys `o`, `k`, `l`, and `;` |
| 3D Rendering | 1:01, change in camera angle and position |
| 3D Simulation | whole video |

### SPH Fluid Simulation

<iframe width="560" height="315" src="https://www.youtube.com/embed/VpA5LzJUj38" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Art Contest Submission

My animations are simple but I still want to submit for the art contest.

![](art-contest.png)

## Credit

As you can tell from the video and project repository, my project was pretty simple but I did use more external resources this time!

I used the following code from Canvas for my camera controller:

* [Processing Example: 3D Camera Code](https://canvas.umn.edu/courses/268733/files/22917781?module_item_id=6799649)
* The Vec2 library provided in the first homework assignment (I used this library as is for the SPH fluid simulation, and modified it for 3D for my cloth simulation)

I also used the pseudocode provided by Prof. Guy during lecture as a jumping off point for both of these simulations.