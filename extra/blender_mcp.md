# Blender MCP

## Overview
Blender MCP connects Blender 3D modeling software to Claude AI through the Model Context Protocol, enabling AI-powered 3D modeling, scene creation, animation, and rendering workflows. This integration allows Claude to directly interact with and control Blender, making 3D content creation accessible through natural language commands.

## Installation

### Prerequisites
- Blender 3.0+ installed on your system
- Claude Desktop application
- Python 3.8+ with Blender Python API access
- Basic understanding of 3D modeling concepts
- Sufficient system resources for 3D rendering

### Install Steps

#### Option 1: Direct Installation
```bash
git clone https://github.com/ahujasid/blender-mcp.git
cd blender-mcp
pip install -r requirements.txt
```

#### Option 2: Via NPM
```bash
npm install blender-mcp-server
```

#### Option 3: Python Package
```bash
pip install blender-mcp
```

#### Option 4: Blender Add-on Installation
1. Download the Blender MCP add-on
2. Open Blender → Edit → Preferences → Add-ons
3. Click "Install" and select the downloaded file
4. Enable the "Blender MCP" add-on

## Configuration

### Claude Desktop Configuration
```json
{
  "mcpServers": {
    "blender": {
      "command": "python",
      "args": [
        "-m", "blender_mcp.server",
        "--blender-path", "/path/to/blender",
        "--port", "8080"
      ]
    }
  }
}
```

### Blender Add-on Configuration
```json
{
  "blender_mcp": {
    "blender_executable": "/Applications/Blender.app/Contents/MacOS/Blender",
    "python_path": "/usr/bin/python3",
    "server_port": 8080,
    "auto_save": true,
    "render_engine": "CYCLES",
    "output_format": "PNG"
  }
}
```

### Advanced Configuration
```json
{
  "blender_settings": {
    "scene_setup": {
      "units": "METRIC",
      "frame_rate": 24,
      "resolution": [1920, 1080],
      "samples": 128
    },
    "rendering": {
      "engine": "CYCLES",
      "device": "GPU",
      "tile_size": 256,
      "max_bounces": 12
    },
    "export_formats": ["OBJ", "FBX", "GLTF", "STL", "PLY"],
    "import_formats": ["OBJ", "FBX", "DAE", "3DS", "STL"]
  }
}
```

## Usage Examples

### Basic 3D Modeling
```
# Create basic shapes
Create a cube at the origin with dimensions 2x2x2 meters.

# Modify objects
Scale the cube by 1.5 on the X-axis and rotate it 45 degrees around the Z-axis.

# Add materials
Add a red metallic material to the cube with roughness 0.3 and metallic value 0.8.

# Create complex objects
Create a detailed coffee mug with a handle, apply a ceramic material, and place it on a wooden table.

# Scene composition
Create a living room scene with a sofa, coffee table, lamp, and decorative objects.
```

### Animation and Rigging
```
# Basic animation
Animate the cube rotating 360 degrees around the Y-axis over 120 frames.

# Character rigging
Create a basic humanoid armature and bind it to the character mesh.

# Keyframe animation
Set keyframes for the character walking from point A to point B over 2 seconds.

# Camera animation
Animate the camera orbiting around the scene over 10 seconds.

# Physics simulation
Add physics properties to objects and simulate them falling under gravity.
```

### Rendering and Output
```
# Render settings
Set up Cycles rendering with 256 samples and denoising enabled.

# Lighting setup
Create a three-point lighting setup with key, fill, and rim lights.

# Render animation
Render the animation sequence as PNG frames at 1920x1080 resolution.

# Export models
Export the scene as FBX format for use in game engines.

# Batch rendering
Render multiple camera angles of the same scene automatically.
```

### Advanced Workflows
```
# Procedural modeling
Create a procedural building generator using geometry nodes.

# Texture painting
Apply procedural textures and paint details directly on the model.

# Sculpting
Use sculpting tools to add fine details to character models.

# Fluid simulation
Create realistic water or smoke simulations for visual effects.

# Architectural visualization
Create photorealistic architectural renderings with proper lighting and materials.
```

## Features

### Core 3D Modeling Capabilities
- **Object Creation**: Create primitive and complex 3D objects
- **Mesh Editing**: Modify vertices, edges, and faces with precision
- **Material System**: Apply and create realistic materials and textures
- **Lighting Setup**: Professional lighting rigs and HDRI environments
- **Camera Control**: Precise camera positioning and animation

### Advanced Modeling Features
- **Procedural Modeling**: Geometry nodes for parametric modeling
- **Sculpting Tools**: High-resolution digital sculpting capabilities
- **Retopology**: Optimize mesh topology for animation and rendering
- **UV Mapping**: Efficient texture coordinate mapping
- **Modifier Stack**: Non-destructive modeling with modifier system

### Animation Capabilities
- **Keyframe Animation**: Traditional keyframe-based animation
- **Rigging System**: Advanced character rigging and constraints
- **Physics Simulation**: Realistic physics-based animation
- **Particle Systems**: Complex particle effects and simulations
- **Motion Graphics**: Text animation and motion graphics

### Rendering Features
- **Cycles Renderer**: Physically-based path tracing renderer
- **Eevee Renderer**: Real-time rendering engine
- **Freestyle**: Non-photorealistic line art rendering
- **Compositing**: Advanced post-processing and compositing
- **Multi-layer Rendering**: Render passes for post-production

## Requirements

### System Requirements
- **Operating System**: Windows 10+, macOS 10.15+, or Linux
- **Memory**: 8GB RAM minimum, 16GB+ recommended
- **Graphics**: OpenGL 3.3 compatible graphics card
- **Storage**: 2GB+ available space for Blender and projects
- **CPU**: Multi-core processor recommended for rendering

### Blender Requirements
```python
# Minimum Blender version requirements
blender_requirements = {
    "version": "3.0.0",
    "python_api": "3.10",
    "opengl": "3.3",
    "memory": "4GB",
    "recommended_version": "4.0+"
}
```

### Performance Recommendations
- **GPU Rendering**: NVIDIA RTX or AMD RDNA2 for optimal Cycles performance
- **CPU Rendering**: High core count processors for faster rendering
- **Storage**: SSD storage for faster file operations and viewport performance
- **Network**: Stable connection for MCP communication

## Security Considerations

### Best Practices
- **File Access Control**: Restrict Blender file system access to project directories
- **Script Execution**: Validate and sandbox Python script execution
- **Network Security**: Secure MCP communication channels
- **Asset Management**: Secure handling of 3D assets and textures
- **Backup Strategy**: Regular project backups and version control

### Secure Configuration
```json
{
  "security": {
    "file_access": {
      "allowed_directories": ["/projects", "/assets", "/renders"],
      "blocked_extensions": [".exe", ".bat", ".sh"],
      "max_file_size": "100MB"
    },
    "script_execution": {
      "sandbox_mode": true,
      "allowed_modules": ["bpy", "bmesh", "mathutils"],
      "execution_timeout": "30s"
    },
    "network": {
      "encryption": true,
      "authentication": "required",
      "rate_limiting": true
    }
  }
}
```

### Data Protection
```python
# Data protection measures
data_protection = {
    "project_encryption": "AES-256",
    "asset_watermarking": "enabled",
    "access_logging": "comprehensive",
    "backup_encryption": "enabled",
    "secure_deletion": "multi_pass"
}
```

## Troubleshooting

### Common Issues

#### Blender Connection Problems
**Problem**: Cannot connect to Blender instance
**Solution**:
```bash
# Check Blender process
ps aux | grep blender

# Verify port availability
netstat -an | grep 8080

# Test Blender Python API
blender --background --python-expr "import bpy; print('Blender API working')"
```

#### Rendering Issues
**Problem**: Slow rendering or crashes during render
**Solution**:
- Reduce sample count for test renders
- Check available memory and GPU VRAM
- Optimize scene complexity and subdivision levels
- Use render regions for testing specific areas

#### Import/Export Problems
**Problem**: Models not importing or exporting correctly
**Solution**:
```python
# Verify file format support
import bpy
print("Supported formats:", bpy.path.extensions_image)

# Check file permissions
import os
file_path = "/path/to/model.fbx"
print("File exists:", os.path.exists(file_path))
print("File readable:", os.access(file_path, os.R_OK))
```

#### Performance Issues
**Problem**: Slow viewport or unresponsive interface
**Solution**:
- Reduce viewport shading complexity
- Optimize mesh density and modifier settings
- Close unnecessary applications to free memory
- Update graphics drivers

### Diagnostic Commands
```bash
# System diagnostics
blender --debug --python-expr "import bpy; bpy.app.debug = True"

# Memory usage check
blender --background --python-expr "import psutil; print(f'Memory: {psutil.virtual_memory().percent}%')"

# GPU information
blender --background --python-expr "import bpy; print(bpy.context.preferences.addons['cycles'].preferences.devices)"
```

## Advanced Configuration

### Custom Material Library
```python
# Material library setup
material_library = {
    "metals": {
        "steel": {"metallic": 1.0, "roughness": 0.2, "base_color": [0.7, 0.7, 0.7]},
        "gold": {"metallic": 1.0, "roughness": 0.1, "base_color": [1.0, 0.8, 0.3]},
        "copper": {"metallic": 1.0, "roughness": 0.3, "base_color": [0.9, 0.4, 0.2]}
    },
    "dielectrics": {
        "glass": {"metallic": 0.0, "roughness": 0.0, "transmission": 1.0, "ior": 1.45},
        "plastic": {"metallic": 0.0, "roughness": 0.5, "base_color": [0.8, 0.8, 0.8]},
        "ceramic": {"metallic": 0.0, "roughness": 0.1, "base_color": [0.9, 0.9, 0.9]}
    }
}
```

### Automated Workflow Scripts
```python
# Automated scene setup
def setup_standard_scene():
    import bpy
    
    # Clear default scene
    bpy.ops.object.select_all(action='SELECT')
    bpy.ops.object.delete()
    
    # Add camera
    bpy.ops.object.camera_add(location=(7, -7, 5))
    camera = bpy.context.object
    camera.rotation_euler = (1.1, 0, 0.785)
    
    # Add lighting
    bpy.ops.object.light_add(type='SUN', location=(5, 5, 10))
    sun = bpy.context.object
    sun.data.energy = 3
    
    # Add ground plane
    bpy.ops.mesh.primitive_plane_add(size=20, location=(0, 0, 0))
    
    # Set render settings
    scene = bpy.context.scene
    scene.render.engine = 'CYCLES'
    scene.render.resolution_x = 1920
    scene.render.resolution_y = 1080
    scene.cycles.samples = 128
```

### Batch Processing
```python
# Batch rendering setup
def batch_render_cameras():
    import bpy
    
    cameras = [obj for obj in bpy.context.scene.objects if obj.type == 'CAMERA']
    
    for i, camera in enumerate(cameras):
        bpy.context.scene.camera = camera
        bpy.context.scene.render.filepath = f"/renders/camera_{i:02d}"
        bpy.ops.render.render(write_still=True)
```

## Workflow Examples

### Architectural Visualization
```python
# Architectural workflow
architectural_workflow = {
    "modeling": [
        "Import floor plans as reference",
        "Create building structure with precise measurements",
        "Add architectural details (windows, doors, trim)",
        "Create interior furniture and fixtures"
    ],
    "materials": [
        "Apply realistic building materials",
        "Set up proper material properties",
        "Add weathering and wear details",
        "Configure glass and metal materials"
    ],
    "lighting": [
        "Set up HDRI environment lighting",
        "Add interior artificial lighting",
        "Configure sun position for time of day",
        "Balance interior and exterior lighting"
    ],
    "rendering": [
        "Set up multiple camera angles",
        "Configure high-quality render settings",
        "Render exterior and interior views",
        "Post-process for presentation"
    ]
}
```

### Product Visualization
```python
# Product visualization workflow
product_workflow = {
    "preparation": [
        "Import CAD models or create from scratch",
        "Optimize mesh topology for rendering",
        "UV unwrap for texture application",
        "Prepare multiple product variants"
    ],
    "materials": [
        "Create photorealistic materials",
        "Add surface imperfections and details",
        "Set up material variations",
        "Configure transparency and reflections"
    ],
    "scene_setup": [
        "Create studio lighting setup",
        "Add background and environment",
        "Position product optimally",
        "Set up multiple camera angles"
    ],
    "output": [
        "Render high-resolution images",
        "Create 360-degree turntable animation",
        "Generate exploded view diagrams",
        "Export for web and print use"
    ]
}
```

### Character Animation
```python
# Character animation workflow
character_workflow = {
    "modeling": [
        "Create base mesh with proper topology",
        "Sculpt high-frequency details",
        "Retopologize for animation",
        "Create clothing and accessories"
    ],
    "rigging": [
        "Create armature with proper bone hierarchy",
        "Add IK/FK controls and constraints",
        "Set up facial rigging for expressions",
        "Create custom bone shapes and controls"
    ],
    "animation": [
        "Block out key poses and timing",
        "Refine animation curves and spacing",
        "Add secondary animation and overlap",
        "Polish facial expressions and details"
    ],
    "rendering": [
        "Set up character lighting",
        "Configure motion blur and depth of field",
        "Render animation sequence",
        "Composite and color correct"
    ]
}
```

## Integration with Other MCPs

### With Git MCP
```
# Version control for 3D projects
1. Use Blender MCP for 3D content creation
2. Use Git MCP for project version control
3. Track .blend files and asset changes
4. Collaborate on 3D projects with team members
```

### With Cloud Storage MCPs
```
# Asset management workflow
1. Use Blender MCP for 3D modeling and rendering
2. Use cloud storage MCPs for asset library management
3. Sync textures, models, and project files
4. Share renders and work-in-progress with clients
```

### With AI Image Generation MCPs
```
# Enhanced creative workflow
1. Use AI image generation for concept art and references
2. Use Blender MCP to create 3D models based on concepts
3. Combine AI-generated textures with 3D models
4. Create hybrid 2D/3D artistic compositions
```

## Performance Optimization

### Rendering Optimization
```python
# Rendering optimization settings
render_optimization = {
    "cycles": {
        "tile_size": "auto",
        "progressive_refine": True,
        "use_denoising": True,
        "max_bounces": 8,
        "caustics_reflective": False,
        "caustics_refractive": False
    },
    "memory": {
        "tile_order": "CENTER",
        "use_persistent_data": True,
        "final_render_persistent_data": True
    },
    "gpu": {
        "device": "CUDA",
        "use_multi_device": True,
        "kernel": "OPTIX"
    }
}
```

### Viewport Optimization
```python
# Viewport performance settings
viewport_optimization = {
    "shading": {
        "type": "MATERIAL",
        "use_scene_lights": False,
        "use_scene_world": False,
        "studio_light": "forest.exr"
    },
    "overlays": {
        "show_wireframes": False,
        "show_face_orientation": False,
        "show_edge_sharp": False
    },
    "simplify": {
        "use_simplify": True,
        "simplify_subdivision": 2,
        "simplify_child_particles": 0.1
    }
}
```

### Memory Management
```python
# Memory management strategies
memory_management = {
    "textures": {
        "limit_size": "2048",
        "use_auto_pack": False,
        "compress_images": True
    },
    "geometry": {
        "use_simplify_subdivision": True,
        "subdivision_render": 2,
        "subdivision_viewport": 1
    },
    "animation": {
        "frame_step": 1,
        "use_preview_range": True,
        "cache_library": "limited"
    }
}
```

## Links

- [Blender MCP Repository](https://github.com/ahujasid/blender-mcp)
- [Blender Official Documentation](https://docs.blender.org/)
- [Blender Python API Reference](https://docs.blender.org/api/current/)
- [Blender MCP Tutorial Videos](https://blender-mcp.com/tutorials.html)
- [Blender Community Forums](https://blenderartists.org/)
- [MCP Specification](https://spec.modelcontextprotocol.io/)

## Community Resources

- [Blender MCP Community](https://github.com/ahujasid/blender-mcp/discussions)
- [Blender Artists Forum](https://blenderartists.org/)
- [Blender Stack Exchange](https://blender.stackexchange.com/)
- [Blender MCP Examples](https://github.com/ahujasid/blender-mcp/tree/main/examples)
- [3D Modeling Best Practices](https://blender-mcp.com/best-practices)
- [Blender MCP Discord](https://discord.gg/blender-mcp)

