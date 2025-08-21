<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Freekshot Scoreboard</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- React, ReactDOM, and Babel for in-browser JSX transformation -->
    <script src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <style>
        body, html, #root { margin: 0; padding: 0; font-family: Segoe UI, Roboto, Helvetica, Arial, Apple SD Gothic Neo, Noto Sans KR, sans-serif; }
        /* OBS/캡처 모드일 때 배경을 완전히 투명하게 만듭니다. */
        .transparent-mode, .transparent-mode #root { background-color: transparent !important; }
        .board-wrapper { padding: 20px; /* 날개가 잘리지 않도록 충분한 여백 확보 */ }
        .board{min-width:520px;max-width:960px;pointer-events:auto;position:relative;padding:10px 16px;border-radius:20px;display:flex;flex-direction:column;align-items:center; color:#e9f1ff;}
        .sc1{background:linear-gradient(180deg,rgba(0,0,0,.72),rgba(0,0,0,.46));border:1px solid rgba(59,214,255,.35);box-shadow:inset 0 0 0 1px rgba(59,214,255,.12),0 8px 22px rgba(0,0,0,.35);backdrop-filter:saturate(120%) blur(2px)}
        .clear{background:transparent;border:none;box-shadow:none;backdrop-filter:none}
        .solid{background:rgba(0,0,0,0.6);border:1px solid rgba(255,255,255,.18);backdrop-filter:none}
        .glass{background:rgba(0,0,0,0.28);border:1px solid rgba(255,255,255,.15);backdrop-filter:saturate(140%) blur(6px)}
        .sc1:before,.sc1:after{content:"";position:absolute;height:3px;left:12px;right:12px;background:linear-gradient(90deg,transparent,var(--accent),transparent);opacity:.9;pointer-events:none}
        .sc1:before{top:4px}.sc1:after{bottom:4px}
        .wing{position:absolute;top:6px;bottom:6px;width:10px;pointer-events:none;filter:drop-shadow(0 2px 8px rgba(0,0,0,.6))}
        .wing.left{left:-8px;clip-path:polygon(0 0,100% 8px,100% calc(100% - 8px),0 100%)}
        .wing.right{right:-8px;clip-path:polygon(100% 0,0 8px,0 calc(100% - 8px),100% 100%)}
        .title .pill.series-glow--soft{ text-shadow:0 0 4px var(--accent, #3bd6ff),0 0 10px var(--accent, #3bd6ff))}
        .title .pill.series-glow--medium{ text-shadow:0 0 6px var(--accent, #3bd6ff),0 0 16px var(--accent, #3bd6ff))}
        .title .pill.series-glow--strong{ text-shadow:0 0 8px var(--accent, #3bd6ff),0 0 22px var(--accent, #3bd6ff))}
        .title .pill.series-glow--neon{ text-shadow:0 0 10px var(--accent, #3bd6ff),0 0 28px var(--accent, #3bd6ff),0 0 42px var(--accent, #3bd6ff))}
        .logo{border:1px solid; border-radius:10px;background:#0b0e12;position:relative;overflow:hidden;box-shadow:inset 0 0 10px rgba(59,214,255,.15)}
        .logo img { filter: brightness(1.75) contrast(1.1); }
        .team{text-shadow:0 0 6px rgba(0,214,255,.25)}
        .vs:before{content:"";position:absolute;inset:0;border:1px solid rgba(59,214,255,.35);border-radius:6px;clip-path:polygon(8% 0,92% 0,100% 50%,92% 100%,8% 100%,0 50%);background:linear-gradient(180deg,rgba(59,214,255,.08),rgba(59,214,255,.02))}
        .num{background:linear-gradient(180deg,rgba(0,214,255,.18),rgba(0,214,255,.04));border:1px solid rgba(0,214,255,.38);box-shadow:inset 0 0 10px rgba(0,214,255,.25),0 2px 10px rgba(0,0,0,.35)}
        .dot{border:1px solid rgba(0,214,255,.45);background:rgba(0,214,255,.08)}
        .dot.on{background:rgba(0,214,255,.9)}
        .race-overlay{position:absolute;top:0;bottom:0;width:40%;opacity:var(--ov,0.12);filter:var(--ovFilter, none);mix-blend-mode:var(--ovBlend, normal);pointer-events:none;background-position:center;background-size:85% auto;background-repeat:no-repeat;z-index:1}
        .race-overlay.left{left:-4px}
        .race-overlay.right{right:-4px;transform:scaleX(-1)}
        .race-box { display:inline-flex; align-items:center; justify-content:center; gap:8px; padding: 5px 12px; border-radius:999px; background-color: rgba(15, 20, 30, 0.5); border: 1px solid rgba(255, 255, 255, 0.15); backdrop-filter: blur(4px); box-shadow: inset 0 0 8px rgba(0,0,0,.35); }
        .race-box span { font-size: 1.3rem; line-height: 1; }
    </style>
</head>
<body id="body">
    
    <div id="root"></div>

    <script type="text/babel">
        const THEMES = { terran: '#ffcc66', protoss: '#3bd6ff', zerg: '#622884' };
        const RACE_COLORS = { T: '#0779b3', P: '#e8cd04', Z: '#622884' };
        const LINEUP_KEY = 'fs_lineup_v2';
        const RHOME_KEY = 'fs_roster_home_v2';
        const RAWAY_KEY = 'fs_roster_away_v2';
        const ACTIVE_KEY = 'fs_active_slot_v2';
        const OV_KEY = 'fs_overlay_urls_v1';
        const ICON_KEY = 'fs_race_icons_v1';

        const loadJSON = (key, def) => { try { const t = localStorage.getItem(key); return t ? JSON.parse(t) : def; } catch (e) { return def; } };
        const saveJSON = (key, val) => { try { localStorage.setItem(key, JSON.stringify(val)); } catch (e) { console.error(e); } };

        const Scoreboard = ({ state }) => {
            const { theme, c1, c2, overlays, w, series, sg, l1, l2, s1, s2, sets, lineup, activeSlot, rosterHome, rosterAway, icons, style } = state;
            const currentPair = lineup[activeSlot - 1] || { h: '', a: '', spL: '', spR: '' };
            const team1 = rosterHome.find(p => p.name === currentPair.h) || { name: currentPair.h, race: '' };
            const team2 = rosterAway.find(p => p.name === currentPair.a) || { name: currentPair.a, race: '' };
            const boardStyle = { '--accent': THEMES[theme], '--c1': c1, '--c2': c2, '--ov': overlays.opacity, minWidth: '520px', maxWidth: '960px', ...(w && { minWidth: 'unset', maxWidth: 'unset', width: /vw|%|px$/.test(w) ? w : `${w}px` }) };
            const team1NameRef = React.useRef(null);
            const team2NameRef = React.useRef(null);
            React.useEffect(() => {
              const checkOverflow = (ref) => {
                if (ref.current) {
                  ref.current.style.fontSize = '';
                  const parentWidth = ref.current.parentElement.offsetWidth;
                  let currentSize = parseFloat(getComputedStyle(ref.current).fontSize);
                  while (ref.current.scrollWidth > parentWidth && currentSize > 10) { currentSize -= 1; ref.current.style.fontSize = `${currentSize}px`; }
                }
              };
              checkOverflow(team1NameRef);
              checkOverflow(team2NameRef);
            }, [team1.name, team2.name, w]);
            const normalizeSets = s => s ? s.toUpperCase().replace(/\s+/g, '').split('').map(ch => ch === 'L' || ch === '1' ? 'L' : (ch === 'R' || ch === '2' ? 'R' : null)).filter(Boolean) : [];
            const getGlowClass = glow => `series-glow--${glow || 'strong'}`;
            return (
                <div className={`board ${style}`} style={boardStyle}>
                    <i className="wing left" style={{ background: `linear-gradient(180deg, color-mix(in srgb,${c1} 85%,transparent), color-mix(in srgb,${c1} 35%,transparent))` }} />
                    <i className="wing right" style={{ background: `linear-gradient(180deg, color-mix(in srgb,${c2} 85%,transparent), color-mix(in srgb,${c2} 35%,transparent))` }} />
                    <div className="race-overlay left" style={{ backgroundImage: `url('${overlays[team1.race]}')`, mixBlendMode: overlays.mode.includes('screen') ? 'screen' : 'normal', filter: overlays.mode.includes('mono') ? 'grayscale(1) brightness(1.15)' : 'none' }} />
                    <div className="race-overlay right" style={{ backgroundImage: `url('${overlays[team2.race]}')`, mixBlendMode: overlays.mode.includes('screen') ? 'screen' : 'normal', filter: overlays.mode.includes('mono') ? 'grayscale(1) brightness(1.15)' : 'none' }} />
                    <div className="topbar w-full grid grid-cols-[1fr_auto_1fr] items-center mb-1.5 relative z-10">
                        <div className="flex justify-start">{l1 && <div className="logo w-14 h-14" style={{ borderColor: c1 }}><img src={l1} alt="Logo 1" className="w-full h-full object-contain" /></div>}</div>
                        <div className="title text-xs uppercase font-semibold text-gray-400 tracking-widest flex items-center justify-center gap-2"><span className={`pill px-2 py-1 rounded-full border text-white text-2xl font-black bg-gradient-to-b from-blue-400/20 to-blue-400/10 shadow-inner shadow-blue-400/40 ${getGlowClass(sg)}`} style={{borderColor: 'var(--accent)'}}>{series}</span></div>
                        <div className="flex justify-end">{l2 && <div className="logo w-14 h-14" style={{ borderColor: c2 }}><img src={l2} alt="Logo 2" className="w-full h-full object-contain" /></div>}</div>
                    </div>
                    <div className="scoreline w-full flex justify-center items-center gap-3 relative z-10">
                        <div className="flex items-center justify-end gap-2 flex-1 min-w-0">
                            <div ref={team1NameRef} className="team text-[1.625rem] font-black text-white whitespace-nowrap overflow-hidden text-ellipsis text-right">{team1.name}</div>
                            <div className="race-box"><span className="font-bold" style={{color: RACE_COLORS[team1.race]}}>{team1.race}</span>{currentPair.spL && <span className="font-bold" style={{ color: c1 }}>{currentPair.spL}</span>}</div>
                            {icons[team1.race] && <img src={icons[team1.race]} alt={`${team1.race} icon`} className="w-5 h-5 opacity-95" />}
                        </div>
                        <div className="num text-center text-[2rem] font-black text-white px-3 py-1 rounded-xl">{s1}</div>
                        <div className="vs text-sm font-black uppercase text-gray-300 tracking-widest px-2 py-1 rounded-md">VS</div>
                        <div className="num text-center text-[2rem] font-black text-white px-3 py-1 rounded-xl">{s2}</div>
                        <div className="flex items-center justify-start gap-2 flex-1 min-w-0">
                            {icons[team2.race] && <img src={icons[team2.race]} alt={`${team2.race} icon`} className="w-5 h-5 opacity-95" />}
                            <div className="race-box"><span className="font-bold" style={{color: RACE_COLORS[team2.race]}}>{team2.race}</span>{currentPair.spR && <span className="font-bold" style={{ color: c2 }}>{currentPair.spR}</span>}</div>
                            <div ref={team2NameRef} className="team text-[1.625rem] font-black text-white whitespace-nowrap overflow-hidden text-ellipsis text-left">{team2.name}</div>
                        </div>
                    </div>
                    <div className="setsline w-full flex justify-between mt-1 relative z-10">
                        <div className="dots flex gap-1.5">{normalizeSets(sets).map((ch, i) => <div key={i} className={`dot w-1.5 h-1.5 rounded-sm ${ch === 'L' ? 'on' : ''}`}></div>)}</div>
                        <div className="dots flex gap-1.5">{normalizeSets(sets).map((ch, i) => <div key={i} className={`dot w-1.5 h-1.5 rounded-sm ${ch === 'R' ? 'on' : ''}`}></div>)}</div>
                    </div>
                </div>
            );
        };
        
        const ControlPanel = React.memo(({ isVisible, state, setState, setPanelOpen }) => {
            const [rosterHomeName, setRosterHomeName] = React.useState('');
            const [rosterAwayName, setRosterAwayName] = React.useState('');
            const [rosterHomeRace, setRosterHomeRace] = React.useState('T');
            const [rosterAwayRace, setRosterAwayRace] = React.useState('P');
            const [localSeries, setLocalSeries] = React.useState(state.series);
            React.useEffect(() => { setLocalSeries(state.series); }, [state.series]);
            
            const handleFilePicker = (callback) => {
                const input = document.createElement('input');
                input.type = 'file'; input.accept = 'image/*';
                input.onchange = (e) => { const file = e.target.files?.[0]; if (file) callback(URL.createObjectURL(file)); input.remove(); };
                input.click();
            };

            const handleAddPlayer = (side) => {
                const name = (side === 'home' ? rosterHomeName : rosterAwayName).trim();
                const race = side === 'home' ? rosterHomeRace : rosterAwayRace;
                if (!name) return;
                const rosterKey = side === 'home' ? 'rosterHome' : 'rosterAway';
                const roster = state[rosterKey];
                if (roster.some(p => p.name === name)) return;
                setState(prevState => ({ ...prevState, [rosterKey]: [...roster, { name, race }] }));
                side === 'home' ? setRosterHomeName('') : setRosterAwayName('');
            };
            const handleBulkClear = (side) => setState(prevState => ({ ...prevState, [side === 'home' ? 'rosterHome' : 'rosterAway']: [] }));
            const applySlot = React.useCallback((slot) => setState(prevState => ({ ...prevState, activeSlot: slot })), [setState]);
            const handleLineupChange = React.useCallback((slotIndex, side, name) => setState(prevState => ({ ...prevState, lineup: prevState.lineup.map((s, i) => i === slotIndex ? { ...s, [side]: name } : s) })), [setState]);
            const handleClearLineupSlot = React.useCallback((slotIndex) => setState(prevState => ({ ...prevState, lineup: prevState.lineup.map((s, i) => i === slotIndex ? { ...s, h: '', a: '' } : s) })), [setState]);
            const handleSpClick = React.useCallback((side, value) => {
                const slotIndex = state.activeSlot - 1;
                setState(prevState => ({ ...prevState, lineup: prevState.lineup.map((s, i) => i === slotIndex ? { ...s, [side]: s[side] === value ? '' : value } : s) }));
            }, [state.activeSlot, setState]);
            
            return (
                <div className="fixed top-4 right-4 z-[2147483647] bg-gray-900/95 border border-white/10 rounded-xl shadow-2xl backdrop-blur-md p-4 min-w-[640px] text-white max-h-[calc(100vh-32px)] overflow-auto resize transition-opacity duration-300" style={{opacity:isVisible?1:0, pointerEvents:isVisible?'auto':'none'}}>
                    <h3 className="text-xs uppercase font-semibold text-gray-400 tracking-widest sticky top-0 bg-gray-900/95 z-10 py-1 flex justify-center">Overlay Controls
                        <button className="absolute top-1/2 -translate-y-1/2 right-3 w-7 h-7 flex items-center justify-center border border-gray-700 rounded-md bg-gray-800 text-white cursor-pointer hover:border-blue-400" onClick={()=>setPanelOpen(false)}>✕</button>
                    </h3>
                    
                    <div className="grid grid-cols-[160px_1fr] gap-2 items-center my-1.5">
                        <label>타이틀</label>
                        <input className="bg-gray-800 border border-gray-700 text-white p-2 rounded-md" value={localSeries} onChange={(e)=>setLocalSeries(e.target.value)} onBlur={()=> setState(p=>({...p, series: localSeries})) } />
                    </div>
                    <div className="grid grid-cols-[160px_1fr] gap-2 items-center my-1.5">
                        <label>Series Glow</label>
                        <select className="bg-gray-800 border border-gray-700 text-white p-2 rounded-md" value={state.sg} onChange={(e)=> setState(p=>({...p, sg: e.target.value}))}>
                            <option value="soft">Soft</option>
                            <option value="medium">Medium</option>
                            <option value="strong">Strong</option>
                            <option value="neon">Neon</option>
                        </select>
                    </div>
                    <div className="grid grid-cols-[160px_1fr] gap-2 items-center my-1.5">
                        <label>좌/우 색</label>
                        <div className="flex gap-2">
                            <input type="color" className="p-1 rounded-md" value={state.c1} onInput={(e)=> setState(p=>({...p, c1: e.target.value}))} />
                            <input type="color" className="p-1 rounded-md" value={state.c2} onInput={(e)=> setState(p=>({...p, c2: e.target.value}))} />
                        </div>
                    </div>
                    <div className="grid grid-cols-[160px_1fr] gap-2 items-center my-1.5">
                        <label>Style</label>
                        <select className="bg-gray-800 border border-gray-700 text-white p-2 rounded-md" value={state.style} onChange={(e)=> setState(p=>({...p, style:e.target.value}))}>
                            <option value="sc1">sc1</option>
                            <option value="clear">clear</option>
                            <option value="glass">glass</option>
                            <option value="solid">solid</option>
                        </select>
                    </div>
                    <div className="grid grid-cols-[160px_1fr] gap-2 items-center my-1.5">
                        <label>Width</label>
                        <input className="bg-gray-800 border border-gray-700 text-white p-2 rounded-md" placeholder="880 or 50vw" value={state.w} onChange={(e)=> setState(p=>({...p, w:e.target.value}))} />
                    </div>
                    <div className="grid grid-cols-[160px_1fr] gap-2 items-center my-1.5">
                        <label>Top</label>
                        <input className="bg-gray-800 border border-gray-700 text-white p-2 rounded-md" placeholder="20 or 4vh" value={state.y} onChange={(e)=> setState(p=>({...p, y:e.target.value}))} />
                    </div>

                    <h3 className="text-xs uppercase font-semibold text-gray-400 tracking-widest my-4">로스터 빠른 추가</h3>
                    <div className="grid grid-cols-[160px_1fr] gap-2 items-center my-1.5">
                        <label>우리팀 추가</label>
                        <div className="flex gap-2 items-center">
                            <input placeholder="이름" className="bg-gray-800 border border-gray-700 text-white p-2 rounded-md min-w-[160px]" value={rosterHomeName} onChange={(e)=> setRosterHomeName(e.target.value)} onKeyDown={(e)=>{ if(e.key==='Enter') handleAddPlayer('home'); }} />
                            <div className="flex gap-1">
                                {['T','P','Z'].map(r=> (<button key={r} className={`px-2 py-1 rounded-md font-bold border ${rosterHomeRace===r? 'bg-blue-400 text-gray-900 border-blue-400':'text-gray-400 border-gray-700'}`} onClick={()=> setRosterHomeRace(r)}>{r}</button>))}
                            </div>
                            <button className="bg-blue-400 text-gray-900 font-bold px-3 py-2 rounded-md" onClick={()=> handleAddPlayer('home')}>추가</button>
                        </div>
                    </div>
                    <div className="grid grid-cols-[160px_1fr] gap-2 items-center my-1.5">
                        <label>상대팀 추가</label>
                        <div className="flex gap-2 items-center">
                            <input placeholder="이름" className="bg-gray-800 border border-gray-700 text-white p-2 rounded-md min-w-[160px]" value={rosterAwayName} onChange={(e)=> setRosterAwayName(e.target.value)} onKeyDown={(e)=>{ if(e.key==='Enter') handleAddPlayer('away'); }} />
                            <div className="flex gap-1">
                                {['T','P','Z'].map(r=> (<button key={r} className={`px-2 py-1 rounded-md font-bold border ${rosterAwayRace===r? 'bg-blue-400 text-gray-900 border-blue-400':'text-gray-400 border-gray-700'}`} onClick={()=> setRosterAwayRace(r)}>{r}</button>))}
                            </div>
                            <button className="bg-blue-400 text-gray-900 font-bold px-3 py-2 rounded-md" onClick={()=> handleAddPlayer('away')}>추가</button>
                        </div>
                    </div>
                    <div className="grid grid-cols-[160px_1fr] gap-2 items-center my-1.5">
                        <label>일괄삭제</label>
                        <div className="flex gap-2">
                            <button className="bg-red-800 text-red-200 font-bold px-3 py-2 rounded-md" onClick={()=> handleBulkClear('home')}>우리팀 전체삭제</button>
                            <button className="bg-red-800 text-red-200 font-bold px-3 py-2 rounded-md" onClick={()=> handleBulkClear('away')}>상대팀 전체삭제</button>
                        </div>
                    </div>

                    <h3 className="text-xs uppercase font-semibold text-gray-400 tracking-widest my-4">라인업 (1–9)</h3>
                    <div className="grid grid-cols-[160px_1fr] gap-2 items-center my-1.5">
                        <label>활성 슬롯</label>
                        <div className="flex gap-2 items-center">
                            <select className="bg-gray-800 border border-gray-700 text-white p-2 rounded-md" value={state.activeSlot} onChange={(e)=> applySlot(parseInt(e.target.value,10))}>
                                {Array.from({length:9},(_,i)=> <option key={i} value={i+1}>{i+1}</option>)}
                            </select>
                            <button className="bg-gray-800 border border-gray-700 text-white p-2 rounded-md" onClick={()=> applySlot(Math.max(1, state.activeSlot-1))}>◀ 이전</button>
                            <button className="bg-gray-800 border border-gray-700 text-white p-2 rounded-md" onClick={()=> applySlot(Math.min(9, state.activeSlot+1))}>다음 ▶</button>
                        </div>
                    </div>
                    <div className="grid grid-cols-[160px_1fr] gap-2 items-center my-1.5">
                        <label>SP(좌/우)</label>
                        <div className="flex gap-2 items-center">
                            {['1','5','7','11'].map(sp=> (<button key={`spL-${sp}`} className={`px-2 py-1 rounded-md text-sm border ${state.lineup[state.activeSlot-1]?.spL===sp? 'bg-blue-400 text-gray-900':'bg-gray-800 text-white border-gray-700'}`} onClick={()=> handleSpClick('spL', sp)}>L:{sp}</button>))}
                            <span className="w-3"></span>
                            {['1','5','7','11'].map(sp=> (<button key={`spR-${sp}`} className={`px-2 py-1 rounded-md text-sm border ${state.lineup[state.activeSlot-1]?.spR===sp? 'bg-blue-400 text-gray-900':'bg-gray-800 text-white border-gray-700'}`} onClick={()=> handleSpClick('spR', sp)}>R:{sp}</button>))}
                        </div>
                    </div>
                    <div className="border border-gray-700 rounded-md p-1 my-2 max-h-64 overflow-auto">
                        {state.lineup.map((pair, index)=> (
                            <div key={index} className="grid grid-cols-[28px_1fr_24px_1fr_auto_auto] gap-1 items-center p-1 border-b border-gray-700 last:border-b-0">
                                <span className="text-center opacity-75">{index+1}</span>
                                <select className="bg-gray-800 border border-gray-700 text-white p-1 rounded-md text-sm" value={pair.h || ''} onChange={(e)=> handleLineupChange(index,'h', e.target.value)}>
                                    <option value="">-</option>
                                    {state.rosterHome.map((p,i)=>(<option key={i} value={p.name}>{p.name} ({p.race})</option>))}
                                </select>
                                <span className="text-center opacity-70 text-sm">vs</span>
                                <select className="bg-gray-800 border border-gray-700 text-white p-1 rounded-md text-sm" value={pair.a || ''} onChange={(e)=> handleLineupChange(index,'a', e.target.value)}>
                                    <option value="">-</option>
                                    {state.rosterAway.map((p,i)=>(<option key={i} value={p.name}>{p.name} ({p.race})</option>))}
                                </select>
                                <button className="px-2 py-1 rounded-md text-xs bg-gray-800 border border-gray-700 text-white" onClick={()=> applySlot(index+1)}>적용</button>
                                <button className="px-2 py-1 rounded-md text-xs bg-gray-800 border border-gray-700 text-white" onClick={()=> handleClearLineupSlot(index)}>지움</button>
                            </div>
                        ))}
                    </div>

                    <h3 className="text-xs uppercase font-semibold text-gray-400 tracking-widest my-4">스코어 / 세트</h3>
                    <div className="grid grid-cols-[160px_1fr] gap-2 items-center my-1.5">
                        <label>Score 1</label>
                        <div className="flex gap-2 items-center">
                            <button className="bg-gray-800 border border-gray-700 text-white p-2 rounded-md" onClick={()=> setState(p=>({...p, s1: Math.max(0, p.s1-1)}))}>-</button>
                            <input type="number" min="0" className="w-[70px] bg-gray-800 border border-gray-700 text-white p-2 rounded-md" value={state.s1} onChange={(e)=> setState(p=>({...p, s1: parseInt(e.target.value,10)||0}))} />
                            <button className="bg-gray-800 border border-gray-700 text-white p-2 rounded-md" onClick={()=> setState(p=>({...p, s1: p.s1+1}))}>+</button>
                        </div>
                    </div>
                    <div className="grid grid-cols-[160px_1fr] gap-2 items-center my-1.5">
                        <label>Score 2</label>
                        <div className="flex gap-2 items-center">
                            <button className="bg-gray-800 border border-gray-700 text-white p-2 rounded-md" onClick={()=> setState(p=>({...p, s2: Math.max(0, p.s2-1)}))}>-</button>
                            <input type="number" min="0" className="w-[70px] bg-gray-800 border border-gray-700 text-white p-2 rounded-md" value={state.s2} onChange={(e)=> setState(p=>({...p, s2: parseInt(e.target.value,10)||0}))} />
                            <button className="bg-gray-800 border border-gray-700 text-white p-2 rounded-md" onClick={()=> setState(p=>({...p, s2: p.s2+1}))}>+</button>
                        </div>
                    </div>
                    <div className="grid grid-cols-[160px_1fr] gap-2 items-center my-1.5">
                        <label>SETS (L/R)</label>
                        <div className="flex gap-2 items-center">
                            <input className="flex-1 bg-gray-800 border border-gray-700 text-white p-2 rounded-md" value={state.sets} onChange={(e)=> setState(p=>({...p, sets:e.target.value}))} />
                            <button className="bg-gray-800 border border-gray-700 text-white p-2 rounded-md" onClick={()=> setState(p=>({...p, sets:(p.sets||'')+'L'}))}>L</button>
                            <button className="bg-gray-800 border border-gray-700 text-white p-2 rounded-md" onClick={()=> setState(p=>({...p, sets:(p.sets||'')+'R'}))}>R</button>
                            <button className="bg-gray-800 border border-gray-700 text-white p-2 rounded-md" onClick={()=> setState(p=>({...p, sets:(p.sets||'').slice(0,-1)}))}>⌫</button>
                            <button className="bg-gray-800 border border-gray-700 text-white p-2 rounded-md" onClick={()=> setState(p=>({...p, sets:''}))}>Clear</button>
                        </div>
                    </div>
                    <div className="grid grid-cols-[160px_1fr] gap-2 items-center my-1.5">
                        <label>OBS URL 복사</label>
                        <button className="bg-green-600 text-white font-bold px-3 py-2 rounded-md" onClick={handleCopyUrl}>복사하기</button>
                    </div>
                </div>
            );
        });

        function App() {
          const [panelOpen, setPanelOpen] = React.useState(false);
          const [isAdmin, setIsAdmin] = React.useState(false);
          const [state, setState] = React.useState({
            theme: 'protoss', style: 'sc1', series: 'Bo5', sg: 'strong', c1: '#e35a5a', c2: '#3bd6ff', s1: 0, s2: 0, sets: '', l1: '', l2: '', w: '', y: '', rosterHome: [], rosterAway: [], lineup: Array.from({ length: 9 }, () => ({ h: '', a: '', spL: '', spR: '' })), activeSlot: 1, overlays: { T: '', P: '', Z: '', opacity: 0.12, mode: 'color' }, icons: { T: '', P: '', Z: '' }, scale: 1,
          });
          
          React.useEffect(() => {
            const qs = new URLSearchParams(window.location.search);
            const isAdminMode = qs.get('admin') === 'true';
            setIsAdmin(isAdminMode);
            setPanelOpen(isAdminMode);

            if (qs.get('style') === 'clear') {
              document.body.classList.add('transparent-mode');
            }
            
            if (!isAdminMode) {
                const newState = {};
                for (let [key, value] of qs.entries()) {
                    try { newState[key] = JSON.parse(value); } catch (e) { newState[key] = value; }
                }
                setState(prev => ({...prev, ...newState}));

            } else {
                const lineup = loadJSON(LINEUP_KEY, Array.from({ length: 9 }, () => ({ h: '', a: '', spL: '', spR: '' })));
                const rosterHome = loadJSON(RHOME_KEY, []);
                const rosterAway = loadJSON(RAWAY_KEY, []);
                const activeSlot = parseInt(localStorage.getItem(ACTIVE_KEY) || '1', 10);
                const overlays = loadJSON(OV_KEY, { T: '', P: '', Z: '', opacity: 0.12, mode: 'color' });
                const icons = loadJSON(ICON_KEY, { T: '', P: '', Z: '' });
                setState(prevState => ({ ...prevState, lineup, rosterHome, rosterAway, activeSlot, overlays, icons }));
            }
          }, []);

          React.useEffect(() => {
            if (isAdmin) {
              saveJSON(LINEUP_KEY, state.lineup);
              saveJSON(RHOME_KEY, state.rosterHome);
              saveJSON(RAWAY_KEY, state.rosterAway);
              localStorage.setItem(ACTIVE_KEY, String(state.activeSlot));
              saveJSON(OV_KEY, state.overlays);
              saveJSON(ICON_KEY, state.icons);
            }
          }, [state, isAdmin]);

          return (
            <div className={`font-sans text-white ${isAdmin ? 'bg-gray-900 min-h-screen' : ''}`}>
                <div className="fixed board-wrapper" style={{ top: state.y || '0px', left: '50%', transform: `translateX(-50%) scale(${state.scale || 1})`, transformOrigin: 'top center' }}>
                  <Scoreboard state={state} />
                </div>
                {isAdmin && <button className="fixed top-4 right-4 z-[2147483650] w-9 h-9 rounded-full bg-blue-400 text-gray-900 font-bold flex items-center justify-center border-none shadow-lg cursor-pointer" onClick={() => setPanelOpen(!panelOpen)}>⚙</button>}
                {isAdmin && <ControlPanel isVisible={panelOpen} state={state} setState={setState} setPanelOpen={setPanelOpen} />}
            </div>
          );
        }

        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<App/>);
    </script>
</body>
</html>
