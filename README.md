# Unity Game Dev Skill

A Claude skill that makes the AI act like a **Principal Game Architect and Senior Unity Engineer**. It turns vague game ideas into buildable specs and produces production-quality, **reusable** and **optimized** Unity 6 C# code.

> Think before coding. Reuse before writing. Measure before optimizing.

---

## Table of Contents

- [What it does](#what-it-does)
- [Key features](#key-features)
- [Repository structure](#repository-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Example prompts](#example-prompts)
- [How it works](#how-it-works)
- [Unity 6 defaults](#unity-6-defaults)
- [Output format](#output-format)
- [Customizing the skill](#customizing-the-skill)
- [Contributing](#contributing)
- [License](#license)

---

## What it does

Give Claude a request such as "build a character controller" or "design a battle pass economy". The skill makes Claude:

1. Classify the request (domain, scope, platform, genre).
2. Expand hidden requirements and mark each as MVP, Later, or Out of scope.
3. Discover connected systems and define clean interfaces between them.
4. Write **Design Notes** before any code (frequency, scale, worst case, data owner, test, metric).
5. Generate compilable, allocation-aware, reusable C# for Unity 6.
6. Provide setup steps, tests, a performance plan, risks, and release checklists.

The depth scales with the request. A small question gets a short answer. A full system gets a full spec. A whole game gets the complete pipeline.

## Key features

| Feature | Description |
|---|---|
| **Think-before-code step** | 10-question pre-code checklist and a Design Notes template |
| **Reusable code rules** | Interfaces, composition, pure C# core, data-driven design, generics, per-module assemblies |
| **Optimized code rules** | 16 default "instead of X, use Y" patterns, escalation ladder, performance contract on every code block |
| **Unity 6 specific** | New Input System, Cinemachine 3, UI Toolkit, Addressables, Awaitable, URP, obsolete API warnings |
| **Architecture defaults** | No global singletons, assembly definitions, ScriptableObject rules, event and state machine patterns |
| **Multiplayer guidance** | Topology choice (Netcode for GameObjects / Entities, Multiplayer Services), authority, prediction |
| **Platform budgets** | Frame and memory starting points for mobile, PC, console, Steam Deck |
| **Testing** | EditMode, PlayMode, performance tests, content validators, CI, device matrix |
| **Live-ops ready** | Versioned saves, economy design, analytics, remote config hooks |
| **Image analysis** | Turns concept art or screenshots into a Unity recreation spec |
| **Release checklists** | Production, Steam, PlayStation, Xbox, Switch, iOS, Android, legal, live service |
| **Quality gate** | Self-check before delivering, plus a list of anti-patterns to avoid |

## Repository structure

```
unity-game-dev/
├── SKILL.md      # The skill (instructions Claude follows)
└── README.md     # This file
```

## Installation

### Claude (claude.ai / desktop app)

1. Download or clone this repository.
2. Make sure the folder is named `unity-game-dev` and contains `SKILL.md`.
3. Zip the folder if your client asks for a zip.
4. Open **Settings → Capabilities / Skills** and upload the skill.
5. Enable the skill.

### Claude Code

Copy the folder into your skills directory:

```bash
# Personal (all projects)
mkdir -p ~/.claude/skills
cp -r unity-game-dev ~/.claude/skills/

# Or per project
mkdir -p .claude/skills
cp -r unity-game-dev .claude/skills/
```

Restart or reload Claude Code, then run `/skills` to confirm `unity-game-dev` is listed.

> Menus and paths can differ between Claude versions. Check the official Claude documentation if a step does not match.

## Usage

The skill triggers automatically when you ask about Unity game design, architecture, code, optimization, multiplayer, UI, AI, saves, economy, or builds. You can also name it directly:

```
Use the unity-game-dev skill to build an enemy AI system.
```

For best results, include:

- **Genre and perspective** (2D/3D, first person, third person, top-down, isometric)
- **Target platforms** (mobile, PC, console, Steam Deck)
- **Single player or multiplayer**
- **Unity version and render pipeline** (URP / HDRP)
- **Existing code or packages** you already use

## Example prompts

```
Build a third-person character controller with walk, run, jump, and slide.
Target PC and Steam Deck. Single player.
```

```
Design an inventory system with stacking, equipment slots, and save/load.
Make it reusable across player, chests, and shops.
```

```
Review this script for performance problems and rewrite it with zero GC allocations.
```

```
Design a 3v3 online arena shooter architecture using Netcode for GameObjects.
Include prediction, lag compensation, and a bandwidth budget.
```

```
Here is a screenshot of a game. Analyze the art style and give me a Unity
recreation spec (URP, camera, shaders, lighting, UI).
```

```
Design the economy and battle pass for a mobile live-service game.
```

## How it works

```
Request
  ↓
Intake: classify domain, scope, platform, context
  ↓
Requirement expansion and system discovery (MVP / Later / Out of scope)
  ↓
Think before you code: Design Notes (frequency, scale, reuse, hot path, test)
  ↓
Architecture: modules, interfaces, events, state flow
  ↓
Code: reusable + optimized + performance contract
  ↓
Setup steps, tests, performance plan, risks
  ↓
Quality gate → Deliver
```

## Unity 6 defaults

| Area | Default |
|---|---|
| Render pipeline | URP (HDRP only for high-end visuals) |
| Input | New Input System with Input Action assets |
| Camera | Cinemachine 3 |
| UI | UI Toolkit (uGUI where world-space or legacy requires it) |
| Content | Addressables for large or optional content |
| Async | Awaitable and cancellation tokens |
| Pooling | `UnityEngine.Pool` |
| Architecture | Composition, interfaces, ScriptableObject data, assembly definitions, no global singletons |
| Multiplayer | Netcode for GameObjects / Entities, Unity Multiplayer Services |
| DOTS / ECS | Only when entity counts or CPU profile justify it |
| Localization | Unity Localization package from the start |

## Output format

Depending on scope, the skill produces some or all of:

1. Summary and assumptions
2. Requirements (MVP / Later) and connected systems
3. Architecture (Mermaid class, data, event, and state diagrams)
4. Design Notes
5. Folder and file list
6. Full C# code with a performance contract per block
7. Editor setup steps
8. Performance plan and how to measure
9. Tests (EditMode, PlayMode, performance)
10. Risks and mitigations
11. Future expansion
12. Production and commercial release checklists (for full games)

## Customizing the skill

Open `SKILL.md` and edit it to fit your team:

- Change **Unity 6 technical defaults** (section 3) to match your stack, for example HDRP, Photon Fusion, or VContainer.
- Edit the **project layout** (section 6) to match your folder conventions.
- Adjust **platform budgets** to your target devices.
- Add your own **coding standards** and **anti-patterns**.
- Add platform-specific checklists for your publishing targets.

Keep the `name` and `description` in the front matter. The description is what tells Claude when to use the skill.

## Contributing

Contributions are welcome.

1. Fork the repository.
2. Create a branch: `git checkout -b feature/your-change`.
3. Make your change and test it with real prompts.
4. Open a pull request describing what changed and why.

Ideas for contributions: reference files for specific systems (combat, inventory, networking), HDRP-specific guidance, console certification details, and more code templates.

## Disclaimer

Generated code and designs are starting points. Always profile on target devices, test thoroughly, and verify APIs against the Unity version your project uses. Platform requirements and store policies change, so check the current official documentation before release.

## License

Add your license here (for example MIT) and include a `LICENSE` file in the repository.
