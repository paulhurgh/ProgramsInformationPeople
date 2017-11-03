..  Copyright (C)  Brad Miller, David Ranum, Jeffrey Elkner, Peter Wentworth, Allen B. Downey, Chris
    Meyers, and Dario Mitchell.  Permission is granted to copy, distribute
    and/or modify this document under the terms of the GNU Free Documentation
    License, Version 1.3 or any later version published by the Free Software
    Foundation; with Invariant Sections being Forward, Prefaces, and
    Contributor List, no Front-Cover Texts, and no Back-Cover Texts.  A copy of
    the license is included in the section entitled "GNU Free Documentation
    License".

Testing classes
---------------

To test a user-defined class, you will create test cases that check whether instances are created properly, and you will create test cases for each of the methods as functions, by invoking them on particular instances and seeing whether they produce the correct return values and side effects, especially side effects that change data stored in the instance variables. To illustrate, we will use the Point class that was used in the :ref:`introduction to classes <classes_chap>`.

To test whether the class constructor (the ``__init__``) method is working correctly, create an instance and then make assertions to see whether its instance variables are set correctly.

A method like ``distanceFromOrigin`` in the ``Point`` class you saw does its work by computing a return value, so it needs to be tested with a return value test. A method like ``move`` in the ``Turtle`` class does its work by changing the contents of a mutable object (the point instance has its instance variable changed) so it needs to be tested with a side effect test.

.. activecode:: python

    class Point:
        """ Point class for representing and manipulating x,y coordinates. """
   
        def __init__(self, initX, initY):
   
            self.x = initX
            self.y = initY
   
        def distanceFromOrigin(self):
            return ((self.x ** 2) + (self.y ** 2)) ** 0.5
   
        def move(self, dx, dy):
            self.x = self.x + dx
            self.y = self.y + dy

    from unittest.gui import TestCaseGui

    class myTests(TestCaseGui):

        def test_int(self):
            p = Point(3, 4)
            self.assertEqual(p.y, 4)
            self.assertEqual(p.x, 3)

        def test_distance(self):
            p = Point(3, 4)
            self.assertEqual(p.distanceFromOrigin(), 5.0)

        def test_move(self):
            p = Point(3, 4)
            p.move(-2, 3)
            self.assertEqual(p.x, 1)
            self.assertEqual(p.y, 7)

    myTests().main()

.. sourcecode:: python

**Check your understanding**

.. mchoice:: test_questionmore_testing_1
   :answer_a: True
   :answer_b: False
   :feedback_a: Each test case checks whether the function works correctly on one input. It's a good idea to check several different inputs, including some extreme cases.
   :feedback_b: It's a good idea to check some extreme cases, as well as the typical cases.
   :correct: b
   :spacedrepetition: True

   For each function, you should create exactly one test case.
 
.. mchoice:: test_questionmore_testing_2
   :answer_a: return value test
   :answer_b: side effect test
   :feedback_a: The method may return the correct value but not properly change the values of instance variables. See the move method of the Point class above. 
   :feedback_b: The move method of the Point class above is a good example.
   :correct: b
   :spacedrepetition: True

   To test a method that changes the value of an instance variable, which kind of test case should you write?

.. mchoice:: test_questionmore_testing_3
   :answer_a: return value test
   :answer_b: side effect test
   :feedback_a: You want to check if maxabs returns the correct value for some input. 
   :feedback_b: The function has no side effects; even though it takes a list L as a parameter, it doesn't alter its contents.
   :correct: a
   :spacedrepetition: True

   To test the function maxabs, which kind of test case should you write?

   .. sourcecode:: python
   
      def maxabs(L):
         """L should be a list of numbers (ints or floats). The return value should be the maximum absolute value of the numbers in L."""
         return max(L, key = abs)

.. mchoice:: test_questionmore_testing_4
   :answer_a: return value test
   :answer_b: side effect test
   :feedback_a: The sort method always returns None, so there's nothing to check about whether it is returning the right value. 
   :feedback_b: You want to check whether it has the correct side effect, whether it correctly mutates the list.
   :correct: b
   :spacedrepetition: True
         
   We have usually used the ``sorted`` function, which takes a list as input and returns a new list containing the same items, possibly in a different order. There is also a method called ``sort`` for lists (e.g. ``[1,6,2,4].sort()``). It changes the order of the items in the list itself, and it returns the value ``None``. Which kind of test case would you use on the sort method?    
   

