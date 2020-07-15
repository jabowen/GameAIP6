JJ Bowen
Yutong Guo

Explanation for generate_successors
	This function first pops the first element of population and sets it to be parent1.
	Then, it goes into a while loop that doesnt end until population is empty. Each
	iteration, it pops the first element(parent2), and the second element(parent3) and
	adds 3 pairs of children to results. These pairs are (parent1, parent2), (parent1, parent3),
	and (parent2, parent3). When the loop ends it returns.
	Note: once the new population is finsihed in ga() it sorts it by fitness, and then 
	removes the the lowest elements until it has only pop_limit elements in population
	
	We tried many differnet selection functions including tournament and eleite, but this
	one consistantly worked the best.

Explanations for Individual_Grid
	mutate(): the mutation rate is .4%. It goes through each index and changes it
			  to a random block (with special constraints on pipes) if 
			  randint(0,500)<2.
	generate_children(): It goes through each possible x and y value and decides
						 randomly whether to take it from parent1 or parent2
	fitness(): in calculate_fitness() changed the paramenter on
		- pathPercentage from .5 to 1.0,
        - emptyPercentage from .6 to 2.0,
        - solvability from 2 to 20.0

Explanations for Individual_DE
	generate_children(): This function gets a random integer for both parents
	                     and takes up to the first integer int on the first parent
						 and after the second int on the second parent, then add those
						 two half genomes together. It then gets the other half for
						 both parents and creates a second genome. Both of these are 
						 mutated, turned into Individual_DE and returned.
	mutate(): If the genome is not empty, and the random number calculated is less than .1
			  (a 10% mutation rate) a random part of the genome is chosen. This then goes
			  through different situations depending on what it is
				-block: 1/3 change to get a random x offset, or, if that fails 2/3 for y
				-qblock: 1/3 change to get a random x offset, or, if that fails 2/3 for y
				-coin: 50% chance to gat a random x offset, if that fails then 100% for y
				-pipe: 50% chance to gat a random x offset, if that fails then 100% for height
				-pipe: 50% chance to gat a random x offset, if that fails then 100% for width
				-stairs: 1/3 change to get a random x offset, or, if that fails 2/3 for height
						 if both fail it inverts
				-platform: 25% change to get a random x offset, or, if that fails 50% for width
						 if both fail 75% for y, and if all else fails, randomly decides whether
						 its a breakable, non-breakable, or ? box
				-enemy: do nothing
				
Explanation for population intitalization
	Added an if at the beggining of ga(). If we are using grid we use .9, and 
	DE uses 1.9 If this number is less than 1 there will be empty individuals in
	the intital population
				
Changes to Individual_DE
	mutate():changed some parameters
		-overall rate: .1 to .8
		-pipe: x change = .5 to .6, height change min: 2 to 1
		-hole: width change min 1 to 0, width change max width-1 to 2
		-stairs: height change min 1 to 0, height change max height-4 to 1
	fitness(): in calculate_fitness() changed the paramenter on
		- pathPercentage from .5 to 1.0,
        - emptyPercentage from .6 to 2.0,
        - solvability from 2 to 20.0