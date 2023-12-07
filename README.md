# **Exploring Game Level Map Generation with ChatGPT**
###### Jayanaka L. Dantanarayana
###### 7th December 2023 

This experiment is on an intriguing experiment—utilizing conversational AI, specifically ChatGPT, to generate game level maps for a Python-based game developed using pygame. The objective was to assess whether an AI model could create simple yet playable game maps based on specific prompts.

## Understanding the Game Map

A python game made using pygame in git repo https://github.com/Jayanaka-98/py-game-RPG is being used. 

The game's map structure consists of a 20x20 grid with various elements:

        'B': Walls
        'E': Enemy Character
        'P': Player Character
        '.': Space

The four edges of the map must be made up of walls and wall barries may be placed inside the map. The mechanics involve players and enemies moving and attacking in four directions (left, right, up, down), resulting in a game over upon collision. Victory requires eliminating all enemies.

## Experiment Setup

- The experiment involved providing ChatGPT with prompts related to map generation and observing its responses.

- I first explained ChatGPT how the game map works.

## Methodology

The game map design and game mechanics are explained to the moedel.

### Prompt 1: 
    "This is a map for a game"
```python
"tilemap = [
    
    'BBBBBBBBBBBBBBBBBBBB',
    'B..E...............B',
    'B..................B',
    'B....BBBB......E...B',
    'B..................B',
    'B..................B',
    'B.........P........B',
    'B..................B',
    'B....E.............B',
    'B..................B',
    'B.......BBB........B',
    'B.........B........B',
    'B.........B....E...B',
    'B.........B........B',
    'BBBBBBBBBBBBBBBBBBBB'

]"
```

    "B means Walls, P means player and E means the enemy. Generate a simmilar map with same size with walls an all sides"

#### ChatGPT: 
```python
tilemap = [
    'BBBBBBBBBBBBBBBBBBBB',
    'B..................B',
    'B..................B',
    'B..................B',
    'B..................B',
    'B..................B',
    'B..................B',
    'B..................B',
    'B..................B',
    'B..................B',
    'B..................B',
    'B..................B',
    'B..................B',
    'B..................B',
    'BBBBBBBBBBBBBBBBBBBB'
]
```

ChatGPT successfully crafted a map of the specified dimensions, enclosing the area with walls along the perimeter. However, it didn't populate the interior with any enemies, players, or additional walls as it was not specified in the prompt.

### Prompt 2: 
    "Give me a different map"

#### ChatGPT: 

```python
tilemap = [
    'BBBBBBBBBBBBBBBBBBBB',
    'B..........E.......B',
    'B..................B',
    'B.......BBBB.......B',
    'B......E...........B',
    'B..................B',
    'B...E..............B',
    'B..................B',
    'B..BBBBB...........B',
    'B.........E........B',
    'B..................B',
    'B............P.....B',
    'B..................B',
    'B.......E..........B',
    'BBBBBBBBBBBBBBBBBBBB'
]
```

This time it managed to produce a playable map whithough it was quite simple. 

### Prompt 3: 
    "Give me another one"

#### ChatGPT: 
```python
tilemap = [
    'BBBBBBBBBBBBBBBBBBBB',
    'B........E.........B',
    'B.................B',
    'B...E.............B',
    'B.........E.......B',
    'B..................B',
    'B..........E.......B',
    'B..................B',
    'B...E..............B',
    'B..................B',
    'B..................B',
    'B.........P........B',
    'B..................B',
    'B..................B',
    'BBBBBBBBBBBBBBBBBBBB'
]
```

This marked a pivotal moment in the experiment where an error in map generation surfaced. Notably, rows 3, 4, and 5 displayed only 19 tiles instead of the reqrequested 20. To confirm this anomaly, I requested another map generation without rectifying the initial problem.

### Prompt 4: 
    "Another"

#### ChatGPT: 

```python
tilemap = [
    'BBBBBBBBBBBBBBBBBBBB',
    'B...........E......B',
    'B..................B',
    'B..........E.......B',
    'B..................B',
    'B......E...........B',
    'B..................B',
    'B..................B',
    'B...E..............B',
    'B..................B',
    'B.......P..........B',
    'B..................B',
    'B........E.........B',
    'B..................B',
    'BBBBBBBBBBBBBBBBBBBB'
]
```

Surprisingly it did not reproduce the map size error. However, as this map is quite simple a harder map was requested.

### Prompt 5: 
    "Give me a harder map"

#### ChatGPT: 
    Creating a more challenging map involves adjusting the placement and density of walls, enemies, and the player. Here's a map with a more intricate layout:

```python
tilemap = [
    'BBBBBBBBBBBBBBBBBBBB',
    'B........E.........B',
    'B..BBBB............B',
    'B..B...............B',
    'B..B........E......B',
    'B..B...............B',
    'B..B.....BBBB......B',
    'B..B..........E....B',
    'B..B...............B',
    'B..B...............B',
    'B..B........P.......B',
    'B..B................B',
    'B..BBBB............B',
    'B.....E............B',
    'BBBBBBBBBBBBBBBBBBBB'
]
```
    This map introduces a more intricate maze-like structure with walls ('B'), enemies ('E') in challenging spots, and the player ('P') placed in a relatively open area. Adjustments like dead ends, narrow paths, and more obstacles make it trickier for the player to navigate without encountering enemies.

**KABOOM!!!** It is a marvelous revelation that this LLM was able to grasp the concept of game level hardness of a level and generate a more challenging map without explaining it what to do.

With this revelation a much harder map was requested.

### Prompt 6: 
    "Give me a harder map"

#### ChatGPT: 

```python
tilemap = [
    'BBBBBBBBBBBBBBBBBBBB',
    'B.......E..........B',
    'B.BB.BB.BB.BB.BB.BB',
    'B..B............B..B',
    'B.B..BB.BB.BB.B..BB',
    'B.............E....B',
    'B.B..BB.BB.BB.BB.BB',
    'B..B............B..B',
    'B.BB.BB.BB.BB.BB.BB',
    'B.....E...........PB',
    'B.BB.BB.BB.BB.BB.BB',
    'B..B............B..B',
    'B.BB.BB.BB.BB.BB.BB',
    'B.............E....B',
    'BBBBBBBBBBBBBBBBBBBB'
]
```

This map was indeed harder, but an issue with the game michanics was revealed as the player character needs at least a 2 tile gap to pass through easily. Otherwise the hitbox of the player must align with the empty space, accurate to the a pixel. Additionally the map size error was also present 

To avoid this issue, ChatGPT was prompted to keep a 2 tile spacing for the player to move.

### Prompt 7: 
- There can only be 20 rows and 20 columns and there should be atleast two empty spaces for the player to move

#### ChatGPT: 
- Understood! Here's a challenging map within the constraints of 20 rows and 20 columns that ensures at least two empty spaces for the player to move:

```python
tilemap = [
    'BBBBBBBBBBBBBBBBBBBB',
    'B..................B',
    'B.BB.BB.BB.BB.BB.BB',
    'B..................B',
    'B.BB.BB.BB.BB.BB.BB',
    'B..B............B..B',
    'B.BB.BB.BB.BB.BB.BB',
    'B..B............B..B',
    'B.BB.BB.BB.BB.BB.BB',
    'B.....E...........PB',
    'B.BB.BB.BB.BB.BB.BB',
    'B..B............B..B',
    'B.BB.BB.BB.BB.BB.BB',
    'B..B............B..B',
    'B.BB.BB.BB.BB.BB.BB',
    'B..................B',
    'B.BB.BB.BB.BB.BB.BB',
    'B..................B',
    'BBBBBBBBBBBBBBBBBBBB'
]
```

Here the map did not change and the error was not corrected. To ensure the gap, the model was asked to maintaina a 2 tile gap.


### Prompt 8: 
    "Spaces should be in both columns and rows as consecutive pairs."

#### ChatGPT: 
    Understood! Here's a revised map with at least two empty spaces arranged in consecutive pairs in both columns and rows:

```python
tilemap = [
    'BBBBBBBBBBBBBBBBBBBB',
    'B..................B',
    'B.BB.BB.BB.BB.BB.BB',
    'B..................B',
    'B.BB.BB.BB.BB.BB.BB',
    'B..................B',
    'B.BB.BB.BB.BB.BB.BB',
    'B..B............B..B',
    'B.BB.BB.BB.BB.BB.BB',
    'B.....E...........PB',
    'B.BB.BB.BB.BB.BB.BB',
    'B..B............B..B',
    'B.BB.BB.BB.BB.BB.BB',
    'B..................B',
    'B.BB.BB.BB.BB.BB.BB',
    'B..................B',
    'B.BB.BB.BB.BB.BB.BB',
    'B..................B',
    'BBBBBBBBBBBBBBBBBBBB'
]
```

Here also the same result was presented. From here onwards the prompts did not change the map significantly or correct the mapsize error.


## Conclusion

While the experiment showcased the potential of language models in generating game maps, it highlighted limitations in reliably creating progressively challenging levels. Fine-tuning the model for this specific task might be necessary to consistently generate playable yet increasingly difficult game levels.

## Key Observations ans Learnings

  - **Model's Capability:** ChatGPT demonstrated an understanding of basic map structures and placements of game elements but struggled to create varied or more intricate maps.

  - **Limitations:** The AI's ability to respond to prompts and iteratively generate increasingly complex or challenging maps was limited.

  - **Fine-tuning Requirement:** To reliably create harder yet playable maps, further fine-tuning of the model specifically for game level map generation might be necessary.

## Future Directions

This experiment unveils the potential for AI-driven game map generation but underscores the need for refinement. Future efforts could focus on refining prompts or training models tailored to game level map creation, enhancing their ability to generate diverse and progressively challenging maps. Furthermore, integration the LLM directly with the game by internal propting and API calls would be pursued as well.