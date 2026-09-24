# Hi3D Agent Skills (`hi3d-skills`)

> **Generate 3D models from Claude or Cursor in one prompt** — AI Agent Skills for HI3D (GLB/OBJ/STL/FBX/USDZ) via `hi3d-cli`.

Official collection of AI Agent Skills for [Hi3D](https://docs.hi3d.ai) 3D Model Generation. Works with Claude Code, Cursor, Antigravity, and any `skills.sh` compatible agent.

## Skills Included

### `hi3d-generate`
Enables AI agents to generate 3D models from 2D images, reliefs, splitting, and multicolor meshes via `hi3d-cli` (Node.js >=18, zero runtime deps).

**Capabilities:**
- **Image-to-3D** — single or multi-view (`--multi-images`, `--multi-images-bit`) → `obj`/`glb`/`stl`/`fbx`/`usdz`/`3mf`
  - Modes: `1` geometry-only, `2` texture staged, `3` all-in-one
  - Models: `hi3dv3.0` (2048quality/master, PBR), `hitem3dv2.1` (1536fast/pro), `hitem3dv2.0`, `hitem3dv1.5`
  - Portrait: `scene-portraitv2.1` (profast/pro)
- **Relief** — image to 3D relief (`pro` 2K / `base` 1K) → `exr`/`png`/`stl`/`glb` with `--height-relief`, `--rmbg`, `--shape-base`, `--thickness-base`, `--sculpmode`
- **Split** — 3D model split (`character` with `--part a..f`, `--joint`, `--merge` / `general` with `--level`)
- **Multicolor** — 3D multicolor mesh (`--number-color` 1..8)

## Quick Start

```bash
# 1. Install CLI (once)
npm i -g hi3d-cli
hi3d setup  # save ak_/sk_ from https://platform.hi3d.ai/console/apiKey

# 2. Install skill to your agent
npx -y skills add MIt9/hi3d-skills/hi3d-generate

# 3. Ask your agent
# "Generate a 3D chair from ./chair.png as GLB with hi3dv3.0"
# "Make a relief from portrait.png with height 2.5 as STL"
```

**Without agent — direct CLI:**
```bash
hi3d run image-to-3d --image ./chair.png --model hi3dv3.0 --format glb --resolution 2048quality --wait --download ./out
hi3d run relief --image ./portrait.png --model pro --height-relief 2.5 --format stl --wait --download ./out
```

## Tools (via `hi3d-cli`)

| Command | Description |
|---|---|
| `hi3d setup` | Interactive wizard for API keys + skill install |
| `hi3d config --set-access-key --set-secret-key` | Save credentials to `~/.hi3d/config.json` |
| `hi3d balance` | Check credit balance |
| `hi3d run image-to-3d --image --model --format --resolution --wait --download` | Single/multi-view 3D generation |
| `hi3d run relief --image --model --format --height-relief ...` | 3D relief generation |
| `hi3d run split --mesh --model --part --joint --format` | Split 3D model |
| `hi3d run multicolor --mesh --number-color --format` | Multicolor mesh |
| `hi3d status <task_id>` | Query task status & download |

See `hi3d run --help` and `hi3d setup --help` for all flags.

## Example Prompt for Agent

> Generate a 3D model from `front.jpg` and `left.jpg` (bit 1010) as `glb` with `hi3dv3.0` 2048quality, then create a multicolor version with 4 colors.

Agent will:
1. `hi3d run image-to-3d --multi-images ./front.jpg,./left.jpg --multi-images-bit 1010 --format glb --model hi3dv3.0 --resolution 2048quality --wait --download ./out`
2. `hi3d run multicolor --mesh ./out/model.glb --number-color 4 --format glb --wait --download ./out`

## Requirements

- Node.js >= 18 (zero runtime dependencies)
- Hi3D API credentials (`ak_...` + `sk_...` from [platform.hi3d.ai](https://platform.hi3d.ai/console/apiKey))
- `hi3d-cli` (`npm i -g hi3d-cli`)

## Installation

Add skill to your AI Agent environment:

```bash
npx -y skills add MIt9/hi3d-skills/hi3d-generate
```

Or copy manually: `skills/hi3d-generate/SKILL.md` → your agent's skills folder.

## Links

- Hi3D Docs: https://docs.hi3d.ai
- CLI: https://github.com/MIt9/hi3d-cli (npm `hi3d-cli`)
- Skills: https://github.com/MIt9/hi3d-skills

## License

MIT
