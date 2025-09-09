# 🎨 Advanced Paint/Drawing Application

A comprehensive real-time drawing application built with vanilla JavaScript and HTML5 Canvas API, featuring advanced layer management and customizable brush textures. Perfect for learning advanced JavaScript concepts and canvas manipulation techniques.

![Paint App Demo](https://img.shields.io/badge/JavaScript-Advanced-yellow) ![Canvas API](https://img.shields.io/badge/Canvas-API-blue) ![No Dependencies](https://img.shields.io/badge/Dependencies-None-green)

## 🌟 Features

### Core Drawing Tools
- **Brush Tool**: Freehand drawing with texture support
- **Eraser**: Remove content with customizable size
- **Shape Tools**: Line, Rectangle, Circle with real-time preview
- **Color System**: Color picker + quick color palette
- **Adjustable Brush Size**: 1-100px with live preview

### Advanced Layer System
- **Multi-layer Support**: Unlimited layers with independent content
- **Layer Visibility**: Toggle layers on/off
- **Opacity Control**: Individual layer transparency (0-100%)
- **Layer Management**: Add, duplicate, delete, and reorder layers
- **Active Layer Selection**: Visual feedback for current working layer

### Brush Texture Engine
- **9 Unique Textures**: Solid, Dots, Lines, Crosshatch, Spray, Fur, Stars, Noise, Watercolor
- **Procedural Generation**: Mathematical algorithms create realistic textures
- **Dynamic Sizing**: Textures scale with brush size
- **Color Integration**: Textures adapt to selected colors

### Professional Features
- **Undo/Redo System**: 20-step history with complete state management
- **Touch Support**: Full mobile compatibility
- **Keyboard Shortcuts**: Professional workflow shortcuts
- **Image Export**: Save artwork as PNG with layer flattening
- **Real-time Feedback**: Mouse coordinates and tool status

## 🚀 Quick Start

1. **Clone or Download**
   ```bash
   git clone https://github.com/DGL213-Applied-JavaScript-2025FA-CVS1-I/dgl213-w2-demo-drawing-app-js.git
   cd docs
   ```

2. **Run the Application**
   ```bash
   # You can start this application as follows:
   npx live-server docs
   ```

3. **Start Drawing**
   - Select a tool from the toolbar
   - Choose colors and brush size
   - Click and drag on the canvas to draw
   - Use layers panel to manage multiple drawing layers

## 🏗️ Architecture Overview

### Core Classes

```javascript
class PaintApplication {
    // Main application controller
    // Manages tools, events, and coordinate all systems
}

class Layer {
    // Individual drawing layer
    // Each layer has its own canvas and properties
}

class BrushTexture {
    // Texture generation system
    // Creates procedural brush patterns
}
```

### System Architecture

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   UI Controls   │───▶│ PaintApplication │───▶│   Canvas API    │
│   (Toolbar)     │    │   (Controller)   │    │   (Rendering)   │
└─────────────────┘    └──────────────────┘    └─────────────────┘
                                │
                                ▼
                       ┌──────────────────┐
                       │  Layer System    │
                       │ ┌──────┐ ┌─────┐ │
                       │ │Layer1│ │Layer2││
                       │ └──────┘ └─────┘ │
                       └──────────────────┘
```

## 📚 Learning Concepts

### 1. **Object-Oriented Programming**
```javascript
class Layer {
    constructor(name, opacity = 1) {
        this.name = name;
        this.canvas = document.createElement('canvas');
        this.ctx = this.canvas.getContext('2d');
        this.opacity = opacity;
        this.visible = true;
    }

    clear() {
        this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height);
    }

    duplicate() {
        const newLayer = new Layer(this.name + ' Copy', this.opacity);
        newLayer.ctx.drawImage(this.canvas, 0, 0);
        return newLayer;
    }
}
```

**Learning Points:**
- Class-based architecture
- Encapsulation of layer properties
- Method chaining and object composition

### 2. **Canvas API Mastery**
```javascript
// Context setup for different tools
setupBrush(ctx) {
    ctx.lineWidth = this.currentSize;
    ctx.lineCap = 'round';
    ctx.lineJoin = 'round';
    
    if (this.currentTool === 'eraser') {
        ctx.globalCompositeOperation = 'destination-out';
    } else {
        ctx.globalCompositeOperation = 'source-over';
        ctx.strokeStyle = this.currentColor;
    }
}
```

**Learning Points:**
- Context state management
- Composite operations for special effects
- Path drawing and shape rendering

### 3. **Event-Driven Programming**
```javascript
initializeEventListeners() {
    // Mouse events for drawing
    this.canvas.addEventListener('mousedown', (e) => this.startDrawing(e));
    this.canvas.addEventListener('mousemove', (e) => this.draw(e));
    this.canvas.addEventListener('mouseup', () => this.stopDrawing());
    
    // Touch events for mobile
    this.canvas.addEventListener('touchstart', (e) => this.handleTouch(e, 'start'));
}
```

**Learning Points:**
- Event listener management
- Cross-platform event handling
- State-based drawing logic

### 4. **Advanced State Management**
```javascript
saveState() {
    const state = {
        layers: this.layers.map(layer => ({
            name: layer.name,
            opacity: layer.opacity,
            visible: layer.visible,
            imageData: layer.canvas.toDataURL()
        })),
        currentLayerIndex: this.currentLayerIndex
    };
    
    this.undoStack.push(JSON.stringify(state));
}
```

**Learning Points:**
- Complex state serialization
- Memory management for undo/redo
- JSON-based data persistence

### 5. **Procedural Graphics Generation**
```javascript
generateTexture(type, size, color) {
    const canvas = document.createElement('canvas');
    const ctx = canvas.getContext('2d');
    
    switch(type) {
        case 'spray':
            for (let i = 0; i < size * 3; i++) {
                const angle = Math.random() * Math.PI * 2;
                const distance = Math.random() * size;
                const x = size + Math.cos(angle) * distance;
                const y = size + Math.sin(angle) * distance;
                // Draw spray particle
            }
            break;
    }
    
    return canvas;
}
```

**Learning Points:**
- Mathematical pattern generation
- Trigonometry in graphics programming
- Canvas-to-canvas composition

## 🎯 Code Structure

### File Organization
```
advanced-paint-app/
│
├── index.html                 # Main application file
├── README.md                  # This documentation
└── assets/
    ├── screenshots/           # Application screenshots
    └── examples/             # Example artworks
```

### Key Components

#### 1. **Application Controller** (`PaintApplication`)
- **Purpose**: Central coordinator for all application functionality
- **Responsibilities**: Event handling, tool management, canvas operations
- **Key Methods**: `startDrawing()`, `draw()`, `stopDrawing()`, `selectTool()`

#### 2. **Layer Management** (`Layer`)
- **Purpose**: Individual drawing surface with independent properties
- **Responsibilities**: Canvas management, opacity control, visibility
- **Key Methods**: `clear()`, `duplicate()`, layer property setters

#### 3. **Texture Engine** (`BrushTexture`)
- **Purpose**: Procedural brush pattern generation
- **Responsibilities**: Create diverse brush textures, color integration
- **Key Methods**: `generateTexture()`, texture-specific algorithms

#### 4. **State Management**
- **Purpose**: Undo/redo functionality with complete state preservation
- **Responsibilities**: History tracking, state serialization/restoration
- **Key Methods**: `saveState()`, `undo()`, `redo()`, `restoreState()`

## 🎮 User Interface

### Toolbar Sections
- **Tools**: Brush, Eraser, Line, Rectangle, Circle
- **Size Control**: Slider with real-time preview (1-100px)
- **Color System**: Color picker + quick color buttons
- **Actions**: Clear layer, Undo, Redo, Save image
- **Preview**: Live brush preview with current settings

### Layer Panel
- **Layer List**: Visual list with thumbnails and controls
- **Layer Controls**: Add, duplicate, delete layers
- **Opacity Sliders**: Individual layer transparency control
- **Visibility Toggles**: Show/hide layers with eye icon

### Texture Panel
- **Texture Grid**: 3x3 grid of texture options
- **Visual Previews**: Each button shows texture style
- **Active Indication**: Current texture highlighted

## ⌨️ Keyboard Shortcuts

| Shortcut | Action | Category |
|----------|--------|----------|
| `B` | Select Brush | Tools |
| `E` | Select Eraser | Tools |
| `L` | Select Line | Tools |
| `R` | Select Rectangle | Tools |
| `C` | Select Circle | Tools |
| `Ctrl+Z` | Undo | History |
| `Ctrl+Shift+Z` | Redo | History |
| `Ctrl+S` | Save Image | File |
| `Ctrl+L` | Add Layer | Layers |
| `Delete` | Clear Layer | Layers |

## 🧪 Advanced Features Deep Dive

### Multi-Layer Composition
The application uses a sophisticated layer system where each layer is an independent canvas:

```javascript
renderLayers() {
    this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height);
    
    this.layers.forEach(layer => {
        if (layer.visible) {
            this.ctx.globalAlpha = layer.opacity;
            this.ctx.drawImage(layer.canvas, 0, 0);
        }
    });
    
    this.ctx.globalAlpha = 1;
}
```

This approach enables:
- **Independent Editing**: Modify layers without affecting others
- **Flexible Compositing**: Control opacity and visibility per layer
- **Efficient Rendering**: Only visible layers are processed

### Brush Texture Algorithms

#### Spray Texture Algorithm
```javascript
case 'spray':
    const sprayCount = size * 3;
    for (let i = 0; i < sprayCount; i++) {
        const angle = Math.random() * Math.PI * 2;
        const distance = Math.random() * size;
        const x = size + Math.cos(angle) * distance;
        const y = size + Math.sin(angle) * distance;
        ctx.beginPath();
        ctx.arc(x, y, Math.random() * 2 + 0.5, 0, Math.PI * 2);
        ctx.fill();
    }
    break;
```

This demonstrates:
- **Polar Coordinates**: Using angle and distance for natural spray pattern
- **Randomization**: Creating organic, non-repetitive textures
- **Scalable Algorithms**: Texture density scales with brush size

## 📱 Mobile Compatibility

The application includes comprehensive touch support:

```javascript
handleTouch(e, action) {
    e.preventDefault();
    const touch = e.touches[0] || e.changedTouches[0];
    const mouseEvent = new MouseEvent(
        action === 'start' ? 'mousedown' : 
        action === 'move' ? 'mousemove' : 'mouseup', 
        {
            clientX: touch.clientX,
            clientY: touch.clientY
        }
    );
    this.canvas.dispatchEvent(mouseEvent);
}
```

## 🔧 Customization and Extension

### Adding New Tools
1. **Add UI Button**: Create button in toolbar HTML
2. **Implement Logic**: Add case in `draw()` method
3. **Register Events**: Add event listener in `initializeEventListeners()`

### Creating New Textures
1. **Add Button**: Create texture button with `data-texture` attribute
2. **Implement Algorithm**: Add case in `generateTexture()` method
3. **Consider Scalability**: Ensure texture works at different sizes

### Extending Layer System
The layer system is designed for extension:
- Add layer effects (blur, brightness, contrast)
- Implement layer blending modes
- Add layer grouping functionality

## 🐛 Troubleshooting

### Common Issues

**Performance with Many Layers**
- Solution: Implement layer caching
- Optimize: Only re-render affected layers

**Mobile Touch Sensitivity**
- Solution: Adjust touch event handling
- Consider: Different touch pressures

**Browser Compatibility**
- Solution: Feature detection for Canvas API
- Fallback: Provide graceful degradation

## 🎓 Educational Usage

### Beginner Concepts
- HTML5 Canvas basics
- Event handling
- Basic drawing operations

### Intermediate Concepts
- Object-oriented design patterns
- State management
- Cross-platform compatibility

### Advanced Concepts
- Complex application architecture
- Memory management
- Performance optimization
- Mathematical graphics programming

## 🤝 Contributing

1. **Fork the Repository**
2. **Create Feature Branch**: `git checkout -b feature/amazing-feature`
3. **Commit Changes**: `git commit -m 'Add amazing feature'`
4. **Push to Branch**: `git push origin feature/amazing-feature`
5. **Open Pull Request**

### Development Guidelines
- Follow existing code style
- Add comments for complex algorithms
- Test on multiple browsers
- Ensure mobile compatibility

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- HTML5 Canvas API documentation
- Modern JavaScript ES6+ features
- Touch event specifications
- Digital art application design patterns
- This entire codebase is generated by Claude AI.

---

**Built for the students enrolled in DGL 213 - Applied JavaScript at North Island College.**
