# Overview
The genetic algorithm has three main components: population initialization, fitness determination, natural selection, and swap mutation. The crossover genetic algorithm
method doesn't currently seem usable for this type of project.

### Why Not Crossover?
The algorithm is based a series of 2D points, which are randomized before execution to prevent unrealistic successes. The nature of the algorithm relies on points to
be in a series in a format like this: [(Ax, Ay), (Bx, By), (Cx, Cy), ...]. To simplify: [A, B, C, ...]. Crossover wouldn't be viable because it is prohibited for the
algorithm to allow point duplicates, it wouldn't make sense in a pathfinding algorithm. Crossover could result in a series that looks like [A, A, C]. Therefore, the
algorithm makes no use of the crossover method.

### Important Notes
* There are four variables that can be changed
  * COORDINATES
    * This is where the set of points is added, in the form of tuples (x, y) in a list. It is later randomly shuffled, leaving only the first index to go untouched
  * BIRTH_SIZE
    * This is the number of offspring a single parent produces. Increasing the number increases the liklihood of there being a "better" child, due to probability. However, increasing it also seems to drastically increase processing times, meaning every set of points has a "sweet spot" for processing time to accuracy
  * NUM_FITTEST_CHILDREN
    * This is something I added for pure redundancy, not necessarily a part of a classic genetic algorithm, to the best of my limited knowledge. The algorithm forever generates children based on their previous parent, choosing the best child offspring as the parents reproduce. However, there becomes a point where the fitness of the offspring nears its peak, signaling that the algorithm should probably terminate the loop and determine a final result. This variable attempts to detect when the algorithm nears its maximum accuracy by measuring the number of offspring that have equal fitness to their parent. If they do, the count of offspring with equal fitness goes up by one. If said count reaches the value of this variable, the loop terminates, and the algorithm displays these children as the fittest. If there is a fitter organism while the loop is iterating between count and this variable, it resets the count to 0, and resumes ticking upwards every time an equally fit child is detected. Increasing the number increases processing time, but also increases accuracy. With more and more children that are being produced, there is an increased liklihood of there being a "fitter" child.
  * MUTATIONS_PER_CHILD
    * This determines how many pairs of coordinates can be swapped in one child. This one proved to be very finicky during my testing. On tests with a lower number of points, the algorithm only became more innacurate while increasing processing time. On those with a higher number, they became more accurate in the beginning of iteration, but reduced their effectiveness as the algorithm approached the true path. Generally, I keep this variable down below 5 for large sets, and below 3 for small ones. I haven't been able to find a "sweet spot" for this one, as it tends to mess with the algorithm while it is running, not just all throughout.
