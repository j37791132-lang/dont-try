# AGENTS.md - Development History

## Project Overview

This is a food chain simulator built with Processing 4, featuring an ecosystem simulation with multiple species including plants, herbivores, and carnivores. The project was demonstrated in a YouTube video and showcases AI-driven creatures with behaviors like hunger, thirst, reproduction, and predator avoidance.

## Initial Commit (2025-11-11)

### Project Setup
- **Commit**: `a5fd6f3` - "Added title.png"
- **Author**: j37791132-lang
- **Date**: November 11, 2025

This was the initial commit that established the complete codebase with all core features implemented.

### Core Components Created

#### Main Application (`Utopia.pde`)
- **Simulation Engine**: Main Processing sketch managing the entire ecosystem
- **Species System**: 6 species types (2 plants, 2 herbivores, 2 carnivores)
  - Pink flower (species 0)
  - Ice flower (species 1)
  - Yellow cow - herbivore (species 2)
  - Teal cow - herbivore (species 3)
  - Red predator - carnivore (species 4)
  - Gray species (species 5) - not yet fully implemented
- **Day/Night Cycle**: 4500 ticks per day with dynamic daylight affecting creature behavior
- **Population Tracking**: Archive system recording population data every 30 ticks (max 200 records)
- **Camera System**: First-person 3D camera with mouse look and creature following
- **Sound System**: 15 sound effects including eating, jumping, splashing, and breeding sounds

#### Creature AI (`Player.pde`)
- **Priority-Based AI System**: 6 priority types influencing behavior
  1. Hunger (food seeking)
  2. Thirst (water seeking)
  3. Reproduction/Mating ("Freaky")
  4. Sleep ("Eepy")
  5. Flee from predators
  6. Caretaking (following offspring)
- **Pathfinding**: Creatures navigate toward targets (food, water, mates) or flee from predators
- **Vision System**: Creatures can see within a 7-tile radius (VISION_DISTANCE)
- **Movement Physics**: Includes walking, jumping, strafing, and wandering behaviors
- **Collision Detection**: 33-unit collision distance for interactions
- **Body Visualization**: 3D stick figure rendering with walking animations, head tilting, and facial expressions

#### Creature Genetics (`Trait.pde`)
- **Individual Traits**: Each creature has unique properties
  - ID number and name (procedurally generated)
  - Generation tracking
  - Parent information
  - Birth weight
  - Priority levels (hunger, thirst, reproduction, etc.)
  - Children list
  - Meal counter
- **UI Display**: 400x700px trait panel showing creature stats and priority bars

#### Terrain System (`Map.pde`)
- **Procedural Generation**: 36x36 tile grid with Perlin noise elevation
- **Water System**: Dynamic water level with wave animation (period: 100 ticks, amplitude: 10 units)
- **Water Pathfinding**: Pre-computed closest water tile for each map position
- **Terrain Colors**: 9-color gradient from water to mountain peaks
- **Visibility Culling**: Tiles only rendered when visible in viewport
- **Elevation Factor**: Height multiplier of 10 for varied terrain

#### Supporting Systems
- **KeyHandler.pde**: Input management for WASD + Space controls
- **Memory.pde**: Memory management utilities
- **Brain.pde**: Neural network placeholder (minimal implementation)
- **Record.pde**: Population snapshot data structure
- **Tile.pde**: Tile occupancy tracking for plants
- **Gut.pde**: Dead creature remains that decay over time
- **ArrayUtils.pde**: Array sorting and manipulation utilities

### Game Mechanics

#### Food Chain System
- **Predation Matrix**: Defines which species can eat which
  - Yellow cows eat pink flowers
  - Teal cows eat ice flowers  
  - Red predators eat both cow species
- **Edibility System**: Creatures are only edible when their hunger/size is between 25-75%
- **Calories System**: Different species provide different calorie multipliers (0.80 to 1.35x)
- **Water Consumption**: Provides 40% thirst restoration

#### Plant Growth
- **Growth Mechanics**: Plants grow based on:
  - Elevation suitability (ideal heights: 0.39 for pink, 0.73 for ice flowers)
  - Tile overpopulation (max 2 plants per tile)
  - Daylight levels
  - Species-specific growth rates
- **Reproduction**: Plants produce seeds at 100% size (resets to 50%)
- **Seed Physics**: Seeds burst outward with random angles, 50% bounce chance

#### Creature Behavior
- **Priority Drain Rates**: Each species has different urgency rates for each priority
- **Speed Mechanics**: Species have different base speeds (0.5-0.54), reduced by hunger
- **Mating System**: 
  - Parents share 1/3 of their hunger with offspring
  - Caretaking priority activates after birth
  - Both parents track recent children
- **Death Conditions**:
  - Starvation (hunger = 0)
  - Dehydration (thirst = 0)
  - Being eaten by predators
  - Plant overpopulation

#### Technical Features
- **Tick System**: Staggered updates using tick buckets (20 buckets) to optimize performance
- **Looping World**: Seamless wraparound for X and Y coordinates
- **3D Rendering**: P3D renderer with dynamic lighting
- **Dual Graphics Buffers**: 1520x1080 main view + 400x1080 UI panel
- **Mouse Control**: Trapped pointer for first-person camera control
- **Distance-Based Audio**: Sound volume attenuates with distance (max 4.3 tiles)

### Audio Assets
Added 15 sound effects in `.wav` format:
- 5 splashing sounds (splash0-4)
- 5 eating sounds (eat1-5)
- Jump, land, seed, baby, and "oof" (death) sounds

### Visual Assets
- **title.png**: UI title image (196 bytes)

### Configuration
- **Player Count**: 110 initial creatures
- **Map Size**: 36x36 tiles
- **Tile Size**: 140 units
- **FPS**: 30 frames per second
- **Viewport**: 1920x1080 pixels
- **Species Distribution**: Weighted starting distribution from START_SPECIES array

### Development Notes
- Player controller is species -1 (user-controlled)
- Species -2 represents water target points
- Camera center point: X=760 (adjustable for drift correction)
- Processing 4 required for compilation
- Mouse pointer confined and hidden during gameplay

---

## Summary

This initial commit represents a complete, feature-rich ecosystem simulator with:
- Multi-species AI with priority-based behavior
- Full 3D rendering with terrain and creature animation
- Genetics tracking across generations
- Dynamic day/night cycle
- Comprehensive food chain mechanics
- Sound effects and UI visualization
- Player exploration and creature following modes

The project demonstrates advanced Processing techniques including 3D graphics, AI pathfinding, procedural generation, and real-time simulation management.
