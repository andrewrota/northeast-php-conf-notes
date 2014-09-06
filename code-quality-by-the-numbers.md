# Code Quality, By The Numbers
** by Anthony Ferrara @ircmaxell**

Even the best code still has some question marks in it.

## What is complexity?

* Many parts where those parts interact with eachother in multiple ways
* The state of not being simple
* A part of something that is complicated

The number of decisions you need to keep track of in order to understand a solution.  Not about the problems, but about the solution itself.

## Types of Complexity

**Essential Complexity**: Complexity that is required to solve the problem.  No simpler solution can exist.

**Accidential Complexity**: Complexity that is introdu ed in the solution, but is not required to solve the problem.

Essential complexity is unavoidable.  But it's impossible to know for certain whether something is only the essential level of complexity.

Complexity is defined by the number of decision points.  Accidential complexity gets introduced in the implementation details.

You can split decision points into reusable pieces.  But that introduces additional complexity to reduce complexity.  That's kind of weird.  Local complexity in each reusable piece is decreased but global complexity is higher.  Making functions smaller requires making more of them.

Decreasing local complexity requires increasing global complexity, and vice versa.

Good design balances local complexity with global complexity.

## Measuring Complexity
	
###Cyclomatic Complexity

Number of decision points in a routine (block of code)

Cyclomatic Complexity in a single method:

1-4: Low complexity
5-7: Moderate complexity
8-10: High complexity
11+: Very high complexity

Average per method (globally) 

1-2: Low
2-4: Moderate
4-6: High
6+: Very high

*We have a higher tolerance for local complexity than global complexity*

Average complexity per line of code or per method.

One metric alone doesn't give us enough information.

Cyclomatic complexity isn't that useful of a metric.  But it's the basis of two additional metrics.

### N Path Complexity

Unique ways of executing a function.

< 16 Low
17-128: Moderate
129-1024: High
1025+: Very high

N Path is the minimum number of tests required to completely test a routine.

### Change Risk Analysis Predictions

Relates complexity and test coverage

If we have a really well covered function that reduces CRAP index

Testing insulates against complexity

< 5 Great
5-15 Acceptable
15-30 Eh
30+ Bad

## Reduce Complexity

Quality is a tradeoff between complexity and bloat.

"lasagna code" (layer upon layer)

## Tools

### PHPLOC

by Sebastian Bergmann (grandfather of testing in PHP)

Summarizes an entire codebase

### PDepend

By Manuel Pichler

Like PHPLoc, but granular

Lower level analysis

Instability/abstraction chart shows how tightly coupled your code is.  Realistically don't worry about that chart.

The Methods+Function chart though is very helpful.  Shows all the complexity metrics mentioned above.  Color codes it based on where you should be.

### PHPMD (Mess Detector)

By Manuel Pichler

Finds "messy" parts of the code base

Finds rule violations

CodeSize, design, naming, unused code, controversial

Tries to prevent complexity from getting into your codebase

## Tools Over Time

Super valuable to chart these over time.

* JenkinsPHP
* Sonar

Doesn't give you many answers, but it does let you ask the right questions.

Don't rely on the numbers alone.  Understand the big picture.  Understand the tradeoffs.

## Questions, etc.

How you name things is probably one of the best things to do to improve legibility of code.  Hard problem to solve, though.

Fanout is the metric that shows the number of times your code is touched from other areas in the system.

Time complexity (big O complexity).  On a global application standpoint you don't have to worry about time complexity.  It's a local concern.

Defects over time metric is what you really care about?  Not number of defects, but how much effort is required to fix a defect or add a feature.  Adding a feature is always going to increase complexity because of essential complexity.