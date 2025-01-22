---
layout: default
title: Particle
nav_order: 15
parent: Uni-verse Interface
grand_parent: Working in Uni-verse Studio
---
# Particle

THIS IS WORK IN PROGRESS

The Particle window streamlines the process of creating dynamic visual effects for your game. Starting with a template provides you with a foundation of pre-configured settings, allowing you to quickly iterate and customize your effects. These templates serve as practical starting points for common effects like fire, smoke, explosions, or magical abilities.

Once you've created your particle system, a wide selection of properties awaits your fine-tuning. The duration setting controls how long your effect plays, while looping determines whether it repeats continuously or plays once and stops. Emission settings govern the rate and pattern of particle generation, fundamentally shaping how your effect builds and maintains itself.

## Main

This component includes system-wide settings that influence all aspects of particle behavior. These settings primarily determine the starting conditions for particles when they first spawn.

![Main]({{site.url}}{{site.baseurl}}/content/images/particle-1-main.png)

**Duration:** The duration for which the particle system remains active
**Looping:** If enabled, the system will automatically restart after completing its duration, creating an endless loop of particle emissions
**Prewarm:** If enabled, the system begins as if it had already run through one complete cycle, simulating a mid-loop state
**Start Delay:** Delay in seconds before the first particles start appearing
**Start Lifetime:** The initial lifetime for particles
**Start Speed:** The initial speed of each particle
**Start Size:** The initial size of each particle
**Start Rotation:** The initial rotation angle of each particle
**Start Color:** The initial color of each particle
**Gravity Source:** Source of gravity for each particle
**Gravity Modifier:** Multiplier for the global gravity
**Simulation Space:** The setting that determines if particles move according to the parent object's coordinate system (following its movements), exist independently in world coordinates, or track the motion of a specified custom object
**Simulation Speed:** Multiplier for the operation speed
**Scaling Mode**: Determines how scaling is applied from the transform component. You can select between Hierarchy, Local, or Shape modes. Local mode only considers the Particle System's own transform scale, disregarding parent object scaling. Shape mode affects particle starting positions while leaving their dimensions unchanged.
**Play on Awake**: If enabled, the particle system starts automatically
**Emitter Velocity Mode**: The system offers different methods for computing particle velocity, which affects both Inherit Velocity and Emission features. It can derive velocity from either an attached Rigidbody component or by monitoring Transform position changes. When no Rigidbody is present, the system automatically defaults to using Transform-based calculations.
**Max Particle**: The maximum number of particles allowed in the system. If the limit is reached, existing particles will be removed when new particles are created

## Emission

This component controls the rate and timing of emissions.

![Emission]({{site.url}}{{site.baseurl}}/content/images/particle-2-emission.png)

**Rate over Time:** The number of particles emitted per unit of time
**Rate over Distance:** The number of particles emitted per unit of distance moved
**Burst:** One spawn of particles. Add bursts to emit particles at certain times

## Shape

The shape property defines the space from which particles emerge – whether they burst from a point, spray in a cone, or emanate from a custom shape. 

![Shape]({{site.url}}{{site.baseurl}}/content/images/particle-3-shape.png)

**Shape:** The particles are emitted to fill this shape





Renderer

The renderer determines how individual particles appear, affecting their basic visual characteristics.

Velocity over life time

Velocity over lifetime influences how particles move through space, allowing for effects like gravity or wind.

Force over life time

Force over lifetime allows you to apply dynamic forces to your particles as they exist, creating effects like gravity, wind, or magnetic attraction that can push, pull, or swirl your particles in various directions throughout their lifespan.

Color over life time

Color over lifetime enables smooth transitions between different hues, perfect for creating ethereal glows or dynamic explosions. 

Size over life time

Size over lifetime controls how particles grow or shrink as they age, while rotation over lifetime determines how they spin through their existence.

Rotation over life time
