# Traveling Salesman Problem
This is a very basic implementation of the traveling salesman problem that works using heuristic algorithms. 
The maps and csv files are from [SimpleMaps](https://simplemaps.com/).
If you woudl like to try out the program itself please download the notebook file or the zip file that contains the Romania shapefile and UK shapefiles (ro.shp and ro.csv).

## How the TSP algorithms work
This program uses 4 algorithm:
- **Nearest Neighbor**
    - This algoritm works by visitng the nearest city until it visits all cities and then returns to the strating city.
- **2-Opt**
    - 2-Opt works by reversing the order between 2 cities, thus eliminating crossing edges.
    - Suppose that there is a unoptimal tour for 8 cities where 1 is the starting city, and the optimal tour is all of the cities in order:
      - Unoptimal tour: [1, 2, 7, 4, 5, 6, 3, 8, 1]
      - Reversing order of cities 7 and 3
      - [1, 2, --- 7, 4, 5, 6, 3, --- 8, 1]
      - [1, 2, --- 3, 6, 5, 4, 7, --- 8, 1]
      - Optimal tour: [1, 2, 3, 6, 5, 4, 7, 8, 1]
        
- **Simulated Annealing**
    - Simulated Annealing is inspired by the annealing process in metallurgy, where hot metals are cooled down forming a strong crystalline structure.
    - In the case of the TSP this works by taking and existing tour, an initial temeprature, final temperature and a cooling rate.
        - Each time that the temeprature is cooled a post processing optimization is applied on the tour (in this case this is 2-Opt optimization).
        - If the tour improves it becomes the existing tour.
        - This process repeats until the temeperature is cooled to the final temperature.
- **Genetic Algoritm**
    - Initial Population
        - The algoritm begin with an initial population of tours.
    - Survivors
        - A filter that orders the population by distance and cuts it in half is used to create the survivors.
    - Offspring
        - 2 random parents are chosen from the survivors
            - A slice from parent 1 tour is placed into the offspring and the rest is filled with cities from parent 2 not present in the slice chosen from parent 1
            - A 2-Opt mutation is applied for every offspring
    - New Population
        - A new population is made from offspring.
        - This process is then repeated for a number of generations.
        - For each generation the best tour is saved, and the best overall tour is chosen out of all of the generations.
