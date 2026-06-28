import React, { useState, useEffect, useRef, useCallback } from 'react';
import { 
  FileText, 
  Image as ImageIcon, 
  Layers, 
  Upload, 
  Trash2, 
  Compass, 
  Moon, 
  Sun, 
  Settings, 
  Search, 
  FileSpreadsheet,
  RotateCcw,
  Download,
  ShieldCheck,
  Send,
  Loader2,
  FileBox,
  MessageSquare,
  Eye,
  EyeOff
} from 'lucide-react';

// ==========================================
// PDF PAGE RENDERER (Single Page)
// ==========================================
const PdfPage = ({ pdf, pageNumber, scale = 1.2 }) => {
  const canvasRef = useRef(null);
  const [isRendered, setIsRendered] = useState(false);

  useEffect(() => {
    let renderTask = null;
    let isMounted = true;

    const renderPage = async () => {
      try {
        const page = await pdf.getPage(pageNumber);
        if (!isMounted) return;

        const canvas = canvasRef.current;
        if (!canvas) return;
        const context = canvas.getContext('2d');
        
        const viewport = page.getViewport({ scale });
        canvas.height = viewport.height;
        canvas.width = viewport.width;

        const renderContext = {
          canvasContext: context,
          viewport: viewport
        };
        
        renderTask = page.render(renderContext);
        await renderTask.promise;
        if (isMounted) setIsRendered(true);
      } catch (error) {
        if (error.name !== 'RenderingCancelledException') {
          console.error(`Error rendering page ${pageNumber}:`, error);
        }
      }
    };

    renderPage();

    return () => {
      isMounted = false;
      if (renderTask && typeof renderTask.cancel === 'function') {
        try { renderTask.cancel(); } catch (e) {}
      }
    };
  }, [pdf, pageNumber, scale]);

  return (
    <div className="mb-6 flex flex-col items-center">
      <div className="relative shadow-md bg-white border border-gray-200/50">
        <canvas ref={canvasRef} className="max-w-full h-auto object-contain" />
        {!isRendered && (
          <div className="absolute inset-0 flex items-center justify-center bg-gray-50 text-gray-400 text-sm">
            <Loader2 className="w-5 h-5 animate-spin mr-2" /> Loading Page {pageNumber}...
          </div>
        )}
      </div>
      <span className="text-xs text-gray-500 mt-2 font-mono">Page {pageNumber}</span>
    </div>
  );
};

// ==========================================
// ALL-PAGE PDF VIEWER & GENERAL DOC VIEWER
// ==========================================
const DocumentViewer = ({ doc, pdfjsLoaded }) => {
  const [pdfRef, setPdfRef] = useState(null);
  const [numPages, setNumPages] = useState(0);
  const [error, setError] = useState(null);

  useEffect(() => {
    if (!doc || doc.isDemo || doc.type !== 'pdf' || !doc.fileUrl || !pdfjsLoaded || !window.pdfjsLib) {
      setPdfRef(null);
      setNumPages(0);
      return;
    }

    let loadingTask;
    let isMounted = true;

    const loadPdf = async () => {
      try {
        setError(null);
        loadingTask = window.pdfjsLib.getDocument(doc.fileUrl);
        const pdf = await loadingTask.promise;
        if (!isMounted) return;
        setPdfRef(pdf);
        setNumPages(pdf.numPages);
      } catch (err) {
        console.error("Failed to load PDF:", err);
        if (isMounted) setError("Could not load PDF document.");
      }
    };

    loadPdf();

    return () => {
      isMounted = false;
      if (loadingTask && typeof loadingTask.destroy === 'function') {
        try { loadingTask.destroy(); } catch (e) {}
      }
    };
  }, [doc, pdfjsLoaded]);

  if (!doc) {
    return <div className="flex-1 flex items-center justify-center text-gray-400">No document selected.</div>;
  }

  // Render Demo / Mock Document
  if (doc.isDemo) {
    return (
      <div className="flex-1 overflow-auto p-8 space-y-8 bg-black/5 rounded-xl border border-black/5">
        {doc.type === 'jpg' ? (
          <div className="p-4 bg-white rounded-lg shadow-sm border border-gray-200">
             <div className="aspect-video bg-gray-100 flex items-center justify-center text-gray-400 border border-dashed border-gray-300 rounded mb-4">
                <ImageIcon className="w-12 h-12 opacity-50" />
                <span className="ml-2 font-medium">Image Preview Unavailable in Mock Mode</span>
             </div>
             <p className="text-sm text-gray-700">{doc.content[0].text}</p>
          </div>
        ) : (
          doc.content.map((page, i) => (
            <div key={i} className="p-8 bg-white rounded-lg shadow-sm border border-gray-200 min-h-[400px]">
              <h3 className="text-lg font-serif font-bold border-b pb-2 mb-4">{page.title}</h3>
              <p className="text-gray-700 leading-relaxed font-serif whitespace-pre-wrap">{page.text}</p>
              <div className="mt-12 text-center text-xs text-gray-400 font-mono">- Page {page.page} -</div>
            </div>
          ))
        )}
      </div>
    );
  }

  // Render Real Uploaded Text File
  if (['txt', 'json', 'csv', 'md'].includes(doc.type)) {
    return (
      <div className="flex-1 overflow-auto p-6 bg-black/5 rounded-xl border border-black/5">
        <div className="bg-white p-6 rounded-lg shadow-sm font-mono text-sm whitespace-pre-wrap break-words border border-gray-200">
          {doc.rawText || "No text content available."}
        </div>
      </div>
    );
  }

  // Render Real Uploaded Image
  if (['jpg', 'jpeg', 'png', 'webp', 'gif'].includes(doc.type)) {
    return (
      <div className="flex-1 overflow-auto p-6 bg-black/5 rounded-xl border border-black/5 flex items-start justify-center">
        <img src={doc.fileUrl} alt={doc.name} className="max-w-full h-auto rounded-lg shadow-sm border border-gray-200 bg-white" />
      </div>
    );
  }

  // Render Real Uploaded PDF
  if (doc.type === 'pdf') {
    if (!pdfjsLoaded) {
      return (
        <div className="flex-1 flex items-center justify-center">
          <Loader2 className="w-6 h-6 animate-spin text-gray-400" />
          <span className="ml-3 text-sm text-gray-500">Loading PDF Engine...</span>
        </div>
      );
    }
    if (error) {
      return (
        <div className="flex-1 flex items-center justify-center text-red-500 text-sm">
          {error}
        </div>
      );
    }
    if (!pdfRef) {
      return (
        <div className="flex-1 flex items-center justify-center">
          <Loader2 className="w-6 h-6 animate-spin text-gray-400" />
          <span className="ml-3 text-sm text-gray-500">Processing document...</span>
        </div>
      );
    }

    // Render all pages
    return (
      <div className="flex-1 overflow-auto p-6 bg-black/5 rounded-xl border border-black/5 flex flex-col items-center">
        {Array.from({ length: numPages }).map((_, index) => (
          <PdfPage key={`${doc.id}-page-${index + 1}`} pdf={pdfRef} pageNumber={index + 1} />
        ))}
      </div>
    );
  }

  // Fallback for unsupported real files
  return (
    <div className="flex-1 flex flex-col items-center justify-center p-8 text-gray-500 bg-black/5 rounded-xl border border-black/5">
      <FileBox className="w-16 h-16 opacity-20 mb-4" />
      <p className="font-medium text-gray-600">Preview not available</p>
      <p className="text-xs mt-2 text-center max-w-xs">This file type cannot be previewed natively. You can still ask questions about it if text was extracted.</p>
    </div>
  );
};


// ==========================================
// MOCK DATA FOR DEMONSTRATION & DEFAULT STATE
// ==========================================
const DEFAULT_DOCUMENTS = [
  {
    id: 'doc-1',
    name: 'Executive_Deed_1794.pdf',
    type: 'pdf',
    size: '1.2 MB',
    pages: 4,
    uploadedAt: 'Jun 28, 2026',
    isDemo: true,
    content: [
      { page: 1, title: 'I. Grant of Title & Hereditaments', text: 'This Indenture witnesseth that the crown lands commonly referred to as the Maple Ridge Woods are hereby transferred to the Sovereign Trust of the Commonwealth, subject to hereditary covenants hereafter specified.' },
      { page: 2, title: 'II. Waterways & Timber Rights', text: 'All riparian rights along the Swift Creek, alongside timber harvesting claims within five hundred cubits of the riverbank, shall reside exclusively under the custodian of the High Chamber of Executive Assessors.' },
      { page: 3, title: 'III. Reserved Sovereignty & Royalties', text: 'A perpetual levy of three grains of fine metal per bushel of wheat harvested, or five parts in ten of mineral wealth discovered, remains payable to the Crown Keeper under the Chamber Gavel.' },
      { page: 4, title: 'IV. Execution of Seals & Notary', text: 'Signed, Sealed and Delivered in the presence of the Under-Secretary on this fourteenth day of November, Anno Domini 1794. Registered under Registry Roll 48-B.' }
    ]
  },
  {
    id: 'doc-2',
    name: 'Acquisition_Briefing.docx',
    type: 'docx',
    size: '412 KB',
    pages: 2,
    uploadedAt: 'Jun 28, 2026',
    isDemo: true,
    content: [
      { page: 1, title: 'Project Autumn: Executive Summary', text: 'Acquisition proposal for the Eastern Valleys Estate. Total proposed cash outlay: 14.2M Sovereign Credits. Core assets include 400 acres of arable timberland and 3 water reservoirs of strategic municipal interest.' },
      { page: 2, title: 'Risk Parameters & Environmental Trust', text: 'A heavy environmental lien exists on Sector G-9. Chamber Analytics projects a mitigation cost of 1.4M Credits over a four-year horizon. High probability of state subsidy approval.' }
    ]
  }
];

const CHAMBER_SYSTEM_PROMPT = `You are the expert legal counsel and archival researcher of "Chamber Analytics".
You have access to the user's uploaded documents.
Always respond in a professional, authoritative, but extremely CLEAR, SIMPLE, and DIRECT tone. Avoid unnecessary legal jargon when explaining findings to the user. Get straight to the point so they can understand immediately.
Strictly provide citations back to the document name and page or slide (e.g., [See Document_Name, Page X]).`;

// ==========================================
// MAIN APP COMPONENT
// ==========================================
export default function App() {
  const [darkMode, setDarkMode] = useState(false);
  const [showDisplayMenu, setShowDisplayMenu] = useState(false);
  const [pdfjsLoaded, setPdfjsLoaded] = useState(false);

  // Simplified API key handling
  const [apiKey, setApiKey] = useState("");
  const [showApiKey, setShowApiKey] = useState(false);
  
  const [documents, setDocuments] = useState(DEFAULT_DOCUMENTS);
  const [selectedDocId, setSelectedDocId] = useState('doc-1');
  const [searchTerm, setSearchTerm] = useState('');
  const [dragActive, setDragActive] = useState(false);

  const [messages, setMessages] = useState([
    {
      id: 'msg-init',
      role: 'assistant',
      text: "Send me your queries here, and I'll try my best to help!",
      timestamp: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' }),
      citation: null
    }
  ]);
  const [chatInput, setChatInput] = useState('');
  const [isLoading, setIsLoading] = useState(false);
  
  const chatEndRef = useRef(null);
  const fileInputRef = useRef(null);

  // Load PDF.js Dynamically and Safely
  useEffect(() => {
    if (window.pdfjsLib) {
      setPdfjsLoaded(true);
      return;
    }
    
    const scriptId = 'pdfjs-script-cdn';
    let script = document.getElementById(scriptId);
    
    if (!script) {
      script = document.createElement('script');
      script.id = scriptId;
      script.src = "https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js";
      document.body.appendChild(script);
    }

    const handleLoad = () => {
      if (window.pdfjsLib) {
        window.pdfjsLib.GlobalWorkerOptions.workerSrc = "https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js";
        setPdfjsLoaded(true);
      }
    };

    script.addEventListener('load', handleLoad);
    return () => script.removeEventListener('load', handleLoad);
  }, []);

  // Auto-scroll chat to bottom
  useEffect(() => {
    chatEndRef.current?.scrollIntoView({ behavior: 'smooth' });
  }, [messages, isLoading]);

  // Clean up Object URLs when unmounting
  useEffect(() => {
    return () => {
      documents.forEach(doc => {
        if (doc.fileUrl && doc.fileUrl.startsWith('blob:')) {
          URL.revokeObjectURL(doc.fileUrl);
        }
      });
    };
  }, []);

  const activeDoc = documents.find(d => d.id === selectedDocId) || documents[0];

  const handleDrag = (e) => {
    e.preventDefault();
    e.stopPropagation();
    if (e.type === "dragenter" || e.type === "dragover") {
      setDragActive(true);
    } else if (e.type === "dragleave") {
      setDragActive(false);
    }
  };

  const handleDrop = (e) => {
    e.preventDefault();
    e.stopPropagation();
    setDragActive(false);
    if (e.dataTransfer.files && e.dataTransfer.files[0]) {
      handleFiles(e.dataTransfer.files);
    }
  };

  const onFileInputChange = (e) => {
    if (e.target.files && e.target.files[0]) {
      handleFiles(e.target.files);
    }
  };

  const handleFiles = (fileList) => {
    const newDocs = Array.from(fileList).map((file, index) => {
      const ext = file.name.split('.').pop().toLowerCase();
      const fileUrl = URL.createObjectURL(file);
      const fileId = `uploaded-${Date.now()}-${index}`;
      
      let parsedRawText = "";
      
      if (ext === 'txt' || ext === 'md' || ext === 'json' || ext === 'csv') {
        const reader = new FileReader();
        reader.onload = (e) => {
          parsedRawText = e.target.result;
          setDocuments(prev => prev.map(d => d.id === fileId ? { ...d, rawText: parsedRawText } : d));
        };
        reader.readAsText(file);
      }

      return {
        id: fileId,
        name: file.name,
        type: ext || 'pdf',
        size: file.size > 1024 * 1024 
          ? `${(file.size / (1024 * 1024)).toFixed(1)} MB` 
          : `${(file.size / 1024).toFixed(0)} KB`,
        pages: 'Native',
        uploadedAt: new Date().toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' }),
        fileUrl: fileUrl,
        rawText: parsedRawText,
        isDemo: false,
        content: [
          {
            page: 1,
            title: `Document Transcript: ${file.name}`,
            text: `Data Stream for ${file.name}. Size: ${(file.size / 1024).toFixed(1)} KB.`
          }
        ]
      };
    });

    setDocuments(prev => [...newDocs, ...prev]);
    if (newDocs.length > 0) {
      setSelectedDocId(newDocs[0].id);
    }
  };

  const deleteDocument = (id, e) => {
    e.stopPropagation();
    const docToDelete = documents.find(d => d.id === id);
    if (docToDelete && docToDelete.fileUrl && docToDelete.fileUrl.startsWith('blob:')) {
      URL.revokeObjectURL(docToDelete.fileUrl);
    }
    const filtered = documents.filter(d => d.id !== id);
    setDocuments(filtered);
    if (selectedDocId === id && filtered.length > 0) {
      setSelectedDocId(filtered[0].id);
    }
  };

  const callGeminiAPI = async (userQuery, contextDoc) => {
    if (!apiKey) {
      return new Promise((resolve) => {
        setTimeout(() => {
          resolve({
            text: `Please enter your Gemini API key in the top bar to perform live analysis on this document.`,
            citation: `System Information`
          });
        }, 1000);
      });
    }

    let docContextString = "";
    if (contextDoc) {
      if (contextDoc.isDemo) {
        docContextString = contextDoc.content.map(p => `[Page ${p.page}: ${p.title}] ${p.text}`).join('\n');
      } else {
        docContextString = `Uploaded File: ${contextDoc.name} (${contextDoc.type})\nFile Data Preview: ${contextDoc.rawText || "Visual/PDF Data only."}`;
      }
    }

    const systemPrompt = CHAMBER_SYSTEM_PROMPT + (contextDoc ? `\n\nCURRENT DOCKET IN FOCUS:\nDocument Name: ${contextDoc.name}\nContent Preview:\n${docContextString}` : "");

    let retries = 3;
    let delay = 1000;

    const payload = {
      contents: [{ parts: [{ text: userQuery }] }],
      systemInstruction: { parts: [{ text: systemPrompt }] }
    };

    while (retries >= 0) {
      try {
        const response = await fetch(
          `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash:generateContent?key=${apiKey}`,
          {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify(payload)
          }
        );

        if (!response.ok) throw new Error(`API HTTP ${response.status}`);
        const data = await response.json();
        const textResponse = data.candidates?.[0]?.content?.parts?.[0]?.text || "No readable answers returned.";
        
        let citation = contextDoc ? `See ${contextDoc.name}` : null;
        const citationMatch = textResponse.match(/\[See [^\]]+\]/);
        let cleanedText = textResponse;
        if (citationMatch) {
          citation = citationMatch[0].replace('[', '').replace(']', '');
          cleanedText = cleanedText.replace(citationMatch[0], '').trim();
        }

        return { text: cleanedText, citation: citation };
      } catch (err) {
        if (retries === 0) throw err;
        await new Promise(res => setTimeout(res, delay));
        delay *= 2;
        retries--;
      }
    }
  };

  const handleSendMessage = async (e) => {
    e.preventDefault();
    if (!chatInput.trim()) return;

    const userMsg = {
      id: `user-${Date.now()}`,
      role: 'user',
      text: chatInput,
      timestamp: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' }),
      citation: null
    };

    setMessages(prev => [...prev, userMsg]);
    setChatInput('');
    setIsLoading(true);

    try {
      const responseData = await callGeminiAPI(userMsg.text, activeDoc);
      
      setMessages(prev => [...prev, {
        id: `assistant-${Date.now()}`,
        role: 'assistant',
        text: responseData.text,
        timestamp: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' }),
        citation: responseData.citation
      }]);
    } catch (error) {
      setMessages(prev => [...prev, {
        id: `assistant-${Date.now()}-err`,
        role: 'assistant',
        text: `Transmission rejected. Verify credentials. System reports: ${error.message}`,
        timestamp: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' }),
        citation: 'Secure Error Protocol'
      }]);
    } finally {
      setIsLoading(false);
    }
  };

  const getFileIcon = (type) => {
    switch (type) {
      case 'pdf': return <FileText className="w-4 h-4 text-red-500" />;
      case 'docx':
      case 'doc': return <FileText className="w-4 h-4 text-blue-500" />;
      case 'jpg':
      case 'jpeg':
      case 'png': return <ImageIcon className="w-4 h-4 text-emerald-500" />;
      case 'ppt':
      case 'pptx': return <Layers className="w-4 h-4 text-amber-500" />;
      default: return <FileSpreadsheet className="w-4 h-4 text-amber-600" />;
    }
  };

  const filteredDocs = documents.filter(doc => 
    doc.name.toLowerCase().includes(searchTerm.toLowerCase())
  );

  return (
    <div className={`h-screen flex flex-col font-sans transition-colors duration-300 ${
      darkMode ? 'bg-[#1A1A1A] text-[#EAE6E1]' : 'bg-gray-50 text-gray-900'
    }`}>
      
      {/* HEADER: CONTROL BENCH */}
      <header className={`flex-none px-4 py-3 flex items-center justify-between border-b transition-colors duration-300 ${
        darkMode ? 'bg-[#24150B] border-[#3D2314] text-white' : 'bg-[#3D2314] border-[#2B1A0A] text-white'
      }`}>
        <div className="flex items-center gap-3 w-1/4">
          <div className={`w-8 h-8 flex items-center justify-center rounded-lg shadow-inner ${darkMode ? 'bg-[#F59E0B]' : 'bg-[#D97736]'}`}>
            <span className="font-serif font-black text-lg text-[#3D2314]">⚖</span>
          </div>
          <div className="hidden sm:block">
            <h1 className="font-serif text-lg font-bold leading-tight">Chamber Analysis LLM</h1>
            <p className="text-[9px] tracking-widest uppercase opacity-75">Document Ledger & Review</p>
          </div>
        </div>

        {/* Center Console: Simple API Key Field */}
        <div className="flex-1 flex justify-center max-w-lg mx-4">
          <div className="relative w-full flex items-center">
            <div className="absolute left-3 text-white/40"><ShieldCheck className="w-4 h-4 text-emerald-400" /></div>
            <input 
              type={showApiKey ? "text" : "password"}
              placeholder="Enter Gemini API Key (e.g. AIzaSy...)"
              value={apiKey}
              onChange={(e) => setApiKey(e.target.value)}
              className={`w-full text-xs pl-9 pr-20 py-2 rounded-md border focus:outline-none transition-all duration-200 ${
                darkMode ? 'bg-[#1A1A1A]/80 border-[#3D2314] text-white focus:border-[#F59E0B]' : 'bg-white/10 border-white/20 text-white placeholder-white/50 focus:border-blue-400/50'
              }`}
            />
            <div className="absolute right-2 top-1.5 flex items-center">
              <button
                type="button"
                onClick={() => setShowApiKey(!showApiKey)}
                className={`p-1.5 rounded text-white/60 hover:text-white hover:bg-white/10 transition-all duration-150`}
                title={showApiKey ? "Hide Key" : "Show Key"}
              >
                {showApiKey ? <EyeOff className="w-3.5 h-3.5" /> : <Eye className="w-3.5 h-3.5" />}
              </button>
            </div>
          </div>
        </div>

        {/* Actions Menu */}
        <div className="flex items-center justify-end w-1/4">
          <div className="relative">
            <button 
              onClick={() => setShowDisplayMenu(!showDisplayMenu)}
              className={`flex items-center gap-2 px-3 py-1.5 rounded-md text-sm border transition-colors duration-200 ${
                darkMode ? 'bg-[#1A1A1A]/50 hover:bg-[#1A1A1A] border-[#3D2314]' : 'bg-white/10 hover:bg-white/20 border-white/10'
              }`}
            >
              <Settings className="w-4 h-4" />
              <span className="hidden sm:inline">Theme</span>
            </button>
            {showDisplayMenu && (
              <div className={`absolute right-0 mt-2 w-48 rounded-lg shadow-xl border z-50 overflow-hidden ${
                darkMode ? 'bg-[#24150B] border-[#3D2314] text-[#EAE6E1]' : 'bg-white border-gray-200 text-gray-800'
              }`}>
                <div className="p-2 border-b border-gray-500/20 text-[10px] uppercase font-bold opacity-60">Display</div>
                <button 
                  onClick={() => { setDarkMode(!darkMode); setShowDisplayMenu(false); }}
                  className="w-full flex items-center justify-between px-3 py-3 text-xs hover:bg-black/5 transition-colors"
                >
                  <span className="flex items-center gap-2">
                    {darkMode ? <Sun className="w-4 h-4" /> : <Moon className="w-4 h-4" />} Toggle Mode
                  </span>
                </button>
              </div>
            )}
          </div>
        </div>
      </header>

      {/* THREE-PANEL LAYOUT */}
      <div className="flex-1 flex overflow-hidden">
        
        {/* PANEL 1: SIDEBAR (Sources) */}
        <aside className={`w-72 flex flex-col border-r transition-colors duration-300 flex-shrink-0 ${
          darkMode ? 'bg-[#1A1A1A] border-[#3D2314]' : 'bg-white border-gray-200'
        }`}>
          <div className="p-4 border-b border-gray-500/10 flex items-center justify-between">
            <h2 className="font-semibold text-sm flex items-center gap-2">
              <Compass className={`w-4 h-4 ${darkMode ? 'text-[#D97736]' : 'text-blue-600'}`} /> Sources
            </h2>
            <span className="text-[10px] font-mono px-2 py-0.5 rounded-full bg-gray-500/10">{documents.length}</span>
          </div>

          <div className="p-3">
            <div className="relative">
              <input 
                type="text" 
                placeholder="Search..."
                value={searchTerm}
                onChange={(e) => setSearchTerm(e.target.value)}
                className={`w-full text-xs pl-8 pr-3 py-2 rounded-lg border transition-all ${
                  darkMode ? 'bg-[#24150B] border-[#3D2314] text-white focus:border-[#F59E0B]' : 'bg-gray-50 border-gray-200 focus:border-blue-500'
                } outline-none`}
              />
              <Search className="absolute left-2.5 top-2 w-3.5 h-3.5 opacity-50" />
            </div>
          </div>

          <div className="px-3 pb-3">
            <div 
              onDragEnter={handleDrag} onDragOver={handleDrag} onDragLeave={handleDrag} onDrop={handleDrop}
              onClick={() => fileInputRef.current.click()}
              className={`border-2 border-dashed rounded-lg p-4 text-center cursor-pointer transition-all ${
                dragActive ? (darkMode ? 'border-[#D97736] bg-[#D97736]/10' : 'border-blue-500 bg-blue-50') 
                : (darkMode ? 'border-gray-700 bg-gray-800/50 hover:bg-gray-800' : 'border-gray-300 bg-gray-50 hover:bg-gray-100')
              }`}
            >
              <Upload className={`w-5 h-5 mx-auto mb-1 ${darkMode ? 'text-[#D97736]' : 'text-blue-500'}`} />
              <p className="text-[11px] font-semibold">Upload Source</p>
              <p className="text-[9px] opacity-60 mt-0.5">PDF, DOCX, TXT</p>
              <input type="file" ref={fileInputRef} onChange={onFileInputChange} className="hidden" multiple />
            </div>
          </div>

          <div className="flex-1 overflow-y-auto px-2">
            {filteredDocs.length === 0 ? (
              <div className="p-4 text-center text-xs opacity-50">No sources found.</div>
            ) : (
              <div className="space-y-1">
                {filteredDocs.map((doc) => {
                  const isSelected = doc.id === selectedDocId;
                  return (
                    <div
                      key={doc.id}
                      onClick={() => setSelectedDocId(doc.id)}
                      className={`p-2.5 flex items-start gap-3 rounded-lg cursor-pointer transition-all duration-150 ${
                        isSelected 
                          ? (darkMode ? 'bg-[#24150B] text-white border border-[#3D2314]' : 'bg-blue-50 text-blue-900 border border-blue-100 shadow-sm')
                          : (darkMode ? 'hover:bg-gray-800 text-gray-400 border border-transparent' : 'hover:bg-gray-50 text-gray-600 border border-transparent')
                      }`}
                    >
                      <div className="mt-0.5 flex-shrink-0 bg-white rounded shadow-sm p-1">
                        {getFileIcon(doc.type)}
                      </div>
                      <div className="flex-1 min-w-0">
                        <h4 className="text-xs font-semibold truncate">{doc.name}</h4>
                        <div className="flex items-center gap-2 mt-0.5 opacity-60 text-[9px] uppercase tracking-wide">
                          <span>{doc.size}</span>
                        </div>
                      </div>
                      <button 
                        onClick={(e) => deleteDocument(doc.id, e)}
                        className="opacity-0 group-hover:opacity-100 hover:text-red-500 p-1 transition-opacity"
                      >
                        <Trash2 className="w-3.5 h-3.5" />
                      </button>
                    </div>
                  );
                })}
              </div>
            )}
          </div>
          
          <div className="p-3 border-t border-gray-500/10">
             <button 
                onClick={() => {
                  documents.forEach(d => { if (d.fileUrl && d.fileUrl.startsWith('blob:')) URL.revokeObjectURL(d.fileUrl); });
                  setDocuments(DEFAULT_DOCUMENTS); setSelectedDocId('doc-1');
                }}
                className="w-full py-2 text-[10px] uppercase font-bold tracking-wider rounded-md hover:bg-gray-500/10 transition-colors"
             >
                <RotateCcw className="w-3 h-3 inline mr-1" /> Reset Defaults
             </button>
          </div>
        </aside>

        {/* PANEL 2: MAIN WORKSPACE (Preview) */}
        <main className={`flex-1 flex flex-col min-w-0 transition-colors duration-300 ${
          darkMode ? 'bg-[#121212]' : 'bg-[#f8f9fa]'
        }`}>
          {/* Main Workspace Header */}
          <div className={`px-6 py-4 border-b flex items-center justify-between shadow-sm z-10 ${
            darkMode ? 'border-[#3D2314] bg-[#1A1A1A]' : 'border-gray-200 bg-white'
          }`}>
            <div>
              <div className="text-[10px] font-bold uppercase tracking-wider text-gray-500 mb-1">
                Document Preview
              </div>
              <h3 className="font-serif text-xl font-bold truncate max-w-lg">
                {activeDoc?.name || 'No Source Selected'}
              </h3>
            </div>
            {activeDoc?.fileUrl && !activeDoc.isDemo && (
              <a 
                href={activeDoc.fileUrl} 
                download={activeDoc.name}
                className="flex items-center gap-1.5 px-3 py-1.5 text-xs font-medium rounded border border-gray-300 hover:bg-gray-100 transition-colors"
              >
                <Download className="w-3.5 h-3.5" /> Download
              </a>
            )}
          </div>

          {/* Document Content Scroll Area */}
          <div className="flex-1 overflow-hidden flex flex-col p-4 md:p-6 bg-inherit">
             <DocumentViewer doc={activeDoc} pdfjsLoaded={pdfjsLoaded} />
          </div>
        </main>

        {/* PANEL 3: CHAT PANEL (Studio) */}
        <aside className={`w-80 md:w-96 flex flex-col border-l shadow-xl transition-colors duration-300 flex-shrink-0 z-20 ${
          darkMode ? 'bg-[#1A1A1A] border-[#3D2314]' : 'bg-white border-gray-200'
        }`}>
          <div className="p-4 border-b border-gray-500/10 flex items-center gap-2">
            <MessageSquare className={`w-5 h-5 ${darkMode ? 'text-[#D97736]' : 'text-blue-600'}`} />
            <h2 className="font-semibold text-sm">Notebook Studio</h2>
          </div>

          {/* Chat Messages */}
          <div className="flex-1 overflow-y-auto p-4 space-y-4">
            {messages.map((msg) => (
              <div key={msg.id} className={`flex flex-col ${msg.role === 'user' ? 'items-end' : 'items-start'}`}>
                <div className={`max-w-[85%] rounded-2xl px-4 py-2.5 text-sm ${
                  msg.role === 'user' 
                    ? (darkMode ? 'bg-[#D97736] text-white' : 'bg-blue-600 text-white')
                    : (darkMode ? 'bg-[#24150B] text-gray-200 border border-[#3D2314]' : 'bg-gray-100 text-gray-800 border border-gray-200')
                }`}>
                  <p className="leading-relaxed whitespace-pre-wrap">{msg.text}</p>
                </div>
                
                <div className="flex items-center gap-2 mt-1.5 px-1">
                  <span className="text-[9px] opacity-50">{msg.timestamp}</span>
                  {msg.citation && (
                    <span className={`text-[9px] px-1.5 py-0.5 rounded font-mono border ${
                      darkMode ? 'bg-[#3D2314] border-[#F59E0B]/30 text-[#F59E0B]' : 'bg-amber-50 border-amber-200 text-amber-700'
                    }`}>
                      {msg.citation}
                    </span>
                  )}
                </div>
              </div>
            ))}
            {isLoading && (
              <div className="flex items-start">
                <div className={`max-w-[85%] rounded-2xl px-4 py-3 border ${
                  darkMode ? 'bg-[#24150B] border-[#3D2314]' : 'bg-gray-100 border-gray-200'
                }`}>
                  <div className="flex gap-1.5">
                    <span className="w-1.5 h-1.5 rounded-full bg-gray-400 animate-bounce" style={{ animationDelay: '0ms' }} />
                    <span className="w-1.5 h-1.5 rounded-full bg-gray-400 animate-bounce" style={{ animationDelay: '150ms' }} />
                    <span className="w-1.5 h-1.5 rounded-full bg-gray-400 animate-bounce" style={{ animationDelay: '300ms' }} />
                  </div>
                </div>
              </div>
            )}
            <div ref={chatEndRef} />
          </div>

          {/* Chat Input */}
          <form onSubmit={handleSendMessage} className="p-4 border-t border-gray-500/10">
            <div className="relative flex items-center">
              <input
                type="text"
                placeholder={apiKey ? "Ask a question..." : "Enter API Key in the top header first!"}
                disabled={!apiKey || isLoading}
                value={chatInput}
                onChange={(e) => setChatInput(e.target.value)}
                className={`w-full text-sm pl-4 pr-12 py-3 rounded-xl border focus:outline-none transition-all ${
                  darkMode 
                    ? 'bg-[#24150B] border-[#3D2314] text-white focus:border-[#F59E0B] disabled:opacity-40' 
                    : 'bg-gray-50 border-gray-200 focus:border-blue-500 disabled:bg-gray-100 disabled:opacity-70'
                }`}
              />
              <button
                type="submit"
                disabled={!chatInput.trim() || !apiKey || isLoading}
                className={`absolute right-2 p-2 rounded-lg transition-all ${
                  darkMode 
                    ? 'text-[#F59E0B] hover:bg-white/5 disabled:opacity-35' 
                    : 'text-blue-600 hover:bg-gray-100 disabled:opacity-35'
                }`}
              >
                <Send className="w-4 h-4" />
              </button>
            </div>
          </form>
        </aside>

      </div>
    </div>
  );
}
