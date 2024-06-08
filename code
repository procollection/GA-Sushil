import random

# Define the programs and time slots
programs = ['M', 'C', 'K', 'S', 'D']
time_slots = ['Morning', 'Late Morning', 'Afternoon', 'Evening', 'Night']

# Viewer preferences for each time slot
preferences = {
    'Morning': 'M',
    'Late Morning': 'C',
    'Afternoon': 'K',
    'Evening': 'S',
    'Night': 'D'
}

# Initialize population
def initialize_population(size):
    population = []
    for _ in range(size):
        chromosome = random.sample(programs, len(programs))
        population.append(chromosome)
    return population

# Fitness function
def fitness(chromosome):
    score = 0
    for i in range(len(chromosome)):
        if chromosome[i] == preferences[time_slots[i]]:
            score += 1
    return score

# Selection using roulette wheel
def selection(population, fitness_scores):
    total_fitness = sum(fitness_scores)
    selection_probs = [score / total_fitness for score in fitness_scores]
    selected_index = random.choices(range(len(population)), weights=selection_probs, k=1)[0]
    return population[selected_index]

# Crossover (single-point)
def crossover(parent1, parent2):
    point = random.randint(1, len(parent1) - 1)
    offspring1 = parent1[:point] + parent2[point:]
    offspring2 = parent2[:point] + parent1[point:]
    return offspring1, offspring2

# Mutation (swap mutation)
def mutate(chromosome, mutation_rate=0.1):
    if random.random() < mutation_rate:
        idx1, idx2 = random.sample(range(len(chromosome)), 2)
        chromosome[idx1], chromosome[idx2] = chromosome[idx2], chromosome[idx1]
    return chromosome

# Genetic Algorithm
def genetic_algorithm(pop_size, generations, mutation_rate=0.1):
    population = initialize_population(pop_size)
    
    for generation in range(generations):
        # Evaluate fitness
        fitness_scores = [fitness(chromosome) for chromosome in population]
        
        new_population = []
        while len(new_population) < pop_size:
            # Selection
            parent1 = selection(population, fitness_scores)
            parent2 = selection(population, fitness_scores)
            
            # Crossover
            offspring1, offspring2 = crossover(parent1, parent2)
            
            # Mutation
            offspring1 = mutate(offspring1, mutation_rate)
            offspring2 = mutate(offspring2, mutation_rate)
            
            new_population.extend([offspring1, offspring2])
        
        population = new_population[:pop_size]
        
        # Check for convergence or maximum fitness
        best_fitness = max(fitness_scores)
        if best_fitness == len(programs):
            break
        
    # Final population evaluation
    final_fitness_scores = [fitness(chromosome) for chromosome in population]
    best_chromosome = population[final_fitness_scores.index(max(final_fitness_scores))]
    
    return best_chromosome

# Parameters
population_size = 10
num_generations = 20
mutation_rate = 0.1

# Run the genetic algorithm
best_schedule = genetic_algorithm(population_size, num_generations, mutation_rate)
print(f"Best Schedule: {best_schedule}")
