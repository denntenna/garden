 ## Quality in Software
Correctness
Elegance

# Philosophy of Forth

find a balance between top down programming and fully planned programming.

imperative programming looks like sequential, if else code. a naive implementation basically?

design phase ensures that you think through the various smaller components.
one metric is that is this function reusable
is this state free and pure, even in its naming

Structured Design outlines 3 factors to for determining how to make divisions of a problem into simple modules.
1. functional strength
   module does one thing
2. Coupling
3. Hierarchical input-process-output desiging

data coupling is acceptable but its best to keep the interface as simple as possible

design a program around other concerns like flow of data and not around control flow.

Hiding information and not decision-structure or calling hierarchy should be the primary basis for design!
that is modules should be used to hide information that might possibly change.

decompose based on 
1. possible reuse
2. possible change

A design in which modules are grouped according to things that may change can readily accomodate change.

Component Programming
"thigns that may change". define your components around that.

how do we minimize impact of change? 

all components involve data objects and algorithms.

a lexicon describes a component
external to a component
a component may also have internal lexicon

these words of a lexicon then become the language for describing the data structures and algorithms of components written at a higher level.

An exercise to plan out how to break down a problem. because this is the most important thing!

## second read
 

# Analysis
The book focuses on Analysis, Design and Implementation
## The iterative approach
a never ending cycle of discovery and refinement. 
Start simple. Get it running. Learn what you're trying to do. Add complexity gradually, as needed to fit the requirements and constraints. Don't be afraid to restat from scratch.

You have to have a balance between having no planning process and spending upfront time in a lot of planning.

sales or product manager come up with the functional spec, then we work through a design and come up with the design specification.

**During the design phase, there is some amount of coding done to test out ceratain ideas. But this code may not be part of the finished product. The idea is to map out your design**

If the application elicits a sense of being lost, i proceed bottom-up. If the application is in familiar territory, then i'll probably use more by the book top down approach.

identify the problem and its boundaries clearly. break it into components.
put together just enough components and ask the user "does this meet your requirement"
then repeat.

testable primitives.

> I will not use a single line of code from this prototype in the final program.



## The analysis phase
requirements definition -> conceptual model
what does this model look like, so i can take feedback from the client/customer?
	use diagram, cartoons, tables
concrete techniques for defining and documenting the conceptual model
1. defining the interfaces
2. defining the rules
3. defining the data structure

think and communicate the error handling

Develop the conceptual model by imagining the data travelling through and being acted upon by the parts of the model.

They say that the conceptual model is forth. but i am not getting what that means.

the goal of analysis is not just understanding but its also simplifying.

# Preliminary Design / Decomposition
Determine what components are necessary to accomplish the requirements.

components and their internal lexicon

> if we had designed according to structure, or according to data transformation through sequential processes—our brittle design would have been shattered by the change

So these are the two ways I have been programming. I am not a hundred percent sure yet of how forth makers are doing this.

Interface Component
- Data structures and the commands involved in the communication of data between modules should be localized in an interface component
so in elixir you can do this by defining a behaviour and have your module implement it
	that takes care of commands. what about structures - this is what structs are for?
maybe if you combined a struct with callbacks, that would be it.

One non magical thing they are saying is to assume, it would be hard to get decomposition right in the first go so start somewhere and explore. Two approaches in this vein are  -  do the thing thats the most fun or do the thing thats the most visible (esp useful when working for a client)

They the book has a tip section giving more examples : pg 91.

## Conclusion
Applications can be decomposed into components and according to sequential complexity. 
Special attention should be paid to those components that serve as interfaces between other components.
Pick a component based on the heuristic above - whats fun or whats visible and implement it.

# Detailed Design / Problem Solving

> Getting stuck comes from trying too hard to follow a single approach. 




---
Component Programming
Having a larger set of simpler words makes it easy to use "component programming"

things can change -> how can we minimize the impact of such change -> by isolating the smallest set of other things that must change along with such a change -> this is called a component - the smallest set of interacting data structures and algorithms that share knowledge about how they collectively work.

component is a resource. could be piece of hardware or software like queue, dictionary etc.

component is a combination of structure and algorithms.

set of words which describe a component is called a lexicon. the lexicon is your interface with the component from the outside.
good lexicon veils the component's datastructure and algorithms.



I am still confused as to what is a component and probably giving up now :P

---
# Information Hiding
In a 1972 paper, Dr David L Parnas showed that the criteria cor decomposing modules should not be steps in a procedure but rather the pieces of information that might possibly change. Modules should be used to hide such information.

Hiding information should be the primary basis for design.

https://www.ultratechnology.com/method.htm

