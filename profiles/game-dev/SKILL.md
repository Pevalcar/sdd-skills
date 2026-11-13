---
name: profile-game-dev
description: "Reglas específicas para desarrollo de videojuegos (Godot, Unity, Unreal, etc.)"
---

# Perfil: Game Development

Reglas específicas para proyectos de videojuegos. Critical para proyectos con netcode, simulación y renderizado en tiempo real.

## Cuándo Cargar

| Indicadores | Acciona este perfil |
|-------------|---------------------|
| `project.godot` presente | Godot engine |
| `.unity` files, `ProjectSettings/` | Unity engine |
| `.uproject`, `Config/DefaultEngine.ini` | Unreal Engine |
| `defold` references | Defold engine |
| Custom engine/build scripts | Custom setup |

## Reglas Core

### Determinismo
- Same input → same output, always
- No floating point依赖 en lógica crítica de network
- State machines must be fully deterministic
- Random must use seeded RNG for reproducibility

### Network Code
- Authoritative server model preferred
- Client-side prediction only for visual feedback
- Lag compensation for hit detection
- Packet validation mandatory (length, bounds, types)
- Timestamp synchronization strategy

### Physics
- Fixed timestep for simulation
- Interpolation for rendering
- Predictive collision when needed
- Document expected precision loss

## Patrones Obligatorios

### State Machine
```gdscript
# Example GDScript state machine pattern
enum State { IDLE, MOVING, ATTACKING }
var current_state: State = State.IDLE

func _process(delta: float) -> void:
    match current_state:
        State.IDLE:
            transition_to_idle()
        State.MOVING:
            transition_to_moving(delta)
        # ...
```

### Network Packet Structure
```
| Header (4 bytes) | Opcode (2 bytes) | Payload (variable) | Checksum (2 bytes) |
```
- Always validate header length before parsing
- Endianness must be explicit (Little-Endian recommended)
- Max payload size enforced to prevent buffer overflows

### Object Pooling
- Reuse objects instead of instantiating/destroying
- Critical for bullets, particles, temporary entities
- Track active/inactive pool state

## Commands Específicos

| Engine | Command | Purpose |
|--------|---------|---------|
| Godot | `godot --headless --path . -e` | Export and run editor |
| Godot | `godot --headless --path . --import` | Force import |
| Godot | `godot --headless --path . -s test_scene.tscn` | Run test scene |
| Unity | `UNITY_BATCHED_MODE=1 unity -batchmode -runTests` | Run tests headless |
| Unity | `unity -executeMethod TestRunner.RunTests` | Execute specific tests |

## Anti-Patterns Específicos

| Anti-pattern | Problema | Solución |
|-------------|----------|----------|
| Floating point math in network code | Desync between clients | Use integer ticks or lockstep |
| Direct node access without null check | NullReferenceException crashes | Optional chaining, validation guards |
| Update() with heavy computation | Frame drops, input lag | Coroutines, async tasks, job system |
| Hardcoded paths/coordinates | Breaks across platforms | Resource paths, world-to-screen conversion |
| Global singleton state | Hard to test, unpredictable | DI, context passing |
| Instantiating during gameplay | GC spikes, stutter | Object pooling |

## Performance Budgets

| Metric | Target | Threshold |
|--------|--------|-----------|
| Frame time | < 16ms (60fps) | > 33ms (30fps) = warn |
| Draw calls | < 100 per frame | > 200 = optimize |
| Memory | Stable over time | Growing = leak investigation |
| Object count | < 1000 active entities | > 5000 = optimization needed |

## Verification Checklist

- [ ] Determinism verified (same seed → same result)
- [ ] Network packets validated (size, type, bounds)
- [ ] State machine has no unreachable states
- [ ] No null dereferences possible
- [ ] Object pooling implemented for frequent instantiation
- [ ] Frame rate stable under load
- [ ] Memory profiling shows no leaks
- [ ] Input handling responsive (< 100ms latency)
