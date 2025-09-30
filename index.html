import React, { useState, useEffect, useCallback, useMemo } from 'react';
// Plotly.js library for high-quality, interactive visualizations
// NOTE: In a real project, Plotly would be installed, but here we use the CDN equivalent library 'react-plotly.js'
import Plot from 'react-plotly.js'; 

// Load Lucide Icons for aesthetic UI elements
const UploadIcon = (props) => (<svg {...props} fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-8l-4-4m0 0L8 8m4-4v12"></path></svg>);
const TrendIcon = (props) => (<svg {...props} fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M13 7h8m0 0v8m0-8L8 21"></path></svg>);
const ReportIcon = (props) => (<svg {...props} fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path></svg>);

// --- 1. Mock Data and Constants ---

// Mock data representing HMPI results for a single location
const initialHMPIResults = {
  location: "Bokaro Sampling Point A",
  overall_hmpi: 78.5,
  pollution_level: "Moderate Risk",
  date: "2025-09-30",
  standard: "WHO 2024",
  metal_contributions: [
    { metal: 'Arsenic (As)', concentration: 0.012, limit: 0.01, contribution_index: 25 },
    { metal: 'Cadmium (Cd)', concentration: 0.005, limit: 0.003, contribution_index: 30 },
    { metal: 'Lead (Pb)', concentration: 0.008, limit: 0.015, contribution_index: 15 },
    { metal: 'Chromium (Cr)', concentration: 0.025, limit: 0.05, contribution_index: 8 },
  ],
};

// Mock data for the GIS Hotspot Map (Simplified Lat/Lon for illustration)
const mockGISData = [
  { id: 1, lat: 23.67, lon: 86.15, hmpi: 125, name: 'Site A (High)', level: 'High Risk' },
  { id: 2, lat: 23.63, lon: 86.12, hmpi: 45, name: 'Site B (Safe)', level: 'Safe' },
  { id: 3, lat: 23.69, lon: 86.19, hmpi: 88, name: 'Site C (Moderate)', level: 'Moderate Risk' },
  { id: 4, lat: 23.71, lon: 86.08, hmpi: 60, name: 'Site D (Moderate)', level: 'Moderate Risk' },
  { id: 5, lat: 23.60, lon: 86.25, hmpi: 25, name: 'Site E (Very Safe)', level: 'Safe' },
];

const getLevelColor = (level, isBg = true) => {
  if (isBg) {
    switch (level) {
      case 'Safe': return 'bg-green-500';
      case 'Moderate Risk': return 'bg-yellow-500';
      case 'High Risk': return 'bg-red-500';
      default: return 'bg-gray-400';
    }
  } else {
     switch (level) {
      case 'Safe': return 'text-green-600';
      case 'Moderate Risk': return 'text-yellow-600';
      case 'High Risk': return 'text-red-600';
      default: return 'text-gray-600';
    }
  }
};

const getMapColor = (level) => {
    switch (level) {
        case 'Safe': return 'rgb(34, 197, 94)'; 
        case 'Moderate Risk': return 'rgb(234, 179, 8)'; 
        case 'High Risk': return 'rgb(239, 68, 68)'; 
        default: return 'rgb(107, 114, 128)'; 
    }
};

// --- 2. Simulated Backend / Service Functions ---

/**
 * @description Simulates the FastAPI /upload endpoint logic.
 */
const simulateDataUpload = (data) => {
    console.log("Simulating API call: /upload", data);
    return new Promise(resolve => {
        setTimeout(() => {
            const success = Math.random() > 0.1; // 90% success rate
            if (success) {
                resolve({ status: 'success', message: `Successfully uploaded ${data.length} readings. Processing HMPI now...` });
            } else {
                resolve({ status: 'error', message: 'Input validation failed on server for some readings.' });
            }
        }, 1500);
    });
};

/**
 * @description Simulates the FastAPI /ml/predict endpoint logic.
 * The prediction is based on the current overall HMPI score.
 */
const simulateMLPrediction = (currentHMPI) => {
    console.log("Simulating ML prediction for HMPI:", currentHMPI);
    return new Promise(resolve => {
        setTimeout(() => {
            // Trend logic: +0% to +10% of current HMPI as predicted score
            const trendFactor = 1 + (Math.random() * 0.1); 
            const predictedHMPI = (currentHMPI * trendFactor).toFixed(1);
            
            let trendMessage = "";
            let level = "";
            if (predictedHMPI > currentHMPI * 1.05) {
                trendMessage = "Significant upward trend predicted, requiring immediate intervention.";
                level = "High Risk";
            } else if (predictedHMPI > currentHMPI) {
                trendMessage = "Slight upward trend expected. Monitor closely.";
                level = "Moderate Risk";
            } else {
                trendMessage = "Stable or declining trend expected. Continued monitoring advised.";
                level = "Safe";
            }

            resolve({ 
                status: 'success', 
                predicted_hmpi: parseFloat(predictedHMPI), 
                trend: trendMessage,
                level: level,
                current_hmpi: currentHMPI
            });
        }, 2000);
    });
};

// --- 3. Core Components ---

const LoadingSpinner = () => (
    <div className="flex items-center justify-center p-4">
        <svg className="animate-spin -ml-1 mr-3 h-5 w-5 text-blue-600" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
            <circle className="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" strokeWidth="4"></circle>
            <path className="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
        </svg>
        Processing...
    </div>
);

// --- 4. Main Application Component ---

const App = () => {
  const [reportData, setReportData] = useState(initialHMPIResults);
  const [activeTab, setActiveTab] = useState('dashboard');
  const [uploadStatus, setUploadStatus] = useState({ loading: false, message: '', type: '' });
  const [mlPrediction, setMlPrediction] = useState({ loading: false, result: null });
  const [dataInputs, setDataInputs] = useState([{ metal: 'Arsenic (As)', concentration: '0.012', unit: 'mg/L' }]);

  // --- Data Upload Handlers ---
  const handleAddInput = () => {
    setDataInputs([...dataInputs, { metal: '', concentration: '', unit: 'mg/L' }]);
  };

  const handleInputChange = (index, field, value) => {
    const newInputs = [...dataInputs];
    newInputs[index][field] = value;
    setDataInputs(newInputs);
  };

  const handleUploadSubmit = async (e) => {
    e.preventDefault();
    setUploadStatus({ loading: true, message: 'Validating and uploading data to MongoDB...', type: 'info' });

    // Format data for simulated API call
    const formattedData = dataInputs.map((input, index) => ({
      location_tag: `UPLOAD-${Date.now()}`,
      timestamp: new Date().toISOString(),
      metal_name: input.metal || `Unknown Metal ${index + 1}`,
      concentration: parseFloat(input.concentration) || 0,
      unit: input.unit,
      sampler_id: 'USER_APP',
    }));

    const result = await simulateDataUpload(formattedData);
    
    if (result.status === 'success') {
        setUploadStatus({ loading: false, message: result.message, type: 'success' });
        // Optionally update the dashboard data with the new results (simulated)
        setReportData(prev => ({
            ...prev,
            overall_hmpi: 78.5 + (Math.random() * 10), // Simulate new HMPI score
            date: new Date().toLocaleDateString(),
        }));
    } else {
        setUploadStatus({ loading: false, message: result.message, type: 'error' });
    }
  };

  // --- ML Prediction Handler ---
  const handlePredictTrend = async () => {
    setMlPrediction({ loading: true, result: null });
    const result = await simulateMLPrediction(reportData.overall_hmpi);
    setMlPrediction({ loading: false, result });
  };
  
  // --- Visualization Logic: HMPI Breakdown Chart ---
  const renderHMPIChart = useMemo(() => {
    const metals = reportData.metal_contributions.map(m => m.metal);
    const contributions = reportData.metal_contributions.map(m => m.contribution_index);
    const limits = reportData.metal_contributions.map(m => m.limit);
    const concentrations = reportData.metal_contributions.map(m => m.concentration);
    
    const hoverTexts = metals.map((m, i) => 
        `Metal: ${m}<br>Measured: ${concentrations[i]} mg/L<br>Limit: ${limits[i]} mg/L<br>Contribution to HMPI: ${contributions[i].toFixed(1)}`
    );

    const data = [
      {
        x: metals,
        y: contributions,
        type: 'bar',
        marker: { color: 'rgb(37, 99, 235)' }, 
        name: 'Pollution Sub-Index',
        hoverinfo: 'text',
        text: hoverTexts,
      },
    ];

    const layout = {
      title: `<span style="font-weight: 600;">Metal Contribution to HMPI (${reportData.standard})</span>`,
      font: { family: 'Inter, sans-serif' },
      xaxis: { title: 'Heavy Metal', tickangle: -20 },
      yaxis: { title: 'Pollution Sub-Index Value (Q_i)', zeroline: true },
      margin: { l: 60, r: 20, t: 70, b: 100 },
      responsive: true,
      paper_bgcolor: 'transparent',
      plot_bgcolor: 'transparent',
    };

    return (
      <Plot
        data={data}
        layout={layout}
        config={{ displayModeBar: false, responsive: true }}
        style={{ width: '100%', minHeight: '350px' }}
      />
    );
  }, [reportData]);

  // --- Visualization Logic: GIS Hotspot Map ---
  const renderGISMap = useMemo(() => {
    const data = [
      {
        type: 'scattergeo',
        locationmode: 'geojson-id',
        mode: 'markers',
        lat: mockGISData.map(d => d.lat),
        lon: mockGISData.map(d => d.lon),
        text: mockGISData.map(d => `${d.name}<br>HMPI: ${d.hmpi}<br>Level: ${d.level}`),
        marker: {
          size: mockGISData.map(d => 10 + d.hmpi / 5), // Size for visibility
          color: mockGISData.map(d => getMapColor(d.level)),
          line: { color: 'black', width: 1 },
          opacity: 0.8
        },
        name: 'Sampling Sites',
        hoverinfo: 'text',
      },
    ];

    const layout = {
      title: `<span style="font-weight: 600;">Regional Pollution Hotspots</span>`,
      font: { family: 'Inter, sans-serif' },
      geo: {
        scope: 'asia', 
        center: { lat: 23.65, lon: 86.15 }, 
        projection: { type: 'mercator' },
        showland: true,
        landcolor: 'rgb(243, 244, 246)', 
        subunitcolor: 'rgb(204, 204, 204)',
        countrycolor: 'rgb(204, 204, 204)',
        showsubunits: true,
        showcountries: true,
        lakecolor: 'rgb(180, 200, 255)',
      },
      margin: { r: 0, t: 50, b: 0, l: 0 },
      responsive: true,
      paper_bgcolor: 'transparent',
      plot_bgcolor: 'transparent',
    };

    return (
      <Plot
        data={data}
        layout={layout}
        config={{ displayModeBar: false, responsive: true }}
        style={{ width: '100%', minHeight: '400px' }}
      />
    );
  }, []);
  
  // --- UI Layout and Content ---

  const renderContent = () => {
    switch (activeTab) {
      case 'upload':
        return (
          <div className="bg-white p-6 md:p-8 rounded-xl shadow-xl border border-gray-100">
            <h2 className="text-2xl font-bold text-gray-800 mb-6">💧 Data Ingestion Portal</h2>
            <form onSubmit={handleUploadSubmit} className="space-y-4">
              {dataInputs.map((input, index) => (
                <div key={index} className="grid grid-cols-1 md:grid-cols-4 gap-4 p-4 border rounded-lg bg-gray-50">
                  <select
                    className="col-span-1 p-2 border rounded-md focus:ring-blue-500 focus:border-blue-500"
                    value={input.metal}
                    onChange={(e) => handleInputChange(index, 'metal', e.target.value)}
                    required
                  >
                    <option value="">-- Select Metal --</option>
                    {['Arsenic (As)', 'Lead (Pb)', 'Cadmium (Cd)', 'Chromium (Cr)', 'Mercury (Hg)', 'Copper (Cu)'].map(m => (
                        <option key={m} value={m}>{m}</option>
                    ))}
                  </select>
                  <input
                    type="number"
                    step="0.0001"
                    className="col-span-2 p-2 border rounded-md focus:ring-blue-500 focus:border-blue-500"
                    placeholder="Concentration Value (e.g., 0.012)"
                    value={input.concentration}
                    onChange={(e) => handleInputChange(index, 'concentration', e.target.value)}
                    required
                  />
                   <select
                    className="col-span-1 p-2 border rounded-md focus:ring-blue-500 focus:border-blue-500"
                    value={input.unit}
                    onChange={(e) => handleInputChange(index, 'unit', e.target.value)}
                    required
                  >
                    <option value="mg/L">mg/L</option>
                    <option value="ppm">ppm</option>
                    <option value="ppb">ppb</option>
                  </select>
                </div>
              ))}
              
              <div className="flex justify-between items-center pt-4">
                <button
                  type="button"
                  onClick={handleAddInput}
                  className="px-4 py-2 text-sm text-blue-600 border border-blue-600 rounded-lg hover:bg-blue-50 transition duration-150"
                >
                  + Add Metal Reading
                </button>
                <button
                  type="submit"
                  disabled={uploadStatus.loading}
                  className="flex items-center px-6 py-3 bg-blue-600 text-white font-semibold rounded-xl shadow-md hover:bg-blue-700 disabled:opacity-50 transition duration-200"
                >
                  {uploadStatus.loading ? <LoadingSpinner /> : (
                      <>
                        <UploadIcon className="w-5 h-5 mr-2" />
                        Upload & Compute HMPI
                      </>
                  )}
                </button>
              </div>
              
              {uploadStatus.message && (
                <div className={`mt-4 p-4 rounded-lg text-sm ${
                    uploadStatus.type === 'success' ? 'bg-green-100 text-green-700' : 'bg-red-100 text-red-700'
                }`}>
                  {uploadStatus.message}
                </div>
              )}
            </form>
          </div>
        );
      
      case 'ml_prediction':
        return (
          <div className="bg-white p-6 md:p-8 rounded-xl shadow-xl border border-gray-100">
            <h2 className="text-2xl font-bold text-gray-800 mb-6">🤖 Predictive HMPI Trend Analysis</h2>
            
            <div className="p-5 border border-blue-200 rounded-lg bg-blue-50 mb-6 flex justify-between items-center">
                <p className="text-lg font-medium text-gray-700">Current HMPI Score: <span className="font-extrabold text-blue-600 text-2xl">{reportData.overall_hmpi.toFixed(1)}</span></p>
                <button 
                    onClick={handlePredictTrend}
                    disabled={mlPrediction.loading}
                    className="flex items-center px-6 py-3 bg-purple-600 text-white font-semibold rounded-xl shadow-md hover:bg-purple-700 disabled:opacity-50 transition duration-200"
                >
                    {mlPrediction.loading ? <LoadingSpinner /> : (
                        <>
                            <TrendIcon className="w-5 h-5 mr-2" />
                            Run Prediction (Next Month)
                        </>
                    )}
                </button>
            </div>
            
            {mlPrediction.result && (
                <div className={`p-6 rounded-xl border-2 ${mlPrediction.result.level === 'High Risk' ? 'border-red-400 bg-red-50' : mlPrediction.result.level === 'Safe' ? 'border-green-400 bg-green-50' : 'border-yellow-400 bg-yellow-50'}`}>
                    <h3 className="text-xl font-bold mb-2 flex items-center">
                        <span className={`w-3 h-3 rounded-full mr-3 ${getLevelColor(mlPrediction.result.level)}`}></span>
                        Predicted HMPI: {mlPrediction.result.predicted_hmpi}
                    </h3>
                    <p className={`text-gray-700 text-md`}>
                        <span className="font-semibold">Trend Analysis:</span> {mlPrediction.result.trend}
                    </p>
                    <p className="mt-3 text-sm text-gray-500">
                        The current score was {mlPrediction.result.current_hmpi.toFixed(1)}. The model forecasts a shift to this new level based on historical data and environmental factors.
                    </p>
                </div>
            )}

            {!mlPrediction.loading && !mlPrediction.result && (
                <div className="p-6 text-center text-gray-500 bg-gray-100 rounded-lg">
                    Click "Run Prediction" to forecast the HMPI score for the next 30 days.
                </div>
            )}
          </div>
        );

      case 'reports':
        return (
            <div className="bg-white p-6 md:p-8 rounded-xl shadow-xl border border-gray-100">
                <h2 className="text-2xl font-bold text-gray-800 mb-6">📄 Generate Detailed Reports</h2>
                <div className="space-y-4">
                    <p className="text-gray-600">
                        Generate comprehensive PDF or Excel reports containing historical HMPI data, raw concentration values, and GIS maps for selected locations and time ranges.
                    </p>
                    
                    <div className="grid grid-cols-1 sm:grid-cols-2 gap-4">
                        <div>
                            <label className="block text-sm font-medium text-gray-700">Start Date</label>
                            <input type="date" className="mt-1 p-2 w-full border rounded-md focus:ring-blue-500 focus:border-blue-500" />
                        </div>
                        <div>
                            <label className="block text-sm font-medium text-gray-700">End Date</label>
                            <input type="date" className="mt-1 p-2 w-full border rounded-md focus:ring-blue-500 focus:border-blue-500" />
                        </div>
                    </div>
                    
                    <div className="pt-4">
                        <button className="flex items-center px-6 py-3 bg-indigo-600 text-white font-semibold rounded-xl shadow-md hover:bg-indigo-700 transition duration-200">
                            <ReportIcon className="w-5 h-5 mr-2" />
                            Generate PDF Report
                        </button>
                        <p className="text-sm text-gray-500 mt-2">
                            (Simulation: This triggers the FastAPI `/reports/generate` endpoint in the full-stack version.)
                        </p>
                    </div>
                </div>
            </div>
        );

      case 'dashboard':
      default:
        // Dashboard View
        return (
          <>
            {/* Summary Card */}
            <div className="grid grid-cols-1 lg:grid-cols-3 gap-6 mb-8">
              <div className={`col-span-1 p-6 rounded-xl shadow-xl transition duration-300 ${getLevelColor(reportData.pollution_level)} bg-opacity-95 text-white`}>
                <p className="text-sm font-medium mb-1 uppercase tracking-wider">Overall HMPI Score ({reportData.standard})</p>
                <h2 className="text-6xl font-extrabold">{reportData.overall_hmpi.toFixed(1)}</h2>
                <p className="text-xl font-semibold mt-2">
                  {reportData.pollution_level}
                </p>
                <div className="flex items-center justify-between mt-4 border-t border-white border-opacity-30 pt-3">
                  <span className="text-xs font-light">Location: {reportData.location}</span>
                  <span className="text-xs font-light">Last Update: {reportData.date}</span>
                </div>
              </div>
              
              {/* KPIs / Quick Stats */}
              <div className="col-span-2 grid grid-cols-1 sm:grid-cols-2 gap-4">
                <div className="bg-white p-6 rounded-xl shadow-lg border border-gray-100">
                    <p className="text-sm font-medium text-gray-500">Critical Metals Exceeded</p>
                    <p className="text-4xl font-bold text-red-600 mt-1">
                        {reportData.metal_contributions.filter(m => m.concentration > m.limit).length}
                    </p>
                    <p className="text-xs text-gray-500 mt-2">Metals exceeding permissible limits (WHO).</p>
                </div>
                <div className="bg-white p-6 rounded-xl shadow-lg border border-gray-100">
                    <p className="text-sm font-medium text-gray-500">Predicted Trend</p>
                    <p className="text-4xl font-bold text-purple-600 mt-1">
                        {mlPrediction.result ? mlPrediction.result.predicted_hmpi : 'N/A'}
                    </p>
                    <p className="text-xs text-gray-500 mt-2">Forecast for next month's HMPI score.</p>
                </div>
              </div>
            </div>

            {/* Visualization Section */}
            <div className="grid grid-cols-1 lg:grid-cols-2 gap-6">
              {/* HMPI Breakdown Chart */}
              <div className="bg-white p-4 sm:p-6 rounded-xl shadow-lg border border-gray-100">
                {renderHMPIChart}
              </div>

              {/* GIS Hotspot Map */}
              <div className="bg-white p-4 sm:p-6 rounded-xl shadow-lg border border-gray-100">
                {renderGISMap}
              </div>
            </div>
            
            {/* Data Table */}
            <div className="bg-white p-4 sm:p-6 rounded-xl shadow-lg border border-gray-100 mt-6">
              <h3 className="text-xl font-semibold text-gray-700 mb-4">Raw Metal Concentration Data</h3>
              <div className="overflow-x-auto">
                  <table className="min-w-full divide-y divide-gray-200">
                      <thead className="bg-gray-50">
                          <tr>
                              <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Metal</th>
                              <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Concentration (mg/L)</th>
                              <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Permissible Limit</th>
                              <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Sub-Index (Q_i)</th>
                          </tr>
                      </thead>
                      <tbody className="bg-white divide-y divide-gray-200">
                          {reportData.metal_contributions.map((metal, index) => (
                              <tr key={index} className={metal.concentration > metal.limit ? 'bg-red-50' : 'hover:bg-gray-50'}>
                                  <td className="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">{metal.metal}</td>
                                  <td className="px-6 py-4 whitespace-nowrap text-sm text-gray-500">{metal.concentration.toFixed(4)}</td>
                                  <td className="px-6 py-4 whitespace-nowrap text-sm text-gray-500">{metal.limit.toFixed(4)}</td>
                                  <td className="px-6 py-4 whitespace-nowrap text-sm font-semibold">
                                      {metal.contribution_index.toFixed(2)}
                                      {metal.concentration > metal.limit && <span className="ml-2 text-red-600 text-xs"> (Exceeded)</span>}
                                  </td>
                              </tr>
                          ))}
                      </tbody>
                  </table>
              </div>
            </div>
          </>
        );
    }
  };

  const navItems = [
    { id: 'dashboard', label: 'Dashboard', icon: (props) => (<svg {...props} fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M3 10h18M3 14h18m-9-4v8m-9-4h18m-9-4v8m-9-4h18m-9-4v8"></path></svg>) },
    { id: 'upload', label: 'Data Upload', icon: UploadIcon },
    { id: 'ml_prediction', label: 'ML Prediction', icon: TrendIcon },
    { id: 'reports', label: 'Reports', icon: ReportIcon },
  ];

  return (
    <div className="min-h-screen bg-gray-50 p-4 sm:p-8 font-['Inter']">
      {/* Header and Navigation */}
      <header className="mb-8 pb-4">
        <h1 className="text-4xl font-extrabold text-gray-900 mb-1 flex items-center">
            <span className="text-blue-600 mr-2">💧</span> AquaSafe
        </h1>
        <p className="text-gray-500">Automated Heavy Metal Pollution Index Monitoring System</p>
      </header>
      
      {/* Tab Navigation */}
      <nav className="mb-8 border-b border-gray-200">
        <ul className="flex flex-wrap -mb-px">
          {navItems.map((item) => {
            const isActive = activeTab === item.id;
            return (
              <li key={item.id} className="mr-2">
                <button
                  onClick={() => setActiveTab(item.id)}
                  className={`inline-flex items-center justify-center p-4 border-b-2 font-medium text-sm rounded-t-lg transition duration-200 
                    ${isActive ? 'text-blue-600 border-blue-600' : 'text-gray-500 border-transparent hover:text-gray-700 hover:border-gray-300'}`
                  }
                >
                  <item.icon className="w-5 h-5 mr-2" />
                  {item.label}
                </button>
              </li>
            );
          })}
        </ul>
      </nav>

      {/* Main Content Area */}
      {renderContent()}

    </div>
  );
};

export default App;
