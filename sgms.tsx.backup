import React, { useState, useEffect } from 'react';
import { 
  Activity, AlertTriangle, Calendar as CalendarIcon, CheckCircle, ChevronDown, 
  ClipboardList, Clock, FileText, Home, Info, LayoutDashboard, Map, 
  Menu, Bell, Search, Settings, ShieldAlert, Thermometer, User, 
  Users, X, Zap, ArrowUpRight, BarChart3, Wrench, BrainCircuit, 
  Paperclip, Camera, MapPin, Database, ArrowRight, Table, Grid, PieChartIcon, Lock, Edit3
} from 'lucide-react';
import { 
  LineChart, Line, BarChart, Bar, XAxis, YAxis, CartesianGrid, 
  Tooltip as RechartsTooltip, Legend, ResponsiveContainer, PieChart, Pie, Cell, AreaChart, Area
} from 'recharts';

const mockEquipos = [
  { id: 1, nombre: 'Resonador Magnético 3T', fabricante: 'Siemens', modelo: 'Magnetom Vida', serie: 'RM-3T-8821', centro: 'Centro Palermo', servicio: 'Diagnóstico por Imágenes', estado: 'Operativo', statusColor: 'bg-emerald-500', ingeniero: 'Martín Torres', tiempoDetenido: '0h', ultimoMantenimiento: '12/05/2026', healthScore: 95, critico: true, tipo: 'Resonador' },
  { id: 2, nombre: 'Tomógrafo PET-CT', fabricante: 'GE Healthcare', modelo: 'Discovery IQ', serie: 'PT-GE-112', centro: 'Clínica Suizo', servicio: 'Medicina Nuclear', estado: 'Mantenimiento', statusColor: 'bg-amber-400', ingeniero: 'Laura Gómez', tiempoDetenido: '4h', ultimoMantenimiento: 'Hoy', healthScore: 70, critico: true, tipo: 'PET-CT' },
  { id: 3, nombre: 'Acelerador Lineal', fabricante: 'Varian', modelo: 'TrueBeam', serie: 'AL-VB-993', centro: 'Instituto Oncológico', servicio: 'Radioterapia', estado: 'Fuera de servicio', statusColor: 'bg-rose-500', ingeniero: 'Carlos Ruiz', tiempoDetenido: '12h', ultimoMantenimiento: '10/04/2026', healthScore: 35, critico: true, tipo: 'Acelerador' },
  { id: 4, nombre: 'Angiógrafo Biplano', fabricante: 'Philips', modelo: 'Azurion 7', serie: 'AN-PH-004', centro: 'Hospital Central', servicio: 'Hemodinamia', estado: 'Esperando repuesto', statusColor: 'bg-orange-500', ingeniero: 'Ana Ledesma', tiempoDetenido: '48h', ultimoMantenimiento: '02/03/2026', healthScore: 55, critico: true, tipo: 'Angiógrafo' },
  { id: 5, nombre: 'Ecógrafo 4D', fabricante: 'Canon', modelo: 'Aplio i900', serie: 'EC-CA-441', centro: 'Centro Caballito', servicio: 'Ecografía', estado: 'En análisis', statusColor: 'bg-blue-500', ingeniero: 'Martín Torres', tiempoDetenido: '2h', ultimoMantenimiento: '15/05/2026', healthScore: 82, critico: false, tipo: 'Ecógrafo' },
  { id: 6, nombre: 'Mamógrafo Digital', fabricante: 'Hologic', modelo: '3D Dimensions', serie: 'MA-HO-772', centro: 'Centro Palermo', servicio: 'Brest Center', estado: 'Operativo', statusColor: 'bg-emerald-500', ingeniero: 'Laura Gómez', tiempoDetenido: '0h', ultimoMantenimiento: '20/05/2026', healthScore: 98, critico: false, tipo: 'Mamógrafo' },
];

const mockTickets = [
  { id: 'T-882', equipo: 'Acelerador Lineal', centro: 'Instituto Oncológico', estado: 'Fuera de servicio', prioridad: 'Alta', fecha: '24/06/2026', ing: 'Carlos Ruiz' },
  { id: 'T-883', equipo: 'Angiógrafo Biplano', centro: 'Hospital Central', estado: 'Esperando repuesto', prioridad: 'Media', fecha: '22/06/2026', ing: 'Ana Ledesma' },
  { id: 'T-884', equipo: 'Tomógrafo PET-CT', centro: 'Clínica Suizo', estado: 'Mantenimiento', prioridad: 'Baja', fecha: '24/06/2026', ing: 'Laura Gómez' },
  { id: 'T-885', equipo: 'Ecógrafo 4D', centro: 'Centro Caballito', estado: 'En análisis', prioridad: 'Alta', fecha: '24/06/2026', ing: 'Martín Torres' },
];

const mockInsights = [
  { id: 1, prioridad: 'Alta', color: 'border-rose-500', bg: 'bg-rose-50', icon: AlertTriangle, equipo: 'Resonador Siemens', centro: 'Centro Palermo', descripcion: 'El Resonador presenta una recurrencia de fallas en el sistema de refrigeración del magneto (Helium Coldhead).', impacto: 'Posible Quench inminente. Riesgo de pérdida total de helio y parada prolongada.', accion: 'Programar mantenimiento preventivo urgente de Coldhead.' },
  { id: 2, prioridad: 'Media', color: 'border-orange-500', bg: 'bg-orange-50', icon: Activity, equipo: 'Tomógrafo GE', centro: 'Clínica Suizo', descripcion: 'Acumula 128 horas fuera de servicio durante el último año móvil (Supera límite KPI 98%).', impacto: 'Alta afectación operativa en guardias. Desvío de pacientes.', accion: 'Revisar contrato de SLA con proveedor. Solicitar auditoría de tubos de rayos X.' },
  { id: 3, prioridad: 'Baja', color: 'border-amber-400', bg: 'bg-amber-50', icon: Thermometer, equipo: 'Múltiples', centro: 'Centro Caballito', descripcion: 'Se incrementó un 31% la cantidad de incidentes reportados respecto al mes anterior.', impacto: 'Saturación del equipo técnico local.', accion: 'Revisar planificación de mantenimiento y condiciones ambientales de salas.' },
  { id: 4, prioridad: 'Info', color: 'border-blue-500', bg: 'bg-blue-50', icon: BrainCircuit, equipo: 'Angiógrafo Philips', centro: 'Hospital Central', descripcion: 'Patrón de voltaje anómalo detectado en generador, similar a falla crítica de 2024.', impacto: 'Parada abrupta en procedimiento intervencionista.', accion: 'Inspección preventiva de placas de potencia.' },
];

const kpiData = [
  { name: 'Ene', disp: 98, fallas: 12 }, { name: 'Feb', disp: 97.5, fallas: 15 },
  { name: 'Mar', disp: 99, fallas: 8 }, { name: 'Abr', disp: 96, fallas: 22 },
  { name: 'May', disp: 98.2, fallas: 10 }, { name: 'Jun', disp: 95.5, fallas: 18 },
];

const donutData = [
  { name: 'Siemens', value: 40, color: '#3b82f6' },
  { name: 'GE', value: 30, color: '#10b981' },
  { name: 'Philips', value: 20, color: '#f59e0b' },
  { name: 'Otros', value: 10, color: '#64748b' },
];

const HealthScoreCircle = ({ score, size = 120 }) => {
  const radius = (size - 20) / 2;
  const circumference = radius * 2 * Math.PI;
  const strokeDashoffset = circumference - (score / 100) * circumference;
  
  let color = '#10b981'; // Green
  let text = 'Excelente';
  if (score < 85) { color = '#3b82f6'; text = 'Muy Bueno'; }
  if (score < 75) { color = '#f59e0b'; text = 'Atención'; }
  if (score < 50) { color = '#f97316'; text = 'Riesgo'; }
  if (score < 30) { color = '#e11d48'; text = 'Crítico'; }

  return (
    <div className="relative flex flex-col items-center justify-center" style={{ width: size, height: size }}>
      <svg className="transform -rotate-90 w-full h-full">
        <circle cx={size/2} cy={size/2} r={radius} stroke="#e2e8f0" strokeWidth="10" fill="transparent" />
        <circle cx={size/2} cy={size/2} r={radius} stroke={color} strokeWidth="10" fill="transparent" 
          strokeDasharray={circumference} strokeDashoffset={strokeDashoffset} className="transition-all duration-1000 ease-out" strokeLinecap="round" />
      </svg>
      <div className="absolute flex flex-col items-center">
        <span className="text-3xl font-bold text-slate-800">{score}</span>
        <span className="text-[10px] uppercase font-semibold text-slate-500">{text}</span>
      </div>
    </div>
  );
};

const MiniHealthScore = ({ score }) => {
  let color = 'bg-emerald-500';
  if (score < 85) color = 'bg-blue-500';
  if (score < 75) color = 'bg-amber-500';
  if (score < 50) color = 'bg-orange-500';
  if (score < 30) color = 'bg-rose-500';

  return (
    <div className="flex items-center space-x-2">
      <div className="w-16 bg-slate-200 rounded-full h-1.5 overflow-hidden">
        <div className={`${color} h-full rounded-full`} style={{ width: `${score}%` }}></div>
      </div>
      <span className="text-xs font-bold text-slate-600 w-6">{score}</span>
    </div>
  );
};

const LoginScreen = ({ onLogin }) => {
  const [email, setEmail] = useState('');
  
  const handleLogin = (e) => {
    e.preventDefault();
    if(email.includes('gerente')) onLogin('gerente');
    else if(email.includes('ingeniero')) onLogin('ingeniero');
    else if(email.includes('tecnico')) onLogin('tecnico');
    else onLogin('gerente'); // Default
  };

  return (
    <div className="min-h-screen bg-slate-50 flex items-center justify-center p-4 relative overflow-hidden">
      <div className="absolute inset-0 z-0">
         <img src="https://images.unsplash.com/photo-1551076805-e1869033e561?auto=format&fit=crop&q=80&w=2000" alt="Hospital Tech" className="w-full h-full object-cover opacity-10" />
         <div className="absolute inset-0 bg-gradient-to-br from-slate-900/80 to-indigo-900/90 mix-blend-multiply"></div>
      </div>
      
      <div className="bg-white rounded-2xl shadow-2xl w-full max-w-md p-8 relative z-10 transform transition-all hover:scale-[1.01] duration-300">
        <div className="flex justify-center mb-8">
          <div className="bg-indigo-600 p-3 rounded-xl shadow-lg">
            <Activity className="text-white w-8 h-8" />
          </div>
        </div>
        <h1 className="text-3xl font-bold text-center text-slate-800 mb-2 tracking-tight">SGMS</h1>
        <p className="text-center text-slate-500 mb-8 text-sm font-medium">Smart Healthcare Management System</p>
        
        <form onSubmit={handleLogin} className="space-y-5">
          <div>
            <label className="block text-sm font-semibold text-slate-700 mb-1">Correo Electrónico Corporativo</label>
            <div className="relative">
              <User className="absolute left-3 top-1/2 transform -translate-y-1/2 text-slate-400 w-5 h-5" />
              <input 
                type="email" 
                value={email}
                onChange={(e) => setEmail(e.target.value)}
                placeholder="usuario@hospital.com" 
                className="w-full pl-10 pr-4 py-3 rounded-lg border border-slate-200 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 transition-all outline-none" 
                required
              />
            </div>
            {/* Auto-fill buttons for pitch */}
            <div className="flex space-x-2 mt-2">
               <button type="button" onClick={()=>setEmail('gerente@sgms.com')} className="text-[10px] bg-slate-100 hover:bg-indigo-100 text-slate-500 px-2 py-1 rounded">gerente@...</button>
               <button type="button" onClick={()=>setEmail('ingeniero@sgms.com')} className="text-[10px] bg-slate-100 hover:bg-indigo-100 text-slate-500 px-2 py-1 rounded">ingeniero@...</button>
               <button type="button" onClick={()=>setEmail('tecnico@sgms.com')} className="text-[10px] bg-slate-100 hover:bg-indigo-100 text-slate-500 px-2 py-1 rounded">tecnico@...</button>
            </div>
          </div>
          <div>
            <label className="block text-sm font-semibold text-slate-700 mb-1">Contraseña</label>
            <div className="relative">
              <ShieldAlert className="absolute left-3 top-1/2 transform -translate-y-1/2 text-slate-400 w-5 h-5" />
              <input type="password" placeholder="••••••••" className="w-full pl-10 pr-4 py-3 rounded-lg border border-slate-200 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 transition-all outline-none" defaultValue="password" />
            </div>
          </div>
          <button type="submit" className="w-full bg-indigo-600 text-white py-3 rounded-lg font-semibold shadow-md hover:bg-indigo-700 hover:shadow-lg transition-all flex justify-center items-center space-x-2 mt-4">
            <span>Iniciar Sesión</span>
            <ArrowRight className="w-4 h-4" />
          </button>
        </form>
      </div>
    </div>
  );
};

const DashboardScreen = ({ navigate, role }) => {
  const [viewMode, setViewMode] = useState('grid');
  
  return (
    <div className="space-y-6 fade-in">
      {/* Top KPIs */}
      <div className="grid grid-cols-1 md:grid-cols-3 lg:grid-cols-6 gap-4">
        {[
          { label: 'Operativos', val: '42', sub: '85% del parque', icon: CheckCircle, color: 'text-emerald-500', bg: 'bg-emerald-50' },
          { label: 'En Mantenimiento', val: '4', sub: 'Preventivo', icon: Wrench, color: 'text-amber-500', bg: 'bg-amber-50' },
          { label: 'Fuera de Servicio', val: '3', sub: 'Correctivo', icon: AlertTriangle, color: 'text-rose-500', bg: 'bg-rose-50' },
          { label: 'Tickets Abiertos', val: '12', sub: 'Prioridad alta: 4', icon: FileText, color: 'text-blue-500', bg: 'bg-blue-50' },
          { label: 'Disponibilidad', val: '97.2%', sub: 'Objetivo: 98%', icon: Activity, color: 'text-indigo-500', bg: 'bg-indigo-50' },
          { label: 'Incidentes Mes', val: '18', sub: '-12% vs mes ant.', icon: BarChart3, color: 'text-purple-500', bg: 'bg-purple-50' },
        ].map((kpi, i) => (
          <div key={i} className="bg-white p-4 rounded-xl shadow-sm border border-slate-100 flex items-start space-x-4 hover:shadow-md transition-all">
            <div className={`p-3 rounded-lg ${kpi.bg}`}>
              <kpi.icon className={`w-6 h-6 ${kpi.color}`} />
            </div>
            <div>
              <p className="text-slate-500 text-xs font-semibold uppercase">{kpi.label}</p>
              <h3 className="text-2xl font-bold text-slate-800">{kpi.val}</h3>
              <p className="text-slate-400 text-xs">{kpi.sub}</p>
            </div>
          </div>
        ))}
      </div>

      {/* Equipment Board Container */}
      <div>
        <div className="flex justify-between items-end mb-4">
          <div>
            <h2 className="text-xl font-bold text-slate-800">Monitor de Equipamiento Biocientífico</h2>
            <p className="text-sm text-slate-500">Vista en tiempo real de equipos de alta complejidad.</p>
          </div>
          <div className="flex space-x-2 items-center">
            {/* View Toggle */}
            <div className="bg-white border border-slate-200 rounded-lg p-1 flex">
              <button onClick={() => setViewMode('grid')} className={`p-1.5 rounded-md transition-colors ${viewMode === 'grid' ? 'bg-indigo-100 text-indigo-700' : 'text-slate-400 hover:text-slate-600'}`}>
                <Grid className="w-4 h-4" />
              </button>
              <button onClick={() => setViewMode('table')} className={`p-1.5 rounded-md transition-colors ${viewMode === 'table' ? 'bg-indigo-100 text-indigo-700' : 'text-slate-400 hover:text-slate-600'}`}>
                <Table className="w-4 h-4" />
              </button>
            </div>
            <button className="px-4 py-2 bg-indigo-600 text-white rounded-lg text-sm font-medium hover:bg-indigo-700 shadow-sm ml-2">
              Generar Reporte
            </button>
          </div>
        </div>

        {viewMode === 'grid' ? (
          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-4">
            {mockEquipos.map(eq => (
              <div key={eq.id} 
                   onClick={() => navigate('equipo', eq)}
                   className="bg-white rounded-xl shadow-sm border border-slate-100 overflow-hidden hover:shadow-lg transition-all cursor-pointer group flex flex-col">
                <div className="p-1">
                   <div className={`h-2 w-full rounded-t-lg ${eq.statusColor}`}></div>
                </div>
                <div className="p-5 flex-1 flex flex-col">
                  <div className="flex justify-between items-start mb-3">
                    <div className="flex items-center space-x-2">
                      <span className={`w-3 h-3 rounded-full ${eq.statusColor} shadow-sm animate-pulse`}></span>
                      <span className="text-xs font-bold uppercase tracking-wider text-slate-500">{eq.estado}</span>
                    </div>
                    {eq.critico && <AlertTriangle className="w-4 h-4 text-rose-500" />}
                  </div>
                  
                  <h3 className="text-lg font-bold text-slate-800 leading-tight mb-1 group-hover:text-indigo-600 transition-colors">{eq.nombre}</h3>
                  <p className="text-sm text-slate-500 mb-4">{eq.fabricante} {eq.modelo}</p>
                  
                  <div className="mt-auto space-y-2 text-sm">
                    <div className="flex items-center text-slate-600">
                      <MapPin className="w-4 h-4 mr-2 text-slate-400" /> {eq.centro}
                    </div>
                    <div className="flex items-center text-slate-600">
                      <User className="w-4 h-4 mr-2 text-slate-400" /> {eq.ingeniero}
                    </div>
                    <div className={`flex items-center font-semibold ${eq.tiempoDetenido !== '0h' ? 'text-rose-500' : 'text-slate-600'}`}>
                      <Clock className="w-4 h-4 mr-2" /> Detenido: {eq.tiempoDetenido}
                    </div>
                  </div>
                </div>
                <div className="bg-slate-50 px-5 py-3 border-t border-slate-100 flex justify-between items-center">
                  <MiniHealthScore score={eq.healthScore} />
                  <span className="text-xs font-semibold text-slate-500">SN: {eq.serie}</span>
                </div>
              </div>
            ))}
          </div>
        ) : (
          <div className="bg-white rounded-xl shadow-sm border border-slate-200 overflow-hidden">
            <table className="w-full text-left text-sm">
              <thead className="bg-slate-50 border-b border-slate-200 text-slate-600 font-semibold">
                <tr>
                  <th className="py-3 px-4">Equipo</th>
                  <th className="py-3 px-4">Centro</th>
                  <th className="py-3 px-4">Estado</th>
                  <th className="py-3 px-4">Detención</th>
                  <th className="py-3 px-4">Salud (HS)</th>
                  <th className="py-3 px-4 text-right">Detalle</th>
                </tr>
              </thead>
              <tbody className="divide-y divide-slate-100">
                {mockEquipos.map(eq => (
                  <tr key={eq.id} onClick={() => navigate('equipo', eq)} className="hover:bg-slate-50 cursor-pointer transition-colors group">
                    <td className="py-3 px-4">
                      <div className="flex items-center space-x-3">
                        {eq.critico ? <AlertTriangle className="w-4 h-4 text-rose-500" /> : <Database className="w-4 h-4 text-slate-400" />}
                        <div>
                          <p className="font-bold text-slate-800">{eq.nombre}</p>
                          <p className="text-xs text-slate-500">{eq.fabricante} {eq.modelo}</p>
                        </div>
                      </div>
                    </td>
                    <td className="py-3 px-4 text-slate-600">{eq.centro}</td>
                    <td className="py-3 px-4">
                      <span className={`inline-flex items-center px-2 py-1 rounded-full text-xs font-bold bg-white border ${eq.statusColor.replace('bg-', 'border-')} ${eq.statusColor.replace('bg-', 'text-')}`}>
                        <span className={`w-1.5 h-1.5 rounded-full mr-1 ${eq.statusColor}`}></span>
                        {eq.estado}
                      </span>
                    </td>
                    <td className={`py-3 px-4 font-semibold ${eq.tiempoDetenido !== '0h' ? 'text-rose-500' : 'text-slate-500'}`}>
                      {eq.tiempoDetenido}
                    </td>
                    <td className="py-3 px-4">
                      <MiniHealthScore score={eq.healthScore} />
                    </td>
                    <td className="py-3 px-4 text-right">
                      <button className="text-slate-400 group-hover:text-indigo-600 p-1">
                        <ArrowUpRight className="w-4 h-4" />
                      </button>
                    </td>
                  </tr>
                ))}
              </tbody>
            </table>
          </div>
        )}
      </div>
    </div>
  );
};

const EquiposScreen = ({ navigate, role }) => {
  const [viewMode, setViewMode] = useState('table');
  const [filtroCentro, setFiltroCentro] = useState('Todos los Centros');

  const equiposFiltrados = filtroCentro === 'Todos los Centros' ? mockEquipos : mockEquipos.filter(e => e.centro === filtroCentro);

  return (
    <div className="space-y-6 fade-in h-full flex flex-col">
      <div className="flex flex-col sm:flex-row justify-between items-start sm:items-end gap-4 mb-4">
        <div>
          <h2 className="text-2xl font-bold text-slate-800">Parque Tecnológico</h2>
          <p className="text-sm text-slate-500">Gestión de inventario y estado operativo.</p>
        </div>
        <div className="flex flex-wrap items-center gap-2">
          <select 
            value={filtroCentro}
            onChange={(e) => setFiltroCentro(e.target.value)}
            className="border border-slate-200 rounded-lg px-3 py-2 text-sm text-slate-600 focus:outline-none focus:ring-2 focus:ring-indigo-500 bg-white"
          >
            <option>Todos los Centros</option>
            <option>Centro Palermo</option>
            <option>Clínica Suizo</option>
            <option>Instituto Oncológico</option>
            <option>Hospital Central</option>
            <option>Centro Caballito</option>
          </select>
          <div className="relative">
            <Search className="absolute left-3 top-1/2 transform -translate-y-1/2 text-slate-400 w-4 h-4" />
            <input type="text" placeholder="Buscar por SN, modelo..." className="pl-9 pr-4 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 w-48" />
          </div>
          <div className="bg-white border border-slate-200 rounded-lg p-1 flex">
            <button onClick={() => setViewMode('table')} className={`p-1.5 rounded-md transition-colors ${viewMode === 'table' ? 'bg-indigo-100 text-indigo-700' : 'text-slate-400 hover:text-slate-600'}`}>
              <Table className="w-4 h-4" />
            </button>
            <button onClick={() => setViewMode('grid')} className={`p-1.5 rounded-md transition-colors ${viewMode === 'grid' ? 'bg-indigo-100 text-indigo-700' : 'text-slate-400 hover:text-slate-600'}`}>
              <Grid className="w-4 h-4" />
            </button>
          </div>
        </div>
      </div>

      {viewMode === 'table' ? (
        <div className="flex-1 bg-white rounded-xl shadow-sm border border-slate-200 overflow-hidden flex flex-col">
          <div className="overflow-x-auto flex-1">
            <table className="w-full text-left text-sm whitespace-nowrap">
              <thead className="bg-slate-50 border-b border-slate-200 text-slate-600 font-semibold sticky top-0 z-10">
                <tr>
                  <th className="py-3 px-4">Equipo</th>
                  <th className="py-3 px-4">Ubicación</th>
                  <th className="py-3 px-4">Estado</th>
                  <th className="py-3 px-4">Health Score</th>
                  <th className="py-3 px-4">Mantenimiento</th>
                  <th className="py-3 px-4 text-right">Acción</th>
                </tr>
              </thead>
              <tbody className="divide-y divide-slate-100">
                {equiposFiltrados.map(eq => (
                  <tr key={eq.id} className="hover:bg-slate-50 transition-colors group">
                    <td className="py-3 px-4 cursor-pointer" onClick={() => navigate('equipo', eq)}>
                      <div className="flex items-center space-x-3">
                        <div className={`p-2 rounded-lg ${eq.statusColor.replace('bg-', 'bg-').replace('500', '100')} ${eq.statusColor.replace('bg-', 'text-')}`}>
                          <Database className="w-4 h-4" />
                        </div>
                        <div>
                          <p className="font-bold text-slate-800 group-hover:text-indigo-600 transition-colors">{eq.nombre}</p>
                          <p className="text-xs text-slate-500">SN: {eq.serie} | {eq.fabricante}</p>
                        </div>
                      </div>
                    </td>
                    <td className="py-3 px-4">
                      <p className="font-semibold text-slate-700">{eq.centro}</p>
                      <p className="text-xs text-slate-500">{eq.servicio}</p>
                    </td>
                    <td className="py-3 px-4">
                      {role === 'ingeniero' ? (
                         <select className="text-xs border border-slate-200 rounded px-2 py-1 bg-white focus:ring-indigo-500" defaultValue={eq.estado}>
                           <option>Operativo</option>
                           <option>En análisis</option>
                           <option>Esperando repuesto</option>
                           <option>Mantenimiento</option>
                           <option>Fuera de servicio</option>
                         </select>
                      ) : (
                        <span className={`inline-flex items-center px-2 py-1 rounded-full text-xs font-bold bg-white border ${eq.statusColor.replace('bg-', 'border-')} ${eq.statusColor.replace('bg-', 'text-')}`}>
                          <span className={`w-1.5 h-1.5 rounded-full mr-1 ${eq.statusColor}`}></span>
                          {eq.estado}
                          {role === 'gerente' && <Lock className="w-3 h-3 ml-1 opacity-50" />}
                        </span>
                      )}
                    </td>
                    <td className="py-3 px-4 w-32">
                      <MiniHealthScore score={eq.healthScore} />
                    </td>
                    <td className="py-3 px-4">
                      <p className="text-sm text-slate-700">{eq.ultimoMantenimiento}</p>
                      <p className="text-xs text-slate-500">Ing: {eq.ingeniero}</p>
                    </td>
                    <td className="py-3 px-4 text-right">
                       <button onClick={() => navigate('equipo', eq)} className="p-2 text-indigo-600 hover:bg-indigo-50 rounded-lg transition-colors font-semibold text-sm">
                         Ver Ficha
                       </button>
                    </td>
                  </tr>
                ))}
              </tbody>
            </table>
          </div>
        </div>
      ) : (
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-4">
           {equiposFiltrados.map(eq => (
             <div key={eq.id} onClick={() => navigate('equipo', eq)} className="bg-white rounded-xl shadow-sm border border-slate-100 p-5 cursor-pointer hover:shadow-md transition-all group">
               {/* Same content as Dashboard cards */}
               <div className="flex justify-between items-start mb-3">
                  <div className="flex items-center space-x-2">
                    <span className={`w-3 h-3 rounded-full ${eq.statusColor} shadow-sm animate-pulse`}></span>
                    <span className="text-xs font-bold uppercase tracking-wider text-slate-500">{eq.estado}</span>
                  </div>
                </div>
                <h3 className="text-lg font-bold text-slate-800 leading-tight mb-1 group-hover:text-indigo-600 transition-colors">{eq.nombre}</h3>
                <p className="text-sm text-slate-500 mb-4">{eq.fabricante} {eq.modelo}</p>
                <div className="space-y-2 text-sm">
                  <div className="flex items-center text-slate-600"><MapPin className="w-4 h-4 mr-2 text-slate-400" /> {eq.centro}</div>
                </div>
             </div>
           ))}
        </div>
      )}
    </div>
  );
};

const EquipoScreen = ({ equipo, onBack }) => {
  const [activeTab, setActiveTab] = useState('resumen');

  if (!equipo) return null;

  return (
    <div className="space-y-6 fade-in">
      <div className="flex items-center space-x-4 mb-2">
        <button onClick={onBack} className="p-2 bg-white rounded-full border border-slate-200 hover:bg-slate-50 transition-colors">
          <ArrowRight className="w-5 h-5 text-slate-600 transform rotate-180" />
        </button>
        <div>
          <h2 className="text-2xl font-bold text-slate-800">Ficha Técnica: {equipo.nombre}</h2>
          <p className="text-slate-500">{equipo.fabricante} {equipo.modelo} - SN: {equipo.serie}</p>
        </div>
      </div>

      <div className="grid grid-cols-1 lg:grid-cols-3 gap-6">
        <div className="lg:col-span-1 space-y-6">
          <div className="bg-white rounded-xl shadow-sm border border-slate-100 overflow-hidden">
            <div className="h-48 bg-slate-200 relative flex items-center justify-center">
              <Database className="w-16 h-16 text-slate-400" />
              <div className="absolute top-4 right-4 bg-white/90 backdrop-blur px-3 py-1 rounded-full text-xs font-bold flex items-center space-x-2 shadow-sm">
                 <span className={`w-2 h-2 rounded-full ${equipo.statusColor}`}></span>
                 <span>{equipo.estado}</span>
              </div>
            </div>
            <div className="p-6">
               <div className="flex justify-center mb-6">
                 <HealthScoreCircle score={equipo.healthScore} size={140} />
               </div>
               <div className="space-y-3 divide-y divide-slate-100 text-sm">
                 <div className="flex justify-between py-2"><span className="text-slate-500">Centro</span><span className="font-semibold text-slate-800">{equipo.centro}</span></div>
                 <div className="flex justify-between py-2"><span className="text-slate-500">Servicio</span><span className="font-semibold text-slate-800">{equipo.servicio}</span></div>
                 <div className="flex justify-between py-2"><span className="text-slate-500">Ingeniero</span><span className="font-semibold text-indigo-600">{equipo.ingeniero}</span></div>
               </div>
            </div>
          </div>
        </div>

        <div className="lg:col-span-2">
          <div className="bg-white rounded-xl shadow-sm border border-slate-100 h-full flex flex-col">
            <div className="flex border-b border-slate-100">
              {['resumen', 'historial', 'documentos'].map(tab => (
                <button 
                  key={tab}
                  onClick={() => setActiveTab(tab)}
                  className={`px-6 py-4 text-sm font-semibold capitalize transition-colors ${activeTab === tab ? 'text-indigo-600 border-b-2 border-indigo-600' : 'text-slate-500 hover:text-slate-800'}`}
                >
                  {tab}
                </button>
              ))}
            </div>
            
            <div className="p-6 flex-1 overflow-auto">
              {activeTab === 'resumen' && (
                <div className="space-y-6">
                  <div>
                    <h3 className="text-lg font-bold text-slate-800 mb-4">Últimos Tickets</h3>
                    <div className="space-y-3">
                      {[1,2].map(i => (
                        <div key={i} className="flex items-center justify-between p-3 border border-slate-100 rounded-lg hover:bg-slate-50 transition-colors cursor-pointer">
                          <div className="flex items-center space-x-3">
                            <CheckCircle className="w-5 h-5 text-emerald-500" />
                            <div>
                              <p className="text-sm font-bold text-slate-800">T-8{i}4 - Revisión general</p>
                              <p className="text-xs text-slate-500">Cerrado por {equipo.ingeniero}</p>
                            </div>
                          </div>
                        </div>
                      ))}
                    </div>
                  </div>
                </div>
              )}
              {activeTab === 'historial' && (
                <div className="relative border-l-2 border-slate-100 ml-4 space-y-8">
                   <div className="relative pl-6">
                     <div className="absolute -left-[9px] top-1 w-4 h-4 rounded-full border-2 border-white bg-amber-400"></div>
                     <p className="text-xs font-bold text-slate-400 mb-1">Hoy, 10:30 AM</p>
                     <h4 className="text-sm font-bold text-slate-800">Mantenimiento iniciado</h4>
                     <p className="text-sm text-slate-600 mt-1">Revisión de rutina.</p>
                   </div>
                </div>
              )}
            </div>
          </div>
        </div>
      </div>
    </div>
  );
};

const TicketsScreen = ({ role }) => {
  const [filtroCentro, setFiltroCentro] = useState('Todos los Centros');
  const ticketsFiltrados = filtroCentro === 'Todos los Centros' ? mockTickets : mockTickets.filter(t => t.centro === filtroCentro);

  return (
    <div className="space-y-6 fade-in h-[calc(100vh-140px)] flex flex-col">
      <div className="flex flex-col sm:flex-row justify-between items-start sm:items-end gap-4 mb-4">
        <div>
          <h2 className="text-2xl font-bold text-slate-800">
            {role === 'gerente' ? 'Monitor de Tickets' : 'Gestión de Tickets'}
          </h2>
          <p className="text-sm text-slate-500">
            {role === 'gerente' 
              ? 'Vista ejecutiva del estado de incidentes (Modo lectura seguro).' 
              : 'Kanban operativo. Arrastre tarjetas para cambiar estados.'}
          </p>
        </div>
        <div className="flex flex-wrap items-center gap-2">
          <select 
            value={filtroCentro}
            onChange={(e) => setFiltroCentro(e.target.value)}
            className="border border-slate-200 rounded-lg px-3 py-2 text-sm text-slate-600 focus:outline-none focus:ring-2 focus:ring-indigo-500 bg-white"
          >
            <option>Todos los Centros</option>
            <option>Centro Palermo</option>
            <option>Clínica Suizo</option>
            <option>Instituto Oncológico</option>
            <option>Hospital Central</option>
            <option>Centro Caballito</option>
          </select>
          <div className="relative">
            <Search className="absolute left-3 top-1/2 transform -translate-y-1/2 text-slate-400 w-4 h-4" />
            <input type="text" placeholder="Buscar ticket..." className="pl-9 pr-4 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500" />
          </div>
          {role === 'ingeniero' && (
            <button className="px-4 py-2 bg-indigo-600 text-white rounded-lg text-sm font-medium hover:bg-indigo-700 shadow-sm flex items-center space-x-2">
              <span className="text-lg leading-none">+</span> <span>Nuevo Ticket</span>
            </button>
          )}
        </div>
      </div>

      <div className="flex-1 flex space-x-4 overflow-x-auto pb-4">
        {['Pendiente', 'En Análisis', 'Esperando Repuesto', 'Reparación'].map((col, idx) => {
          let borderTop = idx === 0 ? 'border-rose-400' : idx === 1 ? 'border-blue-400' : idx === 2 ? 'border-orange-400' : 'border-amber-400';

          return (
            <div key={col} className="bg-slate-50 rounded-xl min-w-[300px] flex flex-col border border-slate-200">
              <div className={`p-3 border-t-4 ${borderTop} rounded-t-xl bg-slate-100 border-b border-slate-200 flex justify-between items-center`}>
                <h3 className="font-bold text-slate-700 text-sm">{col}</h3>
              </div>
              <div className="p-3 space-y-3 flex-1 overflow-y-auto">
                {ticketsFiltrados.filter((_, i) => (i % 4) === idx).map(t => (
                  <div key={t.id} className="bg-white p-4 rounded-lg shadow-sm border border-slate-200 hover:shadow-md hover:border-indigo-300 transition-all group relative">
                    {role === 'gerente' && <Lock className="w-3 h-3 absolute top-3 right-3 text-slate-300" title="Solo lectura" />}
                    {role === 'ingeniero' && <Edit3 className="w-3 h-3 absolute top-3 right-3 text-slate-300 group-hover:text-indigo-500 cursor-pointer" title="Editar" />}
                    
                    <div className="flex justify-between items-start mb-2 pr-6">
                      <span className="text-xs font-bold text-indigo-600 bg-indigo-50 px-2 py-1 rounded">{t.id}</span>
                      <span className={`text-[10px] uppercase font-bold px-2 py-1 rounded-full ${t.prioridad === 'Alta' ? 'bg-rose-100 text-rose-700' : t.prioridad === 'Media' ? 'bg-orange-100 text-orange-700' : 'bg-emerald-100 text-emerald-700'}`}>
                        {t.prioridad}
                      </span>
                    </div>
                    <h4 className="text-sm font-bold text-slate-800 mb-1">{t.equipo}</h4>
                    <p className="text-xs text-slate-500 mb-3"><MapPin className="w-3 h-3 inline mr-1"/>{t.centro}</p>
                  </div>
                ))}
              </div>
            </div>
          )
        })}
      </div>
    </div>
  );
};

const InsightsScreen = () => (
  <div className="space-y-6 fade-in">
     <div>
      <h2 className="text-2xl font-bold text-slate-800 flex items-center space-x-2">
        <BrainCircuit className="w-6 h-6 text-indigo-600" />
        <span>Insights & IA</span>
      </h2>
      <p className="text-sm text-slate-500">Recomendaciones predictivas generadas automáticamente.</p>
    </div>

    <div className="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-3 gap-6">
      {mockInsights.map(ins => (
        <div key={ins.id} className={`bg-white rounded-xl shadow-sm border-t-4 ${ins.color} border-x border-b border-slate-200 overflow-hidden hover:shadow-lg transition-all`}>
          <div className={`p-4 ${ins.bg} flex items-start justify-between border-b border-slate-100`}>
            <div className="flex items-center space-x-3">
              <div className={`p-2 bg-white rounded-lg shadow-sm ${ins.color.replace('border', 'text')}`}>
                <ins.icon className="w-5 h-5" />
              </div>
              <div>
                <h3 className="font-bold text-slate-800">{ins.equipo}</h3>
                <p className="text-xs text-slate-500">{ins.centro}</p>
              </div>
            </div>
          </div>
          <div className="p-5 space-y-4">
            <p className="text-sm text-slate-700 font-medium">{ins.descripcion}</p>
            <div className="bg-slate-50 p-3 rounded-lg border border-slate-100">
              <p className="text-xs font-bold text-slate-500 uppercase mb-1">Impacto Operativo</p>
              <p className="text-sm text-slate-800">{ins.impacto}</p>
            </div>
            <div>
              <p className="text-xs font-bold text-indigo-600 uppercase mb-1">Acción Sugerida</p>
              <p className="text-sm font-semibold text-slate-800">{ins.accion}</p>
            </div>
          </div>
        </div>
      ))}
    </div>
  </div>
);

const ExecutiveDashboardScreen = () => (
  <div className="space-y-6 fade-in">
     <div>
      <h2 className="text-2xl font-bold text-slate-800">KPIs & Métricas</h2>
      <p className="text-sm text-slate-500">Métricas globales de gestión y disponibilidad.</p>
    </div>

    <div className="grid grid-cols-1 lg:grid-cols-3 gap-6">
      <div className="lg:col-span-2 bg-white p-6 rounded-xl shadow-sm border border-slate-100">
        <h3 className="text-lg font-bold text-slate-800 mb-4">Evolución de Disponibilidad Operativa (%)</h3>
        <div className="h-72">
          <ResponsiveContainer width="100%" height="100%">
            <AreaChart data={kpiData}>
              <defs>
                <linearGradient id="colorDisp" x1="0" y1="0" x2="0" y2="1">
                  <stop offset="5%" stopColor="#4f46e5" stopOpacity={0.3}/>
                  <stop offset="95%" stopColor="#4f46e5" stopOpacity={0}/>
                </linearGradient>
              </defs>
              <CartesianGrid strokeDasharray="3 3" vertical={false} stroke="#e2e8f0" />
              <XAxis dataKey="name" axisLine={false} tickLine={false} tick={{fill: '#64748b', fontSize: 12}} />
              <YAxis domain={[90, 100]} axisLine={false} tickLine={false} tick={{fill: '#64748b', fontSize: 12}} />
              <RechartsTooltip contentStyle={{ borderRadius: '8px', border: 'none', boxShadow: '0 4px 6px -1px rgb(0 0 0 / 0.1)' }} />
              <Area type="monotone" dataKey="disp" stroke="#4f46e5" fillOpacity={1} fill="url(#colorDisp)" strokeWidth={3} />
            </AreaChart>
          </ResponsiveContainer>
        </div>
      </div>

      <div className="bg-white p-6 rounded-xl shadow-sm border border-slate-100">
        <h3 className="text-lg font-bold text-slate-800 mb-4">Fallas por Fabricante</h3>
        <div className="h-64 relative flex justify-center items-center">
          <ResponsiveContainer width="100%" height="100%">
            <PieChart>
              <Pie data={donutData} innerRadius={60} outerRadius={80} paddingAngle={5} dataKey="value">
                {donutData.map((entry, index) => (
                  <Cell key={`cell-${index}`} fill={entry.color} />
                ))}
              </Pie>
              <RechartsTooltip />
              <Legend verticalAlign="bottom" height={36} iconType="circle" />
            </PieChart>
          </ResponsiveContainer>
        </div>
      </div>
      
      {/* MTTR / MTBF Cards */}
      <div className="bg-indigo-600 rounded-xl shadow-lg p-6 text-white flex flex-col justify-center">
         <h4 className="text-indigo-200 text-sm font-semibold uppercase mb-1">MTTR (Mean Time To Repair)</h4>
         <div className="flex items-end space-x-3">
           <span className="text-5xl font-bold">14.2</span>
           <span className="text-indigo-200 text-lg mb-1">horas</span>
         </div>
      </div>

      <div className="bg-white rounded-xl shadow-sm border border-slate-100 p-6 flex flex-col justify-center">
         <h4 className="text-slate-500 text-sm font-semibold uppercase mb-1">MTBF (Mean Time Between Failures)</h4>
         <div className="flex items-end space-x-3">
           <span className="text-5xl font-bold text-slate-800">128</span>
           <span className="text-slate-500 text-lg mb-1">días</span>
         </div>
      </div>
    </div>
  </div>
);

const MapScreen = () => (
  <div className="space-y-6 fade-in h-[calc(100vh-140px)] flex flex-col">
     <div>
      <h2 className="text-2xl font-bold text-slate-800">Mapa de Sucursales</h2>
      <p className="text-sm text-slate-500">Monitor geográfico de estado y disponibilidad por centro médico.</p>
    </div>

    <div className="flex-1 flex flex-col md:flex-row gap-4 overflow-hidden">
      {/* Panel Izquierdo: Mapa Visual */}
      <div className="flex-1 bg-slate-200 rounded-xl border border-slate-300 relative overflow-hidden flex items-center justify-center shadow-inner">
        <div className="absolute inset-0 bg-[#e5e7eb] opacity-50" style={{ backgroundImage: 'radial-gradient(#9ca3af 1px, transparent 1px)', backgroundSize: '20px 20px' }}></div>
        <svg className="absolute inset-0 w-full h-full text-slate-300 opacity-40" preserveAspectRatio="none" viewBox="0 0 100 100">
           <path d="M10,20 Q30,10 50,30 T90,20 M20,50 Q40,60 60,40 T80,80 M10,80 Q30,90 50,70 T90,60" stroke="currentColor" strokeWidth="0.5" fill="none" />
        </svg>

        {/* Map Pins */}
        <div className="absolute top-1/4 left-1/4 group z-10">
          <div className="relative">
            <div className="w-6 h-6 bg-emerald-500 rounded-full border-4 border-white shadow-lg animate-bounce cursor-pointer relative"></div>
            <div className="absolute -inset-2 bg-emerald-500 rounded-full animate-ping opacity-20 z-0"></div>
          </div>
        </div>
      </div>

      {/* Panel Derecho: Lista de Sucursales */}
      <div className="w-full md:w-80 bg-white rounded-xl border border-slate-200 shadow-sm overflow-y-auto p-4 flex flex-col shrink-0">
        <h3 className="font-bold text-slate-800 mb-4 flex items-center"><MapPin className="w-5 h-5 mr-2 text-indigo-600"/> Directorio de Sedes</h3>
        <div className="space-y-3">
          {[
            { n: 'Centro Palermo', d: '99.2%', st: 'bg-emerald-500', eq: 12 },
            { n: 'Hospital Central', d: '82.0%', st: 'bg-orange-400', eq: 24 },
            { n: 'Instituto Oncológico', d: '75.0%', st: 'bg-rose-500', eq: 5 },
          ].map((sede, idx) => (
            <div key={idx} className="p-3 border border-slate-100 rounded-lg hover:bg-slate-50 transition-colors cursor-pointer group">
              <div className="flex items-center space-x-2 mb-1">
                <div className={`w-2.5 h-2.5 rounded-full ${sede.st}`}></div>
                <h4 className="text-sm font-bold text-slate-700 group-hover:text-indigo-600">{sede.n}</h4>
              </div>
              <div className="flex justify-between items-center text-xs text-slate-500 ml-4.5">
                 <span>{sede.eq} equipos</span>
                 <span className={`font-bold ${sede.st.replace('bg-', 'text-')}`}>Disp. {sede.d}</span>
              </div>
            </div>
          ))}
        </div>
      </div>
    </div>
  </div>
);

const CalendarScreen = () => {
  const days = Array.from({length: 30}, (_, i) => i + 1);
  return (
    <div className="space-y-6 fade-in h-full flex flex-col">
       <div className="flex justify-between items-end">
        <div>
          <h2 className="text-2xl font-bold text-slate-800">Calendario de Mantenimientos</h2>
          <p className="text-sm text-slate-500">Planificación de PMs y vencimientos de contratos.</p>
        </div>
      </div>

      <div className="flex-1 bg-white border border-slate-200 rounded-xl shadow-sm overflow-hidden flex flex-col">
         <div className="grid grid-cols-7 border-b border-slate-200 bg-slate-50">
            {['Lun', 'Mar', 'Mié', 'Jue', 'Vie', 'Sáb', 'Dom'].map(d => (
              <div key={d} className="py-3 text-center text-xs font-bold text-slate-500 uppercase">{d}</div>
            ))}
         </div>
         <div className="flex-1 grid grid-cols-7 grid-rows-5 gap-px bg-slate-200">
            {days.map(d => {
              const hasPM = d === 12;
              const isToday = d === 24;
              return (
                <div key={d} className={`bg-white p-2 min-h-[100px] hover:bg-slate-50 transition-colors ${isToday ? 'ring-2 ring-inset ring-indigo-500' : ''}`}>
                  <div className={`text-sm font-semibold w-6 h-6 flex items-center justify-center rounded-full mb-2 ${isToday ? 'bg-indigo-600 text-white' : 'text-slate-700'}`}>{d}</div>
                  {hasPM && <div className="bg-indigo-100 text-indigo-700 text-[10px] font-bold px-2 py-1 rounded">PM Tomógrafo GE</div>}
                </div>
              )
            })}
         </div>
      </div>
    </div>
  );
};

const WizardTecnicoScreen = () => {
  const [step, setStep] = useState(1);
  const [centro, setCentro] = useState(null);
  const [equipo, setEquipo] = useState(null);

  const reset = () => { setStep(1); setCentro(null); setEquipo(null); };

  if (step === 4) {
    return (
      <div className="h-full flex flex-col items-center justify-center fade-in text-center p-6">
        <div className="w-20 h-20 bg-emerald-100 text-emerald-600 rounded-full flex items-center justify-center mb-6">
          <CheckCircle className="w-10 h-10" />
        </div>
        <h2 className="text-2xl font-bold text-slate-800 mb-2">Reporte Enviado</h2>
        <p className="text-slate-500 mb-8 max-w-md">El ticket para {equipo.nombre} ha sido generado exitosamente. El equipo de ingeniería ya fue notificado.</p>
        <button onClick={reset} className="bg-slate-900 text-white px-6 py-3 rounded-xl font-bold hover:bg-slate-800 transition-all">Volver al Inicio</button>
      </div>
    );
  }

  return (
    <div className="max-w-2xl mx-auto space-y-8 fade-in pb-10">
      <div className="text-center">
        <h2 className="text-3xl font-bold text-slate-800">Reportar Falla</h2>
        <p className="text-slate-500 mt-2">Siga los pasos para generar el reporte de servicio.</p>
      </div>

      {/* Progress Bar */}
      <div className="flex items-center justify-center space-x-4 mb-8">
        {[1, 2, 3].map(i => (
          <div key={i} className="flex items-center">
            <div className={`w-8 h-8 rounded-full flex items-center justify-center font-bold text-sm ${step === i ? 'bg-indigo-600 text-white ring-4 ring-indigo-100' : step > i ? 'bg-emerald-500 text-white' : 'bg-slate-200 text-slate-400'}`}>
              {step > i ? <CheckCircle className="w-4 h-4"/> : i}
            </div>
            {i < 3 && <div className={`w-12 h-1 ${step > i ? 'bg-emerald-500' : 'bg-slate-200'} mx-2 rounded`}></div>}
          </div>
        ))}
      </div>

      {/* Step 1: Center Selection */}
      {step === 1 && (
        <div className="space-y-4 fade-in">
          <h3 className="text-lg font-bold text-slate-700 text-center mb-6">¿En qué sucursal te encuentras?</h3>
          <div className="grid grid-cols-1 sm:grid-cols-2 gap-4">
            {['Centro Palermo', 'Clínica Suizo', 'Instituto Oncológico', 'Hospital Central'].map(c => (
              <button key={c} onClick={() => { setCentro(c); setStep(2); }} className="p-6 bg-white border-2 border-slate-200 rounded-xl hover:border-indigo-500 hover:bg-indigo-50 transition-all text-left group">
                <MapPin className="w-6 h-6 text-slate-400 group-hover:text-indigo-600 mb-3" />
                <h4 className="font-bold text-slate-800 text-lg group-hover:text-indigo-700">{c}</h4>
              </button>
            ))}
          </div>
        </div>
      )}

      {/* Step 2: Equipment Selection */}
      {step === 2 && (
        <div className="space-y-4 fade-in">
          <div className="flex justify-between items-center mb-6">
            <button onClick={() => setStep(1)} className="text-sm font-semibold text-indigo-600 hover:text-indigo-800 flex items-center"><ArrowRight className="w-4 h-4 mr-1 rotate-180" /> Atrás</button>
            <h3 className="text-lg font-bold text-slate-700">Selecciona el equipo</h3>
          </div>
          <div className="grid grid-cols-1 gap-3">
            {mockEquipos.filter(e => e.centro === centro).map(eq => (
              <button key={eq.id} onClick={() => { setEquipo(eq); setStep(3); }} className="p-4 bg-white border-2 border-slate-200 rounded-xl hover:border-indigo-500 hover:bg-indigo-50 transition-all flex items-center justify-between text-left group">
                <div>
                  <h4 className="font-bold text-slate-800 group-hover:text-indigo-700">{eq.nombre}</h4>
                  <p className="text-sm text-slate-500">SN: {eq.serie} | {eq.fabricante}</p>
                </div>
                <ArrowRight className="w-5 h-5 text-slate-300 group-hover:text-indigo-500" />
              </button>
            ))}
          </div>
        </div>
      )}

      {/* Step 3: Issue Description */}
      {step === 3 && (
        <div className="space-y-6 fade-in bg-white p-6 rounded-2xl shadow-sm border border-slate-200">
          <div className="flex justify-between items-center border-b border-slate-100 pb-4">
             <button onClick={() => setStep(2)} className="text-sm font-semibold text-indigo-600 hover:text-indigo-800 flex items-center"><ArrowRight className="w-4 h-4 mr-1 rotate-180" /> Atrás</button>
             <span className="text-xs font-bold bg-indigo-100 text-indigo-700 px-3 py-1 rounded-full uppercase flex items-center"><Lock className="w-3 h-3 mr-1"/> Selección Bloqueada</span>
          </div>
          
          <div className="bg-slate-50 p-4 rounded-lg flex items-center space-x-4 border border-slate-100">
             <div className="p-3 bg-white rounded-lg shadow-sm text-slate-400"><Database className="w-6 h-6" /></div>
             <div>
               <p className="text-sm font-bold text-slate-800">{equipo.nombre}</p>
               <p className="text-xs text-slate-500">{centro} - SN: {equipo.serie}</p>
             </div>
          </div>

          <div>
             <label className="block text-sm font-bold text-slate-700 mb-2">Descripción del problema *</label>
             <textarea rows="4" className="w-full border-2 border-slate-200 rounded-xl p-3 text-sm focus:border-indigo-500 focus:ring-0 outline-none transition-colors" placeholder="Describa el error que muestra en pantalla o el problema físico..."></textarea>
          </div>

          <div className="grid grid-cols-2 gap-4">
             <button className="flex flex-col items-center justify-center p-4 border-2 border-dashed border-slate-300 rounded-xl text-slate-500 hover:bg-slate-50 hover:border-indigo-400 hover:text-indigo-600 transition-colors">
               <Camera className="w-6 h-6 mb-2" />
               <span className="text-sm font-bold">Tomar Foto</span>
             </button>
             <button className="flex flex-col items-center justify-center p-4 border-2 border-dashed border-slate-300 rounded-xl text-slate-500 hover:bg-slate-50 hover:border-indigo-400 hover:text-indigo-600 transition-colors">
               <Paperclip className="w-6 h-6 mb-2" />
               <span className="text-sm font-bold">Adjuntar Archivo</span>
             </button>
          </div>

          <button onClick={() => setStep(4)} className="w-full bg-rose-600 text-white py-4 rounded-xl font-bold shadow-md hover:bg-rose-700 transition-all flex items-center justify-center text-lg">
             Enviar Reporte de Falla
          </button>
        </div>
      )}
    </div>
  );
};


export default function App() {
  const [userRole, setUserRole] = useState(null);
  const [currentView, setCurrentView] = useState('dashboard');
  const [selectedEquipo, setSelectedEquipo] = useState(null);
  const [isSidebarOpen, setIsSidebarOpen] = useState(true);

  useEffect(() => {
    if (userRole === 'ingeniero') setCurrentView('equipos');
    if (userRole === 'tecnico') setCurrentView('dashboard');
    if (userRole === 'gerente') setCurrentView('dashboard');
  }, [userRole]);

  const navigate = (view, data = null) => {
    setCurrentView(view);
    if (data) setSelectedEquipo(data);
  };

  if (!userRole) return <LoginScreen onLogin={setUserRole} />;

  let menuItems = [];
  if (userRole === 'gerente') {
    menuItems = [
      { id: 'dashboard', label: 'Monitor Principal', icon: LayoutDashboard },
      { id: 'ejecutivo', label: 'KPIs & Métricas', icon: PieChartIcon },
      { id: 'equipos', label: 'Parque Tecnológico', icon: Activity },
      { id: 'tickets', label: 'Monitor de Tickets', icon: ClipboardList },
      { id: 'mapa', label: 'Mapa de Sucursales', icon: Map },
      { id: 'calendario', label: 'Calendario', icon: CalendarIcon },
      { id: 'insights', label: 'Insights AI', icon: BrainCircuit, badge: '4' },
    ];
  } else if (userRole === 'ingeniero') {
    menuItems = [
      { id: 'equipos', label: 'Parque Tecnológico', icon: Activity },
      { id: 'tickets', label: 'Gestión Tickets', icon: ClipboardList },
      { id: 'calendario', label: 'Mantenimientos', icon: CalendarIcon },
    ];
  } else if (userRole === 'tecnico') {
    menuItems = [
      { id: 'dashboard', label: 'Mi Panel', icon: Home },
    ];
  }

  return (
    <div className="min-h-screen bg-slate-50 flex overflow-hidden text-slate-800 font-sans">
      <style dangerouslySetInnerHTML={{__html: `
        .fade-in { animation: fadeIn 0.3s ease-in-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(5px); } to { opacity: 1; transform: translateY(0); } }
      `}} />

      {/* Sidebar */}
      <aside className={`${isSidebarOpen ? 'w-64' : 'w-20'} bg-slate-900 text-slate-300 transition-all duration-300 flex flex-col z-20 shadow-xl shrink-0`}>
        <div className="h-16 flex items-center justify-between px-4 border-b border-slate-800">
          {isSidebarOpen ? (
             <div className="flex items-center space-x-2 text-white">
               <div className="bg-indigo-600 p-1.5 rounded-lg"><Activity className="w-5 h-5" /></div>
               <span className="font-bold text-xl tracking-tight">SGMS</span>
             </div>
          ) : (
            <div className="mx-auto bg-indigo-600 p-1.5 rounded-lg text-white"><Activity className="w-5 h-5" /></div>
          )}
        </div>

        <nav className="flex-1 py-6 px-3 space-y-1 overflow-y-auto">
          {menuItems.map(item => (
            <button
              key={item.id}
              onClick={() => navigate(item.id)}
              className={`w-full flex items-center ${isSidebarOpen ? 'justify-between px-3' : 'justify-center'} py-3 rounded-lg transition-colors group ${currentView === item.id ? 'bg-indigo-600/10 text-indigo-400 font-semibold' : 'hover:bg-slate-800 hover:text-white'}`}
              title={!isSidebarOpen ? item.label : ''}
            >
              <div className="flex items-center space-x-3">
                <item.icon className={`w-5 h-5 ${currentView === item.id ? 'text-indigo-400' : 'text-slate-400 group-hover:text-white'}`} />
                {isSidebarOpen && <span>{item.label}</span>}
              </div>
              {isSidebarOpen && item.badge && (
                <span className="bg-rose-500 text-white text-[10px] font-bold px-2 py-0.5 rounded-full">{item.badge}</span>
              )}
            </button>
          ))}
        </nav>

        <div className="p-4 border-t border-slate-800">
          <button onClick={() => setUserRole(null)} className="w-full flex items-center justify-center p-2 rounded-lg bg-slate-800 hover:bg-rose-600 hover:text-white transition-colors text-sm font-semibold">
            {isSidebarOpen ? 'Cerrar Sesión' : <X className="w-5 h-5" />}
          </button>
        </div>
      </aside>

      {/* Main Content */}
      <main className="flex-1 flex flex-col h-screen overflow-hidden relative">
        <header className="h-16 bg-white border-b border-slate-200 flex items-center justify-between px-6 z-10 shrink-0">
          <div className="flex items-center space-x-4">
             <button onClick={() => setIsSidebarOpen(!isSidebarOpen)} className="text-slate-500 hover:text-indigo-600 transition-colors hidden lg:block"><Menu className="w-5 h-5" /></button>
             <h1 className="text-lg font-bold text-slate-800 hidden sm:block">
               {menuItems.find(i => i.id === currentView)?.label || currentView.replace('-', ' ')}
             </h1>
          </div>

          <div className="flex items-center space-x-4">
            <span className="text-xs font-bold uppercase bg-slate-100 text-slate-600 px-3 py-1 rounded-full shadow-inner border border-slate-200">
              Rol: {userRole}
            </span>
            <button className="relative p-2 text-slate-500 hover:text-indigo-600 hover:bg-indigo-50 rounded-full transition-colors">
              <Bell className="w-5 h-5" />
              <span className="absolute top-1 right-1 w-2.5 h-2.5 bg-rose-500 border-2 border-white rounded-full"></span>
            </button>
          </div>
        </header>

        <div className="flex-1 overflow-y-auto p-4 sm:p-6 bg-slate-50/50">
          <div className="max-w-7xl mx-auto h-full">
            {/* Conditional Rendering based on Role and View */}
            {userRole === 'tecnico' ? (
               <WizardTecnicoScreen />
            ) : (
              <>
                {currentView === 'dashboard' && <DashboardScreen navigate={navigate} role={userRole} />}
                {currentView === 'equipos' && <EquiposScreen navigate={navigate} role={userRole} />}
                {currentView === 'equipo' && <EquipoScreen equipo={selectedEquipo} onBack={() => navigate(userRole === 'gerente' ? 'dashboard' : 'equipos')} />}
                {currentView === 'tickets' && <TicketsScreen role={userRole} />}
                {currentView === 'mapa' && <MapScreen />}
                {currentView === 'calendario' && <CalendarScreen />}
                {currentView === 'ejecutivo' && <ExecutiveDashboardScreen />}
                {currentView === 'insights' && <InsightsScreen />}
              </>
            )}
          </div>
        </div>
      </main>
    </div>
  );
}