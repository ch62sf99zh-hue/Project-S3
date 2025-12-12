# Project-S3
Clarity Map

import React, { useState } from 'react';
import { 
  Leaf, 
  MapPin, 
  Home, 
  Target, 
  LayoutDashboard, 
  Users, 
  TrendingDown,
  Award,
  AlertCircle,
  CheckCircle,
  AlertTriangle,
  Bell,
  User,
  Filter,
  ZoomIn,
  ZoomOut
} from 'lucide-react';

// Mock pollution zones data with positions on the map image
const pollutionZones = [
  { id: 1, name: 'Republic Square', severity: 'medium', top: 52, left: 48, reward: 35, color: '#eab308' },
  { id: 2, name: 'Hrazdan Gorge', severity: 'high', top: 45, left: 35, reward: 55, color: '#ef4444' },
  { id: 3, name: 'Northern Avenue', severity: 'low', top: 50, left: 50, reward: 20, color: '#22c55e' },
  { id: 4, name: 'Cascade Complex', severity: 'low', top: 42, left: 52, reward: 15, color: '#22c55e' },
  { id: 5, name: 'Vernissage Market', severity: 'high', top: 54, left: 45, reward: 50, color: '#ef4444' },
  { id: 6, name: 'Erebuni District', severity: 'high', top: 70, left: 55, reward: 60, color: '#ef4444' },
  { id: 7, name: 'Victory Park', severity: 'medium', top: 38, left: 58, reward: 30, color: '#eab308' },
  { id: 8, name: 'Komitas Avenue', severity: 'medium', top: 28, left: 40, reward: 35, color: '#eab308' },
  { id: 9, name: 'Arabkir District', severity: 'low', top: 25, left: 30, reward: 20, color: '#22c55e' },
  { id: 10, name: 'Mashtots Avenue', severity: 'medium', top: 55, left: 50, reward: 30, color: '#eab308' },
  { id: 11, name: 'Kentron Center', severity: 'high', top: 48, left: 46, reward: 45, color: '#ef4444' },
  { id: 12, name: 'Tsitsernakaberd', severity: 'low', top: 52, left: 25, reward: 15, color: '#22c55e' },
  { id: 13, name: 'Yerevan Lake', severity: 'medium', top: 18, left: 45, reward: 40, color: '#eab308' },
  { id: 14, name: 'Davtashen District', severity: 'high', top: 22, left: 15, reward: 50, color: '#ef4444' },
  { id: 15, name: 'Nork-Marash', severity: 'medium', top: 75, left: 65, reward: 35, color: '#eab308' },
];

export default function App() {
  const [selectedZone, setSelectedZone] = useState<typeof pollutionZones[0] | null>(null);
  const [filterSeverity, setFilterSeverity] = useState<string>('all');
  const [zoom, setZoom] = useState(1);

  const stats = {
    high: pollutionZones.filter(z => z.severity === 'high').length,
    medium: pollutionZones.filter(z => z.severity === 'medium').length,
    low: pollutionZones.filter(z => z.severity === 'low').length,
  };

  const filteredZones = filterSeverity === 'all' 
    ? pollutionZones 
    : pollutionZones.filter(z => z.severity === filterSeverity);

  return (
    <div className="min-h-screen bg-gray-50 flex flex-col">
      {/* Top Navigation Bar */}
      <nav className="bg-white shadow-sm border-b border-gray-200 sticky top-0 z-50">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="flex items-center justify-between h-16">
            {/* Logo */}
            <div className="flex items-center gap-2">
              <div className="flex items-center justify-center w-10 h-10 bg-emerald-100 rounded-lg">
                <Leaf className="size-6 text-emerald-600" />
              </div>
              <span className="text-emerald-600">Clarity Map</span>
            </div>

            {/* Navigation Links */}
            <div className="hidden md:flex items-center gap-1">
              <a 
                href="#" 
                className="flex items-center gap-2 px-4 py-2 rounded-lg bg-emerald-50 text-emerald-600 transition"
              >
                <Home className="size-5" />
                <span>Home</span>
              </a>
              <a 
                href="#" 
                className="flex items-center gap-2 px-4 py-2 rounded-lg text-gray-600 hover:bg-gray-50 transition"
              >
                <Target className="size-5" />
                <span>Missions</span>
              </a>
              <a 
                href="#" 
                className="flex items-center gap-2 px-4 py-2 rounded-lg text-gray-600 hover:bg-gray-50 transition"
              >
                <LayoutDashboard className="size-5" />
                <span>Dashboard</span>
              </a>
            </div>

            {/* Right Side Actions */}
            <div className="flex items-center gap-3">
              <button className="p-2 hover:bg-gray-100 rounded-lg transition relative">
                <Bell className="size-5 text-gray-600" />
                <span className="absolute top-1 right-1 w-2 h-2 bg-red-500 rounded-full"></span>
              </button>
              <button className="p-2 hover:bg-gray-100 rounded-lg transition">
                <User className="size-5 text-gray-600" />
              </button>
            </div>
          </div>
        </div>
      </nav>

      {/* Main Content */}
      <div className="flex-1 flex overflow-hidden">
        {/* Sidebar */}
        <aside className="w-80 bg-white border-r border-gray-200 overflow-y-auto">
          <div className="p-6 space-y-6">
            {/* Stats Overview */}
            <div>
              <h2 className="text-gray-900 mb-4">Pollution Overview</h2>
              
              <div className="space-y-3">
                <div className="bg-red-50 border border-red-200 rounded-lg p-4">
                  <div className="flex items-center justify-between mb-2">
                    <div className="flex items-center gap-2">
                      <AlertCircle className="size-5 text-red-600" />
                      <span className="text-red-900">High Severity</span>
                    </div>
                    <span className="text-red-600">{stats.high}</span>
                  </div>
                  <div className="w-full bg-red-200 rounded-full h-2">
                    <div className="bg-red-600 h-2 rounded-full" style={{ width: `${(stats.high / pollutionZones.length) * 100}%` }}></div>
                  </div>
                </div>

                <div className="bg-yellow-50 border border-yellow-200 rounded-lg p-4">
                  <div className="flex items-center justify-between mb-2">
                    <div className="flex items-center gap-2">
                      <AlertTriangle className="size-5 text-yellow-600" />
                      <span className="text-yellow-900">Medium Severity</span>
                    </div>
                    <span className="text-yellow-600">{stats.medium}</span>
                  </div>
                  <div className="w-full bg-yellow-200 rounded-full h-2">
                    <div className="bg-yellow-600 h-2 rounded-full" style={{ width: `${(stats.medium / pollutionZones.length) * 100}%` }}></div>
                  </div>
                </div>

                <div className="bg-green-50 border border-green-200 rounded-lg p-4">
                  <div className="flex items-center justify-between mb-2">
                    <div className="flex items-center gap-2">
                      <CheckCircle className="size-5 text-green-600" />
                      <span className="text-green-900">Low Severity</span>
                    </div>
                    <span className="text-green-600">{stats.low}</span>
                  </div>
                  <div className="w-full bg-green-200 rounded-full h-2">
                    <div className="bg-green-600 h-2 rounded-full" style={{ width: `${(stats.low / pollutionZones.length) * 100}%` }}></div>
                  </div>
                </div>
              </div>
            </div>

            {/* Quick Stats */}
            <div className="grid grid-cols-2 gap-3">
              <div className="bg-gradient-to-br from-emerald-50 to-teal-50 rounded-lg p-4">
                <div className="flex items-center gap-2 text-emerald-600 mb-1">
                  <Users className="size-5" />
                </div>
                <div className="text-gray-900">1,247</div>
                <div className="text-gray-500">Active Users</div>
              </div>

              <div className="bg-gradient-to-br from-blue-50 to-indigo-50 rounded-lg p-4">
                <div className="flex items-center gap-2 text-blue-600 mb-1">
                  <TrendingDown className="size-5" />
                </div>
                <div className="text-gray-900">-23%</div>
                <div className="text-gray-500">Pollution</div>
              </div>

              <div className="bg-gradient-to-br from-amber-50 to-orange-50 rounded-lg p-4">
                <div className="flex items-center gap-2 text-amber-600 mb-1">
                  <Target className="size-5" />
                </div>
                <div className="text-gray-900">342</div>
                <div className="text-gray-500">Active Missions</div>
              </div>

              <div className="bg-gradient-to-br from-purple-50 to-pink-50 rounded-lg p-4">
                <div className="flex items-center gap-2 text-purple-600 mb-1">
                  <Award className="size-5" />
                </div>
                <div className="text-gray-900">8,921</div>
                <div className="text-gray-500">Total Points</div>
              </div>
            </div>

            {/* Filter */}
            <div>
              <div className="flex items-center gap-2 mb-3">
                <Filter className="size-5 text-gray-600" />
                <h3 className="text-gray-900">Filter Zones</h3>
              </div>
              <div className="flex flex-wrap gap-2">
                <button
                  onClick={() => setFilterSeverity('all')}
                  className={`px-3 py-1.5 rounded-lg border transition ${
                    filterSeverity === 'all'
                      ? 'bg-emerald-600 text-white border-emerald-600'
                      : 'bg-white text-gray-600 border-gray-300 hover:border-emerald-600'
                  }`}
                >
                  All
                </button>
                <button
                  onClick={() => setFilterSeverity('high')}
                  className={`px-3 py-1.5 rounded-lg border transition ${
                    filterSeverity === 'high'
                      ? 'bg-red-600 text-white border-red-600'
                      : 'bg-white text-gray-600 border-gray-300 hover:border-red-600'
                  }`}
                >
                  High
                </button>
                <button
                  onClick={() => setFilterSeverity('medium')}
                  className={`px-3 py-1.5 rounded-lg border transition ${
                    filterSeverity === 'medium'
                      ? 'bg-yellow-600 text-white border-yellow-600'
                      : 'bg-white text-gray-600 border-gray-300 hover:border-yellow-600'
                  }`}
                >
                  Medium
                </button>
                <button
                  onClick={() => setFilterSeverity('low')}
                  className={`px-3 py-1.5 rounded-lg border transition ${
                    filterSeverity === 'low'
                      ? 'bg-green-600 text-white border-green-600'
                      : 'bg-white text-gray-600 border-gray-300 hover:border-green-600'
                  }`}
                >
                  Low
                </button>
              </div>
            </div>

            {/* Selected Zone Info */}
            {selectedZone && (
              <div className="bg-emerald-50 border border-emerald-200 rounded-lg p-4 space-y-3">
                <div className="flex items-start justify-between">
                  <div>
                    <h3 className="text-gray-900">{selectedZone.name}</h3>
                    <div className="flex items-center gap-2 mt-1">
                      <MapPin className="size-4 text-gray-500" />
                      <span className="text-gray-600">Zone #{selectedZone.id}</span>
                    </div>
                  </div>
                  <span className={`px-2 py-1 rounded text-white ${
                    selectedZone.severity === 'high' ? 'bg-red-500' :
                    selectedZone.severity === 'medium' ? 'bg-yellow-500' :
                    'bg-green-500'
                  }`}>
                    {selectedZone.severity.toUpperCase()}
                  </span>
                </div>

                <div className="flex items-center justify-between pt-3 border-t border-emerald-200">
                  <span className="text-gray-600">Reward</span>
                  <div className="flex items-center gap-1">
                    <Award className="size-4 text-emerald-600" />
                    <span className="text-emerald-600">{selectedZone.reward} Points</span>
                  </div>
                </div>

                <button className="w-full bg-emerald-600 hover:bg-emerald-700 text-white py-2.5 rounded-lg transition shadow-lg shadow-emerald-600/30">
                  Start Mission
                </button>
              </div>
            )}
          </div>
        </aside>

        {/* Map Area */}
        <main className="flex-1 relative bg-gradient-to-br from-slate-100 to-slate-200">
          {/* Map Container */}
          <div className="absolute inset-0 p-6">
            <div className="w-full h-full bg-white rounded-2xl shadow-xl overflow-hidden relative">
              {/* Map Background - Static tile from OpenStreetMap */}
              <div className="absolute inset-0">
                <iframe
                  src="https://www.openstreetmap.org/export/embed.html?bbox=44.4523%2C40.1354%2C44.5567%2C40.2231&layer=mapnik&marker=40.1811%2C44.5141"
                  className="w-full h-full border-0"
                  title="Yerevan Map"
                ></iframe>
              </div>

              {/* Pollution Markers Overlay */}
              <div className="absolute inset-0 pointer-events-none">
                {filteredZones.map((zone) => {
                  const size = zone.severity === 'high' ? 50 : zone.severity === 'medium' ? 40 : 32;
                  return (
                    <div
                      key={zone.id}
                      onClick={() => setSelectedZone(zone)}
                      className="absolute cursor-pointer group pointer-events-auto"
                      style={{
                        top: `${zone.top}%`,
                        left: `${zone.left}%`,
                        transform: 'translate(-50%, -50%)',
                      }}
                    >
                      {/* Zone Circle with pulse */}
                      <div
                        className="relative flex items-center justify-center"
                        style={{ width: `${size}px`, height: `${size}px` }}
                      >
                        {/* Pulsing effect */}
                        <div
                          className="absolute inset-0 rounded-full animate-ping opacity-20"
                          style={{ backgroundColor: zone.color }}
                        ></div>
                        
                        {/* Main zone circle */}
                        <div
                          className="absolute inset-0 rounded-full opacity-40 group-hover:opacity-60 transition"
                          style={{ backgroundColor: zone.color }}
                        ></div>

                        {/* Center pin */}
                        <MapPin 
                          className="relative z-10 drop-shadow-lg group-hover:scale-110 transition" 
                          style={{ color: zone.color, width: '24px', height: '24px' }}
                          fill="white"
                        />
                      </div>

                      {/* Zone Label on hover */}
                      <div className="absolute top-full left-1/2 -translate-x-1/2 mt-2 whitespace-nowrap opacity-0 group-hover:opacity-100 transition pointer-events-none">
                        <div className="bg-white px-3 py-2 rounded-lg shadow-lg border border-gray-200">
                          <div className="text-gray-900">{zone.name}</div>
                          <div className="flex items-center gap-1 text-emerald-600">
                            <Award className="size-3" />
                            <span>{zone.reward} pts</span>
                          </div>
                        </div>
                      </div>
                    </div>
                  );
                })}
              </div>

              {/* Map Legend */}
              <div className="absolute bottom-6 left-6 bg-white rounded-lg shadow-lg p-4 border border-gray-200 z-10">
                <div className="text-gray-900 mb-3">Pollution Levels</div>
                <div className="space-y-2">
                  <div className="flex items-center gap-3">
                    <div className="w-6 h-6 rounded-full bg-red-500"></div>
                    <span className="text-gray-600">High Severity</span>
                  </div>
                  <div className="flex items-center gap-3">
                    <div className="w-6 h-6 rounded-full bg-yellow-500"></div>
                    <span className="text-gray-600">Medium Severity</span>
                  </div>
                  <div className="flex items-center gap-3">
                    <div className="w-6 h-6 rounded-full bg-green-500"></div>
                    <span className="text-gray-600">Low Severity</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </main>
      </div>
    </div>
  );
}

                              
