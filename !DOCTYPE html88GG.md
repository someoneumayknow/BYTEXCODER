**<!DOCTYPE html>**

**<html lang="en">**

**<head>+**

&#x20; **<meta charset="UTF-8">**

&#x20; **<meta name="viewport" content="width=device-width, initial-scale=1.0">**

&#x20; **<title>MediKiosk - Full-Stack Clinical Intake Engine</title>**

&#x20; **<script src="https://cdn.tailwindcss.com"></script>**

&#x20; **<link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">**

&#x20; **<style>**

&#x20;   **.pulse-ring {**

&#x20;     **animation: ring 1.5s infinite;**

&#x20;   **}**

&#x20;   **@keyframes ring {**

&#x20;     **0% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(13, 148, 136, 0.7); }**

&#x20;     **70% { transform: scale(1); box-shadow: 0 0 0 15px rgba(13, 148, 136, 0); }**

&#x20;     **100% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(13, 148, 136, 0); }**

&#x20;   **}**

&#x20; **</style>**

**</head>**

**<body class="bg-slate-100 text-slate-800 font-sans min-h-screen flex flex-col">**



&#x20; **<!-- Header -->**

&#x20; **<header class="bg-teal-800 text-white p-4 shadow-xl flex justify-between items-center">**

&#x20;   **<div class="flex items-center space-x-3">**

&#x20;     **<div class="bg-white text-teal-800 p-2.5 rounded-xl font-black text-2xl shadow">**

&#x20;       **<i class="fa-solid fa-notes-medical"></i>**

&#x20;     **</div>**

&#x20;     **<div>**

&#x20;       **<h1 class="text-2xl font-black tracking-tight">MediKiosk AI</h1>**

&#x20;       **<p class="text-xs text-teal-200 font-medium">Automated Clinical Intake \& ABDM Integration Platform</p>**

&#x20;     **</div>**

&#x20;   **</div>**

&#x20;   

&#x20;   **<div class="flex items-center space-x-4">**

&#x20;     **<div class="flex items-center bg-teal-900 rounded-lg p-1 border border-teal-700">**

&#x20;       **<button id="modeAllopathic" onclick="setClinicalMode('allopathic')" class="px-3 py-1.5 rounded-md text-xs font-bold bg-teal-600 text-white transition">Allopathic OPD</button>**

&#x20;       **<button id="modeAyush" onclick="setClinicalMode('ayush')" class="px-3 py-1.5 rounded-md text-xs font-bold text-teal-200 hover:text-white transition">AYUSH OPD</button>**

&#x20;     **</div>**



&#x20;     **<select id="languageSelect" onchange="changeLanguage()" class="bg-teal-900 text-white text-xs font-bold px-3 py-2 rounded-lg border border-teal-700 focus:outline-none">**

&#x20;       **<option value="en-US">English (US/IN)</option>**

&#x20;       **<option value="hi-IN">हिन्दी (Hindi)</option>**

&#x20;     **</select>**

&#x20;   **</div>**

&#x20; **</header>**



&#x20; **<!-- Navigation Stepper -->**

&#x20; **<nav class="bg-white border-b border-slate-200 px-6 py-3 shadow-sm">**

&#x20;   **<div class="max-w-6xl mx-auto flex justify-between items-center text-xs font-bold text-slate-500">**

&#x20;     **<div id="step-btn-1" class="flex items-center text-teal-700">**

&#x20;       **<span class="w-7 h-7 rounded-full bg-teal-700 text-white flex items-center justify-center mr-2 text-sm shadow">1</span>**

&#x20;       **Identity \& Consent**

&#x20;     **</div>**

&#x20;     **<div class="h-0.5 flex-1 mx-4 bg-slate-200"></div>**

&#x20;     **<div id="step-btn-2" class="flex items-center">**

&#x20;       **<span class="w-7 h-7 rounded-full bg-slate-200 text-slate-600 flex items-center justify-center mr-2 text-sm">2</span>**

&#x20;       **Adaptive Interview**

&#x20;     **</div>**

&#x20;     **<div class="h-0.5 flex-1 mx-4 bg-slate-200"></div>**

&#x20;     **<div id="step-btn-3" class="flex items-center">**

&#x20;       **<span class="w-7 h-7 rounded-full bg-slate-200 text-slate-600 flex items-center justify-center mr-2 text-sm">3</span>**

&#x20;       **Document Scan \& Vision**

&#x20;     **</div>**

&#x20;     **<div class="h-0.5 flex-1 mx-4 bg-slate-200"></div>**

&#x20;     **<div id="step-btn-4" class="flex items-center">**

&#x20;       **<span class="w-7 h-7 rounded-full bg-slate-200 text-slate-600 flex items-center justify-center mr-2 text-sm">4</span>**

&#x20;       **Doctor EMR Summary**

&#x20;     **</div>**

&#x20;   **</div>**

&#x20; **</nav>**



&#x20; **<!-- Emergency Priority Triage Banner -->**

&#x20; **<div id="redFlagBanner" class="hidden bg-red-600 text-white font-black px-6 py-3 text-center flex items-center justify-center space-x-3 text-sm animate-pulse shadow-lg">**

&#x20;   **<i class="fa-solid fa-triangle-exclamation text-2xl"></i>**

&#x20;   **<span>CRITICAL RED-FLAG DETECTED: Priority Triage Alert generated. Transferring patient to Emergency Desk 01 immediately.</span>**

&#x20; **</div>**



&#x20; **<!-- Main Container -->**

&#x20; **<main class="flex-grow max-w-6xl w-full mx-auto p-6">**



&#x20;   **<!-- STEP 1: AUTHENTICATION \& DPDP CONSENT -->**

&#x20;   **<section id="step1" class="bg-white rounded-2xl shadow-sm border border-slate-200 p-8">**

&#x20;     **<h2 class="text-xl font-bold text-teal-800 mb-1 flex items-center">**

&#x20;       **<i class="fa-solid fa-id-card text-teal-600 mr-2"></i> Step 1: Patient Identity \& Data Consent**

&#x20;     **</h2>**

&#x20;     **<p class="text-slate-500 text-xs mb-6">Connect your Ayushman Bharat Health Account (ABHA) or enter registration details.</p>**



&#x20;     **<div class="grid grid-cols-1 md:grid-cols-2 gap-6">**

&#x20;       **<div class="bg-slate-50 p-5 rounded-xl border border-slate-200">**

&#x20;         **<label class="block text-xs font-bold text-slate-700 uppercase tracking-wider mb-2">ABHA Address / ID Number</label>**

&#x20;         **<div class="flex space-x-2">**

&#x20;           **<input type="text" id="abhaIdInput" placeholder="12-3456-7890-1234 or user@abdm" class="flex-grow border border-slate-300 rounded-lg px-3 py-2 text-sm focus:outline-none focus:border-teal-600 font-mono">**

&#x20;           **<button onclick="fetchABHAProfile()" class="bg-teal-700 text-white px-4 py-2 rounded-lg text-xs font-bold hover:bg-teal-800 transition">Fetch ABHA</button>**

&#x20;         **</div>**

&#x20;         **<p class="text-\[11px] text-slate-500 mt-2"><i class="fa-solid fa-shield-halved text-teal-600"></i> Connected to ABDM Health Information Exchange (HIE)</p>**

&#x20;       **</div>**



&#x20;       **<div class="bg-slate-50 p-5 rounded-xl border border-slate-200 space-y-3">**

&#x20;         **<div>**

&#x20;           **<label class="block text-xs font-bold text-slate-600">Patient Full Name</label>**

&#x20;           **<input type="text" id="patientName" value="Rajesh Kumar" class="w-full border border-slate-300 rounded-lg px-3 py-1.5 text-sm font-semibold">**

&#x20;         **</div>**

&#x20;         **<div class="grid grid-cols-2 gap-3">**

&#x20;           **<div>**

&#x20;             **<label class="block text-xs font-bold text-slate-600">Age</label>**

&#x20;             **<input type="number" id="patientAge" value="52" class="w-full border border-slate-300 rounded-lg px-3 py-1.5 text-sm font-semibold">**

&#x20;           **</div>**

&#x20;           **<div>**

&#x20;             **<label class="block text-xs font-bold text-slate-600">Gender</label>**

&#x20;             **<select id="patientGender" class="w-full border border-slate-300 rounded-lg px-3 py-1.5 text-sm font-semibold">**

&#x20;               **<option>Male</option>**

&#x20;               **<option>Female</option>**

&#x20;               **<option>Other</option>**

&#x20;             **</select>**

&#x20;           **</div>**

&#x20;         **</div>**

&#x20;       **</div>**

&#x20;     **</div>**



&#x20;     **<!-- DPDP Consent Module -->**

&#x20;     **<div class="mt-6 bg-teal-50 border border-teal-200 rounded-xl p-5">**

&#x20;       **<div class="flex items-start space-x-3">**

&#x20;         **<input type="checkbox" id="dpdpConsent" class="mt-1 h-5 w-5 text-teal-600 rounded border-slate-300 focus:ring-teal-500">**

&#x20;         **<div>**

&#x20;           **<h4 class="text-xs font-bold text-teal-900 uppercase tracking-wide">Digital Personal Data Protection (DPDP) Act 2023 Consent Notice</h4>**

&#x20;           **<p class="text-xs text-teal-800 mt-1 leading-relaxed">**

&#x20;             **I grant explicit consent to MediKiosk to capture my voice narration, digitize my uploaded medical records, generate a structured clinical summary, and transmit this data securely over FHIR APIs to the hospital's EMR and my ABHA health locker. Session data will be cleared automatically post-consultation.**

&#x20;           **</p>**

&#x20;         **</div>**

&#x20;       **</div>**

&#x20;     **</div>**



&#x20;     **<div class="mt-8 text-right">**

&#x20;       **<button onclick="navigateStep(2)" class="bg-teal-700 text-white px-8 py-3 rounded-xl font-bold shadow-lg hover:bg-teal-800 transition">**

&#x20;         **Start Clinical Intake <i class="fa-solid fa-arrow-right ml-2"></i>**

&#x20;       **</button>**

&#x20;     **</div>**

&#x20;   **</section>**



&#x20;   **<!-- STEP 2: CONVERSATIONAL AI INTERVIEW -->**

&#x20;   **<section id="step2" class="hidden bg-white rounded-2xl shadow-sm border border-slate-200 p-8">**

&#x20;     **<div class="flex justify-between items-center mb-4">**

&#x20;       **<div>**

&#x20;         **<h2 class="text-xl font-bold text-teal-800 flex items-center">**

&#x20;           **<i class="fa-solid fa-hospital-user text-teal-600 mr-2"></i> Step 2: Adaptive Conversational Interview**

&#x20;         **</h2>**

&#x20;         **<p class="text-xs text-slate-500">Speak naturally in your preferred language or tap response cards.</p>**

&#x20;       **</div>**

&#x20;       **<span id="clinicalModeBadge" class="bg-teal-100 text-teal-800 text-xs font-black px-3 py-1 rounded-full uppercase">Allopathic Mode</span>**

&#x20;     **</div>**



&#x20;     **<!-- Live Voice Studio -->**

&#x20;     **<div class="bg-slate-900 text-white rounded-2xl p-6 mb-6 flex flex-col items-center justify-center text-center relative overflow-hidden shadow-inner">**

&#x20;       **<div id="recordingStatus" class="text-teal-400 text-xs font-mono font-bold tracking-widest uppercase mb-3">**

&#x20;         **<i class="fa-solid fa-circle text-\[8px] animate-ping mr-1"></i> Voice Engine Ready**

&#x20;       **</div>**



&#x20;       **<button id="micBtn" onclick="toggleVoiceRecognition()" class="w-20 h-20 bg-teal-600 hover:bg-teal-500 rounded-full flex items-center justify-center text-white text-3xl shadow-2xl transition focus:outline-none mb-4">**

&#x20;         **<i class="fa-solid fa-microphone"></i>**

&#x20;       **</button>**



&#x20;       **<p id="systemPromptText" class="text-lg font-medium text-slate-100 max-w-2xl leading-snug">**

&#x20;         **"Hello Rajesh. What is the main medical problem that brings you to the hospital today?"**

&#x20;       **</p>**



&#x20;       **<!-- Live Voice Speech Transcript Bar -->**

&#x20;       **<div class="mt-4 w-full max-w-xl bg-slate-800/80 border border-slate-700 rounded-lg p-2.5 text-xs text-slate-300 font-mono text-left flex items-center">**

&#x20;         **<span class="text-teal-400 font-bold mr-2">Live Transcript:</span>**

&#x20;         **<span id="speechTranscriptText" class="italic text-slate-400">Waiting for user voice input...</span>**

&#x20;       **</div>**

&#x20;     **</div>**



&#x20;     **<!-- Touch Option Cards -->**

&#x20;     **<div class="mb-6">**

&#x20;       **<label class="block text-xs font-bold text-slate-500 uppercase tracking-wider mb-3">Touch Option Cards:</label>**

&#x20;       **<div id="touchOptionsContainer" class="grid grid-cols-2 md:grid-cols-4 gap-3">**

&#x20;         **<!-- Dynamically Injected -->**

&#x20;       **</div>**

&#x20;     **</div>**



&#x20;     **<!-- Elicited Clinical Detail Stream -->**

&#x20;     **<div class="bg-slate-50 rounded-xl p-4 border border-slate-200 mb-6">**

&#x20;       **<h3 class="text-xs font-bold text-slate-600 uppercase tracking-wider mb-2 flex items-center">**

&#x20;         **<i class="fa-solid fa-stream mr-2 text-teal-600"></i> Captured Clinical Findings Stream**

&#x20;       **</h3>**

&#x20;       **<ul id="clinicalLogStream" class="text-xs space-y-2 font-mono text-slate-700">**

&#x20;         **<li class="italic text-slate-400 font-sans">No responses captured yet...</li>**

&#x20;       **</ul>**

&#x20;     **</div>**



&#x20;     **<div class="flex justify-between">**

&#x20;       **<button onclick="navigateStep(1)" class="bg-slate-200 text-slate-700 px-6 py-2.5 rounded-xl font-bold hover:bg-slate-300">Back</button>**

&#x20;       **<button onclick="navigateStep(3)" class="bg-teal-700 text-white px-8 py-2.5 rounded-xl font-bold shadow-lg hover:bg-teal-800">**

&#x20;         **Proceed to Document Digitization <i class="fa-solid fa-arrow-right ml-2"></i>**

&#x20;       **</button>**

&#x20;     **</div>**

&#x20;   **</section>**



&#x20;   **<!-- STEP 3: DOCUMENT DIGITIZATION \& VISION OCR -->**

&#x20;   **<section id="step3" class="hidden bg-white rounded-2xl shadow-sm border border-slate-200 p-8">**

&#x20;     **<h2 class="text-xl font-bold text-teal-800 mb-1 flex items-center">**

&#x20;       **<i class="fa-solid fa-file-medical-scan text-teal-600 mr-2"></i> Step 3: Medical Document Digitization Engine**

&#x20;     **</h2>**

&#x20;     **<p class="text-slate-500 text-xs mb-6">Upload physical prescriptions or lab reports to extract clinical entities.</p>**



&#x20;     **<div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">**

&#x20;       **<!-- File Input Dropzone -->**

&#x20;       **<div class="border-2 border-dashed border-teal-300 bg-teal-50/40 rounded-2xl p-6 flex flex-col items-center justify-center text-center">**

&#x20;         **<i class="fa-solid fa-file-pdf text-4xl text-teal-600 mb-3"></i>**

&#x20;         **<p class="text-sm font-bold text-slate-700">Upload Prescription / Lab Report Image</p>**

&#x20;         **<p class="text-xs text-slate-500 mb-4">PNG, JPG, or JPEG document formats supported</p>**



&#x20;         **<input type="file" id="documentFileInput" accept="image/\*" class="hidden" onchange="processUploadedDocument(event)">**

&#x20;         **<button onclick="document.getElementById('documentFileInput').click()" class="bg-teal-700 text-white px-5 py-2.5 rounded-xl text-xs font-bold shadow hover:bg-teal-800 transition">**

&#x20;           **<i class="fa-solid fa-upload mr-2"></i> Choose Local File**

&#x20;         **</button>**



&#x20;         **<div class="my-3 text-xs text-slate-400 font-bold">- OR SIMULATE DEMO -</div>**



&#x20;         **<button onclick="runSimulatedOCR()" class="bg-slate-800 text-white px-4 py-2 rounded-lg text-xs font-bold hover:bg-slate-900 transition">**

&#x20;           **Run Sample Prescription OCR**

&#x20;         **</button>**

&#x20;       **</div>**



&#x20;       **<!-- Vision/OCR Extraction Feedback Panel -->**

&#x20;       **<div class="bg-slate-50 rounded-2xl p-5 border border-slate-200 flex flex-col">**

&#x20;         **<h3 class="text-xs font-bold text-slate-700 uppercase tracking-wider mb-3 flex justify-between items-center">**

&#x20;           **<span>Extracted Clinical Entities</span>**

&#x20;           **<span id="ocrStatusTag" class="hidden bg-emerald-100 text-emerald-800 text-\[10px] font-extrabold px-2 py-0.5 rounded">Parsed Successfully</span>**

&#x20;         **</h3>**



&#x20;         **<div id="ocrOutputContent" class="flex-grow text-xs space-y-2 text-slate-600 font-mono bg-white p-3 rounded-xl border border-slate-200 overflow-y-auto max-h-56">**

&#x20;           **<p class="italic text-slate-400 font-sans">No document scanned. Upload a file or click simulate to test extraction.</p>**

&#x20;         **</div>**

&#x20;       **</div>**

&#x20;     **</div>**



&#x20;     **<div class="flex justify-between">**

&#x20;       **<button onclick="navigateStep(2)" class="bg-slate-200 text-slate-700 px-6 py-2.5 rounded-xl font-bold hover:bg-slate-300">Back</button>**

&#x20;       **<button onclick="generatePhysicianSummary()" class="bg-teal-700 text-white px-8 py-2.5 rounded-xl font-bold shadow-lg hover:bg-teal-800">**

&#x20;         **Generate Doctor Summary <i class="fa-solid fa-arrow-right ml-2"></i>**

&#x20;       **</button>**

&#x20;     **</div>**

&#x20;   **</section>**



&#x20;   **<!-- STEP 4: PHYSICIAN CLINICAL SUMMARY -->**

&#x20;   **<section id="step4" class="hidden bg-white rounded-2xl shadow-sm border border-slate-200 p-8">**

&#x20;     **<div class="flex justify-between items-center mb-6 pb-4 border-b border-slate-200">**

&#x20;       **<div>**

&#x20;         **<h2 class="text-xl font-bold text-slate-800 flex items-center">**

&#x20;           **<i class="fa-solid fa-user-doctor text-teal-700 mr-2"></i> Physician Structured EMR Summary**

&#x20;         **</h2>**

&#x20;         **<p class="text-xs text-slate-500">Auto-generated pre-consultation draft. Review, amend, and sync with hospital EMR.</p>**

&#x20;       **</div>**

&#x20;       **<div class="flex space-x-2">**

&#x20;         **<button onclick="window.print()" class="bg-slate-100 border border-slate-300 text-slate-700 px-4 py-2 rounded-xl text-xs font-bold hover:bg-slate-200">**

&#x20;           **<i class="fa-solid fa-print mr-1"></i> Print Summary**

&#x20;         **</button>**

&#x20;       **</div>**

&#x20;     **</div>**



&#x20;     **<!-- Structured Summary Card -->**

&#x20;     **<div class="bg-slate-50 border border-slate-300 rounded-2xl p-6 space-y-4 text-slate-800 text-sm">**

&#x20;       

&#x20;       **<!-- Header Metadata -->**

&#x20;       **<div class="grid grid-cols-2 md:grid-cols-4 gap-4 pb-4 border-b border-slate-200 text-xs">**

&#x20;         **<div><span class="font-bold text-slate-500">Patient:</span> <p id="summaryName" class="font-bold text-slate-900">Rajesh Kumar</p></div>**

&#x20;         **<div><span class="font-bold text-slate-500">Age/Gender:</span> <p id="summaryAgeGender" class="font-bold text-slate-900">52 / Male</p></div>**

&#x20;         **<div><span class="font-bold text-slate-500">ABHA Number:</span> <p id="summaryAbha" class="font-mono font-bold text-slate-900">12-3456-7890-1234</p></div>**

&#x20;         **<div><span class="font-bold text-slate-500">Intake Mode:</span> <p id="summaryMode" class="font-bold text-teal-700">Allopathic OPD</p></div>**

&#x20;       **</div>**



&#x20;       **<!-- Chief Complaint -->**

&#x20;       **<div>**

&#x20;         **<h4 class="font-bold text-teal-800 text-xs uppercase tracking-wider mb-1">1. Chief Complaint (CC)</h4>**

&#x20;         **<div id="summaryCC" class="bg-white p-3 rounded-xl border border-slate-200 text-slate-800 text-xs font-semibold">**

&#x20;           **Not recorded**

&#x20;         **</div>**

&#x20;       **</div>**



&#x20;       **<!-- HPI / SOCRATES -->**

&#x20;       **<div>**

&#x20;         **<h4 class="font-bold text-teal-800 text-xs uppercase tracking-wider mb-1">2. History of Present Illness (HPI - SOCRATES)</h4>**

&#x20;         **<div id="summaryHPI" class="bg-white p-3 rounded-xl border border-slate-200 text-slate-800 text-xs font-mono space-y-1">**

&#x20;           **Not recorded**

&#x20;         **</div>**

&#x20;       **</div>**



&#x20;       **<!-- AYUSH Panel -->**

&#x20;       **<div id="ayushSummaryPanel" class="hidden bg-emerald-50 border border-emerald-200 p-4 rounded-xl">**

&#x20;         **<h4 class="font-bold text-emerald-800 text-xs uppercase tracking-wider mb-2">**

&#x20;           **<i class="fa-solid fa-leaf mr-1"></i> AYUSH Dashavidha Pariksha Parameters**

&#x20;         **</h4>**

&#x20;         **<div id="summaryAyushData" class="grid grid-cols-2 md:grid-cols-3 gap-2 text-xs font-mono text-slate-800">**

&#x20;           **<!-- Dynamically populated -->**

&#x20;         **</div>**

&#x20;       **</div>**



&#x20;       **<!-- Medical History \& Document Flags -->**

&#x20;       **<div class="grid grid-cols-1 md:grid-cols-2 gap-4">**

&#x20;         **<div>**

&#x20;           **<h4 class="font-bold text-teal-800 text-xs uppercase tracking-wider mb-1">3. Past Medical \& Drug History</h4>**

&#x20;           **<div id="summaryPastHistory" class="bg-white p-3 rounded-xl border border-slate-200 text-slate-700 text-xs space-y-1">**

&#x20;             **<p>• Known Type 2 Diabetes Mellitus (5 years)</p>**

&#x20;             **<p>• Known Allergy: Penicillin</p>**

&#x20;           **</div>**

&#x20;         **</div>**



&#x20;         **<div>**

&#x20;           **<h4 class="font-bold text-teal-800 text-xs uppercase tracking-wider mb-1">4. Digitized Document \& Lab Flags</h4>**

&#x20;           **<div id="summaryLabFlags" class="bg-white p-3 rounded-xl border border-slate-200 text-slate-700 text-xs space-y-1 font-mono">**

&#x20;             **<p class="italic text-slate-400 font-sans">No abnormal lab flags extracted.</p>**

&#x20;           **</div>**

&#x20;         **</div>**

&#x20;       **</div>**



&#x20;     **</div>**



&#x20;     **<div class="mt-6 flex justify-between items-center">**

&#x20;       **<button onclick="navigateStep(3)" class="bg-slate-200 text-slate-700 px-6 py-2.5 rounded-xl font-bold hover:bg-slate-300">Back</button>**

&#x20;       **<button onclick="syncToEMR()" class="bg-teal-700 text-white px-8 py-3 rounded-xl font-bold shadow-lg hover:bg-teal-800 transition">**

&#x20;         **<i class="fa-solid fa-cloud-arrow-up mr-2"></i> Push to Hospital EMR \& ABHA Locker**

&#x20;       **</button>**

&#x20;     **</div>**

&#x20;   **</section>**



&#x20; **</main>**



&#x20; **<script>**

&#x20;   **// State Architecture**

&#x20;   **let currentMode = 'allopathic'; // 'allopathic' | 'ayush'**

&#x20;   **let currentStep = 1;**

&#x20;   **let isListening = false;**

&#x20;   **let selectedLanguage = 'en-US';**

&#x20;   **let currentQuestionIdx = 0;**



&#x20;   **let clinicalData = {**

&#x20;     **chiefComplaint: "",**

&#x20;     **hpiDetails: \[],**

&#x20;     **ayushDetails: {**

&#x20;       **prakriti: "Not assessed",**

&#x20;       **agni: "Not assessed",**

&#x20;       **koshtha: "Not assessed"**

&#x20;     **},**

&#x20;     **ocrEntities: \[]**

&#x20;   **};**



&#x20;   **// Question Libraries**

&#x20;   **const allopathicQuestions = \[**

&#x20;     **{**

&#x20;       **prompt: "What is your main medical problem or symptom today?",**

&#x20;       **options: \["Chest Pain", "High Fever \& Cough", "Severe Abdominal Pain", "Joint Pain \& Swelling"],**

&#x20;       **key: "Chief Complaint"**

&#x20;     **},**

&#x20;     **{**

&#x20;       **prompt: "When did this complaint start, and how severe is it right now?",**

&#x20;       **options: \["Sudden onset (2 hours ago)", "Gradual (3 days ago)", "Chronic (Several months)"],**

&#x20;       **key: "Onset \& Duration"**

&#x20;     **},**

&#x20;     **{**

&#x20;       **prompt: "Does the pain or discomfort radiate anywhere else, like your arm, back, or jaw?",**

&#x20;       **options: \["Radiates to Left Arm \& Jaw", "Radiates to Back", "Stays in one localized spot"],**

&#x20;       **key: "Radiation"**

&#x20;     **}**

&#x20;   **];**



&#x20;   **const ayushQuestions = \[**

&#x20;     **{**

&#x20;       **prompt: "Describe your digestion and bowel habits (Koshtha Pariksha).",**

&#x20;       **options: \["Hard stools / Constipation (Krura)", "Loose stools (Mridu)", "Regular / Balanced (Madhyama)"],**

&#x20;       **key: "Koshtha"**

&#x20;     **},**

&#x20;     **{**

&#x20;       **prompt: "How is your appetite and digestive fire (Agni Pariksha)?",**

&#x20;       **options: \["Irregular (Vishamagni)", "Excessive / Burning (Tikshnagni)", "Sluggish / Low (Mandagni)"],**

&#x20;       **key: "Agni"**

&#x20;     **}**

&#x20;   **];**



&#x20;   **// Speech Recognition Setup**

&#x20;   **const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;**

&#x20;   **let recognition = null;**



&#x20;   **if (SpeechRecognition) {**

&#x20;     **recognition = new SpeechRecognition();**

&#x20;     **recognition.continuous = false;**

&#x20;     **recognition.interimResults = true;**



&#x20;     **recognition.onresult = (event) => {**

&#x20;       **let transcript = '';**

&#x20;       **for (let i = event.resultIndex; i < event.results.length; ++i) {**

&#x20;         **transcript += event.results\[i]\[0].transcript;**

&#x20;       **}**

&#x20;       **document.getElementById('speechTranscriptText').innerText = transcript;**



&#x20;       **if (event.results\[0].isFinal) {**

&#x20;         **handleVoiceAnswer(transcript);**

&#x20;       **}**

&#x20;     **};**



&#x20;     **recognition.onend = () => {**

&#x20;       **if (isListening) {**

&#x20;         **stopListeningUI();**

&#x20;       **}**

&#x20;     **};**

&#x20;   **}**



&#x20;   **function toggleVoiceRecognition() {**

&#x20;     **if (!SpeechRecognition) {**

&#x20;       **alert("Web Speech API is not supported in this browser. Please use Chrome or Edge.");**

&#x20;       **return;**

&#x20;     **}**



&#x20;     **if (!isListening) {**

&#x20;       **recognition.lang = selectedLanguage;**

&#x20;       **recognition.start();**

&#x20;       **isListening = true;**

&#x20;       **document.getElementById('micBtn').classList.add('bg-red-600', 'pulse-ring');**

&#x20;       **document.getElementById('recordingStatus').innerText = "LISTENING... SPEAK NOW";**

&#x20;       **document.getElementById('recordingStatus').classList.replace('text-teal-400', 'text-red-400');**

&#x20;     **} else {**

&#x20;       **stopListeningUI();**

&#x20;     **}**

&#x20;   **}**



&#x20;   **function stopListeningUI() {**

&#x20;     **if (recognition) recognition.stop();**

&#x20;     **isListening = false;**

&#x20;     **document.getElementById('micBtn').classList.remove('bg-red-600', 'pulse-ring');**

&#x20;     **document.getElementById('recordingStatus').innerText = "VOICE ENGINE READY";**

&#x20;     **document.getElementById('recordingStatus').classList.replace('text-red-400', 'text-teal-400');**

&#x20;   **}**



&#x20;   **function speakText(text) {**

&#x20;     **if ('speechSynthesis' in window) {**

&#x20;       **window.speechSynthesis.cancel();**

&#x20;       **const utterance = new SpeechSynthesisUtterance(text);**

&#x20;       **utterance.lang = selectedLanguage;**

&#x20;       **window.speechSynthesis.speak(utterance);**

&#x20;     **}**

&#x20;   **}**



&#x20;   **function setClinicalMode(mode) {**

&#x20;     **currentMode = mode;**

&#x20;     **currentQuestionIdx = 0;**

&#x20;     **const btnAllo = document.getElementById('modeAllopathic');**

&#x20;     **const btnAyu = document.getElementById('modeAyush');**

&#x20;     **const badge = document.getElementById('clinicalModeBadge');**



&#x20;     **if (mode === 'ayush') {**

&#x20;       **btnAyu.className = "px-3 py-1.5 rounded-md text-xs font-bold bg-teal-600 text-white transition";**

&#x20;       **btnAllo.className = "px-3 py-1.5 rounded-md text-xs font-bold text-teal-200 hover:text-white transition";**

&#x20;       **badge.innerText = "AYUSH Mode";**

&#x20;       **badge.className = "bg-emerald-100 text-emerald-800 text-xs font-black px-3 py-1 rounded-full uppercase";**

&#x20;     **} else {**

&#x20;       **btnAllo.className = "px-3 py-1.5 rounded-md text-xs font-bold bg-teal-600 text-white transition";**

&#x20;       **btnAyu.className = "px-3 py-1.5 rounded-md text-xs font-bold text-teal-200 hover:text-white transition";**

&#x20;       **badge.innerText = "Allopathic Mode";**

&#x20;       **badge.className = "bg-teal-100 text-teal-800 text-xs font-black px-3 py-1 rounded-full uppercase";**

&#x20;     **}**

&#x20;     **renderActiveQuestion();**

&#x20;   **}**



&#x20;   **function changeLanguage() {**

&#x20;     **selectedLanguage = document.getElementById('languageSelect').value;**

&#x20;     **renderActiveQuestion();**

&#x20;   **}**



&#x20;   **function navigateStep(step) {**

&#x20;     **if (step === 2 \&\& !document.getElementById('dpdpConsent').checked) {**

&#x20;       **alert("Please review and accept the DPDP Act consent terms before continuing.");**

&#x20;       **return;**

&#x20;     **}**



&#x20;     **document.querySelectorAll('main > section').forEach(sec => sec.classList.add('hidden'));**

&#x20;     **document.getElementById(`step${step}`).classList.remove('hidden');**



&#x20;     **for (let i = 1; i <= 4; i++) {**

&#x20;       **const btn = document.getElementById(`step-btn-${i}`);**

&#x20;       **const span = btn.querySelector('span');**

&#x20;       **if (i <= step) {**

&#x20;         **btn.classList.add('text-teal-700');**

&#x20;         **span.className = "w-7 h-7 rounded-full bg-teal-700 text-white flex items-center justify-center mr-2 text-sm shadow";**

&#x20;       **} else {**

&#x20;         **btn.classList.remove('text-teal-700');**

&#x20;         **span.className = "w-7 h-7 rounded-full bg-slate-200 text-slate-600 flex items-center justify-center mr-2 text-sm";**

&#x20;       **}**

&#x20;     **}**



&#x20;     **currentStep = step;**

&#x20;     **if (step === 2) {**

&#x20;       **renderActiveQuestion();**

&#x20;     **}**

&#x20;   **}**



&#x20;   **function renderActiveQuestion() {**

&#x20;     **const questions = currentMode === 'ayush' ? ayushQuestions : allopathicQuestions;**

&#x20;     **const q = questions\[currentQuestionIdx] || questions\[0];**



&#x20;     **document.getElementById('systemPromptText').innerText = `"${q.prompt}"`;**

&#x20;     **speakText(q.prompt);**



&#x20;     **const optionsBox = document.getElementById('touchOptionsContainer');**

&#x20;     **optionsBox.innerHTML = '';**



&#x20;     **q.options.forEach(opt => {**

&#x20;       **const btn = document.createElement('button');**

&#x20;       **btn.className = "bg-slate-50 border border-slate-300 hover:bg-teal-50 hover:border-teal-600 rounded-xl p-3 text-xs font-bold text-slate-700 transition text-left flex items-center justify-between";**

&#x20;       **btn.innerHTML = `<span>${opt}</span> <i class="fa-solid fa-circle-chevron-right text-teal-600"></i>`;**

&#x20;       **btn.onclick = () => recordClinicalFinding(q.key, opt);**

&#x20;       **optionsBox.appendChild(btn);**

&#x20;     **});**

&#x20;   **}**



&#x20;   **function handleVoiceAnswer(transcript) {**

&#x20;     **const questions = currentMode === 'ayush' ? ayushQuestions : allopathicQuestions;**

&#x20;     **const q = questions\[currentQuestionIdx] || questions\[0];**

&#x20;     **recordClinicalFinding(q.key, transcript);**

&#x20;   **}**



&#x20;   **function recordClinicalFinding(key, value) {**

&#x20;     **// Append to findings log**

&#x20;     **const stream = document.getElementById('clinicalLogStream');**

&#x20;     **if (stream.querySelector('.italic')) stream.innerHTML = '';**



&#x20;     **const li = document.createElement('li');**

&#x20;     **li.className = "bg-white p-2 rounded border border-slate-200 flex justify-between items-center";**

&#x20;     **li.innerHTML = `<span><strong class="text-teal-800">${key}:</strong> ${value}</span> <i class="fa-solid fa-check text-emerald-600"></i>`;**

&#x20;     **stream.appendChild(li);**



&#x20;     **// Save into clinical data model**

&#x20;     **if (key === "Chief Complaint") {**

&#x20;       **clinicalData.chiefComplaint = value;**

&#x20;     **} else if (currentMode === 'ayush') {**

&#x20;       **clinicalData.ayushDetails\[key.toLowerCase()] = value;**

&#x20;     **} else {**

&#x20;       **clinicalData.hpiDetails.push(`${key}: ${value}`);**

&#x20;     **}**



&#x20;     **// Red Flag Emergency Detection Logic**

&#x20;     **const lower = value.toLowerCase();**

&#x20;     **if (lower.includes("chest pain") || lower.includes("left arm") || lower.includes("breathlessness")) {**

&#x20;       **document.getElementById('redFlagBanner').classList.remove('hidden');**

&#x20;     **}**



&#x20;     **// Advance question index**

&#x20;     **const questions = currentMode === 'ayush' ? ayushQuestions : allopathicQuestions;**

&#x20;     **if (currentQuestionIdx < questions.length - 1) {**

&#x20;       **currentQuestionIdx++;**

&#x20;       **renderActiveQuestion();**

&#x20;     **}**

&#x20;   **}**



&#x20;   **function fetchABHAProfile() {**

&#x20;     **const abha = document.getElementById('abhaIdInput').value || "12-3456-7890-1234";**

&#x20;     **document.getElementById('patientName').value = "Rajesh Kumar";**

&#x20;     **document.getElementById('patientAge').value = "52";**

&#x20;     **alert("ABHA Profile fetched successfully via ABDM Mock Gateway.");**

&#x20;   **}**



&#x20;   **// Client-side Document OCR Parsing Simulation**

&#x20;   **function processUploadedDocument(event) {**

&#x20;     **const file = event.target.files\[0];**

&#x20;     **if (!file) return;**



&#x20;     **const output = document.getElementById('ocrOutputContent');**

&#x20;     **const tag = document.getElementById('ocrStatusTag');**



&#x20;     **output.innerHTML = `<p class="text-teal-600 font-bold animate-pulse"><i class="fa-solid fa-spinner fa-spin mr-2"></i> Analyzing ${file.name} via Vision OCR...</p>`;**



&#x20;     **setTimeout(() => {**

&#x20;       **tag.classList.remove('hidden');**

&#x20;       **output.innerHTML = `**

&#x20;         **<div class="space-y-1">**

&#x20;           **<p><strong>File Name:</strong> ${file.name}</p>**

&#x20;           **<p><strong>Document Type:</strong> Prior Hospital Discharge Summary</p>**

&#x20;           **<p><strong>Extracted Diagnosis:</strong> Type 2 Diabetes Mellitus, Hypertension</p>**

&#x20;           **<p><strong>Active Meds:</strong> Metformin 500mg BD, Telmisartan 40mg OD</p>**

&#x20;           **<p class="text-red-600 font-bold mt-2"><i class="fa-solid fa-triangle-exclamation"></i> Lab Flag: HbA1c = 8.2% (High / Uncontrolled)</p>**

&#x20;         **</div>**

&#x20;       **`;**

&#x20;       **clinicalData.ocrEntities = \[**

&#x20;         **"Dx: Type 2 Diabetes Mellitus, Hypertension",**

&#x20;         **"Rx: Metformin 500mg BD, Telmisartan 40mg OD",**

&#x20;         **"Lab Flag: HbA1c 8.2% (Above reference range > 6.5%)"**

&#x20;       **];**

&#x20;     **}, 1500);**

&#x20;   **}**



&#x20;   **function runSimulatedOCR() {**

&#x20;     **const output = document.getElementById('ocrOutputContent');**

&#x20;     **const tag = document.getElementById('ocrStatusTag');**



&#x20;     **output.innerHTML = `<p class="text-teal-600 font-bold animate-pulse"><i class="fa-solid fa-spinner fa-spin mr-2"></i> Parsing Demo Prescription OCR...</p>`;**



&#x20;     **setTimeout(() => {**

&#x20;       **tag.classList.remove('hidden');**

&#x20;       **output.innerHTML = `**

&#x20;         **<div class="space-y-1">**

&#x20;           **<p><strong>Extracted Prescription:</strong> AIIMS OPD Record</p>**

&#x20;           **<p><strong>Extracted Diagnosis:</strong> Essential Hypertension</p>**

&#x20;           **<p><strong>Prescribed Meds:</strong> Tab Amlodipine 5mg OD</p>**

&#x20;           **<p class="text-red-600 font-bold mt-2"><i class="fa-solid fa-triangle-exclamation"></i> Lab Flag: Fasting Blood Sugar 160 mg/dL (Abnormal)</p>**

&#x20;         **</div>**

&#x20;       **`;**

&#x20;       **clinicalData.ocrEntities = \[**

&#x20;         **"Prescription: AIIMS OPD - Essential Hypertension",**

&#x20;         **"Meds: Tab Amlodipine 5mg OD",**

&#x20;         **"Lab Flag: Fasting Blood Sugar 160 mg/dL (Abnormal)"**

&#x20;       **];**

&#x20;     **}, 1200);**

&#x20;   **}**



&#x20;   **function generatePhysicianSummary() {**

&#x20;     **navigateStep(4);**



&#x20;     **document.getElementById('summaryName').innerText = document.getElementById('patientName').value;**

&#x20;     **document.getElementById('summaryAgeGender').innerText = `${document.getElementById('patientAge').value} / ${document.getElementById('patientGender').value}`;**

&#x20;     **document.getElementById('summaryAbha').innerText = document.getElementById('abhaIdInput').value || "12-3456-7890-1234";**

&#x20;     **document.getElementById('summaryMode').innerText = currentMode === 'ayush' ? "AYUSH OPD" : "Allopathic OPD";**



&#x20;     **document.getElementById('summaryCC').innerText = clinicalData.chiefComplaint || "Chest Pain \& mild dyspnea";**



&#x20;     **const hpiBox = document.getElementById('summaryHPI');**

&#x20;     **if (clinicalData.hpiDetails.length > 0) {**

&#x20;       **hpiBox.innerHTML = clinicalData.hpiDetails.map(item => `<p>• ${item}</p>`).join('');**

&#x20;     **} else {**

&#x20;       **hpiBox.innerHTML = `<p>• Sudden onset retrosternal pain (2 hours ago)</p><p>• Radiates to Left Arm \& Jaw</p>`;**

&#x20;     **}**



&#x20;     **// Render AYUSH Data**

&#x20;     **const ayushPanel = document.getElementById('ayushSummaryPanel');**

&#x20;     **if (currentMode === 'ayush') {**

&#x20;       **ayushPanel.classList.remove('hidden');**

&#x20;       **document.getElementById('summaryAyushData').innerHTML = `**

&#x20;         **<div><strong>Koshtha:</strong> ${clinicalData.ayushDetails.koshtha || "Krura"}</div>**

&#x20;         **<div><strong>Agni:</strong> ${clinicalData.ayushDetails.agni || "Mandagni"}</div>**

&#x20;         **<div><strong>Prakriti:</strong> Vata-Pitta</div>**

&#x20;       **`;**

&#x20;     **} else {**

&#x20;       **ayushPanel.classList.add('hidden');**

&#x20;     **}**



&#x20;     **// Render Document/Lab Flags**

&#x20;     **const flagsBox = document.getElementById('summaryLabFlags');**

&#x20;     **if (clinicalData.ocrEntities.length > 0) {**

&#x20;       **flagsBox.innerHTML = clinicalData.ocrEntities.map(f => `<p class="text-slate-800">• ${f}</p>`).join('');**

&#x20;     **} else {**

&#x20;       **flagsBox.innerHTML = `<p class="italic text-slate-400 font-sans">No abnormal lab flags extracted.</p>`;**

&#x20;     **}**

&#x20;   **}**



&#x20;   **function syncToEMR() {**

&#x20;     **alert("Success! Clinical history JSON payload and FHIR bundle pushed to Hospital Information System (HIS) and linked to ABHA profile.");**

&#x20;   **}**

&#x20; **</script>**

**</body>**

**</html>**



