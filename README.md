
# AI Task Automator Masterplan

## 1. App Overview
**Vision**: A browser-based Excalidraw-style canvas where non-technical users chain pre-built AI tasks into workflows, annotate freely, and export/share as visual diagrams.  
**Phase 1 Goal**: MVP with 5 core AI tasks, local workflow storage, and client-side execution.

## 2. Target Audience
- Small business owners
- Non-technical startup teams
- Users needing code/docs/media automation without coding

## 3. Core Features (Phase 1)
| Feature | Implementation |
|---------|----------------|
| **Excalidraw-Style Canvas** | Open-source drawing library with pen/shapes/text tools (decoration only) |
| **Drag-and-Drop AI Tasks** | Auto-connect tasks when placed nearby (Zapier-style proximity linking) |
| **Pre-Built AI Tasks** | Prioritized: Code Writing → Debugging, Flowchart Generation, Resume Optimization, OCR, Unit Tests |
| **Workflow Export** | PDF/JPG export with annotations intact |
| **Local Storage** | Browser localStorage for workflows (IndexedDB fallback if size >5MB) |
| **Safety Limits** | 10MB file upload cap + CPU/RAM warnings |

## 4. Technical Stack Recommendations
| Component | Choice | Reasoning |
|-----------|--------|-----------|
| **Frontend Framework** | SvelteKit | Lightweight, fast for canvas interactions |
| **Canvas Library** | Excalidraw (OSS) | Proven drawing tools, MIT license |
| **AI Runtime** | Hybrid: Transformers.js (client-side) + External APIs | Balance capability & complexity |
| **Code Tasks** | OpenAI API (GPT-4) | Best code generation quality |
| **OCR** | Tesseract.js | Browser-based, no API keys |
| **PDF Processing** | PDF.js (client-side) | Avoid server costs |

## 5. Data Model (Conceptual)  
```javascript
Workflow = {
  id: string,
  tasks: [{
    type: "IMAGE_BG_REMOVE" | "OCR" | ...,
    params: {model: "rembg", threshold: 0.5},
    position: {x,y},
  }],
  annotations: [ExcalidrawElement[]], // SVG paths/texts/shapes
  files: {input: File, output: Blob},
}
## 6. User Interface Design Principles

**Guiding Philosophy:** "Simple enough for a coffee shop owner, powerful enough for a startup CTO"

| Principle               | Implementation Example |
|------------------------|----------------------|
| **Zero-Config Onboarding** | Blank canvas opens immediately with floating task palette |
| **Visual Affordances** | Glowing connector dots when dragging tasks near compatible nodes |
| **Progressive Disclosure** | Advanced settings (model params) hidden behind "⚙️" icons by default |
| **Instant Gratification** | Auto-preview results at every workflow step (e.g., cleaned OCR text) |
| **Fail Visibly** | Animated red "bounce" effect on incompatible task connections |
| **Performance Transparency** | Subtle GPU meter icon when heavy tasks run (e.g., OCR processing) |

## 7. Security Considerations

**Balancing Ease-of-Use with Basic Protections**

| Aspect          | Approach |
|---------------|----------|
| **API Keys** | Ephemeral browser memory storage (cleared on tab close) |
| **File Handling** | `sandbox` attribute for iframe-based processing |
| **CORS** | Strict same-origin policy for client-side ops |
| **HTTPS** | Mandatory for deployment (service worker registration) |
| **Data Lifecycle** | IndexedDB auto-purge after 7 days of inactivity |
| **Model Security** | Only load signed WASM binaries from verified CDNs |

## 8. Development Phases

### **Phase 0 - Foundation (4 Weeks)**
- Set up SvelteKit + Excalidraw core
- Implement image processing workflow (Upload → Remove BG → Download)
- Basic `localStorage` persistence

### **Phase 1 - MVP Launch (8 Weeks)**
#### **Core Image Features:**
- Background removal (`rembg.js`)
- Image → PDF conversion

#### **Demo System:**
- First-time user interactive walkthrough
- Pre-built "Portrait to Professional Headshot" demo workflow

#### **Safety & UX:**
- File size validation
- CPU overload warnings

### **Phase 2 - Task Expansion (6 Weeks)**
- Add 10+ secondary AI tasks from your list
- Workflow templating ("Save as Recipe")
- Basic version history (undo/redo stack)

### **Phase 3 - Collaboration Readiness (Future)**
- Shareable workflow URLs (read-only)
- Multi-user cursor presence
- Comment threading system

### **Phase 4 - Monetization (Future)**
- "AI Credit" system for premium models
- Team workspace management
- Priority support channel

## 9. Key Challenges & Mitigations

| Challenge                 | Risk Level | Mitigation Strategy |
|--------------------------|-----------|--------------------|
| **Browser OOM Crashes** | High | Web Workers + 60s timeout kills stalled tasks |
| **Model Loading Times** | Medium | Lazy-load WASM binaries only when task first used |
| **Cross-Browser Issues** | Medium | Limit to Chromium/WebKit + Firefox ESR |
| **API Key Leakage** | High | Never write keys to disk, even during exports |
| **Workflow Complexity** | Medium | Auto-simplify flows >10 steps with "sub-workflow" grouping |
| **GPU Variability** | Low | Fallback to CPU mode with performance warning |

## 10. Future Expansion Possibilities

### **Near-Term (6-12 Months)**
- **Desktop App:** Electron wrapper with local model caching
- **Workflow Marketplace:** User-submitted templates with rating system
- **AI Agent Mode:** "Fix this workflow" auto-optimization button

### **Long-Term (12+ Months)**
- **Mobile Workflow Player:** iOS/Android app for workflow monitoring
- **Custom Model Training:** Browser-based fine-tuning UI
- **Real-Time Collaboration:** Figma-style multiplayer editing

