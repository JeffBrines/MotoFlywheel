# MotoFlywheel# Motorcycle Flywheel Weight Placement Analysis

A Python tool to mathematically analyze the effects of flywheel weight placement on motorcycle handling and engine response.

## The Question

Does placing flywheel weight on the **outer edge** (bolt-on weight) vs **integrated throughout** affect gyroscopic handling?

## The Answer

**TL;DR: Weight placement significantly affects ENGINE RESPONSE (~20% difference) but has negligible effect on GYROSCOPIC HANDLING (<15% even in extreme conditions).**

This tool proves it mathematically.

## What This Tool Does

Analyzes two separate effects:

### 1. Engine Rotational Inertia 
- Outer placement: **20%+ more rotational inertia**
- Effects: Smoother power delivery, less stalling, better traction
- **Very perceptible** to riders

### 2. Gyroscopic Handling 
- Wheels dominate gyroscopic effects (84-97% depending on speed)

### Key Physics Insight

The crankshaft/flywheel rotates **opposite** to the wheels, so their gyroscopic torques **subtract** rather than add. This is critical to understanding why flywheel placement barely affects handling.

## Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/motorcycle-gyro-analysis.git
cd motorcycle-gyro-analysis

# No external dependencies needed! Uses Python standard library only
python3 gyro_analysis.py
```

## Usage

### Run Default Analysis
Tests 5 standard riding conditions (6-50 mph, 5000-10000 RPM):

```bash
python3 gyro_analysis.py
```

### Custom Single Condition
```bash
python3 gyro_analysis.py --speed 25 --rpm 7000 --lean 2.2 --name "My Riding Style"
```

### Custom Bike Parameters
```bash
python3 gyro_analysis.py --flywheel-mass 1.5 --added-weight 14 --outer-radius 0.08
```

### Quiet Mode (Summary Only)
```bash
python3 gyro_analysis.py --quiet
```

### Command Line Options

```
Bike Configuration:
  --flywheel-mass    Stock flywheel mass in kg (default: 1.2)
  --added-weight     Added weight in ounces (default: 11)
  --outer-radius     Outer placement radius in meters (default: 0.07)
  --inner-radius     Inner placement radius in meters (default: 0.03)

Custom Condition:
  --speed           Speed in mph
  --rpm             Engine RPM
  --lean            Lean rate in rad/s
  --name            Name for the condition

Output Options:
  -q, --quiet       Show summary only
  -v, --verbose     Show extra details
```

## Example Output

```
======================================================================
ANALYSIS: Trail Riding
======================================================================
Conditions: 20 mph, 6000 RPM, 2.0 rad/s lean rate

----------------------------------------------------------------------
GYRO HANDLING DIFFERENCE (Outer vs Inner):
  Absolute difference: 1.568 N⋅m
  Percentage difference: 3.67%
  Assessment: ✅ NOT PERCEPTIBLE (< 5% threshold)

----------------------------------------------------------------------
ENGINE RESPONSE (Rotational Inertia):
  Outer vs Inner difference: 20.3%
  ✅ THIS IS VERY PERCEPTIBLE in throttle response!
```

## The Physics

### Moment of Inertia
```
I = m × r²
```
Weight farther from the center has exponentially more effect on rotational inertia.

### Gyroscopic Torque
```
τ = I × ω × Ω
```
Where:
- τ = gyroscopic torque (resistance to leaning)
- I = moment of inertia
- ω = spin rate of the rotating part
- Ω = angular rate of bike lean

### Critical: Opposite Rotation
Engine/flywheel rotates **opposite** to wheels:
```
τ_net = τ_wheels - τ_engine
```

## Results Summary

| Speed Condition | Net Gyro (N⋅m) | Placement Difference | Perceptible? |
|----------------|----------------|---------------------|--------------|
| 6 mph (crawling) | 5.53 | 15.06% | Barely |
| 20 mph (trail) | 41.12 | 3.67% | NO |
| 50 mph (fast) | 165.82 | 2.31% | NO |

**Engine inertia difference: 20.3% at ALL speeds** ✅ Very perceptible!

## Why This Matters

### What Riders Actually Feel
When riders claim they can "feel" the difference with bolt-on flywheel weight, they're feeling:
- ✅ Smoother engine response (20% more inertia)
- ✅ Better traction from consistent power
- ✅ Less tendency to stall
- ❌ NOT gyroscopic handling effects

### The Myth
"Bolt-on weight creates more gyro effect and makes handling heavier."

### The Reality
Bolt-on weight at the outer edge:
- Gives 5-6x more rotational inertia for engine response
- Changes handling gyro by <4% at realistic speeds
- Actually slightly **reduces** net gyroscopic resistance (opposes wheel gyro)

## Technical Details

### Default Bike Configuration
Based on KTM 300 2-stroke enduro:
- Stock flywheel: 1.2 kg at 70mm radius
- Added weight: 11 oz (0.312 kg)
- Outer placement: 70mm (bolt-on ring)
- Inner placement: 30mm (near hub)
- Front wheel: 8 kg, 330mm radius (21")
- Rear wheel: 10 kg, 300mm radius (18")

### Assumptions
- Simplified flywheel as point mass (conservative)
- Wheels modeled as solid disks
- No gear reduction effects (cancels out in comparison)
- Human perception threshold: 5-10% for Just Noticeable Difference

## Contributing

Contributions welcome! Areas for improvement:
- More sophisticated flywheel models (disk vs ring)
- Visualization/plotting capabilities
- CSV export for data analysis
- Additional bike presets
- Gear reduction analysis

## License

MIT License - feel free to use, modify, and distribute.

## References

- Gyroscopic torque fundamentals
- Motorcycle dynamics research
- Human perception studies (JND thresholds)

## Author

Created to settle the debate: Does flywheel weight placement affect handling?

**Answer: No, but it dramatically affects engine response!**

---

## Quick Start

```bash
# Download and run
curl -O https://raw.githubusercontent.com/yourusername/motorcycle-gyro-analysis/main/gyro_analysis.py
python3 gyro_analysis.py
```

That's it! No dependencies, no installation, just pure physics. 🏍️
