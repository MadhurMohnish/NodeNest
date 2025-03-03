# NodeNest
# AI Automation Tool

## Overview
The **AI Automation Tool** is a web-based platform that allows users to create automated AI workflows by dragging and connecting AI-powered operations. Users can design workflows that automate various tasks such as text generation, code writing, image processing, file conversion, and more without writing any code.

## Features
- **User Authentication**: Login and manage personalized workflows.
- **Drag-and-Drop Workflow Builder**: Users can visually create automation pipelines.
- **AI-Powered Operations**:
  - Text generation (e.g., content writing, summarization, translation)
  - Code generation and formatting
  - File format conversion (PDF, CSV, DOCX, etc.)
  - Image processing (background removal, enhancement, filtering)
  - Diagram and chart creation
  - Clipboard automation
- **Workflow Execution**: Once a user builds and connects the workflow elements, a single click executes the entire automation.
- **Real-Time Processing**: Instant AI-powered operations based on the sequence designed by the user.
- **Export and Share**: Save, export, and share automated workflows.

## How It Works
1. **Login/Register**: Users sign in to the platform.
2. **Create a Workflow**:
   - Drag and drop different AI modules (e.g., "Write Code", "Copy to Clipboard", "Remove Background", etc.).
   - Connect modules in a logical sequence.
3. **Run the Workflow**: Click the "Run" button to execute the defined automation.
4. **Get Output**: The system processes the workflow and delivers the expected results automatically.

### Example Workflows
#### 1. **Code Generation Workflow**
- Drag **Write Code** module
- Drag **Copy to Clipboard** module
- Connect the two modules
- Run the workflow to generate code and copy it automatically

#### 2. **Image Processing Workflow**
- Drag **Input Image** module
- Drag **Remove Background** module
- Drag **Add Background Color** module
- Drag **Image Output** module
- Connect the modules and run the workflow

## Tech Stack
- **Frontend**: React.js, Tailwind CSS
- **Backend**: Node.js, Express.js, Python (FastAPI for AI operations)
- **Database**: MongoDB / PostgreSQL
- **AI Models**: OpenAI API, TensorFlow, OpenCV
- **Authentication**: Firebase/Auth0
- **Deployment**: AWS/GCP/Vercel
## Contact
For any queries, feel free to reach out via email or open an issue on GitHub.

------------------------------------------------------------------------------------
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
