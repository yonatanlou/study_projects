## README

Simulation of the world using OOP principals.
<p align="center">
  <img src="https://github.com/yonatanlou/study_projects/blob/main/Introduction%20to%20OOP/pepse/Screen%20Recording%202022-02-09%20at%2023.50.02.gif?raw=true" width="350" title="gif">
</p>






The UML are pretty similiar due to the fact that mandatory requests were pretty straight forward.
The main things that we didnt think aboout them are the inheritance of the Leaf class from the Block Class,
and the inheritance of the Tree class from the Terrain class.
We didnt think before hand about the connection of the SunHalo and the Sum and thought it will make sense
to do it with composition or delegation. But we actually use Functional interface.

<p align="center">
  <img src="https://github.com/yonatanlou/study_projects/blob/main/Introduction%20to%20OOP/pepse/uml_after.png?raw=true" width="550" title="uml">
</p>

To implement the infinite world we use composition inside PepseGameManager. and override the update method of the class.
Those, we were manage to control the simulation objects from the manager (remove and create) and also to know
in each update were is the center right now.

Implementation of trees - The Tree class extends Terrain, and by that can accsess the exact coords of the terrain.
Then, weve crrated a class for the Leaf which will control on the whole life cycle of the leaf (using the
Transition and ScheduledTask, combining lambda expressions and method references.

We thought maybe to implement Tree with composition of Terrain, and to save in a static field in terrain all of
the coords of the terrain. Then we could access the coords of the terrain without inheritance. But we wanted to
inherit more properties of the Terrain which seems important in that time.
For the infinite world we try another way, which was to control the while process inside the terrain with a subclass
of that contain update method, but it was to complex.


1. The sky is getting red when the energy of the avatar is less than 10 - a simple condition in the update
method of the PepseGameManager class, then changing the color of the sky with a static method.
2. You can make the avatar running faster with the arrows+Z (depending on your energy) - as we do for the whole
other input listener.


=============================
=      File description     =
=============================
PepseGameManager.java
    pepse/world/Sky.java - Creating the sky of the whole simulation.
    pepse/world/Avatar.java - Creating a moving object which the user can control with keyboard input.
    pepse/world/Terrain.java - Creating the terrain of the simulation.
    pepse/world/Block.java - creating the atomic building block of the whole simulation (practically most of the
    objects are made from this clas).

        pepse/world/trees/Tree.java - The class that creating the trees with the leafs in already (using composition).
        pepse/world/trees/Leaf.java - Using a base leaf object which inherit from the block class.

        pepse/world/daynight/Sun.java - Making the sun of the simulation, when the sun behaving
        like a real sun (in context of movement).
        pepse/world/daynight/SunHalo.java - Making the Halo of the sun.
        pepse/world/daynight/Night.java - Making the effect of night in the simulation which is
        correlated with the sun.



=          Design           =


PepseGameManager - The PepseGameManager is managing the whole simulation, when we using composition with each one of the objects.

Block - The Block class is the basic class which we create most of the other classes with this block (or it least with
his main property-size).

Terrain - To extend the terrain properties for the infinite world, we implement this with composition in combination of
the overriding the update method of the gameManager.

SunHalo - We are using the sun properties inside the sunHalo so we will the sun size.

Tree - The Tree class is extending the terrain class. we decided to do it because mainly for the placement of the tree.
We thought about other solution - to save the terrain coordinates in public field in terrain and to
access only the coords with composition, but we wanted for the tree class to be more flexible.

Leaf - We decided that the Leaf class will inherit directly from the block class because we wanted to extend the leaf
properties in a flexible wey, and used composition inside the Tree class.

Avatar - becasue the avatar is practically a GameObject, it was pretty easy to control his movement.

The design of the Sky is pretty straightforward (just simple composition in pepseGameManager)



=  Implementation details   =



The SunHalo is connecting to the Sun with Functional Interface which override the update method and each
update setting the center of sunHalo in the sun.

In the Sky class we use the power of static objects to change the sky color for some conditions.

The terrain extension for the infinite world is implemented in pepseGameManager by that we building a new world
for the current window camera + GROUND_INFINITE_INCREMENT. We also deleting the game objects that are out of the
scope that we defined to make the game run faster.

The leaf class is the most complex class - we are using there in the combination of the Transition and ScheduledTask
classes with method references and lambda expressions.
We combined a set of methods which invoke one after another to create the while circlelife of one leaf,
and with the power of randomness our leafs are behave like a real leaf.

The sun movement is implemented by the Transition class with LINEAR_INTERPOLATOR_FLOAT from 0 to 360 degrees
(so that the sun is doing infinite circles).



=          Bonuses          =

1. The sky is getting red when the energy of the avatar is less than 10.
2. You can make the avatar running faster with the arrows+Z (depending on your energy).



