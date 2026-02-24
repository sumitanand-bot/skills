# Algorithmic Art Steering

## Metadata

- **Name**: algorithmic-art
- **Description**: Create gallery-quality algorithmic art using p5.js. Guide for creating computational artwork that lives and breathes through mathematical processes, particle systems, and generative algorithms. Perfect for creating interactive HTML artifacts with seed-based variation.

## Triggers

Use this steering when:
- User asks for "algorithmic art", "generative art", or "computational art"
- User wants to create art that uses mathematical processes
- User mentions "p5.js" in the context of art creation
- User wants seed-based artwork with variations
- User asks for interactive visual art artifacts

## Instructions

### Creative Process Overview

**User request** → **Algorithmic philosophy** → **Implementation**

1. **Interpret the user's intent** - What aesthetic is being sought?
2. **Create an algorithmic philosophy** (4-6 paragraphs) describing the computational approach
3. **Implement it in code** - Build the algorithm that expresses this philosophy
4. **Design appropriate parameters** - What should be tunable?
5. **Build matching UI controls** - Sliders/inputs for those parameters

### Step 1: Create Algorithmic Philosophy

Create a VISUAL PHILOSOPHY that will be expressed through:
- Form, space, color, composition
- Temporal evolution and system states
- Parametric variation and emergent complexity

**CRITICAL GUIDELINES:**
- **Avoid redundancy**: Each algorithmic aspect should be mentioned once
- **Emphasize craftsmanship REPEATEDLY**: Stress that the final algorithm should appear meticulously crafted, the product of deep computational expertise
- **Leave creative space**: Be specific about direction, but concise enough for interpretive implementation choices

### Step 2: Read the Template

**CRITICAL: BEFORE writing any HTML:**

1. **Read** `skills/algorithmic-art/templates/viewer.html`
2. **Study** the exact structure, styling, and Anthropic branding
3. **Use that file as the LITERAL STARTING POINT**
4. **Keep all FIXED sections exactly as shown** (header, sidebar structure, seed controls, action buttons)
5. **Replace only the VARIABLE sections** (algorithm, parameters, UI controls)

### Step 3: P5.js Implementation

**Seeded Randomness (Art Blocks Pattern)**:
```javascript
let seed = 12345;
randomSeed(seed);
noiseSeed(seed);
```

**Parameter Structure**:
```javascript
let params = {
  seed: 12345,
  // Add parameters that control YOUR algorithm:
  // - Quantities, Scales, Probabilities
  // - Ratios, Angles, Thresholds
};
```

**Canvas Setup**:
```javascript
function setup() {
  createCanvas(1200, 1200);
  // Initialize your system
}

function draw() {
  // Your generative algorithm
}
```

### Craftsmanship Requirements

- **Balance**: Complexity without visual noise, order without rigidity
- **Color Harmony**: Thoughtful palettes, not random RGB values
- **Composition**: Even in randomness, maintain visual hierarchy and flow
- **Performance**: Smooth execution, optimized for real-time if animated
- **Reproducibility**: Same seed ALWAYS produces identical output

### Interactive Artifact Features

**Required Features:**
1. **Parameter Controls** - Sliders for numeric parameters, color pickers for palette
2. **Seed Navigation** - Previous/Next/Random buttons, input field to jump to specific seed
3. **Single Artifact Structure** - Self-contained HTML with p5.js from CDN

### What's Fixed vs Variable

**FIXED (always include):**
- Layout structure (header, sidebar, canvas area)
- Anthropic branding (UI colors, fonts, gradients)
- Seed section in sidebar
- Actions section (Regenerate, Reset, Download)

**VARIABLE (customize for each artwork):**
- The entire p5.js algorithm
- The parameters object
- The Parameters section in sidebar
- Colors section (optional)

### Philosophy Examples

**"Organic Turbulence"**: Flow fields driven by layered Perlin noise. Thousands of particles following vector forces.

**"Quantum Harmonics"**: Particles initialized on a grid with phase values that interfere when near each other.

**"Recursive Whispers"**: Branching structures that subdivide recursively with L-systems.

**"Field Dynamics"**: Vector fields constructed from mathematical functions. Particles flow along field lines.

### Output Format

1. **Algorithmic Philosophy** - As markdown explaining the generative aesthetic
2. **Single HTML Artifact** - Self-contained interactive generative art built from `templates/viewer.html`

## Resources

- `skills/algorithmic-art/templates/viewer.html` - Required starting point for HTML artifacts
- `skills/algorithmic-art/templates/generator_template.js` - Reference for p5.js best practices
