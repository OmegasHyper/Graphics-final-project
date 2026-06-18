# Virtual Ambulance Emergency Response Simulation

## A Blender-Based 3D Medical Emergency Training Visualization

---

##  Table of Contents

1. [Project Overview](#project-overview)
2. [Team Members](#team-members)
3. [Technical Specifications](#technical-specifications)
4. [Virtual Environment](#virtual-environment)
5. [Hero Objects](#hero-objects)
6. [Character System](#character-system)
7. [Emergency Scenarios](#emergency-scenarios)
8. [Lighting & Rendering](#lighting--rendering)
9. [Physics & Simulations](#physics--simulations)
10. [Project Structure](#project-structure)
11. [Installation & Setup](#installation--setup)
12. [Video Showcase](#video-showcase)
13. [Asset Credits](#asset-credits)
14. [AI Tools Usage](#ai-tools-usage)
15. [Future Enhancements](#future-enhancements)
16. [License](#license)

---

## 🏥 Project Overview

**Virtual Ambulance Emergency Response Simulation** is a comprehensive 3D visualization project developed as the final course project for **Computer Graphics and Visualization** (SBEG353/SBES140) at the **Spring 2025/2026** semester.

The simulation models a complete urban emergency medical response workflow, encompassing a multi-scene virtual environment that includes:
- City streets with traffic infrastructure
- Hospital interiors with reception areas
- Night-time accident sites with vehicle collisions
- Ambulance dispatch and patient evacuation sequences
- **Hospital arrival and fire emergency scenario**

This project demonstrates the practical application of core computer graphics concepts including environment modeling, UV mapping, texture application, skeletal character animation, physics-based rendering, advanced lighting, and collision handling.

👥 Team Members
  

## ⚙️ Technical Specifications

| Category | Specification |
|----------|---------------|
| **Software** | Blender 3.x |
| **Render Engine** | Cycles (Path Tracing) |
| **Resolution** | 1920 × 1080 pixels |
| **Samples** | 256 samples per pixel (adaptive sampling enabled) |
| **Denoising** | OptiX AI Denoiser |
| **Simulation Rate** | 60 frames per second (physics) |
| **Polygon Count** | ~15,000 triangles (ambulance) |
| **Character Bones** | 65 bones per rig (including finger chains) |


---
## The Final Video:

<video width="700" controls>
  <source src="Assets/video_2026-06-18_14-23-03.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

---

## 🌆 Virtual Environment

### Urban Street and City Block

The primary outdoor environment represents a dense urban district modeled from reference photographs of mid-rise commercial blocks. The city block was constructed with careful attention to scale and proportion, ensuring realistic spatial relationships between vehicles, pedestrians, and buildings.

**Key Features:**
- High-rise glass office towers with grid-pattern façades
- Multi-lane intersection with pedestrian crosswalks
- Street lamps with warm point lighting
- Traffic signals and planted trees
- PBR materials (glass panels with specular BSDF, concrete with diffuse-rough BSDF)
- Road surfaces with asphalt materials and appropriate roughness values

### Hospital Exterior and Interior

A dedicated hospital building features a prominent red cross emblem on its facade and a ground-floor glazed entrance. The exterior follows contemporary hospital architecture with clean geometric lines and functional window placement.

**Interior Elements:**
- Curved wooden desk labeled "Welcome / Reception"
- Office chairs and flat-panel monitors
- CAUTION: WET FLOOR sign
- Wheelchair
- Department signage (Intensive Care Unit, Emergency Department, Radiology)
- Material variety: wood shader with anisotropic reflections, specular terrazzo floor tiles, transparent BSDF glass partitions

### Accident Site

A night-time urban intersection serves as the accident site, chosen for its dramatic lighting potential and clear visual contrast between emergency responders' vehicles and the dark environment.

**Features:**
- Two-car collision with debris particles
- Volumetric fog (Volume Scatter node in world shader)
- Dynamic street lighting
- Misty atmospheric conditions for dramatic effect

---

## 🚑 Hero Objects

Per the project specification, the team modeled **three hero objects** entirely from scratch:

### 1. Ambulance Vehicle (Centerpiece)
- **Modeling:** Box-modeling from subdivision-surface base mesh
- **Polygon Count:** ~15,000 triangles
- **Details:** Side mirrors, windshield wipers, door handles, emergency lighting arrays
- **Texturing:** Individual UV unwrapping for body panels, roof light bar, side doors, Star-of-Life decal, "EMERGENCY MEDICAL SERVICES / Keep Back" livery
- **Materials:** Specular maps for realistic environmental reflections, normal maps for panel-line depth

### 2. Medical Stretcher
- **Modeling:** Primitive cylinders (legs and wheel axles), cubes (frame rails), subdivided plane (mattress)
- **Design:** Standard hospital stretcher dimensions with adjustable backrest geometry
- **Materials:** Orange vinyl upholstery (rough diffuse shader), stainless steel frame (metallic PBR material)
- **Optimization:** Instanced wheel geometry for lightweight mesh

### 3. Hospital Reception Desk
- **Modeling:** Circular arc extruded along Z-axis with beveled top (2m radius)
- **Texture:** Wood grain texture (1K albedo + roughness + normal) via smart UV unwrapping
- **Typography:** Embossed "Welcome" text using Blender's text-to-mesh workflow

---

## 🧍 Character System

### Character Archetypes
1. **Receptionist** - Male in dark business suit with tie
2. **Paramedic** - White hazmat-style jumpsuit with blue gloves and medical vest
3. **Patient** - White shirt and dark trousers (civilian casualty)

### Rigging System
- **Skeleton:** Full humanoid armature with 65 bones including finger chains and facial control bones
- **Spine Hierarchy:** root → pelvis → spine1-3 → neck → head chain
- **IK Constraints:** Applied to wrists and ankles for realistic grip and foot placement
- **Source:** Characters sourced from Mixamo, refined in Blender

### Animations Created
| Animation | Description |
|-----------|-------------|
| **Phone Call** | Receptionist holds receiver to ear with natural arm position and subtle body sway |
| **Stretcher Push** | Paramedic pushes loaded stretcher with synchronized walking cycle |
| **Patient Lying** | Supine rest pose on stretcher with arms resting on chest |
| **Triage Crouch** | Paramedic crouches beside fallen patient using lower-body IK |
| **Walking** | Bystander walk cycle with natural arm swing and gait |

---

## 🎬 Emergency Scenarios

### Scenario 1: Traffic Collision and On-Scene Response 🚗💥

A black classic car collides with a stopped vehicle at a fog-covered night intersection.
- **Physics:** Rigid-body simulation with vehicle tipping onto side
- **Visual Effects:** Dynamic lighting from headlights and street lamps, dramatic shadows
- **Response:** Ambulance arrival, scene assessment, patient extraction
- **Atmosphere:** Volumetric fog, particle-based rain and debris

<div align="center">
  <img src=".\Assests for readme\photo_2026-06-18_15-53-48.jpg" alt="Scenario 1 Preview" width="800"/>
  <br>
  <sub><i>Traffic Collision and On-Scene Response</i></sub>
</div>

### Scenario 2: Patient Evacuation by Stretcher 🏥🚑

Following the collision, the patient is loaded onto the stretcher and transported to the waiting ambulance.
- **Character-Object Interaction:** Paramedic's hands constrained to stretcher handle via IK targets
- **Animation Sync:** Stretcher movement timed to match paramedic's walking pace
- **Detail:** Ambulance rear doors remain open, showcasing interior modeling

<div align="center">
  <img src="./assets/screenshots/scenario-2-preview.png" alt="Scenario 2 Preview" width="800"/>
  <br>
  <sub><i>Patient Evacuation by Stretcher</i></sub>
</div>

### Scenario 3: Hospital Arrival and Fire Emergency 🏨🔥

The ambulance arrives at the hospital, completing the emergency response chain. This scenario unfolds in two distinct phases:

#### Phase 1: Hospital Arrival & Patient Handover
- The ambulance pulls up to the hospital entrance with emergency lights flashing
- Paramedics unload the stretcher with the patient
- Patient is wheeled into the hospital reception area
- Receptionist character interacts at the curved wooden desk
- **Key moment:** The paramedic hands over the patient to hospital staff, demonstrating the complete emergency response workflow from accident scene to medical facility

#### Phase 2: Fire Emergency Overlay
- A fire-alarm scenario is triggered within the hospital building
- **Visual Effect:** Bright red volumetric light floods the hospital interior, simulating emergency lighting during a building fire
- **Fire Simulation:** Particle system for fire spread across the roof
- **Ambulance Response:** The ambulance is dispatched to a new emergency outside the burning building
- **Integrated Effects:** Volumetric lighting, particle systems, and dynamic camera perspectives

<div align="center">
  <img src="./assets/screenshots/scenario-3-preview.png" alt="Scenario 3 Preview" width="800"/>
  <br>
  <sub><i>Hospital Arrival and Fire Emergency</i></sub>
</div>

**This scenario effectively demonstrates:**
- Complete patient transport workflow (accident → ambulance → hospital)
- Medical handover procedures between paramedics and hospital staff
- Volumetric lighting for emergency situations
- Particle system fire simulation
- Dynamic scene transitions
- Integration of multiple emergency response elements

---

## 💡 Lighting & Rendering

All scenes were rendered using **Blender's Cycles path-tracing engine** with high-quality settings.

### Lighting Types

| Light Type | Application | Technical Details |
|------------|-------------|-------------------|
| **Sun (Directional)** | Daytime outdoor scenes | Intensity: 1.0, Angle: 0.5° for sharp shadows |
| **Point Lights** | Street lamp illumination | Color temp: ~2800K, Radius: 0.3m, Warm white |
| **Spotlights** | Ambulance headlamps, rear floodlight | Cut-off: 30°, Penumbra: 5° |
| **Emission Materials** | Light bar LEDs, neon signs | Self-illumination with controlled intensity |
| **Volumetric Lighting** | Fire/alarm scenes | Red Volume Scatter medium inside building |

### Rendering Settings
- **Engine:** Cycles Path Tracing
- **Resolution:** 1920 × 1080
- **Samples:** 256 per pixel (adaptive sampling)
- **Denoising:** OptiX AI Denoiser
- **Motion Blur:** Shutter angle 180°, Strength 0.5

---

## 🔬 Physics & Simulations

### Vehicle Impact Dynamics
- **Physics Engine:** Blender's rigid-body system
- **Simulation Rate:** 60 fps
- **Vehicle Mass:** 1,800 kg
- **Restitution:** 0.3
- **Friction:** 0.8
- **Collision Shape:** Mesh
- **Baking:** 250 frames, cached as Visual Transform

### Atmospheric Weather Particles
- **Rain System:** 50,000 elongated mesh instances (scale 0.02)
- **Force Fields:** -Y world-space with randomized turbulence (strength 1.5)
- **Debris System:** 3,000 spark/debris objects from collision impact
- **Initial Burst:** High velocity with drag

### Fire Particle System (Scenario 3)
- **Emitter:** Hospital roof surface
- **Particle Count:** 5,000+ particles
- **Motion:** Upward convection with turbulence
- **Visual:** Orange-red emissive materials with glow
- **Integration:** Synchronized with volumetric red lighting

---

## 📁 Project Structure

```
virtual-ambulance-simulation/
├── README.md
├── Report.pdf
├── assets/
│   ├── textures/
│   │   ├── ambulance/
│   │   ├── buildings/
│   │   ├── hospital/
│   │   └── environment/
│   ├── models/
│   │   ├── ambulance.blend
│   │   ├── stretcher.blend
│   │   ├── reception_desk.blend
│   │   ├── city_block.blend
│   │   └── hospital.blend
│   ├── characters/
│   │   ├── paramedic.blend
│   │   ├── receptionist.blend
│   │   └── patient.blend
│   ├── animations/
│   │   ├── scenario_1.blend
│   │   ├── scenario_2.blend
│   │   └── scenario_3.blend
│   ├── screenshots/
│   │   ├── scenario-1-preview.png
│   │   ├── scenario-2-preview.png
│   │   ├── scenario-3-preview.png
│   │   └── behind-the-scenes.png
│   └── videos/
│       ├── final_video.mp4
│       ├── scenario_1.mp4
│       ├── scenario_2.mp4
│       └── scenario_3.mp4
├── renders/
│   └── final_output/
├── docs/
│   ├── IEEE_Conference_Paper.pdf
│   └── project_presentation.pptx
└── scripts/
    └── ambulance_light_flicker.py
```

---

## 🚀 Installation & Setup

### Prerequisites
- **Blender 3.x** or higher ([Download](https://www.blender.org/download/))
- **System Requirements:** 8GB+ RAM, GPU with CUDA support recommended for Cycles rendering

### Setup Instructions

1. **Clone the repository:**
   ```bash
   git clone https://github.com/yourusername/virtual-ambulance-simulation.git
   cd virtual-ambulance-simulation
   ```

2. **Open Blender:**
   - Launch Blender 3.x or higher

3. **Load the project:**
   - Open the main project file: `assets/models/main_scene.blend`
   - Or navigate to individual scenario files in `assets/animations/`

4. **Configure render settings:**
   - Go to Render Properties tab
   - Select Cycles as render engine
   - Adjust samples as needed (256 recommended for final render)
   - Enable OptiX AI Denoiser for faster clean results

5. **Render the animation:**
   - Go to Output Properties
   - Set output format (FFmpeg video or image sequence)
   - Click Render → Render Animation (F12)

### Quick Render Tips
- For preview renders, reduce samples to 64-128
- Enable adaptive sampling for faster rendering
- Use denoising for noise reduction with fewer samples
- Render in image sequence format for easier error recovery

---

## 🎥 Video Showcase

### Complete Simulation Video
<div align="center">
  <a href="./assets/videos/final_video.mp4">
    <img src="./assets/screenshots/behind-the-scenes.png" alt="Full Simulation Video" width="100%"/>
  </a>
  <br>
  <sub><i>Click to watch the complete emergency response simulation</i></sub>
</div>

### Scenario Breakdown Videos

<div align="center">
  <table>
    <tr>
      <td align="center">
        <a href="./assets/videos/scenario_1.mp4">
          <img src="./assets/screenshots/scenario-1-preview.png" width="400"/>
          <br>
          <b>Traffic Collision</b>
        </a>
      </td>
      <td align="center">
        <a href="./assets/videos/scenario_2.mp4">
          <img src="./assets/screenshots/scenario-2-preview.png" width="400"/>
          <br>
          <b>Patient Evacuation</b>
        </a>
      </td>
    </tr>
    <tr>
      <td align="center">
        <a href="./assets/videos/scenario_3.mp4">
          <img src="./assets/screenshots/scenario-3-preview.png" width="400"/>
          <br>
          <b>Hospital Arrival & Fire</b>
        </a>
      </td>
      <td align="center">
        <a href="./assets/videos/final_video.mp4">
          <img src="./assets/screenshots/behind-the-scenes.png" width="400"/>
          <br>
          <b>Behind the Scenes</b>
        </a>
      </td>
    </tr>
  </table>
</div>

---

## 📦 Asset Credits

### External Assets Used

| Asset | Source | License |
|-------|--------|---------|
| City Building Pack | Sketchfab | CC-BY 4.0 |
| Street Furniture | BlenderKit | Free Tier |
| Character Base Meshes | Mixamo | Adobe EULA |
| Ambulance Textures | Textures.com | Standard |
| Tree Foliage | Botaniq (Lite) | GPL |

All hero objects (ambulance, stretcher, reception desk) were modeled entirely by team members.

---

## 🤖 AI Tools Usage

In compliance with the course AI usage policy:

| Tool | Purpose | Implementation |
|------|---------|----------------|
| **ChatGPT 4o** | Script generation for ambulance light-bar flicker animation | Generated Python drivers; reviewed and modified by team |
| **Midjourney v6** | Reference mood board for scene color grading and lighting | Inspiration only; no AI-generated images used in final renders |

All creative modeling, rigging, animation, and rendering work was performed manually by team members in Blender, ensuring original artistic contribution.

---

## 🔮 Future Enhancements

The simulation provides a solid foundation for future extension into interactive training experiences:

| Enhancement | Description |
|-------------|-------------|
| **Interactive User Control** | Game engine integration (Unreal Engine or Godot) |
| **Patient Vital Signs** | Real-time monitoring with medical parameter visualization |
| **Branching Scenarios** | Multiple response paths for training purposes |
| **Multiplayer Support** | Team training with multiple simultaneous responders |
| **VR/AR Integration** | Immersive training with head-mounted displays |
| **Performance Analytics** | Metrics collection for training assessment |
| **Medical Equipment Interaction** | Detailed simulation of medical devices and procedures |

---

## 📄 License

This project is developed for educational purposes as part of the Computer Graphics and Visualization course (SBEG353/SBES140).

---

## 📚 References

1. Caballero, A. R., & Niguidula, J. D. (2018). "Disaster Risk Management and Emergency Preparedness: A Case-Driven Training Simulation Using Immersive Virtual Reality." *Proc. 4th Int. Conf. HCI and User Experience in Indonesia*, ACM, pp. 31-37.

2. Lu, S., Xu, W., Wang, F., Li, X., & Yang, J. (2021). "Serious Game: Confined Space Rescue Based on Virtual Reality Technology." *Proc. 2nd Int. Conf. Video, Signal and Image Processing*, ACM, pp. 66-73.

3. Chen, Y., Fennedy, K., Zhang, J., Sim, Y. J., Zheng, C., & Yen, C. C. (2025). "Bridging Simulation and Reality: Augmented Virtuality for Mass Casualty Triage Training." *Proc. CHI '25 Conf. Human Factors in Computing Systems*, ACM, Article 36.

4. Uhl, J. C., Gutierrez, R., Regal, G., Schrom-Feiertag, H., Schuster, B., & Tscheligi, M. (2024). "Choosing the Right Reality: A Comparative Analysis of Tangibility in Immersive Trauma Simulations." *Proc. CHI '24 Conf. Human Factors in Computing Systems*, ACM, Article 187.

---

## 📞 Contact

For questions or collaboration inquiries, please contact the team:

- **Project Supervisor:** Course Instructor, SBEG353/SBES140
- **Team Lead:** Jana Gamal Abdelzaher (91240240)
- **Repository:** [GitHub Link]

---

<div align="center">
  <sub>Built with ❤️ using Blender 3.x | Spring 2025/2026</sub>
</div>
