# 🎮 Godot Game Development Repository

A personal game development repository built with the [Godot Engine](https://godotengine.org/). Each subdirectory is a self-contained Godot project — a small game, a mechanic prototype, or a learning exercise — developed as a way to build intuition for Godot's scene system, GDScript, and 2D game loops.

> **Engine version:** Godot **4.7** (Forward+ renderer, Jolt Physics)
> **Language:** GDScript

## 📌 Table of Contents

- [Overview](#-overview)
- [Projects](#-projects)
- [Tech Stack](#-tech-stack)
- [Repository Structure](#-repository-structure)
- [Getting Started](#-getting-started)
- [Running a Project](#-running-a-project)
- [Repository Conventions](#-repository-conventions)
- [Git & Godot Best Practices](#-git--godot-best-practices)
- [Known Issues](#-known-issues)
- [Contributing](#-contributing)
- [License](#-license)

## 🔍 Overview

This repository is a growing collection of Godot projects, ordered by progression. Rather than one large game, the goal is to build many small, complete projects that each isolate a specific concept — physics bodies and collision, input handling, scene instancing, UI, and animation.

Each project is intentionally standalone so it can be opened, run, and understood on its own without depending on scaffolding from a previous project.

## 🎮 Projects

| # | Project | Genre / Focus | Engine | Status |
|---|---------|---------------|--------|--------|
| 1 | [`1-pong/`](1-pong/) | Pong — 2D physics, input, scene instancing | Godot 4.7 | 🚧 Scaffold |

### 1 — Pong

A two-paddle Pong clone, the classic "first game" for learning 2D physics and input handling.

**Scope**

- Paddle movement driven by input actions
- Ball with constant velocity and wall/paddle collision
- Score tracking between two players
- Serve/reset flow after a point is scored
- Simple score UI

**Current state:** The project is a working scaffold. `scenes/ui.tscn` is the main scene and sets up the UI layer with a `Play` button wired to `_on_button_pressed()`, and it instances `scenes/main.tscn` as the game board. `scripts/ui.gd` currently contains only placeholder callbacks, and `scenes/main.tscn` is still an empty `Node2D` root — the paddles, ball, and scoring logic are not implemented yet.

**How to run:** See [Running a Project](#running-a-project).

## 🛠 Tech Stack

| Component | Choice |
|-----------|--------|
| **Engine** | Godot 4.7 |
| **Renderer** | Forward+ (Vulkan) |
| **Language** | GDScript |
| **Physics** | Jolt Physics (3D), Godot's built-in 2D physics |
| **Version Control** | Git |
| **Platform / Editor** | Linux, macOS, Windows |

## 📂 Repository Structure

```
.
├── 📁 1-pong/                  # Pong clone (Godot project)
│   ├── 📁 assets/
│   │   └── 📁 placeholder/     # Icon and temporary art
│   ├── 📁 scenes/              # .tscn scene files
│   ├── 📁 scripts/             # .gd GDScript files
│   ├── .editorconfig           # Editor formatting rules
│   ├── .gitattributes          # Line-ending normalization
│   ├── .gitignore              # Godot-specific ignores
│   └── project.godot           # Project settings & main scene
├── LICENSE.txt                 # Apache License 2.0
└── README.md                   # This file
```

## 🚀 Getting Started

### Prerequisites

- [Godot Engine](https://godotengine.org/download) **4.7 or newer**
  - Use the **standard** build, not the *export templates* or *console* builds.
  - Make sure your build includes **Jolt Physics**, which `1-pong` selects in its project settings.
- [Git](https://git-scm.com/)

Verify your install:

```bash
godot --version
# Godot Engine v4.7.2.stable...
```

### Installation

1. **Clone the repository:**

   ```bash
   git clone https://github.com/OakJustify/LEARN_GODOT.git
   ```

2. **Navigate into the project you want to work on:**

   ```bash
   cd LEARN_GODOT/1-pong
   ```

3. **Open it in the Godot editor:**

   ```bash
   godot --editor .
   ```

   Or launch Godot normally and use **Project → Import → Browse** to select the folder containing `project.godot`.

On the first open, Godot reimports assets and generates the `.godot/` cache directory. This takes a few seconds and is expected — that folder is intentionally not tracked by Git.

## 💻 Running a Project

From inside a project directory:

```bash
# Run the game
godot .

# Open in the editor
godot --editor .
```

From the repository root, target a specific project with `--path`:

```bash
# Run 1-pong
godot --path 1-pong
```

To smoke-test a project without opening a window (useful in CI):

```bash
godot --headless --path 1-pong --quit-after 3
```

## 📐 Repository Conventions

- **Numbered project folders.** Projects are prefixed with a sequence number and a slug: `1-pong`, `2-<name>`, and so on. This keeps the folder order in the file browser matching the intended learning progression.
- **One Godot project per folder.** A directory is a Godot project if it contains a `project.godot` file. Don't nest projects inside each other.
- **Keep the default Godot layout.** Use `scenes/`, `scripts/`, and `assets/` rather than inventing new top-level folders, so structure stays consistent across projects.
- **Use tabs for GDScript indentation** — this is what the Godot editor produces and what `.editorconfig` enforces.
- **Name scenes and scripts in lowercase** (`main.tscn`, `ui.gd`), matching the scenes already in the repository.

## 🔀 Git & Godot Best Practices

These are the rules that keep a Godot repository clean. Most are already applied by the per-project `.gitignore`.

- **Never commit `.godot/`.** This is the engine's import cache and editor state. It is machine-specific, large, and regenerates automatically. It is already ignored in `1-pong/.gitignore`.
- **Do commit `*.import` files.** These hold the import settings (compression, mipmaps, filters) for each asset. Godot's official guidance is to version them so every machine imports assets identically. `icon.svg.import` is tracked for this reason.
- **Do commit `.uid` files.** Since Godot 4.4, scripts, scenes, and resources have unique IDs used by `uid://` references. Deleting these breaks references. `scripts/ui.gd.uid` is tracked for this reason.
- **Add `export_presets.cfg` when you need to build an executable.** It is intentionally absent until a project has an export target, since it embeds local paths and credentials.
- **Avoid committing exported builds** unless the project explicitly distributes them.
- **Prefer small, focused commits** — one feature or one fix per commit.

## ⚠️ Known Issues

Items currently outstanding in the repository:

- **`1-pong/project.godot` points `config/icon` at `res://icon.svg`,** but the icon actually lives at `res://assets/placeholder/icon.svg`. The path should be corrected or the icon moved to the project root.
- **`1-pong/scripts/ui.gd` is a stub.** `_on_button_pressed()` ends in a bare `get_tree()` call that does nothing yet, and `_ready()` / `_process()` are empty.
- **`1-pong/scenes/main.tscn` is an empty `Node2D`.** No game objects, collision shapes, or nodes exist yet.
- **No root-level `.gitignore`.** The `.gitignore` lives inside `1-pong/`, so a `.godot/` folder created at the repository root would not be ignored. Add a root `.gitignore` if any project is ever moved up a level.
- **`LICENSE.txt` still contains the Apache boilerplate placeholders** (`[yyyy]` and `[name of copyright owner]`) rather than a real copyright line.

## 🤝 Contributing

Contributions, feedback, and suggestions are welcome.

1. Fork the repository.
2. Create a branch for your work (`git switch -c feature/your-feature`).
3. Make your changes — keep them scoped, and commit source files only (never `.godot/`).
4. Commit with a descriptive message (`git commit -m 'Add ball bounce to 1-pong'`).
5. Push the branch (`git push origin feature/your-feature`).
6. Open a Pull Request describing what changed and what you tested.

Before opening a PR, verify the project still runs:

```bash
godot --headless --path <project-dir> --quit-after 3
```

## 📜 License

Distributed under the [Apache License 2.0](LICENSE.txt). See [`LICENSE.txt`](LICENSE.txt) for the full terms.

Godot Engine itself is licensed separately under the MIT License and is not part of this repository.
