import React, { useState, useEffect } from 'react';
import { RefreshCw, Search, ShieldAlert, Zap, TrendingUp, AlertTriangle, ChevronDown, ChevronUp, Copy, Check, Settings, Save, LayoutTemplate, ExternalLink, ArrowRight, LayoutGrid, ShoppingBag, Sparkles, Target, Megaphone, Calendar, Clock, Globe, Code, RotateCcw } from 'lucide-react';

// --- DEFAULT CONFIGURATIONS ---

const DEFAULT_INFI_PROFILE = `**INFI Profile:**
- **Category:** Restaurant Growth Platform.
- **Core Value:** "Guided Growth" (We don't just sell software; we guide implementation and success).
- **Product Suite:** Unified Kiosk, Mobile App, Online Ordering, and Merchant-Facing Fulfillment Tools (V2).
- **Differentiation:** Unifying guest data across channels to build relationships (vs. just processing transactions).
- **Brand Tone:** Confident, Human, Relatable, Visionary (Mentor-like).`;

const DEFAULT_COMPETITORS = `1. **Ecosystem Giants:** Toast POS, Square (Restaurants/Kiosks), Clover.
2. **Aggregators:** DoorDash (Storefront), Chowly, UberEats.
3. **Emerging/Niche:** App building agencies, Solo Kiosk vendors.`;

const DEFAULT_FOCUS_AREAS = "New Kiosk hardware, Mobile App updates, Online Ordering pricing changes, Loyalty program integrations, Merchant fulfillment tools.";

const TIME_RANGES = {
  'Past Month': 'last 30 days',
  'Past Quarter': 'last 90 days',
  'Past Year': 'last 12 months'
};

const DEFAULT_PROMPT_TEMPLATE = `Using the Google Search tool, perform a deep dive search for news, product updates, and pricing changes from the **{{TIME_RANGE_QUERY}}** (relative to today, {{TODAY_DATE}}) for the following competitors and topics.

**Target Competitors:**
{{COMPETITORS}}

**Focus Areas:**
{{FOCUS_AREAS}}

**Context on INFI:**
{{INFI_PROFILE}}

**Source Strategy (CRITICAL):**
- **Prioritize Authoritative Sources:** You MUST prioritize searching for and citing official sources (e.g., official company blogs, press release pages, investor relations PDFs, changelogs). Examples: 'toasttab.com/news', 'squareup.com', 'investor.doordash.com'.
- **Secondary Sources:** Use reputable industry analysis (e.g., Restaurant Dive, Pyments) only if official announcements are not available.

**Requirement:** 1. Categorize findings into "Ecosystem", "Aggregator", or "Trend".
2. Include a specific Source/URL for every claim. **Prefer the official company URL.**
3. Output STRICT JSON format only. Do not include markdown formatting if possible, but if you do, wrap it in a json code block.
4. IMPORTANT: Ensure all findings are strictly within the **{{TIME_RANGE_QUERY}}**.

**Expected JSON Structure:**
{
  "date": "string (e.g. Oct 24, 2025)",
  "time_range": "{{TIME_RANGE_LABEL}}",
  "signals": [
    { 
      "category": "Ecosystem" | "Aggregator" | "Trend", 
      "competitor": "string", 
      "update": "string (summary of the news)", 
      "source_url": "string",
      "source_name": "string (e.g. Toast Investor Relations, Square Blog)"
    }
  ],
  "stressTest": [
     { "update": "string", "threat": "string (Why it hurts INFI)", "counter": "string (Sales/Product response)" }
  ],
  "actions": {
     "sales": "string", "product": "string", "marketing": "string"
  }
}`;

// --- COMPONENT ---

const App = () => {
  // Application State
  const [activeTab, setActiveTab] = useState('monitor'); // 'monitor' | 'config'
  const [apiKey, setApiKey] = useState('AIzaSyAOQ_UL4tvQmh4S9EGgyNurQTiARLdMusQ');
  const [timeRange, setTimeRange] = useState('Past Month');
  
  // Configuration State
  const [infiProfile, setInfiProfile] = useState(DEFAULT_INFI_PROFILE);
  const [competitors, setCompetitors] = useState(DEFAULT_COMPETITORS);
  const [focusAreas, setFocusAreas] = useState(DEFAULT_FOCUS_AREAS);
  const [promptTemplate, setPromptTemplate] = useState(DEFAULT_PROMPT_TEMPLATE);
  
  // Report State
  const [loading, setLoading] = useState(false);
  const [reportData, setReportData] = useState(null); // Now stores JSON object
  const [error, setError] = useState(null);
  const [copied, setCopied] = useState(false);
  
  // Initialize API key from local storage
  useEffect(() => {
    const storedKey = localStorage.getItem('gemini_api_key');
    if (storedKey) setApiKey(storedKey);
  }, []);

  const handleSaveKey = (e) => {
    const key = e.target.value;
    setApiKey(key);
    localStorage.setItem('gemini_api_key', key);
  };

  const handleResetConfig = () => {
    if (window.confirm("Are you sure you want to reset all settings (including the prompt) to default?")) {
      setInfiProfile(DEFAULT_INFI_PROFILE);
      setCompetitors(DEFAULT_COMPETITORS);
      setFocusAreas(DEFAULT_FOCUS_AREAS);
      setPromptTemplate(DEFAULT_PROMPT_TEMPLATE);
    }
  };

  const handleResetPrompt = () => {
    if (window.confirm("Reset just the prompt template to default?")) {
      setPromptTemplate(DEFAULT_PROMPT_TEMPLATE);
    }
  };

  const generateReport = async () => {
    if (!apiKey) {
      setError("Please enter a valid Gemini API Key.");
      return;
    }

    setLoading(true);
    setError(null);
    setReportData(null);
    setActiveTab('monitor'); 

    try {
      const timeRangeQuery = TIME_RANGES[timeRange];
      const today = new Date().toLocaleDateString();

      // Dynamic Prompt Construction
      let finalPrompt = promptTemplate
        .replace('{{TIME_RANGE_QUERY}}', timeRangeQuery)
        .replace('{{TIME_RANGE_QUERY}}', timeRangeQuery) // Replace again if appears twice
        .replace('{{TODAY_DATE}}', today)
        .replace('{{COMPETITORS}}', competitors)
        .replace('{{FOCUS_AREAS}}', focusAreas)
        .replace('{{INFI_PROFILE}}', infiProfile)
        .replace('{{TIME_RANGE_LABEL}}', timeRange);

      const response = await fetch(
        `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`,
        {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({
            contents: [{ parts: [{ text: finalPrompt }] }],
            systemInstruction: {
              parts: [{ text: `You are a strategic product analyst for INFI. You must return valid JSON only.` }],
            },
            tools: [{ google_search: {} }]
          }),
        }
      );

      if (!response.ok) {
        const errData = await response.json();
        throw new Error(errData.error?.message || 'Failed to generate report');
      }

      const data = await response.json();
      let generatedText = data.candidates?.[0]?.content?.parts?.[0]?.text;
      
      if (generatedText) {
        // CLEANUP: Extract JSON if wrapped in markdown code blocks
        if (generatedText.includes("```json")) {
            generatedText = generatedText.replace(/```json\n?|\n?```/g, "");
        } else if (generatedText.includes("```")) {
            generatedText = generatedText.replace(/```\n?|\n?```/g, "");
        }
        
        try {
            const parsedJson = JSON.parse(generatedText);
            setReportData(parsedJson);
        } catch (parseError) {
            console.error("JSON Parse Error:", parseError);
            console.log("Raw Text:", generatedText);
            throw new Error("AI returned invalid JSON format. Check your prompt or try again.");
        }
      } else {
        throw new Error("No content generated. Please try again.");
      }

    } catch (err) {
      setError(err.message);
    } finally {
      setLoading(false);
    }
  };

  const copyToClipboard = () => {
    if (!reportData) return;
    // Simple text representation for copying
    const textRep = `INFI Report (${reportData.date} - ${timeRange})\n\nSIGNALS:\n${reportData.signals.map(s => `- ${s.competitor}: ${s.update} (Source: ${s.source_url})`).join('\n')}`;
    const textArea = document.createElement("textarea");
    textArea.value = textRep;
    document.body.appendChild(textArea);
    textArea.select();
    try {
      document.execCommand('copy');
      setCopied(true);
      setTimeout(() => setCopied(false), 2000);
    } catch (err) {
      console.error('Failed to copy', err);
    }
    document.body.removeChild(textArea);
  };

  // Helper to get category styles
  const getCategoryStyle = (cat) => {
    const c = (cat || '').toLowerCase();
    if (c.includes('ecosystem')) return { bg: 'bg-blue-100', text: 'text-blue-700', icon: <LayoutGrid className="w-3 h-3"/> };
    if (c.includes('aggregator')) return { bg: 'bg-orange-100', text: 'text-orange-700', icon: <ShoppingBag className="w-3 h-3"/> };
    return { bg: 'bg-purple-100', text: 'text-purple-700', icon: <Sparkles className="w-3 h-3"/> };
  };

  // Helper for report title
  const getReportTitle = (range) => {
      switch(range) {
          case 'Past Quarter': return 'Quarterly Monitor';
          case 'Past Year': return 'Annual Monitor';
          default: return 'Bi-Weekly Monitor';
      }
  };

  return (
    <div className="min-h-screen bg-slate-50 text-slate-900 font-sans flex flex-col">
      {/* Header */}
      <header className="bg-slate-900 text-white p-4 shadow-lg sticky top-0 z-20 border-b border-slate-700">
        <div className="max-w-6xl mx-auto flex flex-col md:flex-row justify-between items-center gap-4">
          <div className="flex items-center gap-3">
            <div className="bg-blue-600 p-2 rounded-lg shadow-inner">
              <Zap className="text-white w-6 h-6" />
            </div>
            <div>
              <h1 className="text-xl font-bold tracking-tight text-white">INFI Competitor Radar</h1>
              <p className="text-slate-400 text-xs font-medium">AI-Powered Strategic Intelligence</p>
            </div>
          </div>
          
          <div className="flex flex-col md:flex-row items-center gap-3 w-full md:w-auto">
             {/* Time Range Selector */}
             <div className="relative">
                <select 
                    value={timeRange}
                    onChange={(e) => setTimeRange(e.target.value)}
                    className="appearance-none bg-slate-800 text-white text-sm font-medium border border-slate-600 rounded-lg px-4 py-2 pr-8 focus:outline-none focus:ring-2 focus:ring-blue-500 cursor-pointer hover:bg-slate-700 transition-colors"
                >
                    {Object.keys(TIME_RANGES).map(range => (
                        <option key={range} value={range}>{range}</option>
                    ))}
                </select>
                <div className="absolute right-3 top-1/2 transform -translate-y-1/2 pointer-events-none text-slate-400">
                    <Clock className="w-3 h-3" />
                </div>
             </div>

             <input
              type="password"
              placeholder="Enter Gemini API Key"
              value={apiKey}
              onChange={handleSaveKey}
              className="px-3 py-2 rounded bg-slate-800 border border-slate-600 text-white placeholder-slate-400 text-sm focus:outline-none focus:ring-2 focus:ring-blue-500 w-full md:w-32"
            />
            <button 
              onClick={generateReport}
              disabled={loading || !apiKey}
              className={`flex items-center gap-2 px-5 py-2 rounded-lg font-semibold shadow-md transition-all whitespace-nowrap w-full md:w-auto justify-center ${
                loading || !apiKey 
                  ? 'bg-slate-700 text-slate-500 cursor-not-allowed' 
                  : 'bg-blue-600 hover:bg-blue-500 text-white hover:shadow-lg transform hover:-translate-y-0.5'
              }`}
            >
              {loading ? (
                <>
                  <RefreshCw className="w-4 h-4 animate-spin" />
                  Scanning...
                </>
              ) : (
                <>
                  <Search className="w-4 h-4" />
                  Scan Market
                </>
              )}
            </button>
          </div>
        </div>
      </header>

      {/* Tabs */}
      <div className="bg-white border-b border-slate-200 sticky top-[73px] z-10 shadow-sm">
        <div className="max-w-6xl mx-auto flex gap-8 px-4 md:px-8">
            <button 
              onClick={() => setActiveTab('monitor')}
              className={`py-4 text-sm font-bold flex items-center gap-2 border-b-2 transition-all ${activeTab === 'monitor' ? 'border-blue-600 text-blue-600' : 'border-transparent text-slate-500 hover:text-slate-800'}`}
            >
              <ShieldAlert className="w-4 h-4" />
              Monitor Dashboard
            </button>
            <button 
              onClick={() => setActiveTab('config')}
              className={`py-4 text-sm font-bold flex items-center gap-2 border-b-2 transition-all ${activeTab === 'config' ? 'border-blue-600 text-blue-600' : 'border-transparent text-slate-500 hover:text-slate-800'}`}
            >
              <Settings className="w-4 h-4" />
              Configuration
            </button>
        </div>
      </div>

      <main className="max-w-6xl mx-auto p-4 md:p-8 w-full flex-grow">
        
        {/* === MONITOR TAB === */}
        {activeTab === 'monitor' && (
          <div className="space-y-8">
            {/* Intro / Empty State */}
            {!reportData && !loading && !error && (
              <div className="text-center py-20 px-4">
                <div className="bg-white rounded-2xl p-10 max-w-2xl mx-auto shadow-sm border border-slate-200">
                  <div className="flex justify-center mb-6">
                    <div className="bg-blue-50 p-4 rounded-full">
                       <TrendingUp className="w-12 h-12 text-blue-400" />
                    </div>
                  </div>
                  <h2 className="text-2xl font-bold text-slate-900 mb-3">Ready to scan the landscape?</h2>
                  <p className="text-slate-500 mb-8 leading-relaxed">
                    This tool uses AI to search for recent updates ({timeRange}) from your configured competitors.
                    <br/>
                    Current Targets: <span className="font-semibold text-slate-700">Toast, Square, Clover, DoorDash...</span>
                  </p>
                  
                  <button 
                    onClick={() => setActiveTab('config')}
                    className="text-sm text-blue-600 hover:text-blue-800 flex items-center justify-center gap-1 font-bold mx-auto border border-blue-100 bg-blue-50 px-4 py-2 rounded-full transition-colors hover:bg-blue-100"
                  >
                    <Settings className="w-4 h-4"/>
                    Customize Targets & Branding
                  </button>
                </div>
              </div>
            )}

            {/* Loading State */}
            {loading && (
              <div className="flex flex-col items-center justify-center py-32 space-y-6">
                <div className="relative">
                  <div className="w-16 h-16 border-4 border-slate-200 border-t-blue-600 rounded-full animate-spin"></div>
                  <div className="absolute inset-0 flex items-center justify-center">
                    <Search className="w-6 h-6 text-blue-600" />
                  </div>
                </div>
                <p className="text-slate-500 font-medium animate-pulse">Scanning official sources for the <strong>{timeRange}</strong>...</p>
              </div>
            )}

            {/* Error State */}
            {error && (
              <div className="bg-red-50 border-l-4 border-red-500 p-6 rounded-lg shadow-sm my-8 flex items-start gap-4">
                <div className="bg-red-100 p-2 rounded-full">
                  <AlertTriangle className="text-red-600 w-6 h-6 flex-shrink-0" />
                </div>
                <div>
                  <h3 className="font-bold text-red-800 text-lg">Scan Failed</h3>
                  <p className="text-red-700 mt-1">{error}</p>
                </div>
              </div>
            )}

            {/* Report Display */}
            {reportData && (
              <div className="animate-fade-in-up space-y-8">
                
                {/* 1. Header Section */}
                <div className="flex flex-col md:flex-row justify-between items-start md:items-center gap-4 border-b border-slate-200 pb-6">
                  <div>
                    <h2 className="text-3xl font-bold text-slate-900 flex items-center gap-3">
                      {getReportTitle(timeRange)}
                      <span className="text-lg font-normal text-slate-400 bg-slate-100 px-3 py-1 rounded-full">{reportData.date}</span>
                    </h2>
                    <p className="text-slate-500 mt-2 flex items-center gap-2">
                        <Clock className="w-4 h-4" />
                        Strategic intelligence for: <span className="font-semibold text-slate-700">{timeRange}</span>
                    </p>
                  </div>
                  <button 
                    onClick={copyToClipboard}
                    className="flex items-center gap-2 text-sm font-semibold text-slate-600 hover:text-blue-600 transition-colors bg-white px-4 py-2 rounded-lg border border-slate-200 shadow-sm hover:shadow"
                  >
                    {copied ? <Check className="w-4 h-4 text-emerald-500" /> : <Copy className="w-4 h-4" />}
                    {copied ? "Copied Summary" : "Copy Summary"}
                  </button>
                </div>

                {/* 2. Market Signals Grid */}
                <div>
                   <h3 className="text-lg font-bold text-slate-800 mb-4 flex items-center gap-2">
                     <ShieldAlert className="w-5 h-5 text-blue-600"/> 
                     Market Signals (The Watch List)
                   </h3>
                   <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                     {reportData.signals && reportData.signals.length > 0 ? (
                       reportData.signals.map((signal, idx) => {
                         const style = getCategoryStyle(signal.category);
                         return (
                           <div key={idx} className="bg-white rounded-xl p-5 border border-slate-200 shadow-sm hover:shadow-md transition-shadow flex flex-col h-full">
                             <div className="flex justify-between items-start mb-3">
                               <h4 className="font-bold text-slate-900 text-lg">{signal.competitor}</h4>
                               <span className={`text-[10px] uppercase font-bold px-2 py-1 rounded-full flex items-center gap-1 ${style.bg} ${style.text}`}>
                                 {style.icon} {signal.category}
                               </span>
                             </div>
                             <p className="text-slate-600 text-sm leading-relaxed mb-4 flex-grow">
                               {signal.update}
                             </p>
                             {signal.source_url && (
                               <a 
                                 href={signal.source_url} 
                                 target="_blank" 
                                 rel="noreferrer"
                                 className="text-xs font-medium text-blue-500 hover:text-blue-700 flex items-center gap-1 mt-auto pt-3 border-t border-slate-50"
                               >
                                 <Globe className="w-3 h-3" />
                                 {signal.source_name || 'View Official Source'}
                               </a>
                             )}
                           </div>
                         );
                       })
                     ) : (
                       <div className="col-span-full text-center text-slate-500 py-8 bg-slate-50 rounded-lg border border-dashed border-slate-300">
                         No significant market signals found for the {timeRange}.
                       </div>
                     )}
                   </div>
                </div>

                {/* 3. Stress Test Table */}
                {reportData.stressTest && reportData.stressTest.length > 0 && (
                  <div className="bg-white rounded-xl border border-slate-200 shadow-sm overflow-hidden">
                    <div className="bg-slate-50 px-6 py-4 border-b border-slate-200">
                      <h3 className="text-lg font-bold text-slate-800 flex items-center gap-2">
                        <Zap className="w-5 h-5 text-amber-500"/>
                        The "INFI Difference" Stress Test
                      </h3>
                    </div>
                    <div className="overflow-x-auto">
                      <table className="w-full text-sm text-left">
                        <thead className="text-xs text-slate-500 uppercase bg-slate-50 border-b border-slate-200">
                          <tr>
                            <th className="px-6 py-3 w-1/3">Competitor Update</th>
                            <th className="px-6 py-3 w-1/3 text-red-600">Threat to INFI</th>
                            <th className="px-6 py-3 w-1/3 text-emerald-600">Counter / Action</th>
                          </tr>
                        </thead>
                        <tbody className="divide-y divide-slate-100">
                          {reportData.stressTest.map((item, idx) => (
                            <tr key={idx} className="hover:bg-slate-50/50">
                              <td className="px-6 py-4 font-medium text-slate-900">{item.update}</td>
                              <td className="px-6 py-4 text-slate-600">{item.threat}</td>
                              <td className="px-6 py-4 text-slate-600 bg-emerald-50/30">{item.counter}</td>
                            </tr>
                          ))}
                        </tbody>
                      </table>
                    </div>
                  </div>
                )}

                {/* 4. Strategic Actions */}
                {reportData.actions && (
                  <div>
                     <h3 className="text-lg font-bold text-slate-800 mb-4 flex items-center gap-2">
                       <Target className="w-5 h-5 text-emerald-600"/> 
                       Strategic Action Plan
                     </h3>
                     <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
                        {/* Sales */}
                        <div className="bg-gradient-to-b from-blue-50 to-white rounded-xl p-6 border border-blue-100 shadow-sm relative overflow-hidden">
                          <div className="absolute top-0 left-0 w-1 h-full bg-blue-500"></div>
                          <h4 className="font-bold text-blue-900 mb-3 flex items-center gap-2">
                            <TrendingUp className="w-4 h-4" /> Sales
                          </h4>
                          <p className="text-sm text-slate-700 leading-relaxed">{reportData.actions.sales || "No specific sales actions identified."}</p>
                        </div>

                        {/* Product */}
                        <div className="bg-gradient-to-b from-purple-50 to-white rounded-xl p-6 border border-purple-100 shadow-sm relative overflow-hidden">
                           <div className="absolute top-0 left-0 w-1 h-full bg-purple-500"></div>
                          <h4 className="font-bold text-purple-900 mb-3 flex items-center gap-2">
                            <LayoutTemplate className="w-4 h-4" /> Product
                          </h4>
                          <p className="text-sm text-slate-700 leading-relaxed">{reportData.actions.product || "No specific product actions identified."}</p>
                        </div>

                        {/* Marketing */}
                        <div className="bg-gradient-to-b from-amber-50 to-white rounded-xl p-6 border border-amber-100 shadow-sm relative overflow-hidden">
                           <div className="absolute top-0 left-0 w-1 h-full bg-amber-500"></div>
                          <h4 className="font-bold text-amber-900 mb-3 flex items-center gap-2">
                            <Megaphone className="w-4 h-4" /> Marketing
                          </h4>
                          <p className="text-sm text-slate-700 leading-relaxed">{reportData.actions.marketing || "No specific marketing actions identified."}</p>
                        </div>
                     </div>
                  </div>
                )}

              </div>
            )}
          </div>
        )}

        {/* === CONFIG TAB === */}
        {activeTab === 'config' && (
          <div className="max-w-4xl mx-auto animate-fade-in">
             <div className="flex justify-between items-end mb-6">
                <div>
                  <h2 className="text-2xl font-bold text-slate-800">Configuration</h2>
                  <p className="text-slate-500 text-sm mt-1">Customize the AI's context and search targets.</p>
                </div>
                <button 
                  onClick={handleResetConfig}
                  className="text-xs text-red-500 hover:text-red-700 font-medium bg-red-50 px-3 py-1 rounded-full"
                >
                  Reset All to Defaults
                </button>
             </div>

             <div className="grid gap-8">
                {/* Section 1: INFI Branding */}
                <div className="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                  <div className="flex items-center gap-3 mb-4">
                    <div className="bg-blue-100 p-2 rounded-lg text-blue-600">
                      <LayoutTemplate className="w-5 h-5" />
                    </div>
                    <h3 className="text-lg font-bold text-slate-800">INFI Brand & Products</h3>
                  </div>
                  <p className="text-sm text-slate-500 mb-3">Define your company profile. The AI uses this to understand "who" it is acting as.</p>
                  <textarea 
                    className="w-full h-40 p-4 text-sm border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 font-mono bg-slate-50 leading-relaxed"
                    value={infiProfile}
                    onChange={(e) => setInfiProfile(e.target.value)}
                  />
                </div>

                {/* Section 2: Competitors */}
                <div className="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                   <div className="flex items-center gap-3 mb-4">
                    <div className="bg-emerald-100 p-2 rounded-lg text-emerald-600">
                      <ShieldAlert className="w-5 h-5" />
                    </div>
                    <h3 className="text-lg font-bold text-slate-800">Competitor Watchlist</h3>
                  </div>
                  <p className="text-sm text-slate-500 mb-3">List the specific competitors you want the AI to search for.</p>
                  <textarea 
                    className="w-full h-32 p-4 text-sm border border-slate-300 rounded-lg focus:ring-2 focus:ring-emerald-500 focus:border-emerald-500 font-mono bg-slate-50 leading-relaxed"
                    value={competitors}
                    onChange={(e) => setCompetitors(e.target.value)}
                  />
                </div>

                {/* Section 3: Focus Areas */}
                <div className="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                   <div className="flex items-center gap-3 mb-4">
                    <div className="bg-purple-100 p-2 rounded-lg text-purple-600">
                      <Search className="w-5 h-5" />
                    </div>
                    <h3 className="text-lg font-bold text-slate-800">Search Focus Areas</h3>
                  </div>
                  <p className="text-sm text-slate-500 mb-3">What topics matter this week?</p>
                  <textarea 
                    className="w-full h-24 p-4 text-sm border border-slate-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-purple-500 font-mono bg-slate-50 leading-relaxed"
                    value={focusAreas}
                    onChange={(e) => setFocusAreas(e.target.value)}
                  />
                </div>

                {/* Section 4: Advanced Prompt Config */}
                <div className="bg-slate-50 p-6 rounded-xl border border-slate-300 shadow-inner">
                   <div className="flex items-center justify-between mb-4">
                    <div className="flex items-center gap-3">
                      <div className="bg-slate-200 p-2 rounded-lg text-slate-600">
                        <Code className="w-5 h-5" />
                      </div>
                      <div>
                        <h3 className="text-lg font-bold text-slate-800">AI Prompt Configuration</h3>
                        <p className="text-xs text-slate-500">Advanced: Edit the raw instructions sent to Gemini.</p>
                      </div>
                    </div>
                    <button 
                      onClick={handleResetPrompt}
                      className="text-xs flex items-center gap-1 text-slate-500 hover:text-slate-800 bg-white border border-slate-300 px-3 py-1 rounded"
                    >
                      <RotateCcw className="w-3 h-3" /> Reset Prompt
                    </button>
                  </div>
                  
                  <div className="mb-3 text-xs text-slate-500 bg-blue-50 p-3 rounded border border-blue-100">
                    <strong>Tip:</strong> Use the placeholders <code>{'{{COMPETITORS}}'}</code>, <code>{'{{FOCUS_AREAS}}'}</code>, and <code>{'{{TIME_RANGE_QUERY}}'}</code> to keep the prompt dynamic.
                  </div>

                  <textarea 
                    className="w-full h-64 p-4 text-xs border border-slate-300 rounded-lg focus:ring-2 focus:ring-slate-500 focus:border-slate-500 font-mono bg-white leading-relaxed"
                    value={promptTemplate}
                    onChange={(e) => setPromptTemplate(e.target.value)}
                  />
                </div>

                <div className="flex justify-end pt-4 pb-12">
                   <button 
                    onClick={() => { setActiveTab('monitor'); }}
                    className="bg-blue-600 hover:bg-blue-700 text-white px-8 py-3 rounded-xl font-bold flex items-center gap-2 shadow-lg hover:shadow-xl transition-all transform hover:-translate-y-0.5"
                   >
                     <Save className="w-4 h-4" />
                     Save Configuration
                   </button>
                </div>
             </div>
          </div>
        )}

      </main>
    </div>
  );
};

export default App;
