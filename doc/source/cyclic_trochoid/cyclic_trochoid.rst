.. Project on the Cyclic Trochoid

Celestial Wheels
################

This project draws a loopy curve,
that mathematicians call an epitrochoid,
and everyone else calls a spirograph pattern.
It introduces the idea of an object and its methods.


Turtles, turtles, turtles
*************************

.. _empty Trinket: https://trinket.io/embed/python

In earlier projects we used only one turtle, with no name,
and your commands like ``forward`` and ``left``,
went to that unnamed turtle.
Here you'll create two other turtles,
and send commands to each of them by name.

First, let's see how this works.
Start the project with an `empty Trinket`_.
Type in the editor::

   # Epitrochoids
   from turtle import *

   # Test
   ted = Turtle()

This is how you make a new turtle,
and a variable ``ted`` to refer to it.
Now we can give ``ted`` the turtle some things to do.
**Add** and run this::

   ted.color("blue")
   ted.left(60)
   ted.forward(100)

These instructions work like function calls, but addressed to ``ted``.
A function addressed to a particular object is called a *method*.
The dot ``.`` is how you address a *method* to an object in Python.
It has to be something the object knows how to do,
so you can't say ``ted.print()``, because turtles don't know that word.
The unnamed turtle is still there and waiting for your instructions::

   forward(100)

**Delete** the test code so your Trinket looks like this again::

   # Epitrochoids
   from turtle import *

   # Test

Setting up the guide turtles
****************************

For the next part,
we need two "guide" turtles,
each of which draws a circle.
Each guide has to be set up a certain distance from home,
so **add** these two functions to your code (above ``# Test``),
so it looks like this:

.. code-block:: python

   # Epitrochoids
   from turtle import *

   def new_guide(r, c):
     "Return a new guide turtle of radius r and colour c"
     t = Turtle()
     t.speed("fastest")
     t.color(c)

     # Go to (r,0) without drawing
     t.penup()
     t.setposition(r,0)
     t.left(90)
     t.pendown()

     return t

   def mid(p, q):
     "Half way between positions p and q"
     x = (p[0] + q[0]) / 2
     y = (p[1] + q[1]) / 2
     return x, y

   # Test

Notice that the ``new_guide`` function *returns* a turtle.
**Add** this code starting after ``# Test`` and run the program:

.. code-block:: python

   g = new_guide(100, "blue")
   start = g.position()
   g.circle(50, 90)
   end = g.position()
   setposition(mid(start,end))

In that last line we did two things at one:
the ``mid`` function calculates the half-way point between ``start`` and ``end``,
then ``setposition`` takes your unnamed turtle there.
You should see this:

   .. image:: epi_midpoint.png

The unnamed turtle (black)
has moved halfway between start and end of the blue arc.
When that works, **delete** the test code again.


Moving the guides
*****************

The first job is to make the guides move in their orbits.
**Add** this function to your program,
and call it as a test:

.. code-block:: python

   def epitrochoid(a, b, L, M=1):
     ta = new_guide(a, "blue")
     tb = new_guide(b, "red")

     # N little steps s make one circle
     N = 500
     s = 360/N
     for i in range(N):
       ta.circle(a, L*s)
       tb.circle(b, M*s)

   # Test
   epitrochoid(90, 100, 3, 2)

Run that.
You should see blue and red circles drawn.

The blue turtle goes round L=3 times, and the red turtle M=2 times.
You can see how this works in the code.
``N`` just has to be a big enough number to make the final curve smooth.
``N`` steps of size ``s`` make 360 degrees, exactly one circle.
So ``N`` steps of ``L`` or ``M`` steps make ``L`` or ``M`` full circles.

``M=1`` on the first line says that,
if you don't give it a value in the call to ``epitrochoid``,
``M`` will be equal to 1.


Compute the shape
*****************

The shape we are looking for is drawn by
keeping our unnamed turte mid-way between the two guide turtles.

**Add** lines to the ``epitrochoid`` function so it reads like this:

.. code-block:: python
   :emphasize-lines: 5-9, 16-17

   def epitrochoid(a, b, L, M=1):
     ta = new_guide(a, "blue")
     tb = new_guide(b, "red")

     # Set start position for unnamed turtle
     penup()
     setposition((a+b)/2, 0)
     pendown()

     # N little steps s make one circle
     N = 500
     s = 360/N
     for i in range(N):
       ta.circle(a, L*s)
       tb.circle(b, M*s)
       m = mid(ta.pos(), tb.pos())
       setposition(m)

Run the code.
You should see this:

.. image:: epi_90_100_3_2.png



.. sidebar:: Roman astronomy

   Early astronomers took the Earth to be stationary,
   with the Sun, Moon and planets moving round it.   
   If you take careful measurements of the position of a planet in the sky,
   you find it speeds up, slows down, and sometimes travels backwards.
   The Roman astronomer Ptolemy (around AD 145)
   deduced from this that the planets moved in cycles
   like the ones you are drawing.

   .. image:: 244px-Cassini_apparent.jpg
      :align: center
      :height: 220px

   In this theory,
   the orbit of Venus has the shape you get from::

       epitrochoid(150, 200, 13, 8)

   This is because Venus is about 3/4 the distance of Earth from the Sun,
   and goes around the Sun 13 times in 8 Earth years.

   .. image:: epi_venus.png
      :align: center
      :height: 220px

   In the 16th century,
   when the telescope let us see the planets more clearly,
   we understood that the Earth and Venus both orbit the Sun.
   The *difference* of these two orbits is the motion Ptolemy observed.



Tidy up
*******

It would be nice if the guide circles were not on the final drawing.
**Change** the function ``new_guide``,
so guide turtles are invisiible (``hideturtle``)
and do not draw (do not ``pendown``).

.. code-block:: python
   :emphasize-lines: 11-12

   def new_guide(r, c):
     "Return a new guide turtle of radius r and colour c"
     t = Turtle()
     t.speed("fastest")
     t.color(c)

     # Go to (r,0) without drawing
     t.penup()
     t.setposition(r,0)
     t.left(90)
     t.hideturtle()
     #t.pendown()

     return t


Style the unnamed turtle to your liking:

.. code-block:: python

   # Test
   speed("fastest")
   width(5)
   color("lime green")
   epitrochoid(90, 100, 3, 2)

   hideturtle()


Inspiring examples
******************

Try changing the numbers in the call to ``epitrochoid`` like this::

   a, b = 50, 150
   epitrochoid(a, b, 4)

   color("goldenrod")
   epitrochoid(a, b, 5)

   color("sienna")
   epitrochoid(a, b, 6)

(Remember, M=1 if you don't give a fourth argument.)
Suppose you change just one line now::

   a, b = -50, 150

and run again. When the loops point outwards,
the shape is called a hypotrochoid.

What's happening here?

.. code-block:: python

   a, b = 250, 300
   epitrochoid(a, b, 4)

   color("goldenrod")
   epitrochoid(a, b, 5)

   color("sienna")
   epitrochoid(a, b, 6)

And what about here?

.. code-block:: python

   L = 6
   a, x = 20, 50
   epitrochoid(a, L*a, L)

   color("goldenrod")
   epitrochoid(a, L*a + x, L)

   color("sienna")
   epitrochoid(a, L*a - x, L)

Find other interesting shapes of your own.


Some advanced questions
***********************

If you like investigating mathematical patterns,
this code project poses some interesting questions.

* What determines the number of loops?
* What values for ``a`` and ``b`` make the curve pass through (0,0)?
  (Hint: where would the guide turtles be at that moment?)

A shape in this family, where the curve passes through zero, is called a "rose".

.. image:: epi_200_200_6.png
   :align: center
   :scale: 80%

* When do the loops become points?
* Both curves below have 3 loops: what is the difference between them?
  (Hint: imagine you are standing in the middle, then walk to the outside.
  What is the smallest number of green lines you have to cross? And brown?)

.. image:: epi_200_300_4_1.png
   :align: center
   :scale: 60%

