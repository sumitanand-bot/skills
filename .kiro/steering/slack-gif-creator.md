# Slack GIF Creator Steering

## Metadata

- **Name**: slack-gif-creator
- **Description**: Knowledge and utilities for creating animated GIFs optimized for Slack. Provides constraints, validation tools, and animation concepts. Use when users request animated GIFs for Slack like "make me a GIF of X doing Y for Slack."

## Triggers

Use this steering when:
- User asks to create a GIF for Slack
- User mentions "Slack emoji" or "custom emoji"
- User wants an animated GIF with Slack-specific constraints
- User mentions creating GIFs with specific dimensions (128x128, 480x480)

## Instructions

A toolkit providing utilities and knowledge for creating animated GIFs optimized for Slack.

### Slack Requirements

**Dimensions:**
- Emoji GIFs: 128x128 (recommended)
- Message GIFs: 480x480

**Parameters:**
- FPS: 10-30 (lower is smaller file size)
- Colors: 48-128 (fewer = smaller file size)
- Duration: Keep under 3 seconds for emoji GIFs

### Core Workflow

```python
from core.gif_builder import GIFBuilder
from PIL import Image, ImageDraw

# 1. Create builder
builder = GIFBuilder(width=128, height=128, fps=10)

# 2. Generate frames
for i in range(12):
    frame = Image.new('RGB', (128, 128), (240, 248, 255))
    draw = ImageDraw.Draw(frame)
    # Draw your animation using PIL primitives
    builder.add_frame(frame)

# 3. Save with optimization
builder.save('output.gif', num_colors=48, optimize_for_emoji=True)
```

### Drawing Graphics

**Working with User-Uploaded Images:**
```python
from PIL import Image
uploaded = Image.open('file.png')
```

**Drawing from Scratch:**
```python
from PIL import ImageDraw

draw = ImageDraw.Draw(frame)

# Circles/ovals
draw.ellipse([x1, y1, x2, y2], fill=(r, g, b), outline=(r, g, b), width=3)

# Stars, triangles, any polygon
draw.polygon(points, fill=(r, g, b), outline=(r, g, b), width=3)

# Lines
draw.line([(x1, y1), (x2, y2)], fill=(r, g, b), width=5)
```

**Making Graphics Look Good:**
- Use thicker lines (width=2 or higher)
- Add visual depth with gradients
- Layer multiple shapes for complexity
- Use vibrant, complementary colors

### Available Utilities

**GIFBuilder** (`core.gif_builder`):
```python
builder = GIFBuilder(width=128, height=128, fps=10)
builder.add_frame(frame)
builder.save('out.gif', num_colors=48, optimize_for_emoji=True)
```

**Validators** (`core.validators`):
```python
from core.validators import validate_gif, is_slack_ready
passes, info = validate_gif('my.gif', is_emoji=True, verbose=True)
```

**Easing Functions** (`core.easing`):
```python
from core.easing import interpolate
y = interpolate(start=0, end=400, t=t, easing='ease_out')
# Available: linear, ease_in, ease_out, ease_in_out, bounce_out, elastic_out, back_out
```

### Animation Concepts

- **Shake/Vibrate**: Offset position with `math.sin()`/`math.cos()`
- **Pulse/Heartbeat**: Scale size with sine wave (0.8 to 1.2 of base)
- **Bounce**: Use `interpolate()` with `easing='bounce_out'`
- **Spin/Rotate**: `image.rotate(angle, resample=Image.BICUBIC)`
- **Fade In/Out**: Adjust alpha channel or use `Image.blend()`
- **Slide**: Use `interpolate()` with `easing='ease_out'`
- **Explode/Particle Burst**: Generate particles with random angles and velocities

### Optimization (Only When Asked)

1. **Fewer frames** - Lower FPS or shorter duration
2. **Fewer colors** - `num_colors=48` instead of 128
3. **Smaller dimensions** - 128x128 instead of 480x480
4. **Remove duplicates** - `remove_duplicates=True`

### Dependencies

```bash
pip install pillow imageio numpy
```

## Resources

- `skills/slack-gif-creator/core/gif_builder.py` - GIF assembly and optimization
- `skills/slack-gif-creator/core/validators.py` - Slack requirement validation
- `skills/slack-gif-creator/core/easing.py` - Animation easing functions
- `skills/slack-gif-creator/core/frame_composer.py` - Frame helper utilities
