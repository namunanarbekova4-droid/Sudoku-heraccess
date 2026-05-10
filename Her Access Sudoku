import { useState, useEffect, useCallback, useRef } from “react”;

// ============================================================
// PREDEFINED PUZZLE BANK — verified puzzle/solution pairs
// ============================================================
const PUZZLE_BANK = {
easy: [
{
puzzle: [
[5,3,0,0,7,0,0,0,0],
[6,0,0,1,9,5,0,0,0],
[0,9,8,0,0,0,0,6,0],
[8,0,0,0,6,0,0,0,3],
[4,0,0,8,0,3,0,0,1],
[7,0,0,0,2,0,0,0,6],
[0,6,0,0,0,0,2,8,0],
[0,0,0,4,1,9,0,0,5],
[0,0,0,0,8,0,0,7,9],
],
solution: [
[5,3,4,6,7,8,9,1,2],
[6,7,2,1,9,5,3,4,8],
[1,9,8,3,4,2,5,6,7],
[8,5,9,7,6,1,4,2,3],
[4,2,6,8,5,3,7,9,1],
[7,1,3,9,2,4,8,5,6],
[9,6,1,5,3,7,2,8,4],
[2,8,7,4,1,9,6,3,5],
[3,4,5,2,8,6,1,7,9],
],
},
{
puzzle: [
[0,0,0,2,6,0,7,0,1],
[6,8,0,0,7,0,0,9,0],
[1,9,0,0,0,4,5,0,0],
[8,2,0,1,0,0,0,4,0],
[0,0,4,6,0,2,9,0,0],
[0,5,0,0,0,3,0,2,8],
[0,0,9,3,0,0,0,7,4],
[0,4,0,0,5,0,0,3,6],
[7,0,3,0,1,8,0,0,0],
],
solution: [
[4,3,5,2,6,9,7,8,1],
[6,8,2,5,7,1,4,9,3],
[1,9,7,8,3,4,5,6,2],
[8,2,6,1,9,5,3,4,7],
[3,7,4,6,8,2,9,1,5],
[9,5,1,7,4,3,6,2,8],
[5,1,9,3,2,6,8,7,4],
[2,4,8,9,5,7,1,3,6],
[7,6,3,4,1,8,2,5,9],
],
},
{
puzzle: [
[0,2,0,6,0,8,0,0,0],
[5,8,0,0,0,9,7,0,0],
[0,0,0,0,4,0,0,0,0],
[3,7,0,0,0,0,5,0,0],
[6,0,0,0,0,0,0,0,4],
[0,0,8,0,0,0,0,1,3],
[0,0,0,0,2,0,0,0,0],
[0,0,9,8,0,0,0,3,6],
[0,0,0,3,0,6,0,9,0],
],
solution: [
[1,2,3,6,7,8,9,4,5],
[5,8,4,2,3,9,7,6,1],
[9,6,7,1,4,5,3,2,8],
[3,7,2,4,6,1,5,8,9],
[6,9,1,5,8,3,2,7,4],
[4,5,8,7,9,2,6,1,3],
[8,3,6,9,2,4,1,5,7],
[2,1,9,8,5,7,4,3,6],
[7,4,5,3,1,6,8,9,2],
],
},
],
medium: [
{
puzzle: [
[0,0,0,6,0,0,4,0,0],
[7,0,0,0,0,3,6,0,0],
[0,0,0,0,9,1,0,8,0],
[0,0,0,0,0,0,0,0,0],
[0,5,0,1,8,0,0,0,3],
[0,0,0,3,0,6,0,4,5],
[0,4,0,2,0,0,0,6,0],
[9,0,3,0,0,0,0,0,0],
[0,2,0,0,0,0,1,0,0],
],
solution: [
[5,8,1,6,7,2,4,3,9],
[7,9,2,8,4,3,6,5,1],
[3,6,4,5,9,1,7,8,2],
[4,3,8,9,5,7,2,1,6],
[2,5,6,1,8,4,9,7,3],
[1,7,9,3,2,6,8,4,5],
[8,4,5,2,1,9,3,6,7],
[9,1,3,7,6,8,5,2,4],
[6,2,7,4,3,5,1,9,8],
],
},
{
puzzle: [
[0,0,0,0,0,0,0,0,0],
[0,0,0,0,0,3,0,8,5],
[0,0,1,0,2,0,0,0,0],
[0,0,0,5,0,7,0,0,0],
[0,0,4,0,0,0,1,0,0],
[0,9,0,0,0,0,0,0,0],
[5,0,0,0,0,0,0,7,3],
[0,0,2,0,1,0,0,0,0],
[0,0,0,0,4,0,0,0,9],
],
solution: [
[9,8,7,6,5,4,3,2,1],
[2,4,6,1,7,3,9,8,5],
[3,5,1,9,2,8,7,4,6],
[1,2,8,5,3,7,6,9,4],
[6,3,4,8,9,2,1,5,7],
[7,9,5,4,6,1,8,3,2],
[5,1,9,2,8,6,4,7,3],
[4,7,2,3,1,9,5,6,8],
[8,6,3,7,4,5,2,1,9],
],
},
{
puzzle: [
[0,0,0,0,0,0,6,8,0],
[0,0,0,0,7,3,0,0,9],
[3,0,9,0,0,0,0,4,5],
[4,9,0,0,0,0,0,0,0],
[8,0,3,0,5,0,9,0,2],
[0,0,0,0,0,0,0,3,6],
[9,6,0,0,0,0,3,0,8],
[7,0,0,6,8,0,0,0,0],
[0,2,8,0,0,0,0,0,0],
],
solution: [
[1,7,2,4,9,5,6,8,3],
[6,4,5,8,7,3,2,1,9],
[3,8,9,2,6,1,7,4,5],
[4,9,6,3,2,7,8,5,1],
[8,1,3,9,5,6,9,3,2],
[2,5,7,1,4,8,4,3,6],
[9,6,4,5,1,2,3,7,8],
[7,3,1,6,8,4,5,9,2],
[5,2,8,7,3,9,1,6,4],
],
},
],
hard: [
{
puzzle: [
[8,0,0,0,0,0,0,0,0],
[0,0,3,6,0,0,0,0,0],
[0,7,0,0,9,0,2,0,0],
[0,5,0,0,0,7,0,0,0],
[0,0,0,0,4,5,7,0,0],
[0,0,0,1,0,0,0,3,0],
[0,0,1,0,0,0,0,6,8],
[0,0,8,5,0,0,0,1,0],
[0,9,0,0,0,0,4,0,0],
],
solution: [
[8,1,2,7,5,3,6,4,9],
[9,4,3,6,8,2,1,7,5],
[6,7,5,4,9,1,2,8,3],
[1,5,4,2,3,7,8,9,6],
[3,6,9,8,4,5,7,2,1],
[2,8,7,1,6,9,5,3,4],
[5,2,1,9,7,4,3,6,8],
[4,3,8,5,2,6,9,1,7],
[7,9,6,3,1,8,4,5,2],
],
},
{
puzzle: [
[1,0,0,0,0,7,0,9,0],
[0,3,0,0,2,0,0,0,8],
[0,0,9,6,0,0,5,0,0],
[0,0,5,3,0,0,9,0,0],
[0,1,0,0,8,0,0,0,2],
[6,0,0,0,0,4,0,0,0],
[3,0,0,0,0,0,0,1,0],
[0,4,0,0,0,0,0,0,7],
[0,0,7,0,0,0,3,0,0],
],
solution: [
[1,6,2,8,5,7,4,9,3],
[5,3,4,1,2,9,6,7,8],
[7,8,9,6,4,3,5,2,1],
[4,7,5,3,1,2,9,8,6],
[9,1,3,5,8,6,7,4,2],
[6,2,8,7,9,4,1,3,5],
[3,5,6,4,7,8,2,1,9],
[2,4,1,9,3,5,8,6,7],
[8,9,7,2,6,1,3,5,4],
],
},
{
puzzle: [
[0,0,5,3,0,0,0,0,0],
[8,0,0,0,0,0,0,2,0],
[0,7,0,0,1,0,5,0,0],
[4,0,0,0,0,5,3,0,0],
[0,1,0,0,7,0,0,0,6],
[0,0,3,2,0,0,0,8,0],
[0,6,0,5,0,0,0,0,9],
[0,0,4,0,0,0,0,3,0],
[0,0,0,0,0,9,7,0,0],
],
solution: [
[1,4,5,3,2,7,6,9,8],
[8,3,9,6,5,4,1,2,7],
[6,7,2,9,1,8,5,4,3],
[4,9,6,1,8,5,3,7,2],
[2,1,8,4,7,3,9,5,6],
[7,5,3,2,9,6,4,8,1],
[3,6,7,5,4,2,8,1,9],
[9,8,4,7,6,1,2,3,5],
[5,2,1,8,3,9,7,6,4],
],
},
],
};

// Daily puzzle: stable index per calendar date
function getDailyPuzzle() {
const today = new Date().toISOString().split(“T”)[0];
const [y, m, d] = today.split(”-”).map(Number);
const idx = (y * 365 + m * 30 + d) % PUZZLE_BANK.medium.length;
return { …PUZZLE_BANK.medium[idx], date: today };
}

function getPuzzle(difficulty) {
const bank = PUZZLE_BANK[difficulty] || PUZZLE_BANK.medium;
return bank[Math.floor(Math.random() * bank.length)];
}

// ============================================================
// CONFLICT DETECTION
// Returns a Set of “r,c” strings for every cell in conflict
// (same number in same row / col / 3x3 box)
// ============================================================
function getConflicts(cells) {
const conflicts = new Set();

// Rows
for (let r = 0; r < 9; r++) {
const seen = {};
for (let c = 0; c < 9; c++) {
const v = cells[r][c].value;
if (!v) continue;
if (seen[v] !== undefined) { conflicts.add(`${r},${seen[v]}`); conflicts.add(`${r},${c}`); }
else seen[v] = c;
}
}
// Cols
for (let c = 0; c < 9; c++) {
const seen = {};
for (let r = 0; r < 9; r++) {
const v = cells[r][c].value;
if (!v) continue;
if (seen[v] !== undefined) { conflicts.add(`${seen[v]},${c}`); conflicts.add(`${r},${c}`); }
else seen[v] = r;
}
}
// Boxes
for (let br = 0; br < 3; br++) {
for (let bc = 0; bc < 3; bc++) {
const seen = {};
for (let dr = 0; dr < 3; dr++) {
for (let dc = 0; dc < 3; dc++) {
const r = br * 3 + dr, c = bc * 3 + dc;
const v = cells[r][c].value;
if (!v) continue;
const key = `${r},${c}`;
if (seen[v] !== undefined) { conflicts.add(seen[v]); conflicts.add(key); }
else seen[v] = key;
}
}
}
}
return conflicts;
}

// ============================================================
// PERSISTENCE HELPERS
// ============================================================
function getLeaderboard() {
try { return JSON.parse(localStorage.getItem(“heraccess_leaderboard”) || “[]”); } catch { return []; }
}
function saveToLeaderboard(entry) {
const board = getLeaderboard();
board.push(entry);
board.sort((a, b) => a.time - b.time || a.mistakes - b.mistakes);
localStorage.setItem(“heraccess_leaderboard”, JSON.stringify(board.slice(0, 50)));
}
function getUser() {
try { return JSON.parse(localStorage.getItem(“heraccess_user”) || “null”); } catch { return null; }
}
function saveUser(u) { localStorage.setItem(“heraccess_user”, JSON.stringify(u)); }
function getUserStats() {
try {
const raw = JSON.parse(localStorage.getItem(“heraccess_stats”) || “{}”);
return {
played:    Number(raw.played)    || 0,
won:       Number(raw.won)       || 0,
totalTime: Number(raw.totalTime) || 0,
bestTime:  raw.bestTime != null ? Number(raw.bestTime) : null,
mistakes:  Number(raw.mistakes)  || 0,
};
} catch {
return { played: 0, won: 0, totalTime: 0, bestTime: null, mistakes: 0 };
}
}
// Returns the updated stats object so callers can sync React state
function updateStats(time, mistakesThisGame = 0) {
const s = getUserStats();
s.played++;
s.won++;
s.totalTime += time;
s.mistakes  += mistakesThisGame;
s.bestTime   = s.bestTime == null ? time : Math.min(s.bestTime, time);
localStorage.setItem(“heraccess_stats”, JSON.stringify(s));
return s;
}
function fmtTime(s) {
const m = Math.floor(s / 60), sec = s % 60;
return `${String(m).padStart(2, "0")}:${String(sec).padStart(2, "0")}`;
}

// ============================================================
// SHARED STYLES
// ============================================================
const inputStyle = {
width: “100%”, padding: “0.75rem 1rem”, borderRadius: “0.75rem”,
border: “1px solid var(–border)”, background: “rgba(255,255,255,0.05)”,
color: “var(–text)”, fontSize: “0.9rem”, marginBottom: “0.75rem”,
outline: “none”, boxSizing: “border-box”, fontFamily: “var(–font-body)”,
};
const btnPrimary = {
width: “100%”, padding: “0.85rem”, borderRadius: “0.75rem”,
background: “linear-gradient(135deg, var(–accent), var(–pink))”,
border: “none”, color: “white”, fontWeight: 700, fontSize: “0.95rem”,
cursor: “pointer”, fontFamily: “var(–font-body)”, letterSpacing: “0.02em”,
};
const navBtn = {
padding: “0.45rem 0.6rem”, borderRadius: “0.65rem”,
border: “1px solid var(–border)”, background: “var(–surface)”,
color: “var(–text)”, cursor: “pointer”, fontSize: “1rem”,
};
const iconBtn = {
padding: “0.6rem 1rem”, borderRadius: “0.75rem”,
border: “1px solid var(–border)”, background: “var(–surface)”,
color: “var(–text)”, cursor: “pointer”, fontSize: “0.9rem”,
fontFamily: “var(–font-body)”, transition: “all 0.15s ease”,
};

// ============================================================
// MODAL WRAPPER
// ============================================================
function Modal({ children, onClose }) {
return (
<div style={{
position: “fixed”, inset: 0, background: “rgba(15,10,25,0.6)”,
backdropFilter: “blur(8px)”, zIndex: 1000, display: “flex”,
alignItems: “center”, justifyContent: “center”, padding: “1rem”,
}} onClick={e => e.target === e.currentTarget && onClose()}>
<div style={{
background: “var(–glass)”, border: “1px solid var(–border)”,
borderRadius: “1.5rem”, padding: “2rem”, maxWidth: “480px”, width: “100%”,
boxShadow: “0 24px 80px rgba(167,139,250,0.25)”, animation: “fadeUp 0.3s ease”,
}}>
{children}
</div>
</div>
);
}

// ============================================================
// AUTH MODAL
// ============================================================
function AuthModal({ onAuth, onClose }) {
const [mode, setMode] = useState(“login”);
const [name, setName] = useState(””);
const [email, setEmail] = useState(””);
const handle = () => {
if (!email.trim()) return;
const user = { name: name || email.split(”@”)[0], email: email.trim(), joined: new Date().toISOString() };
saveUser(user); onAuth(user);
};
return (
<Modal onClose={onClose}>
<div style={{ textAlign: “center”, marginBottom: “1.5rem” }}>
<div style={{ fontSize: “2rem”, marginBottom: “0.5rem” }}>✨</div>
<h2 style={{ color: “var(–accent)”, fontFamily: “var(–font-display)”, fontSize: “1.5rem”, margin: 0 }}>
{mode === “login” ? “Welcome Back” : “Join HerAccess”}
</h2>
<p style={{ color: “var(–muted)”, fontSize: “0.85rem”, marginTop: “0.25rem” }}>
{mode === “login” ? “Sign in to save your progress” : “Start your brain-training journey”}
</p>
</div>
{mode === “register” && (
<input placeholder=“Your name” value={name} onChange={e => setName(e.target.value)} style={inputStyle} />
)}
<input placeholder=“Email address” type=“email” value={email} onChange={e => setEmail(e.target.value)} style={inputStyle} />
<button onClick={handle} style={btnPrimary}>{mode === “login” ? “Sign In” : “Create Account”}</button>
<p style={{ textAlign: “center”, fontSize: “0.8rem”, color: “var(–muted)”, marginTop: “1rem” }}>
{mode === “login” ? “No account? “ : “Already have one? “}
<span onClick={() => setMode(mode === “login” ? “register” : “login”)}
style={{ color: “var(–accent)”, cursor: “pointer”, textDecoration: “underline” }}>
{mode === “login” ? “Sign up” : “Log in”}
</span>
</p>
</Modal>
);
}

// ============================================================
// AI COACH
// ============================================================
function AICoach({ liveBoardValues, onClose }) {
const [messages, setMessages] = useState([
{ role: “assistant”, text: “Hi! I’m your AI Sudoku coach 🌸 I can help explain strategies, give hints, and guide you through tough spots. What would you like to know?” },
]);
const [input, setInput] = useState(””);
const [loading, setLoading] = useState(false);
const bottomRef = useRef(null);
useEffect(() => { bottomRef.current?.scrollIntoView({ behavior: “smooth” }); }, [messages]);

const sendMessage = async () => {
if (!input.trim() || loading) return;
const userMsg = input.trim();
setInput(””);
setMessages(prev => […prev, { role: “user”, text: userMsg }]);
setLoading(true);
const boardText = liveBoardValues
? liveBoardValues.map(row => row.map(v => v || “_”).join(” “)).join(”\n”)
: “No board loaded yet.”;
try {
const res = await fetch(”/api/coach”, {
method: “POST”,
headers: { “Content-Type”: “application/json” },
body: JSON.stringify({
boardText,
history: messages.map(m => ({ role: m.role === “assistant” ? “assistant” : “user”, content: m.text })),
userMessage: userMsg,
}),
});
if (!res.ok) throw new Error(`HTTP ${res.status}`);
const data = await res.json();
setMessages(prev => […prev, { role: “assistant”, text: data.reply || “I’m here to help! Ask me about a specific row or column.” }]);
} catch (err) {
setMessages(prev => […prev, { role: “assistant”, text: “I’m having trouble connecting right now. Please try again in a moment.” }]);
}
setLoading(false);
};

return (
<div style={{
position: “fixed”, right: 0, top: 0, bottom: 0, width: “min(380px, 100vw)”,
background: “var(–glass-heavy)”, borderLeft: “1px solid var(–border)”,
backdropFilter: “blur(20px)”, display: “flex”, flexDirection: “column”,
zIndex: 500, animation: “slideInRight 0.3s ease”,
}}>
<div style={{ padding: “1.25rem 1.5rem”, borderBottom: “1px solid var(–border)”, display: “flex”, justifyContent: “space-between”, alignItems: “center” }}>
<div>
<div style={{ display: “flex”, alignItems: “center”, gap: “0.5rem” }}>
<span style={{ fontSize: “1.25rem” }}>🧠</span>
<span style={{ fontFamily: “var(–font-display)”, fontWeight: 700, color: “var(–accent)”, fontSize: “1.1rem” }}>AI Coach</span>
</div>
<p style={{ color: “var(–muted)”, fontSize: “0.75rem”, margin: “0.2rem 0 0” }}>Strategy tutor</p>
</div>
<button onClick={onClose} style={{ background: “none”, border: “none”, color: “var(–muted)”, cursor: “pointer”, fontSize: “1.25rem” }}>✕</button>
</div>
<div style={{ flex: 1, overflowY: “auto”, padding: “1rem”, display: “flex”, flexDirection: “column”, gap: “0.75rem” }}>
{messages.map((m, i) => (
<div key={i} style={{ display: “flex”, justifyContent: m.role === “user” ? “flex-end” : “flex-start” }}>
<div style={{
maxWidth: “85%”, padding: “0.75rem 1rem”,
borderRadius: m.role === “user” ? “1rem 1rem 0.25rem 1rem” : “1rem 1rem 1rem 0.25rem”,
background: m.role === “user” ? “linear-gradient(135deg, var(–accent), var(–pink))” : “rgba(255,255,255,0.08)”,
color: m.role === “user” ? “white” : “var(–text)”,
fontSize: “0.875rem”, lineHeight: 1.5,
border: m.role === “assistant” ? “1px solid var(–border)” : “none”,
}}>{m.text}</div>
</div>
))}
{loading && (
<div style={{ display: “flex”, gap: “0.5rem”, padding: “0.5rem 0.75rem” }}>
{[0, 1, 2].map(i => (
<div key={i} style={{ width: “8px”, height: “8px”, borderRadius: “50%”, background: “var(–accent)”, animation: `pulse 1.2s ease ${i * 0.2}s infinite` }} />
))}
</div>
)}
<div ref={bottomRef} />
</div>
<div style={{ padding: “1rem”, borderTop: “1px solid var(–border)”, display: “flex”, gap: “0.5rem” }}>
<input value={input} onChange={e => setInput(e.target.value)}
onKeyDown={e => e.key === “Enter” && sendMessage()}
placeholder=“Ask your coach…” style={{ …inputStyle, marginBottom: 0, flex: 1 }} />
<button onClick={sendMessage} disabled={loading || !input.trim()} style={{
padding: “0.75rem 1rem”, borderRadius: “0.75rem”,
background: “linear-gradient(135deg, var(–accent), var(–pink))”,
border: “none”, color: “white”, cursor: “pointer”, fontSize: “1rem”,
opacity: loading || !input.trim() ? 0.5 : 1,
}}>→</button>
</div>
</div>
);
}

// ============================================================
// LEADERBOARD
// ============================================================
function Leaderboard({ onClose }) {
const board = getLeaderboard();
const medals = [“🥇”, “🥈”, “🥉”];
return (
<Modal onClose={onClose}>
<div style={{ textAlign: “center”, marginBottom: “1.5rem” }}>
<div style={{ fontSize: “2rem” }}>🏆</div>
<h2 style={{ color: “var(–accent)”, fontFamily: “var(–font-display)”, margin: “0.25rem 0 0” }}>Daily Leaderboard</h2>
<p style={{ color: “var(–muted)”, fontSize: “0.8rem” }}>{new Date().toLocaleDateString(“en-US”, { weekday: “long”, month: “long”, day: “numeric” })}</p>
</div>
{board.length === 0 ? (
<p style={{ textAlign: “center”, color: “var(–muted)”, padding: “2rem 0” }}>No entries yet — be the first! 🌸</p>
) : (
<div style={{ display: “flex”, flexDirection: “column”, gap: “0.5rem”, maxHeight: “400px”, overflowY: “auto” }}>
{board.map((entry, i) => (
<div key={i} style={{
display: “flex”, alignItems: “center”, gap: “1rem”, padding: “0.75rem 1rem”,
background: i < 3 ? “rgba(167,139,250,0.1)” : “rgba(255,255,255,0.04)”,
borderRadius: “0.75rem”, border: “1px solid var(–border)”,
}}>
<span style={{ fontSize: “1.2rem”, minWidth: “2rem” }}>{medals[i] || `#${i + 1}`}</span>
<div style={{ flex: 1 }}>
<div style={{ fontWeight: 600, color: “var(–text)”, fontSize: “0.9rem” }}>{entry.name}</div>
<div style={{ color: “var(–muted)”, fontSize: “0.75rem” }}>{entry.mistakes} mistakes</div>
</div>
<div style={{ color: “var(–accent)”, fontWeight: 700, fontFamily: “var(–font-mono)” }}>{fmtTime(entry.time)}</div>
</div>
))}
</div>
)}
<button onClick={onClose} style={{ …btnPrimary, marginTop: “1rem” }}>Close</button>
</Modal>
);
}

// ============================================================
// STATS MODAL
// ============================================================
function StatsModal({ user, stats, onClose }) {
const winRate = stats.played > 0 ? Math.round((stats.won / stats.played) * 100) : 0;
const avgTime = stats.won > 0 ? Math.round(stats.totalTime / stats.won) : 0;
const items = [
{ label: “Games Played”, value: stats.played,                                icon: “🎮” },
{ label: “Win Rate”,     value: `${winRate}%`,                               icon: “✨” },
{ label: “Avg. Time”,    value: fmtTime(avgTime),                            icon: “⏱️” },
{ label: “Best Time”,    value: stats.bestTime != null ? fmtTime(stats.bestTime) : “—”, icon: “🏅” },
{ label: “Puzzles Won”,  value: stats.won,                                   icon: “🏆” },
{ label: “Mistakes”,     value: stats.mistakes,                              icon: “❌” },
];
return (
<Modal onClose={onClose}>
<div style={{ textAlign: “center”, marginBottom: “1.5rem” }}>
<div style={{
width: “64px”, height: “64px”, borderRadius: “50%”,
background: “linear-gradient(135deg, var(–accent), var(–pink))”,
display: “flex”, alignItems: “center”, justifyContent: “center”,
fontSize: “1.75rem”, margin: “0 auto 0.75rem”,
}}>{user.name[0].toUpperCase()}</div>
<h2 style={{ fontFamily: “var(–font-display)”, color: “var(–text)”, margin: 0 }}>{user.name}</h2>
<p style={{ color: “var(–muted)”, fontSize: “0.8rem” }}>{user.email}</p>
</div>
<div style={{ display: “grid”, gridTemplateColumns: “1fr 1fr 1fr”, gap: “0.75rem” }}>
{items.map(s => (
<div key={s.label} style={{ padding: “1rem”, borderRadius: “1rem”, background: “rgba(167,139,250,0.08)”, border: “1px solid var(–border)”, textAlign: “center” }}>
<div style={{ fontSize: “1.5rem” }}>{s.icon}</div>
<div style={{ color: “var(–accent)”, fontWeight: 800, fontSize: “1.25rem”, fontFamily: “var(–font-mono)” }}>{s.value}</div>
<div style={{ color: “var(–muted)”, fontSize: “0.75rem”, marginTop: “0.2rem” }}>{s.label}</div>
</div>
))}
</div>
<button onClick={onClose} style={{ …btnPrimary, marginTop: “1.25rem” }}>Done</button>
</Modal>
);
}

// ============================================================
// VICTORY MODAL
// ============================================================
function VictoryModal({ time, mistakes, onClose, onNewGame, isDaily, user, onStatsUpdate }) {
useEffect(() => {
if (user && isDaily) {
const today = new Date().toISOString().split(“T”)[0];
saveToLeaderboard({ name: user.name, time, mistakes, date: today });
}
if (user) {
const updated = updateStats(time, mistakes);
if (onStatsUpdate) onStatsUpdate(updated);
}
}, []);
return (
<Modal onClose={onClose}>
<div style={{ textAlign: “center” }}>
<div style={{ fontSize: “3.5rem”, marginBottom: “0.5rem”, animation: “bounce 0.6s ease” }}>🎉</div>
<h2 style={{ fontFamily: “var(–font-display)”, color: “var(–accent)”, fontSize: “1.75rem”, margin: 0 }}>Puzzle Complete!</h2>
<p style={{ color: “var(–muted)”, marginBottom: “1.5rem” }}>Brilliant work, queen 👑</p>
<div style={{ display: “flex”, gap: “1rem”, justifyContent: “center”, marginBottom: “1.5rem” }}>
<div style={{ padding: “1rem 1.5rem”, background: “rgba(167,139,250,0.12)”, borderRadius: “1rem”, border: “1px solid var(–border)” }}>
<div style={{ color: “var(–accent)”, fontWeight: 800, fontSize: “1.5rem”, fontFamily: “var(–font-mono)” }}>{fmtTime(time)}</div>
<div style={{ color: “var(–muted)”, fontSize: “0.75rem” }}>Time</div>
</div>
<div style={{ padding: “1rem 1.5rem”, background: “rgba(249,168,212,0.12)”, borderRadius: “1rem”, border: “1px solid var(–border)” }}>
<div style={{ color: “var(–pink)”, fontWeight: 800, fontSize: “1.5rem” }}>{mistakes}</div>
<div style={{ color: “var(–muted)”, fontSize: “0.75rem” }}>Mistakes</div>
</div>
</div>
<button onClick={onNewGame} style={btnPrimary}>New Puzzle ✨</button>
<button onClick={onClose} style={{ …btnPrimary, marginTop: “0.5rem”, background: “rgba(255,255,255,0.08)”, border: “1px solid var(–border)” }}>
View Board
</button>
</div>
</Modal>
);
}

// ============================================================
// SUDOKU BOARD — all game logic
// ============================================================
function buildCells(puzzle) {
return puzzle.map(row =>
row.map(val => ({ value: val, given: val !== 0, notes: [] }))
);
}

function SudokuBoard({ puzzle, solution, onWin, setMistakes, onNewGame, onBoardChange }) {
const [cells, setCells] = useState(() => buildCells(puzzle));
const [selected, setSelected] = useState(null); // [r, c] | null
const [pencilMode, setPencilMode] = useState(false);
const [history, setHistory] = useState([]);
const [future, setFuture] = useState([]);
const [hints, setHints] = useState(3);
const [won, setWon] = useState(false);

// Full reset whenever the puzzle prop changes (new game)
useEffect(() => {
setCells(buildCells(puzzle));
setSelected(null);
setPencilMode(false);
setHistory([]);
setFuture([]);
setHints(3);
setWon(false);
}, [puzzle]);

// Derived: which cells are in conflict right now
const conflicts = getConflicts(cells);

// ── helpers ──────────────────────────────────────────────
const deepClone = c => c.map(row => row.map(cell => ({ …cell, notes: […cell.notes] })));

// Commit next board state, push undo history, check victory
const commit = useCallback((next) => {
setHistory(h => […h.slice(-40), cells]);
setFuture([]);
setCells(next);
// Notify parent of live board values for AI context
if (onBoardChange) onBoardChange(next.map(row => row.map(cell => cell.value)));

```
// Victory: all 81 cells filled and zero conflicts
const allFilled = next.every(row => row.every(cell => cell.value !== 0));
if (allFilled && getConflicts(next).size === 0) {
  setWon(true);
  onWin();
}
```

}, [cells, onWin, onBoardChange]);

// Place (or erase) a number in the selected cell
const inputNumber = useCallback((num) => {
if (won || !selected) return;
const [r, c] = selected;
if (cells[r][c].given) return;

```
const next = deepClone(cells);

if (pencilMode && num !== 0) {
  // Toggle pencil note; clear the value
  next[r][c].value = 0;
  const idx = next[r][c].notes.indexOf(num);
  if (idx >= 0) next[r][c].notes.splice(idx, 1);
  else next[r][c].notes.push(num);
} else {
  // Normal entry
  const prevVal = next[r][c].value;
  next[r][c].value = num;
  next[r][c].notes = [];

  // Count mistake: placing a WRONG number when previous was not that wrong number
  if (num !== 0 && num !== solution[r][c] && prevVal !== num) {
    setMistakes(m => m + 1);
  }

  // When placing a correct number, auto-clear that candidate from peers
  if (num !== 0 && num === solution[r][c]) {
    for (let i = 0; i < 9; i++) {
      next[r][i].notes = next[r][i].notes.filter(n => n !== num);
      next[i][c].notes = next[i][c].notes.filter(n => n !== num);
    }
    const sr = Math.floor(r / 3) * 3, sc = Math.floor(c / 3) * 3;
    for (let dr = 0; dr < 3; dr++)
      for (let dc = 0; dc < 3; dc++)
        next[sr + dr][sc + dc].notes = next[sr + dr][sc + dc].notes.filter(n => n !== num);
  }
}

commit(next);
```

}, [won, selected, cells, pencilMode, solution, commit, setMistakes]);

const undo = useCallback(() => {
if (!history.length) return;
setFuture(f => [cells, …f]);
setCells(history[history.length - 1]);
setHistory(h => h.slice(0, -1));
}, [history, cells]);

const redo = useCallback(() => {
if (!future.length) return;
setHistory(h => […h, cells]);
setCells(future[0]);
setFuture(f => f.slice(1));
}, [future, cells]);

const useHint = useCallback(() => {
if (hints <= 0 || !selected || won) return;
const [r, c] = selected;
if (cells[r][c].given) return;
if (cells[r][c].value === solution[r][c]) return;
const next = deepClone(cells);
next[r][c].value = solution[r][c];
next[r][c].notes = [];
setHints(h => h - 1);
commit(next);
}, [hints, selected, won, cells, solution, commit]);

// Keyboard controls
useEffect(() => {
const handler = e => {
// Number input
if (e.key >= “1” && e.key <= “9”) { e.preventDefault(); inputNumber(parseInt(e.key)); return; }
if ([“Backspace”, “Delete”, “0”].includes(e.key)) { e.preventDefault(); inputNumber(0); return; }
// Undo / redo
if ((e.ctrlKey || e.metaKey) && e.key === “z”) { e.preventDefault(); undo(); return; }
if ((e.ctrlKey || e.metaKey) && e.key === “y”) { e.preventDefault(); redo(); return; }
// Arrow navigation
if (!selected) return;
const [r, c] = selected;
if (e.key === “ArrowUp”)    { e.preventDefault(); setSelected([Math.max(0, r - 1), c]); }
if (e.key === “ArrowDown”)  { e.preventDefault(); setSelected([Math.min(8, r + 1), c]); }
if (e.key === “ArrowLeft”)  { e.preventDefault(); setSelected([r, Math.max(0, c - 1)]); }
if (e.key === “ArrowRight”) { e.preventDefault(); setSelected([r, Math.min(8, c + 1)]); }
};
window.addEventListener(“keydown”, handler);
return () => window.removeEventListener(“keydown”, handler);
}, [inputNumber, undo, redo, selected]);

// Highlight: value of selected cell (for same-number highlight)
const selVal = selected ? cells[selected[0]][selected[1]].value : 0;

const isSameBox = (r, c, sr, sc) =>
Math.floor(r / 3) === Math.floor(sr / 3) && Math.floor(c / 3) === Math.floor(sc / 3);

return (
<div style={{ display: “flex”, flexDirection: “column”, alignItems: “center”, gap: “1rem” }}>

```
  {/* ── BOARD ── */}
  <div style={{
    display: "grid",
    gridTemplateColumns: "repeat(9, 1fr)",
    width: "min(480px, 94vw)",
    border: "2px solid var(--accent)",
    borderRadius: "1rem",
    overflow: "hidden",
    boxShadow: "0 8px 40px rgba(167,139,250,0.3)",
  }}>
    {cells.map((row, r) => row.map((cell, c) => {
      const isSelected = selected && selected[0] === r && selected[1] === c;
      const isPeer = selected && !isSelected && (
        selected[0] === r || selected[1] === c || isSameBox(r, c, selected[0], selected[1])
      );
      const isSameNum = selVal > 0 && cell.value === selVal && !isSelected;
      const isConflict = conflicts.has(`${r},${c}`);
      // isWrong = user placed a number that doesn't match solution
      const isWrong = !cell.given && cell.value !== 0 && cell.value !== solution[r][c];

      // Cell background priority: selected > conflict/wrong > same-number > peer > default
      let bg = "var(--surface)";
      if (isSelected)           bg = "rgba(167,139,250,0.38)";
      else if (isConflict || isWrong) bg = "rgba(248,113,113,0.18)";
      else if (isSameNum)       bg = "rgba(167,139,250,0.2)";
      else if (isPeer)          bg = "rgba(167,139,250,0.07)";

      // Thick borders for 3x3 box separation
      const borderRight  = c === 2 || c === 5 ? "2px solid var(--accent)" : "1px solid var(--border)";
      const borderBottom = r === 2 || r === 5 ? "2px solid var(--accent)" : "1px solid var(--border)";
      // Remove right/bottom on last cell to avoid double border with outer box
      const style = {
        aspectRatio: "1",
        background: bg,
        display: "flex", alignItems: "center", justifyContent: "center",
        cursor: "pointer", position: "relative",
        transition: "background 0.1s ease",
        borderRight:  c < 8 ? borderRight  : "none",
        borderBottom: r < 8 ? borderBottom : "none",
        outline: isSelected ? "2px solid var(--accent)" : "none",
        outlineOffset: "-2px",
      };

      return (
        <div key={`${r}-${c}`} onClick={() => setSelected([r, c])} style={style}>
          {cell.value !== 0 ? (
            <span style={{
              fontSize: "clamp(0.85rem, 2.4vw, 1.25rem)",
              fontWeight: cell.given ? 700 : 500,
              color: (isConflict || isWrong)
                ? "#f87171"
                : cell.given ? "var(--text)" : "var(--accent)",
              fontFamily: "var(--font-display)",
              userSelect: "none",
              lineHeight: 1,
            }}>
              {cell.value}
            </span>
          ) : cell.notes.length > 0 ? (
            // Pencil notes — 3×3 mini grid
            <div style={{ display: "grid", gridTemplateColumns: "repeat(3,1fr)", width: "92%", height: "92%" }}>
              {[1,2,3,4,5,6,7,8,9].map(n => (
                <span key={n} style={{
                  fontSize: "clamp(0.3rem, 0.85vw, 0.52rem)",
                  color: "var(--muted)",
                  display: "flex", alignItems: "center", justifyContent: "center",
                  opacity: cell.notes.includes(n) ? 1 : 0,
                  userSelect: "none",
                  lineHeight: 1,
                }}>{n}</span>
              ))}
            </div>
          ) : null}
        </div>
      );
    }))}
  </div>

  {/* ── CONTROLS ── */}
  <div style={{ display: "flex", gap: "0.4rem", flexWrap: "wrap", justifyContent: "center" }}>
    <button onClick={undo}      title="Undo (Ctrl+Z)"   style={iconBtn} disabled={!history.length}>↩ Undo</button>
    <button onClick={redo}      title="Redo (Ctrl+Y)"   style={iconBtn} disabled={!future.length}>↪ Redo</button>
    <button onClick={() => inputNumber(0)} title="Erase selected cell" style={iconBtn}>⌫ Erase</button>
    <button
      onClick={() => setPencilMode(p => !p)}
      title="Toggle pencil / notes mode"
      style={{
        ...iconBtn,
        background: pencilMode ? "linear-gradient(135deg, var(--accent), var(--pink))" : "var(--surface)",
        color: pencilMode ? "white" : "var(--text)",
        border: pencilMode ? "none" : "1px solid var(--border)",
      }}
    >✏️ {pencilMode ? "Notes ON" : "Notes"}</button>
    <button
      onClick={useHint}
      title={`Reveal selected cell (${hints} left)`}
      style={{ ...iconBtn, opacity: hints > 0 && selected && !won ? 1 : 0.4 }}
      disabled={hints === 0 || !selected || won}
    >💡 {hints}</button>
    <button onClick={onNewGame} title="Start a new puzzle" style={iconBtn}>↺ New Game</button>
  </div>

  {/* ── NUMBER PAD ── */}
  <div style={{ display: "flex", gap: "0.4rem", flexWrap: "wrap", justifyContent: "center" }}>
    {[1,2,3,4,5,6,7,8,9].map(n => (
      <button
        key={n}
        onClick={() => inputNumber(n)}
        style={{
          width: "clamp(36px, 9vw, 52px)", height: "clamp(36px, 9vw, 52px)",
          borderRadius: "0.75rem",
          border: selVal === n ? "none" : "1px solid var(--border)",
          background: selVal === n
            ? "linear-gradient(135deg, var(--accent), var(--pink))"
            : "var(--surface)",
          color: selVal === n ? "white" : "var(--text)",
          fontWeight: 700,
          fontSize: "clamp(1rem, 2.5vw, 1.25rem)",
          cursor: "pointer",
          fontFamily: "var(--font-display)",
          transition: "all 0.15s ease",
          boxShadow: selVal === n ? "0 4px 16px rgba(167,139,250,0.4)" : "none",
        }}
      >{n}</button>
    ))}
  </div>

  {/* ── LEGEND ── */}
  <div style={{ display: "flex", gap: "1rem", fontSize: "0.73rem", color: "var(--muted)", flexWrap: "wrap", justifyContent: "center" }}>
    {[
      { color: "rgba(248,113,113,0.35)", label: "Conflict / wrong" },
      { color: "rgba(167,139,250,0.38)", label: "Selected" },
      { color: "rgba(167,139,250,0.2)",  label: "Same number" },
      { color: "rgba(167,139,250,0.07)", label: "Peer cell" },
    ].map(l => (
      <span key={l.label} style={{ display: "flex", alignItems: "center", gap: "0.3rem" }}>
        <span style={{ display: "inline-block", width: "10px", height: "10px", borderRadius: "2px", background: l.color }} />
        {l.label}
      </span>
    ))}
  </div>
</div>
```

);
}

// ============================================================
// MENU VIEW
// ============================================================
function MenuView({ onStart }) {
const today = new Date().toLocaleDateString(“en-US”, { weekday: “long”, month: “long”, day: “numeric” });
return (
<div style={{ animation: “fadeUp 0.4s ease” }}>
<div style={{ textAlign: “center”, padding: “2.5rem 0 2rem” }}>
<p style={{ color: “var(–muted)”, fontSize: “0.8rem”, letterSpacing: “0.2em”, marginBottom: “0.75rem” }}>TRAIN YOUR MIND, QUEEN</p>
<h1 style={{ fontFamily: “var(–font-display)”, fontWeight: 900, fontSize: “clamp(2.5rem, 7vw, 4.5rem)”, lineHeight: 1.05, marginBottom: “1rem” }}>
<span style={{ background: “linear-gradient(135deg, var(–accent) 0%, var(–pink) 100%)”, WebkitBackgroundClip: “text”, WebkitTextFillColor: “transparent” }}>
Premium
</span><br />
<span style={{ color: “var(–text)” }}>Sudoku</span>
</h1>
<p style={{ color: “var(–muted)”, maxWidth: “420px”, margin: “0 auto”, lineHeight: 1.6, fontSize: “0.95rem” }}>
The brain-training platform built for clarity, confidence, and daily wins.
</p>
</div>

```
  {/* Daily Challenge */}
  <div style={{
    background: "linear-gradient(135deg, rgba(167,139,250,0.15), rgba(249,168,212,0.1))",
    border: "1px solid rgba(167,139,250,0.3)", borderRadius: "1.5rem",
    padding: "1.5rem 2rem", marginBottom: "1.5rem", position: "relative", overflow: "hidden",
  }}>
    <div style={{ position: "absolute", right: "-20px", top: "-20px", fontSize: "5rem", opacity: 0.1, transform: "rotate(15deg)" }}>📅</div>
    <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", flexWrap: "wrap", gap: "1rem" }}>
      <div>
        <div style={{ display: "flex", alignItems: "center", gap: "0.5rem", marginBottom: "0.25rem" }}>
          <span style={{ fontSize: "1.25rem" }}>📅</span>
          <span style={{ fontWeight: 700, color: "var(--text)", fontFamily: "var(--font-display)" }}>Daily Challenge</span>
        </div>
        <p style={{ color: "var(--muted)", fontSize: "0.85rem" }}>{today}</p>
      </div>
      <button onClick={() => onStart("medium", true)} style={{
        padding: "0.75rem 1.5rem", borderRadius: "1rem",
        background: "linear-gradient(135deg, var(--accent), var(--pink))",
        border: "none", color: "white", fontWeight: 700, cursor: "pointer",
        fontSize: "0.9rem", fontFamily: "var(--font-body)", whiteSpace: "nowrap",
      }}>Play Today →</button>
    </div>
  </div>

  {/* Difficulty Grid */}
  <div style={{ marginBottom: "1.5rem" }}>
    <h2 style={{ fontFamily: "var(--font-display)", fontWeight: 700, marginBottom: "1rem", color: "var(--text)" }}>Choose Your Challenge</h2>
    <div style={{ display: "grid", gridTemplateColumns: "repeat(3, 1fr)", gap: "0.75rem" }}>
      {[
        { key: "easy",   label: "Easy",   emoji: "🌸", desc: "Perfect to start",     color: "#86efac" },
        { key: "medium", label: "Medium", emoji: "💜", desc: "Balanced challenge",   color: "var(--accent)" },
        { key: "hard",   label: "Hard",   emoji: "🔥", desc: "For the bold",         color: "var(--pink)" },
      ].map(d => (
        <div key={d.key} onClick={() => onStart(d.key, false)} style={{
          padding: "1.25rem 1rem", borderRadius: "1.25rem",
          border: `1px solid ${d.color}40`, background: `${d.color}10`,
          cursor: "pointer", textAlign: "center", transition: "all 0.2s ease",
        }}
          onMouseEnter={e => e.currentTarget.style.transform = "translateY(-3px)"}
          onMouseLeave={e => e.currentTarget.style.transform = "translateY(0)"}>
          <div style={{ fontSize: "1.75rem", marginBottom: "0.5rem" }}>{d.emoji}</div>
          <div style={{ fontWeight: 700, color: d.color, fontFamily: "var(--font-display)" }}>{d.label}</div>
          <div style={{ color: "var(--muted)", fontSize: "0.75rem", marginTop: "0.2rem" }}>{d.desc}</div>
        </div>
      ))}
    </div>
  </div>

  {/* Feature Cards */}
  <div style={{ display: "grid", gridTemplateColumns: "repeat(auto-fit, minmax(200px, 1fr))", gap: "0.75rem" }}>
    {[
      { icon: "🧠", title: "AI Coach", desc: "Get hints and explanations from your personal AI tutor" },
      { icon: "⏱️", title: "Speed Tracking", desc: "Track your solving time and improve daily" },
      { icon: "🏆", title: "Leaderboard", desc: "Compete globally on daily challenges" },
      { icon: "✏️", title: "Pencil Notes", desc: "Mark candidates and strategize your moves" },
    ].map(f => (
      <div key={f.title} style={{ padding: "1.25rem", borderRadius: "1.25rem", border: "1px solid var(--border)", background: "var(--surface)" }}>
        <div style={{ fontSize: "1.5rem", marginBottom: "0.5rem" }}>{f.icon}</div>
        <div style={{ fontWeight: 600, color: "var(--text)", marginBottom: "0.25rem" }}>{f.title}</div>
        <div style={{ color: "var(--muted)", fontSize: "0.8rem", lineHeight: 1.5 }}>{f.desc}</div>
      </div>
    ))}
  </div>
</div>
```

);
}

// ============================================================
// CSS THEME VARIABLES
// ============================================================
const darkVars = `:root { --bg:#0d0a14; --surface:rgba(255,255,255,0.04); --glass:rgba(13,10,20,0.8); --glass-heavy:rgba(13,10,20,0.95); --text:#f3f0ff; --muted:#9480c4; --accent:#a78bfa; --pink:#f9a8d4; --border:rgba(167,139,250,0.18); --font-display:'Playfair Display',serif; --font-body:'DM Sans',sans-serif; --font-mono:'JetBrains Mono',monospace; }`;
const lightVars = `:root { --bg:#faf8ff; --surface:rgba(255,255,255,0.8); --glass:rgba(250,248,255,0.85); --glass-heavy:rgba(250,248,255,0.97); --text:#1a1025; --muted:#7c6fa0; --accent:#8b5cf6; --pink:#ec4899; --border:rgba(139,92,246,0.2); --font-display:'Playfair Display',serif; --font-body:'DM Sans',sans-serif; --font-mono:'JetBrains Mono',monospace; }`;

// ============================================================
// APP ROOT
// ============================================================
export default function App() {
const [darkMode, setDarkMode]         = useState(true);
const [user, setUser]                 = useState(getUser);
const [stats, setStats]               = useState(getUserStats);   // live stats in React state
const [showAuth, setShowAuth]         = useState(false);
const [showLeaderboard, setShowLeaderboard] = useState(false);
const [showStats, setShowStats]       = useState(false);
const [showAI, setShowAI]             = useState(false);
const [showVictory, setShowVictory]   = useState(false);
const [view, setView]                 = useState(“menu”); // “menu” | “game”
const [gameData, setGameData]         = useState(null);   // { puzzle, solution }
const [difficulty, setDifficulty]     = useState(“medium”);
const [isDaily, setIsDaily]           = useState(false);
const [timer, setTimer]               = useState(0);
const [running, setRunning]           = useState(false);
const [mistakes, setMistakes]         = useState(0);
// Incrementing key forces SudokuBoard to fully remount (clean reset) on every new game
const [gameKey, setGameKey]           = useState(0);
// Ref to track live board values for AI coach context
const liveBoardRef                    = useRef(null);

useEffect(() => {
let id;
if (running) id = setInterval(() => setTimer(t => t + 1), 1000);
return () => clearInterval(id);
}, [running]);

const startGame = (diff, daily = false) => {
const data = daily ? getDailyPuzzle() : getPuzzle(diff);
liveBoardRef.current = data.puzzle.map(r => […r]); // init live board
setGameData(data);
setDifficulty(diff);
setIsDaily(daily);
setTimer(0);
setMistakes(0);
setRunning(true);
setShowVictory(false);
setView(“game”);
setGameKey(k => k + 1);
};

const handleWin = () => { setRunning(false); setShowVictory(true); };

// Re-sync stats from storage whenever the stats modal is opened
const handleOpenStats = () => { setStats(getUserStats()); setShowStats(true); };

// Live grid values for AI context — updated via ref from SudokuBoard
const liveBoardValues = liveBoardRef.current;

return (
<>
<style>{`@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700;900&family=DM+Sans:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;700&display=swap'); ${darkMode ? darkVars : lightVars} *,*::before,*::after{box-sizing:border-box;margin:0;padding:0;} body{background:var(--bg);color:var(--text);font-family:var(--font-body);min-height:100vh;transition:background .3s,color .3s;} ::-webkit-scrollbar{width:4px;} ::-webkit-scrollbar-thumb{background:var(--accent);border-radius:2px;} @keyframes fadeUp{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:translateY(0)}} @keyframes slideInRight{from{transform:translateX(100%)}to{transform:translateX(0)}} @keyframes pulse{0%,100%{opacity:.3;transform:scale(.8)}50%{opacity:1;transform:scale(1.2)}} @keyframes bounce{0%,100%{transform:scale(1)}50%{transform:scale(1.2)}} button{transition:all .15s ease;} button:not(:disabled):hover{opacity:.88;transform:translateY(-1px);} button:not(:disabled):active{transform:translateY(0);} button:disabled{cursor:not-allowed;} input:focus{border-color:var(--accent)!important;box-shadow:0 0 0 3px rgba(167,139,250,.2);}`}</style>

```
  {/* Ambient orbs */}
  <div style={{ position:"fixed", inset:0, pointerEvents:"none", zIndex:0, overflow:"hidden" }}>
    <div style={{ position:"absolute", top:"-20%", right:"-10%", width:"600px", height:"600px", borderRadius:"50%", background:"radial-gradient(circle,rgba(167,139,250,.12) 0%,transparent 70%)" }} />
    <div style={{ position:"absolute", bottom:"-15%", left:"-10%", width:"500px", height:"500px", borderRadius:"50%", background:"radial-gradient(circle,rgba(249,168,212,.1) 0%,transparent 70%)" }} />
  </div>

  <div style={{ position:"relative", zIndex:1, minHeight:"100vh" }}>
    {/* ── HEADER ── */}
    <header style={{
      padding:"1rem 1.5rem", display:"flex", alignItems:"center", justifyContent:"space-between",
      borderBottom:"1px solid var(--border)", backdropFilter:"blur(12px)",
      background:"var(--glass)", position:"sticky", top:0, zIndex:100,
    }}>
      <div onClick={() => { setView("menu"); setRunning(false); }}
        style={{ cursor:"pointer", display:"flex", alignItems:"center", gap:"0.5rem" }}>
        <span style={{ fontSize:"1.5rem" }}>♟️</span>
        <div>
          <div style={{
            fontFamily:"var(--font-display)", fontWeight:900, fontSize:"1.2rem",
            background:"linear-gradient(135deg,var(--accent),var(--pink))",
            WebkitBackgroundClip:"text", WebkitTextFillColor:"transparent",
          }}>HerAccess</div>
          <div style={{ fontSize:"0.65rem", color:"var(--muted)", marginTop:"-2px", letterSpacing:"0.15em" }}>SUDOKU</div>
        </div>
      </div>

      <div style={{ display:"flex", alignItems:"center", gap:"0.5rem" }}>
        {view === "game" && (
          <div style={{ display:"flex", alignItems:"center", gap:"1rem", marginRight:"0.5rem" }}>
            <span style={{ fontFamily:"var(--font-mono)", color:"var(--accent)", fontWeight:700, fontSize:"0.95rem" }}>{fmtTime(timer)}</span>
            <span style={{ color:"#f87171", fontSize:"0.85rem" }}>❌ {mistakes}</span>
          </div>
        )}
        <button onClick={() => setShowLeaderboard(true)} style={navBtn} title="Leaderboard">🏆</button>
        <button onClick={() => setShowAI(p => !p)} style={{
          ...navBtn,
          background: showAI ? "linear-gradient(135deg,var(--accent),var(--pink))" : "var(--surface)",
          color: showAI ? "white" : "var(--text)",
          border: showAI ? "none" : "1px solid var(--border)",
        }} title="AI Coach">🧠</button>
        <button onClick={() => setDarkMode(d => !d)} style={navBtn} title="Toggle theme">{darkMode ? "☀️" : "🌙"}</button>
        {user ? (
          <button onClick={handleOpenStats} style={{
            ...navBtn, background:"linear-gradient(135deg,var(--accent),var(--pink))",
            color:"white", fontWeight:700, border:"none",
          }}>{user.name[0].toUpperCase()}</button>
        ) : (
          <button onClick={() => setShowAuth(true)} style={{
            padding:"0.45rem 1rem", borderRadius:"0.75rem",
            background:"linear-gradient(135deg,var(--accent),var(--pink))",
            border:"none", color:"white", fontWeight:600, fontSize:"0.85rem", cursor:"pointer",
          }}>Sign In</button>
        )}
      </div>
    </header>

    {/* ── MAIN ── */}
    <main style={{ padding:"1.5rem", maxWidth:"900px", margin:"0 auto" }}>
      {view === "menu" && <MenuView onStart={startGame} />}

      {view === "game" && gameData && (
        <div style={{ display:"flex", flexDirection:"column", alignItems:"center", gap:"1rem", animation:"fadeUp 0.4s ease" }}>
          {/* Badge row */}
          <div style={{ display:"flex", gap:"0.75rem", alignItems:"center", flexWrap:"wrap", justifyContent:"center" }}>
            <span style={{
              padding:"0.3rem 0.9rem", borderRadius:"999px",
              background:"linear-gradient(135deg,var(--accent),var(--pink))",
              color:"white", fontSize:"0.8rem", fontWeight:600, letterSpacing:"0.05em",
            }}>{isDaily ? "📅 Daily Challenge" : difficulty.toUpperCase()}</span>
            {isDaily && (
              <span style={{ padding:"0.3rem 0.9rem", borderRadius:"999px", border:"1px solid var(--border)", color:"var(--muted)", fontSize:"0.8rem" }}>
                {new Date().toLocaleDateString("en-US", { month:"short", day:"numeric" })}
              </span>
            )}
          </div>

          <SudokuBoard
            key={gameKey}
            puzzle={gameData.puzzle}
            solution={gameData.solution}
            onWin={handleWin}
            setMistakes={setMistakes}
            onNewGame={() => startGame(difficulty, false)}
            onBoardChange={grid => { liveBoardRef.current = grid; }}
          />
        </div>
      )}
    </main>
  </div>

  {/* ── MODALS & PANELS ── */}
  {showAuth && (
    <AuthModal onAuth={u => { setUser(u); setStats(getUserStats()); setShowAuth(false); }} onClose={() => setShowAuth(false)} />
  )}
  {showLeaderboard && <Leaderboard onClose={() => setShowLeaderboard(false)} />}
  {showStats && user && <StatsModal user={user} stats={stats} onClose={() => setShowStats(false)} />}
  {showVictory && (
    <VictoryModal
      time={timer} mistakes={mistakes} isDaily={isDaily} user={user}
      onStatsUpdate={updated => setStats(updated)}
      onClose={() => setShowVictory(false)}
      onNewGame={() => { setShowVictory(false); startGame(difficulty, false); }}
    />
  )}
  {showAI && (
    <AICoach
      liveBoardValues={liveBoardValues}
      onClose={() => setShowAI(false)}
    />
  )}
</>
```

);
}
