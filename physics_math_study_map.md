# Physics & Math Study Map
*Built for pencil-and-paper physics, game development, and coding. Anchored on the twilight project (trig, vectors, cross products, exponential decay, Taylor approximations, numeric integration, lookup tables).*

---

## MATH TRACK

### M1. Algebra & Functions
- Rearrangement discipline; logarithms/exponentials
- `e^(−x/H)` decay, log-log linearization (plot slope = exponent)
- **Coding payoff:** any error/model tuning; reading log-scale graphs

### M2. Trigonometry
- sin/cos law, Pythagoras, small-angle tricks
- `sinθ ≈ θ`, `(1−cosθ) ≈ θ²/2` for θ in radians
- **Coding:** aiming/angles, shadow math on paper

### M3. Geometry (2D/3D)
- Circles/spheres, tangents, similar triangles, the sagitta
- `a(s) = √(R²+s²) − R ≈ s²/2R` (horizon/dip math)
- **Coding:** collision shapes, distance algorithms, smooth curves (Bézier = geometry in motion)

### M4. Vectors — *the most-used tool in physics and games*
- Dot = projection ("how much along"), cross = perpendicularity ("shadow cylinder test")
- Components/coordinate frames, `|v|² = v·v`
- **Coding:** EVERYTHING — movement, cameras, lighting. `dir·lightDir` is toon lighting

### M5. Linear Algebra
- Matrices as transforms: rotation matrices, `M @ v`, composite transforms, projections, determinant
- Optional: quaternions (rotations without gimbal lock)
- **Coding:** model/view/projection in every 3D engine

### M6. Probability & Statistics
- Expected value, uniform vs gaussian vs weighted distributions, law of large numbers
- `E[X] = Σ pᵢxᵢ`; rejection sampling; inverse-CDF sampling
- **Coding:** loot tables, procedural gen, particle systems, Monte Carlo integration

### M7. Calculus I — derivatives = rates of change
- Chain/product rules; **Taylor series:** `f ≈ f₀ + f'·h + f''·h²/2` → linearization of anything
- **Coding:** easing curves, PID control, "what changes per frame"

### M8. Calculus II — integrals = accumulation
- `∫ v dt = x`, numeric vs symbolic; center of mass, arc length
- **Coding:** the game loop IS an integrator

### M9. Numerical Methods — *the coding-superset of calculus*
- Eulers (forward / semi-implicit), **Verlet**, RK4; timestep (dt) stability
- Interpolation (linear/cubic), lookup tables + `np.interp`, bisection/Newton root-finding, `O(dt²)` error talk
- **Coding:** physics engines, path smoothing, camera damping

### M10. Approximation & Fermi Estimation
- Convergence, dominant terms, orders of magnitude
- **Coding:** performance budgeting, LOD decisions

---

## PHYSICS TRACK

### P1. Units & Dimensional Analysis
- If units don't match, your formula (and your code) has a bug
- **Payoff:** instant sanity-check for any equation

### P2. Kinematics
- `x = x₀ + v₀t + ½at²`, `v² = v₀² + 2a·Δx`, projectile arcs
- **Coding:** jump arcs, bullets, thrown objects; tuned `g` = game-feel

### P3. Newton's Laws & Forces
- `F = ma`, friction `F = μN`, drag `F = −cv` or `−cv²`
- **Coding:** platformer physics, vehicles, friction models

### P4. Energy & Momentum
- `E = ½mv² + mgh`, `p = mv`, restitution `e` in collisions
- **Coding:** impulse-based collision resolution; "did my solver leak energy?" tests

### P5. Circular Motion & Rotation
- `v = ωr`, `F = mv²/r`, `τ = Iα` (twilight used ω = 15°/hr)
- **Coding:** steering, wheels, orbiting objects, turret tracking

### P6. Gravitation & Orbits
- `F = Gm₁m₂/r²`, vis-viva `v² = GM(2/r − 1/a)`, escape velocity
- **Coding:** n-body sims (Verlet), space games

### P7. Oscillations & Waves — *most reused physics in game-feel*
- `F = −kx`, damped `mẍ + cẋ + kx = 0`; critical damping `c = 2√(km)`; `ω = √(k/m)`
- **Coding:** camera smoothing (critically damped spring), recoil, UI easing, cloth

### P8. Fluids & Gas Basics
- `P = ρgh`, exponential atmosphere `ρ(z) = ρ₀e^(−z/H)`, `H = kT/mg` (Earth: H ≈ 8.5 km)
- **Coding:** water, weather, atmosphere LODs, altitude effects

### P9. Optics & Light Transport — *ray tracing from first principles*
- Snell `n₁sinθ₁ = n₂sinθ₂`, mirror law, **Beer-Lambert** `I = I₀e^(−τλ)`, Rayleigh `σ ∝ λ⁻⁴`
- Rendering equation concept: radiance = integrate over paths (Monte Carlo)
- **Coding:** shaders, fog (`e^(−dist·density)`), sky simulation, GI basics

### P10. Waves, Acoustics & EM-lite
- Wave equation `∂²u/∂t² = c²∇²u`, intensity ∝ 1/r², light speed invariant
- **Coding:** sound falloff, ripples, ping/delay lines, Doppler

### P11. Special Relativity (consequences only)
- `t = t₀γ`, `E = γmc²`, nothing beats c; GPS corrections ≈ 38 μs/day

---

## THE PHYSICIST'S PLAYBOOK (transferable problem-solving)

1. **Model → assumption → formula → invalid test** ("test at α = 0: does it collapse sanely?")
2. **Dimensional analysis** — derive the *form* of unknown formulas from units alone (`T ∝ √(l/g)`)
3. **Conservation laws = invariants** — free unit tests for simulations
4. **Approximation ladder** — exact → Taylor → lookup table
5. **Integration mindset** — `state += f(state)·dt` is 90% of physics engines
6. **Fermi estimation** — pen-and-paper answer before code

---

## SUGGESTED STUDY ORDER

```
Parallel now:   M1–M4 + P1–P3      (paper physics + vector fluency)
Next:           M5–M7 + P4–P7      (transforms, springs, energy — game-feel base)
Then:           M8–M9 + P8–P10     (integration methods = engines, optics = shaders)
Anytime:        M6, M10, P11, Playbook
```

**Resources by unit:**
- Khan Academy → M1–M8
- 3Blue1Brown series → M4–M9 intuition
- Halliday/Resnick or Giancoli → P2–P8
- Feynman Lectures vol. 1 → P6–P7 intuition
- *Nature of Code* → M6 + procedural content
- Gaffer On Games (free articles) → M9 applied ("Fix Your Timestep")
- Best method: implement each topic as a small simulator, like the twilight project — study and verify in one motion

---

## APPENDIX: The anchor worked example (paper, no computer)

**Constants:** `R = 6371 km`, `H = 8.5 km`, `ω = 15°/hr` (1° = 4 min), `h_top ≈ 100 km`, `τ₀(550nm) ≈ 0.10`, Rayleigh `σ ∝ λ⁻⁴`

**Ladder:**
1. Sagitta: `a(s) = √(R² + s²) − R ≈ s²/2R`
2. Shadow cylinder (sunlit ⟺ perpendicular distance from Earth's center to the sun-ray > R):
   - West: `s_west = R(1−cosα)/sin(ξ+α)` (ξ=0 → `R·tan(α/2)`)
   - East: `s_east = R(1−cosα)/sin(ξ−α)` (needs ξ > α; ξ=0 → never lit → dark segment)
   - N/S: `s ≈ R·sinα`;  Zenith: `a_zenith = R(1−cosα)/cosα ≈ Rα²/2`
3. Brightness: `I = ∫ ρ(a(s))·[sunlit]·(1+cos²θ)·e^(−τ) ds`, `τ ≈ τ₀·(550/λ)⁴·airmass`

**Worked numbers, sun 3° below horizon (~12 min after sunset):**
- `a_zenith ≈ 8.7 km` → `e^(−8.7/8.5) ≈ 36%` column lit → zenith dimming, not black
- `s_west = 6371·tan(1.5°) ≈ 167 km` → floor at ≈ 2.2 km → 77% density → bright west
- `s_N/S ≈ 333 km`; `s_east(ξ=10°) ≈ 72 km` (floor ≈ 16 km); `s_east(ξ=0) = ∞` → dark segment
- east/west ratio proxy ≈ `e^(−(16−2.2)/8.5)` ≈ 0.2–0.3 → "light blue" vs "bright blue"

**Outdoor experiment checklist (notepad + wristwatch):**

| Measure outdoors | Formula |
|---|---|
| Zenith goes fully dark | `Rα²/2 > 30 km` → α ≈ 5.6° → ~23 min |
| East low sky dark (blue hour end) | 25–35 min |
| West horizon dims | lit floor `Rα²/8` > 2–3 km → ~10–15 min |
| Your hill's horizon dip | `dip = √(2h/R)` (200 m → 0.45°) — derive it from the sagitta |

**Derivation exercises (increasing difficulty):**
1. Horizon dip from your hill
2. Sunrise timing change at altitude
3. What R keeps the east horizon glowing one hour after sunset? (invert the formulas)
4. Off-axis general case: `s²(1−cos²Δ·cos²α) + 2Rs·sinα·cosΔ·cosα − R²sin²α > 0`
