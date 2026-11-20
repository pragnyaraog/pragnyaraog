
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Pragnya | Developer Profile</title>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: monospace;
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 25px;
    transition: 0.4s;
}

body.dark {
    --bg1: #030712;
    --bg2: #0b1220;
    --panel: rgba(15, 23, 42, 0.85);
    --text: #f8fafc;
    --muted: #94a3b8;
    --accent: #22d3ee;
    --purple: #7c3aed;
    --pill: #1e293b;
    --border: #334155;
    --glow: rgba(34, 211, 238, .2);
    background: linear-gradient(135deg, var(--bg1), var(--bg2));
}

body.light {
    --bg1: #ffffff;
    --bg2: #eef6ff;
    --panel: rgba(255,255,255,.88);
    --text: #0f172a;
    --muted: #475569;
    --accent: #2563eb;
    --purple: #06b6d4;
    --pill: #eff6ff;
    --border: #bfdbfe;
    --glow: rgba(37, 99, 235, .15);
    background: linear-gradient(135deg, var(--bg1), var(--bg2));
}

.container {
    width: 100%;
    max-width: 1180px;
    padding: 2px;
    border-radius: 24px;
    background: linear-gradient(135deg, #7c3aed, #22d3ee, #10b981);
    animation: borderGlow 5s infinite alternate;
}

@keyframes borderGlow {
    0% { filter: hue-rotate(0deg); }
    100% { filter: hue-rotate(80deg); }
}

.main {
    position: relative;
    border-radius: 22px;
    padding: 25px;
    background: var(--bg2);
    overflow: hidden;
    color: var(--text);
}

.main::before {
    content: "";
    position: absolute;
    inset: 0;
    background:
        radial-gradient(circle at 10% 10%, var(--glow), transparent 35%),
        radial-gradient(circle at 90% 90%, var(--glow), transparent 35%);
    pointer-events: none;
}

.grid-bg {
    position: absolute;
    inset: 0;
    opacity: .06;
    background-image:
        linear-gradient(var(--accent) 1px, transparent 1px),
        linear-gradient(90deg, var(--accent) 1px, transparent 1px);
    background-size: 32px 32px;
    pointer-events: none;
}

.topbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 25px;
    position: relative;
    z-index: 1;
}

.dots {
    display: flex;
    gap: 10px;
}

.dot {
    width: 12px;
    height: 12px;
    border-radius: 50%;
}

.red { background: #ff5f56; }
.yellow { background: #ffbd2e; }
.green { background: #27c93f; }

.terminal-title {
    color: var(--muted);
    margin-left: 20px;
    font-size: 13px;
}

.online {
    color: #10b981;
    font-size: 12px;
}

.theme-btn {
    background: var(--pill);
    color: var(--text);
    border: 1px solid var(--border);
    padding: 8px 12px;
    border-radius: 8px;
    cursor: pointer;
    font-family: monospace;
}

.content {
    display: grid;
    grid-template-columns: 408px 1fr;
    gap: 24px;
    position: relative;
    z-index: 1;
}

.panel {
    background: var(--panel);
    border: 1px solid var(--border);
    border-radius: 16px;
    overflow: hidden;
    backdrop-filter: blur(10px);
}

.panel-heading {
    text-align: center;
    padding: 16px;
    letter-spacing: 4px;
    font-size: 12px;
    color: var(--accent);
    border-bottom: 1px solid var(--border);
}

.left-panel {
    text-align: center;
    padding-bottom: 20px;
}

.ascii {
    height: 330px;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
    position: relative;
}

.ascii pre {
    font-size: 10px;
    line-height: 1.05;
    white-space: pre;
    background: linear-gradient(var(--purple), var(--accent));
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
    animation: float 5s ease-in-out infinite;
}

@keyframes float {
    0%,100% { transform: translateY(0); }
    50% { transform: translateY(-5px); }
}

.scan {
    position: absolute;
    left: 0;
    width: 100%;
    height: 35px;
    background: linear-gradient(transparent, var(--glow), transparent);
    animation: scan 5s linear infinite;
}

@keyframes scan {
    0% { top: 0; }
    100% { top: 100%; }
}

.profile-label {
    color: var(--muted);
    font-size: 11px;
    letter-spacing: 3px;
    margin-top: 10px;
}

.profile-title {
    color: var(--accent);
    margin: 15px 0;
    font-size: 20px;
}

.profile-info {
    font-size: 12px;
    color: var(--muted);
}

.terminal {
    margin-top: 20px;
    color: var(--text);
    font-size: 12px;
}

.cursor {
    color: var(--accent);
    animation: blink 1s infinite;
}

@keyframes blink {
    50% { opacity: 0; }
}

/* Right panel */

.right-panel {
    padding: 25px;
}

.command {
    color: var(--muted);
    font-size: 13px;
    margin-bottom: 25px;
}

.command span {
    color: #10b981;
}

.info-row {
    display: grid;
    grid-template-columns: 125px 1fr;
    gap: 10px;
    margin-bottom: 25px;
    align-items: center;
}

.label {
    color: var(--accent);
    font-size: 12px;
    letter-spacing: 2px;
    text-align: right;
}

.name {
    font-size: 25px;
    font-weight: bold;
}

.role {
    color: var(--accent);
    font-weight: bold;
    font-size: 17px;
    height: 25px;
}

.value {
    font-size: 13px;
    color: var(--text);
}

.skills {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
}

.skill {
    display: flex;
    align-items: center;
    gap: 8px;
    background: var(--pill);
    border: 1px solid var(--border);
    border-radius: 30px;
    padding: 6px 12px;
    font-size: 12px;
    animation: skillFloat 4s ease-in-out infinite;
}

.skill:nth-child(even) {
    animation-delay: 1s;
}

.skill::before {
    content: "";
    width: 6px;
    height: 6px;
    background: #10b981;
    border-radius: 50%;
}

@keyframes skillFloat {
    0%,100% { transform: translateY(0); }
    50% { transform: translateY(-2px); }
}

.project {
    font-size: 13px;
    margin-bottom: 18px;
}

.project strong {
    color: var(--accent);
}

.divider {
    border: none;
    border-top: 1px solid var(--border);
    margin: 20px 0;
}

.links {
    font-size: 13px;
    line-height: 2;
}

.links a {
    color: var(--accent);
    text-decoration: none;
}

.links a:hover {
    text-decoration: underline;
}

.fade {
    opacity: 0;
    animation: reveal .8s ease forwards;
}

@keyframes reveal {
    to { opacity: 1; }
}

/* Responsive */

@media(max-width: 900px) {
    .content {
        grid-template-columns: 1fr;
    }

    .ascii {
        height: 300px;
    }
}

@media(max-width: 500px) {
    body {
        padding: 10px;
    }

    .main {
        padding: 15px;
    }

    .right-panel {
        padding: 15px;
    }

    .info-row {
        grid-template-columns: 95px 1fr;
    }

    .label {
        font-size: 10px;
    }

    .name {
        font-size: 19px;
    }

    .role {
        font-size: 14px;
    }

    .value {
        font-size: 11px;
    }

    .ascii pre {
        font-size: 8px;
    }
}
</style>
</head>

<body class="dark">

<div class="container">
<div class="main">

<div class="grid-bg"></div>

<!-- Top Bar -->
<div class="topbar">
    <div style="display:flex;align-items:center">
        <div class="dots">
            <div class="dot red"></div>
            <div class="dot yellow"></div>
            <div class="dot green"></div>
        </div>
        <span class="terminal-title">pragnya@developer:~</span>
    </div>

    <div style="display:flex;gap:15px;align-items:center">
        <span class="online">● [ ONLINE ]</span>
        <button class="theme-btn" onclick="toggleTheme()">☀ / ☾</button>
    </div>
</div>

<div class="content">

<!-- Left Side -->
<div class="panel left-panel fade">

    <div class="panel-heading">VISUAL.MAP</div>

    <div class="ascii">
        <div class="scan"></div>
        <pre id="asciiArt"></pre>
    </div>

    <div class="profile-label">[ PROFILE / ENGINEERING ]</div>

    <div class="profile-title">Full-Stack Developer</div>

    <div class="profile-info">
        CS Undergrad · KITSW · Class of 2027
    </div>

    <div class="terminal">
        ~/profile $ build --ship
        <span class="cursor">▌</span>
    </div>

</div>

<!-- Right Side -->
<div class="panel right-panel fade">

    <div class="panel-heading">SYSTEM.INFO</div>

    <div class="command">
        <span>pragnya@developer</span>:~$ ./profile.sh
    </div>

    <div class="info-row">
        <div class="label">&gt; NAME</div>
        <div class="name">Gujjula Pragnya</div>
    </div>

    <div class="info-row">
        <div class="label">&gt; ROLE</div>
        <div class="role" id="role"></div>
    </div>

    <div class="info-row">
        <div class="label">&gt; LOCATION</div>
        <div class="value">Telangana, India</div>
    </div>

    <div class="info-row">
        <div class="label">&gt; EDUCATION</div>
        <div class="value">B.Tech CSE · KITS Warangal · CGPA 9.17</div>
    </div>

    <div class="info-row">
        <div class="label">&gt; EXPERIENCE</div>
        <div class="value">Full Stack Developer Intern · KITSW Startup</div>
    </div>

    <div class="info-row">
        <div class="label">&gt; FOCUS</div>
        <div class="value">Full-Stack · REST APIs · RAG / LLMs</div>
    </div>

    <div class="info-row">
        <div class="label">&gt; STACK</div>
        <div>
            <div class="skills">
                <span class="skill">Java</span>
                <span class="skill">Python</span>
                <span class="skill">React.js</span>
                <span class="skill">Node.js</span>
                <span class="skill">Express.js</span>
            </div>

            <div class="skills" style="margin-top:10px">
                <span class="skill">MongoDB</span>
                <span class="skill">Supabase</span>
                <span class="skill">MySQL</span>
                <span class="skill">REST APIs</span>
                <span class="skill">Git & GitHub</span>
            </div>
        </div>
    </div>

    <div class="info-row">
        <div class="label">&gt; PROJECTS</div>
        <div>
            <div class="project">
                <strong>Focus Room</strong><br>
                AI study assistant (RAG + LLMs)
            </div>

            <div class="project">
                <strong>EduCampus</strong><br>
                MERN college management portal
            </div>
        </div>
    </div>

    <hr class="divider">

    <div class="info-row">
        <div class="label">&gt; LINKS</div>
        <div class="links">
            <a href="https://github.com/" target="_blank">GitHub</a> ·
            <a href="https://linkedin.com/" target="_blank">LinkedIn</a> ·
            <a href="mailto:pragnyarao8@gmail.com">pragnyarao8@gmail.com</a>
        </div>
    </div>

</div>
</div>
</div>
</div>

<script>
/* ASCII ART GENERATOR */

const G = [
"01110",
"10001",
"10000",
"10111",
"10001",
"10001",
"01110"
];

const P = [
"11110",
"10001",
"10001",
"11110",
"10000",
"10000",
"10000"
];

const W = 40;
const H = 24;

let grid = Array.from(
    {length:H},
    () => Array(W).fill(false)
);

function put(glyph,c0) {
    glyph.forEach((row,r) => {
        [...row].forEach((ch,c) => {
            if(ch === "1") {
                for(let dy=0;dy<2;dy++) {
                    for(let dx=0;dx<3;dx++) {
                        grid[5+r*2+dy][c0+c*3+dx] = true;
                    }
                }
            }
        });
    });
}

put(G,3);
put(P,22);

const NB = "\u00a0";
const bg = [];
const fg = [];

function random(seed) {
    let x = seed;
    return function() {
        x = (x * 16807) % 2147483647;
        return (x - 1) / 2147483646;
    };
}

const rnd = random(7);

for(let y=0;y<H;y++) {
    let b="",f="";

    for(let x=0;x<W;x++) {
        if(grid[y][x]) {

            let edge = [
                [1,0],[-1,0],[0,1],[0,-1]
            ].some(([dx,dy]) => {
                let ny=y+dy,nx=x+dx;
                return !(ny>=0 && ny<H && nx>=0 && nx<W && grid[ny][nx]);
            });

            f += edge ? "%" : "@";
            b += NB;

        } else {
            f += NB;

            let d = Math.hypot(
                (x-19.5)/19.5,
                (y-11.5)/11.5
            );

            if(d<1 && rnd()<0.85-0.65*d) {
                let ramp = d<0.6 ? ".·:+" : ".·.:";
                b += ramp[Math.floor(rnd()*ramp.length)];
            } else {
                b += NB;
            }
        }
    }

    bg.push(b);
    fg.push(f);
}

document.getElementById("asciiArt").textContent =
    bg.map((line,i) => line + "\n" + fg[i]).join("\n");


/* ROLE ANIMATION */

const roles = [
    "Full-Stack Developer",
    "MERN Stack Builder",
    "AI / RAG Builder"
];

const roleElement = document.getElementById("role");

let roleIndex = 0;
let charIndex = 0;
let deleting = false;

function typeRole() {

    let current = roles[roleIndex];

    if(!deleting) {
        roleElement.textContent =
            current.substring(0,charIndex+1);

        charIndex++;

        if(charIndex === current.length) {
            deleting = true;
            setTimeout(typeRole,1500);
            return;
        }

    } else {

        roleElement.textContent =
            current.substring(0,charIndex-1);

        charIndex--;

        if(charIndex === 0) {
            deleting = false;
            roleIndex = (roleIndex+1)%roles.length;
        }
    }

    setTimeout(typeRole,deleting ? 45 : 90);
}

typeRole();


/* THEME TOGGLE */

function toggleTheme() {
    document.body.classList.toggle("dark");
    document.body.classList.toggle("light");
}
</script>

</body>
</html>
