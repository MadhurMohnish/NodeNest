
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
    type: "CODE_GEN" | "OCR" | ...,
    params: {model: "GPT-4", temperature: 0.7},
    position: {x,y},
  }],
  annotations: [ExcalidrawElement[]], // SVG paths/texts/shapes
  files: {input: File, output: Blob},
}
