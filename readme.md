# Virtual Ambulance Emergency Response Simulation

**Final Course Project — Computer Graphics and Visualization (SBEG353/SBES140)**
**Spring 2025/2026 — Cairo University**

---

##  Table of Contents

- [Project Overview](#-project-overview)
- [Team Members](#-team-members)
- [Technical Specifications](#-technical-specifications)
- [Virtual Environment](#-virtual-environment)
- [Hero Objects](#-hero-objects)
- [Character System](#-character-system)
- [Emergency Response Sequence](#-emergency-response-sequence)
- [Lighting & Rendering](#-lighting--rendering)
- [Physics & Simulations](#-physics--simulations)
- [Object Interaction & Collision](#-object-interaction--collision)
- [Audio & Narration](#-audio--narration)
- [AI Tools Usage](#-ai-tools-usage)
- [Asset Credits](#-asset-credits)
- [Installation & Setup](#-installation--setup)
- [Future Enhancements](#-future-enhancements)
- [References](#-references)

---

##  Project Overview

**Virtual Ambulance Emergency Response Simulation** is a comprehensive 3D visualization project that models a complete urban emergency medical response workflow. The simulation follows a chronological emergency response sequence:

- **Car crash** at a night-time urban intersection with vehicle collision physics
- **Emergency call** received at the hospital reception desk
- **CPR** administered by a paramedic at the accident scene
- **Ambulance arrives** at the hospital with dynamic reflective emergency lighting

The project demonstrates practical application of core computer graphics concepts, including environment modeling, UV mapping and texturing, skeletal character animation with inverse kinematics, physics-based rigid-body and particle simulation, multi-source lighting design, and object/character collision handling.

---

##  Team Members

<img width="336" height="557" alt="image" src="https://github.com/user-attachments/assets/4e15fd05-ee5b-4c8a-96ca-98d978f640d5" />

---

## Project Resources

<a href="https://drive.google.com/drive/u/2/folders/1B-ugdRD1HMusHSiMQmOXK2HNwXu8TAU5"> Google Drive Link </a>

**This link contains:**

- Full animation video
- Blender files
- Assets
- report
---

##  Technical Specifications

| Category | Specification |
|----------|----------------|
| **Software** | Blender 3.x |
| **Render Engine** | Cycles (Path Tracing) |
| **Resolution** | 1440px × 810px |
| **Samples** | 256 - 500 samples per pixel (adaptive sampling enabled) (depending on hardware) |
| **Denoising** | OptiX AI Denoiser |
| **Simulation Rate** | 24 frames per second (physics) |
| **Polygon Count** | ~15,000 triangles (ambulance) |
| **Character Rig** | 65 bones per character (including finger chains) |
| **Spine Hierarchy** | root → pelvis → spine1–3 → neck → head chain |
| **Physics Engine** | Blender Rigid Body |

---

##  Virtual Environment

### Urban Street and City Block

The primary outdoor environment represents a dense urban district modeled from reference photographs of mid-rise commercial blocks, with careful attention to scale and proportion between vehicles, pedestrians, and buildings.

**Key features:**
- High-rise glass office towers with grid-pattern façades
- Multi-lane intersection with pedestrian crosswalks
- Street lamps with warm point lighting (2800K, 0.3m radius)
- Traffic signals and planted trees
- PBR materials: glass panels with specular BSDF, concrete with diffuse-rough BSDF
- Asphalt road surfaces with tuned roughness values

**Materials Implementation:**
| Surface | Material Type | Shader Nodes |
|---------|--------------|--------------|
| Glass | Specular | Glass BSDF + Glossy |
| Concrete | Diffuse | Diffuse BSDF + Roughness |
| Asphalt | Rough | Principled BSDF (roughness 0.9) |

### Hospital Exterior and Interior

A dedicated hospital building features a prominent red-cross emblem and a ground-floor glazed entrance, following contemporary hospital architecture with clean geometric lines.

**Exterior Elements:**
- Red-cross emblem on façade
- Ground-floor glazed entrance
- Clean geometric architecture
- Hospital signage

**Interior Elements:**
- Curved wooden desk labeled "Welcome / Reception"
- Office chairs and flat-panel monitors
- CAUTION: WET FLOOR sign
- Wheelchair
- Department signage (Intensive Care Unit, Emergency Department, Radiology)
- Material variety: wood shader with anisotropic reflections, specular terrazzo flooring, transparent BSDF glass partitions

**Materials Implementation:**
| Element | Material Type | Shader Nodes |
|---------|--------------|--------------|
| Reception Desk | Wood | Principled BSDF + Anisotropic |
| Floor Tiles | Terrazzo | Principled BSDF + Specular |
| Glass Partition | Transparent | Transparent BSDF + Refraction |

### Accident Site

A night-time urban intersection serves as the accident site, chosen for dramatic lighting potential and contrast between emergency vehicles and the dark environment.

**Features:**
- Two-car collision with debris particles
- Volumetric fog via a Volume Scatter node in the world shader
- Dynamic street lighting
- Wet asphalt materials supporting reflective emergency-light rendering

---

##  Hero Objects

Per the project specification, a team of six requires **three hero objects** (⌈6/2⌉ = 3), modeled entirely from scratch by the team.

### 1. Male Character (Reciptionist)

**Modeling Process:**
- Sculpted base mesh with topology optimized for animation and rigging
- Progressive refinement of facial features, hair geometry, and clothing layers
- **Polygon Count:** ~25,000–30,000 triangles (including hair cards and clothing)
- **Details:** Separately modeled hair volume, shirt collar, detailed hands, and a low-poly vintage cordless phone prop

**Texturing:**
- UV-unwrapped head and skin coordinates for seamless face textures
- UV-unwrapped clothing meshes (sweater and pants)
- Dedicated UV mapping for the hand-held phone accessory
- Clean procedural mapping for fabric folds and wrinkles

**Materials:**
- Sweater: Dark satin/synthetic fabric shader with a smooth specular gloss map for surface highlights
- Pants: Dark, high-gloss leather or vinyl material with sharp specular reflections
- Skin: Subsurface scattering (SSS) shader with low roughness for a realistic skin sheen
- Hair: Dark diffuse material with subtle anisotropic reflections

### 2. Medical Stretcher

**Modeling Process:**
| Component | Primitive Used |
|-----------|----------------|
| Legs | Cylinders |
| Wheel Axles | Cylinders |
| Frame Rails | Cubes |
| Cross-braces | Cubes |
| Mattress Surface | Subdivided Plane |

**Design:** Standard hospital stretcher dimensions with adjustable backrest geometry

**Materials:**
| Component | Material | Shader Type |
|-----------|----------|-------------|
| Mattress | Orange Vinyl | Rough Diffuse |
| Frame | Stainless Steel | Metallic PBR |

**Optimization:** Instanced wheel geometry for a lightweight mesh

### 3. Hospital Reception Desk

**Modeling Process:**
- Circular arc extruded along the Z-axis
- Beveled top (radius 2 m) to accommodate multiple staff positions
- Embossed "Welcome" text using Blender's text-to-mesh workflow

**Texturing:**
- Wood-grain texture (1K albedo + roughness + normal)
- Smart UV unwrapping
- Typography integration

---

##  Character System

### Character Archetypes

| Character | Description | Attire |
|-----------|-------------|--------|
| **Receptionist** | Male, professional | Dark business suit with tie |
| **Paramedic** | Emergency responder | White hazmat-style jumpsuit, blue gloves, medical vest |
| **Patient** | Civilian casualty | White shirt, dark trousers |

### Rigging System

**Skeleton Structure:**
- Full humanoid armature
- **65 bones** including finger chains and facial control bones
- **Spine hierarchy:** root → pelvis → spine1–3 → neck → head chain

**IK Constraints Applied:**
- Wrists: For realistic grip on equipment and stretcher
- Ankles: For proper foot placement on terrain
- Elbows: For natural arm bending during CPR
- Knees: For natural leg bending during kneeling

**Source:** Base meshes from Mixamo, refined and rigged in Blender

### Animations Created

| Animation | Character | Description | IK Application |
|-----------|-----------|-------------|----------------|
| **Phone Call** | Receptionist | Holds receiver to ear with natural arm position and subtle body sway | Wrist IK to phone position |
| **CPR Compressions** | Paramedic | Kneels over fallen patient performing rhythmic chest-compression motion | Hand IK to patient's chest, elbow lock |
| **Stretcher Push** | Paramedic | Pushes loaded stretcher with walking cycle synchronized to forward motion | Hand IK to stretcher handle, foot IK to ground |
| **Patient Lying** | Patient | Supine rest pose on stretcher with arms resting on chest | Full body rest pose |
| **Walking** | Bystander | Walk cycle with natural arm swing and gait | Foot IK for ground contact |

### Animation Keyframes

| Animation | Duration | Keyframes | Sync Rate |
|-----------|----------|-----------|-----------|
| Phone Call | 5 seconds | 150 frames | 30 fps |
| CPR Cycle | 2 seconds | 60 frames | 30 fps |
| Stretcher Push | 8 seconds | 240 frames | 30 fps |
| Walking Cycle | 2 seconds | 60 frames | 30 fps |

---

##  Emergency Response Sequence

The simulation follows a linear emergency response sequence with four distinct phases, satisfying the requirement of ⌈6/2⌉ = 3 scenarios for a six-person team.

### Phase 1: Car Crash 

A traffic collision occurs at a fog-covered night intersection. An SUV impacts a stationary vehicle, triggering debris particles and volumetric fog.

**Technical Implementation:**

| Parameter | Value |
|-----------|-------|
| Physics Engine | Blender Rigid Body |
| Simulation Rate | 60 fps |
| Vehicle Mass | 1,800 kg |
| Restitution | 0.3 |
| Friction | 0.8 |
| Collision Shape | Mesh |
| Baking Duration | 250 frames |
| Baking Cache | Visual Transform |

**Effects Applied:**
- Particle-based debris (3,000 particles)
- Volumetric fog (Volume Scatter node)
- Dynamic headlight illumination
- Street-lamp lighting
- Dramatic shadows

### Phase 2: Emergency Call at Hospital Reception 

Simultaneously, inside the hospital reception, the receptionist answers the emergency call.

**Technical Implementation:**

| Element | Description |
|---------|-------------|
| Animation | Phone-call with natural arm position and subtle body sway |
| Duration | 10 seconds |
| Props | Monitors, keyboard, CAUTION: WET FLOOR sign, wheelchair |
| Signage | ICU, Emergency Department, Radiology |
| Environment | Curved wooden desk, terrazzo flooring, glass partitions |

### Phase 3: CPR at the Scene 

Following the collision, a paramedic kneels beside the fallen patient and performs cardiopulmonary resuscitation (CPR).

**Technical Implementation:**

| Element | Description |
|---------|-------------|
| Animation | Rhythmic chest-compression cycle |
| Keyframes | 60 frames per 2-second cycle |
| IK Setup | Paramedic's hands constrained to patient's chest |
| Compression Depth | ~5 cm (visual) |
| Compression Rate | ~100-120 compressions per minute |
| Patient Position | Supine with arms resting on chest |

### Phase 4: Ambulance Arrives at Hospital 

The ambulance arrives at the hospital entrance with emergency lights flashing, completing the emergency response chain.

**Technical Implementation:**

| Element | Description |
|---------|-------------|
| Lighting | Emissive shader nodes (alternating red and blue) |
| Reflection Type | Ray-traced coloured streaks |
| Surfaces | Wet asphalt, glass façade |
| Character Interaction | Paramedic pushes loaded stretcher |
| Walk Sync | Walking cycle synchronised to forward motion |
| Duration | 15 seconds |

---

##  Lighting & Rendering

All scenes were rendered using Blender's Cycles path-tracing engine with high-quality settings.

### Light Types

| Light Type | Application | Technical Details |
|------------|-------------|---------------------|
| **Sun (Directional)** | Outdoor shadows | Intensity 1.0, angle 0.5° |
| **Point Lights** | Street-lamp illumination | 2800K color temp, 0.3m radius, warm white |
| **Spotlights** | Ambulance headlamps, rear floodlight | 30° cut-off, 5° penumbra |
| **Emission Materials** | Light-bar LEDs, neon signs | Self-illumination with controlled intensity |
| **Volumetric Scatter** | Fog for night-time accident site | Volume Scatter node in world shader |

### Lighting Scenes

| Scene | Light Sources | Color Temperature | Purpose |
|-------|--------------|-------------------|---------|
| Urban Day | Sun, Ambient | 6500K | Natural daylight |
| Urban Night | Point (street lamps), Ambient | 2800K | Warm night atmosphere |
| Accident Site | Point, Spot, Volumetric | 2800K-3200K | Dramatic emergency lighting |
| Hospital Interior | Point, Ambient | 3500K | Indoor professional lighting |
| Hospital Arrival | Emission (light-bar), Spot | Mixed | Dynamic emergency lighting |

### Rendering Settings

| Parameter | Setting |
|-----------|---------|
| Engine | Cycles |
| Samples | 256 (adaptive) |
| Denoiser | OptiX AI |
| Resolution | 1920×1080 |
| Motion Blur | 180° shutter, strength 0.5 |
| Render Time | ~30 minutes per frame (GPU) |

---

## 🔬 Physics & Simulations

### Vehicle Impact Dynamics

| Parameter | Value | Description |
|-----------|-------|-------------|
| Engine | Blender Rigid Body | Physics simulation engine |
| Simulation Rate | 60 fps | Frames per second |
| Vehicle Mass | 1,800 kg | SUV weight |
| Restitution | 0.3 | Bounce coefficient |
| Friction | 0.8 | Surface friction |
| Collision Shape | Mesh | Detailed collision geometry |
| Baking Duration | 250 frames | Simulation duration |
| Caching | Visual Transform | For artistic control |

### Atmospheric Weather Particles

**Rain System:**
| Parameter | Value |
|-----------|-------|
| Particle Count | 50,000 |
| Geometry | Elongated icospheres |
| Scale | 0.02 |
| Force Field | -Y direction |
| Turbulence | Strength 1.5 |
| Wind | Randomized |

**Debris System:**
| Parameter | Value |
|-----------|-------|
| Particle Count | 3,000 |
| Geometry | Spark/fragment objects |
| Initial Burst | High velocity |
| Drag | Moderate |
| Visual | Flying glass and fragments |

### Fire Particle System (Optional)

| Parameter | Value |
|-----------|-------|
| Emitter | Hospital roof surface |
| Particle Count | 5,000+ |
| Motion | Upward convection |
| Turbulence | Strong |
| Visual | Orange-red emissive materials |
| Lighting | Red volumetric lighting |

---

## 🔄 Object Interaction & Collision

### Character Path Navigation

- **Method:** Follow Path constraints linked to Bézier curves
- **Paths:** Pavements, ramps, and corridors
- **Avoidance:** Implicit obstacle avoidance (no full navigation mesh)
- **Movement:** Characters move through environment (not in-place)

### Rigid-Body Vehicle Collision

- **Active Body:** SUV (Rigid Body - Active)
- **Collision Shape:** Mesh
- **Passive Body:** Road surface
- **Keyframed Impulse:** Frame 60
- **Baking:** 250 frames
- **Cache:** Visual Transform for artistic control

### Stretcher-Character Interaction

| Constraint Type | Application | Purpose |
|-----------------|-------------|---------|
| Copy Location | Hand bones to stretcher frame | Hands follow stretcher |
| Damped Track | Hand bones to stretcher handle | Hands oriented to grip |
| IK Constraint | Wrists to hand empties | Natural arm bending |
| Parent | Hand empties to stretcher | Maintain grip position |

### Collision Types Implemented

| Collision Type | Objects | Method |
|----------------|---------|--------|
| Vehicle-Road | SUV, Road | Rigid Body Physics |
| Vehicle-Vehicle | SUV, Stationary Car | Rigid Body Physics |
| Character-Ground | Characters, Ground | IK constraints |
| Character-Stretcher | Paramedic, Stretcher | Copy Location constraints |
| Object-Environment | Stretcher, Hospital | Manual path placement |

---

## 🎙️ Audio & Narration

A scripted voice-over narration accompanies the final demonstration video, guiding the viewer through each phase of the emergency response sequence.

**Narration Structure:**

| Phase | Content |
|-------|---------|
| Introduction | Project overview, objectives |
| Phase 1 | Car crash, physics simulation, debris |
| Phase 2 | Emergency call, hospital reception |
| Phase 3 | CPR, paramedic animation, IK system |
| Phase 4 | Ambulance arrival, reflective lighting |
| Conclusion | Summary, future work |

**Audio Specifications:**
- Format: MP3
- Bitrate: 192 kbps
- Sample Rate: 44.1 kHz
- Channels: Stereo

---

## 🤖 AI Tools Usage

In compliance with the course AI usage policy:

| Tool | Purpose | Implementation |
|------|---------|----------------|
| **ChatGPT 4o** | Script generation | Generated Python drivers for ambulance light-bar flicker animation; documentation assistance for this report. All generated scripts were reviewed and modified by the team. |
| **Midjourney v6** | Reference mood board | Used for scene color grading and lighting direction inspiration. No AI-generated images used in final renders. |

**Compliance Statement:** All creative modeling, rigging, animation, and rendering work was performed manually by team members in Blender, ensuring original artistic contribution.

---

## 📦 Asset Credits

| Category | Asset | Source | License |
|----------|-------|--------|---------|
| Environment | City building pack | Sketchfab | CC-BY 4.0 |
| Environment | Street furniture | BlenderKit | Free Tier |
| Environment | Tree foliage | Botaniq (Lite) | GPL |
| Characters | Character base meshes | Mixamo | Adobe EULA |
| Vehicles | Ambulance textures | Textures.com | Standard |

**Hero Objects (Team Created):**
- Ambulance Vehicle
- Medical Stretcher
- Hospital Reception Desk

---

## 🛠️ Installation & Setup

### Prerequisites

- **Blender 3.x** or higher ([Download](https://www.blender.org/download/))
- **System Requirements:** 8GB+ RAM, GPU with CUDA support recommended for Cycles rendering
- **Git** (optional, for cloning repository)

### Quick Setup

```bash
# Clone the repository
git clone https://github.com/yourusername/virtual-ambulance-simulation.git
cd virtual-ambulance-simulation

# Open Blender and load the project
blender assets/models/main_scene.blend

# Configure render settings:
# 1. Render Properties → Cycles
# 2. Samples: 256 (adaptive)
# 3. OptiX AI Denoiser: Enabled

# Render animation:
# Output Properties → FFmpeg video or image sequence
# Render → Render Animation (F12)
