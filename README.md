# Sexual Reproduction Genetic Algorithm | General Overview

## Objective
Determine the shortest distance to traverse a set of points using a genetic algorithm to minimize processing time and retain accuracy.

## Keywords
Path: A set of points tracing the coordinates provided by the user. Also referred to as an organism.

Gene: A single coordinate point.

Mutation: The process of swapping two genes while producing a child.

Civilization: Refers to the set of organisms that stemmed from two original parents. Every civilization begins with parents whose paths are randomly ordered.

Generational Iteration: Refers to each time the algorithm creates a new set of parents, birthing a new civilization, within a fresh start iteration.

Fresh Start Iteration: Refers to each time a new civilization is created and a fittest child is determined.

## Initial Processing
The set of coordinates is initially inputted by the user. It is copied and shuffled once per fresh start iteration, to prevent the user accidentally giving the algorithm a set of “accurate points” when testing. Two parents are created before generational iteration begins, both with random paths.

Note: The 25-point set I used is provided in this repo as coordinates.csv

## Generational Iteration
Per generational iteration, two parents are inputted, and two children are outputted. The outputted children become the parents of the next generation. 

The parents are initially crossed at random, though the fittest parent gets greater weight, which the user can modify. A weight of 0.5 will give both parents equal weight. The cross method chooses a child’s path gene by gene. It begins at index 1 (skipping index 0 because the starting point is never modified), and continues until the end of the path. It begins by selecting a parent at random, via the weight described earlier. The gene at the current index is passed to the child if the gene does not already exist in the child’s path. If it does, the unselected parent can pass its gene at the current index to the child. If both parents are unable to provide a new gene to the child, the algorithm takes the first new gene from the selected parent and passes it to the child’s current index, regardless of the position of the parent’s gene.

A set number of children are created per generational iteration, chosen by the user, each crossed and mutated individually. Two fittest children are selected, based on their fitness, and every other child is discarded. The algorithm does not randomly choose children weighted based on their fitness, though it would be interesting to implement.

Those two children then become the parents of the next generation, and the next generational iteration begins, only terminating when a fittest child is determined, or the maximum number of generational iterations is reached.

## Criteria for Selection
One fittest child is selected per fresh start iteration, based on the number of equivalent paths produced. Per generational iteration, new children are produced, whose fitness may be less than, equal to, or greater than their parents’ fitness. If their fitness is greater than, they are discarded. If less than, one of the two fittest paths are replaced. A child is determined as having an equivalent path when its fitness is equal to that of the fittest parent. When an equivalent child is detected, the algorithm increments a count variable that tracks the number of equivalencies. It is important to note that when a new fittest child is found, this count resets to zero. When the algorithm reaches a maximum count of equivalencies, set by the user, it terminates, and returns the path of the fittest child, determining it as the fittest.

## Issues With Generational Iteration
Generational iteration is excellent at converging on a better path than the initial path provided. What it is not good at, however, is finding inefficiencies in its path, such as the (exaggerated) figure [here](https://drive.google.com/file/d/1Jzd1lI8p3RGG-NSmsS6Y9Mx9pj0RR7Rr/view?usp=sharing).


The obvious inefficiencies seen in the figure are difficult to identify and resolve by the algorithm.

For instance, consider the path [(1,1), (1,2), (1,4), (1,3)] . To make the path the most efficient, indices 2 and 3 must be swapped. However, the algorithm chooses the indices to swap at random. The probability of the algorithm swapping these exact two genes is 44.4%, assuming the starting index is to remain unchanged. As the path’s length increases, however, the probability of a certain two genes being swapped decreases significantly. If the above path extended to (1,50), the probability of two genes being swapped decreases to just 0.16%. Because of this, it is difficult to have the algorithm fix inefficiencies on a path it has already begun to converge upon. In this algorithm, fresh start iteration is used to discard these inefficient paths.

## Fresh Start Iteration
Fresh start iteration aims to solve the issues found in generational iteration by repeating generational iteration on an entirely new civilization.

To do this, the algorithm runs generational iteration and determines a fittest child a set number of times on a new civilization, with new, random gene parents. Each civilization determines the fittest child, and terminates, allowing a new civilization to undergo generational iteration. The algorithm records the fittest child produced by each civilization, and determines the final path based on the fittest child from every generation. Because the initial paths are randomly selected, fresh start iteration should resolve the convergence issue in generational iteration described above.

## Example
[Here's](https://drive.google.com/file/d/1V_gwUQg9ryqyJn08Rjjqiq-MbhKbPazR/view?usp=sharing) an actual final product of the algorithm working on a 25-point system. It took around 20 minutes to complete but was 100% accurate.
