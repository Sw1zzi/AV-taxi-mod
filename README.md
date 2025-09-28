# GDD: Air Vehicle Autopilot Mod (Cyberpunk 2077)

## 1. General Idea
The mod adds an **autopilot system for Air Vehicles (AVs)**, working through "air roads" (corridors).  
The player can summon an AV, which will fly along a pre-built route in automatic mode, including takeoff and landing.

---

## 2. Mod Goals
- Provide the player with the feeling of a true "flying taxi" in cyberpunk style (similar to cutscenes in certain missions).
- Implement a convenient AV transportation system across the city.
- Integrate the mechanic with existing systems (ground vehicle autopilot, fast travel, cutscenes).

---

## 3. Key Features
1. **Air Roads (Corridors)**
    - 2D/3D grid of routes above the city.
    - Nodes connected by edges, forming a graph (as one possible implementation).
    - Support for different altitudes and route types.

2. **AV Autopilot**
    - Enters the nearest corridor if the player is far away.
    - Builds the shortest path from entry to exit nodes.
    - Flies along the route while considering altitude.

3. **Landing/Takeoff**
    - Cutscene system (camera animation during landing/takeoff).
    - Option for teleportation/hidden substitution as a simpler solution.
    - Possibility of landing anywhere on the map / only at special call points.

4. **Interface**
    - AV call menu (similar to Delamain taxi).
    - Destination selection (via list or map).

---

## 4. Gameplay Flow
1. Player summons AV → chooses destination.
2. AV arrives → landing cutscene plays.
3. AV flies automatically along the calculated route.
4. AV arrives at the destination → disembark cutscene.
5. Player regains control.

---

## 5. Technical Implementation

### 5.1. Route Graph (currently main approach)
- Nodes: coordinates (X, Y, Z).
- Edges: connections between nodes, weight = distance/time.
- Pathfinding algorithm: **A\*** (heuristic = straight-line distance).
- Storage: JSON (nodes/edges).

### 5.2. Autopilot
- Based on the existing ground vehicle autopilot (or written manually; neural net is optional but probably excessive).
- Added support for Z (altitude).
- Script logic:
    - find nearest node to start,
    - find nearest node to destination,
    - build route,
    - AV follows nodes.

### 5.3. Cutscenes
- Camera switches to a cinematic mode.
- Takeoff/landing animation → transition back to player control.
- Minimal version: scripted camera + movement.
- Advanced version: integration with actual animations via WolvenKit.

### 5.4. Interface
- Call menu (CET UI).
- Destination selection from a list.
- Future: integration with in-game map.

---

## 6. Development Roadmap

### MVP (Minimum Viable Product)
- JSON with routes.
- A\* pathfinding.
- AV follows waypoints.
- Teleport/simple cutscene for landing.

### Version 1.0
- Proper cutscenes.
- UI for AV call.
- Multiple route types (low/high altitude).

### Future
- Integration with quests/events.
- Dynamic traffic of other AVs in corridors.
- Upgradable AVs (faster, armored, etc.).

---

## 7. Risks and Limitations
- Cyberpunk 2077 engine limitations (navmesh, cutscenes).
- Optimization: too many AVs may cause performance issues.
- Complexity of integrating with the in-game map UI.

---

## 8. Tools
- **Cyber Engine Tweaks (Lua)** — logic, scripting.
- **WolvenKit** — animations, resources.
- **JSON** — graph storage.
- **C++** — for native extensions if required.  
