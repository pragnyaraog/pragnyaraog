import math, random
from xml.sax.saxutils import escape as E

NB="\u00a0"
G=["01110","10001","10000","10111","10001","10001","01110"]
P=["11110","10001","10001","11110","10000","10000","10000"]
W,H=40,24
grid=[[False]*W for _ in range(H)]
def put(glyph,c0):
    for r,row in enumerate(glyph):
        for c,ch in enumerate(row):
            if ch=="1":
                for dy in range(2):
                    for dx in range(3):
                        grid[5+r*2+dy][c0+c*3+dx]=True
put(G,3); put(P,22)
rnd=random.Random(7)
bg=[];fg=[]
for y in range(H):
    b="";f=""
    for x in range(W):
        if grid[y][x]:
            edge=any(not(0<=y+dy<H and 0<=x+dx<W and grid[y+dy][x+dx]) for dx,dy in((1,0),(-1,0),(0,1),(0,-1)))
            f+="%" if edge else "@"; b+=NB
        else:
            f+=NB
            d=math.hypot((x-19.5)/19.5,(y-11.5)/11.5)
            if d<1 and rnd.random()<0.85-0.65*d:
                ramp=".·:+" if d<0.6 else ".·.:"
                b+=rnd.choice(ramp)
            else: b+=NB
    bg.append(b);fg.append(f)

ROLES=["Full-Stack Developer","MERN Stack Builder","AI / RAG Builder"]
CW=10.8

THEMES={
"dark":dict(bg1="#030712",bg2="#0B1220",glow1="#7C3AED",glow2="#22D3EE",panel="#0F172A",pa=".45",
  text="#F8FAFC",muted="#94A3B8",label="#22D3EE",a1="#7C3AED",a2="#22D3EE",a3="#10B981",
  pill="#1E293B",pills="#334155",grid="#22D3EE",gridop=".05",ascii1="#A78BFA",ascii2="#22D3EE",
  bright1="#F8FAFC",bright2="#67E8F9",scan="#22D3EE",accent_text="#67E8F9"),
"light":dict(bg1="#FFFFFF",bg2="#EEF6FF",glow1="#2563EB",glow2="#06B6D4",panel="#FFFFFF",pa=".65",
  text="#0F172A",muted="#475569",label="#0369A1",a1="#2563EB",a2="#06B6D4",a3="#10B981",
  pill="#EFF6FF",pills="#BFDBFE",grid="#2563EB",gridop=".06",ascii1="#7C9CF5",ascii2="#06B6D4",
  bright1="#1E3A8A",bright2="#0E7490",scan="#2563EB",accent_text="#1D4ED8"),
}

def reveal(d,dur=.5):
    return f'<set attributeName="opacity" to="0" begin="0s"/><animate attributeName="opacity" from="0" to="1" begin="{d}s" dur="{dur}s" fill="freeze"/>'

def role_block(T,x,y):
    out=[];D=12.0
    for i,r in enumerate(ROLES):
        n=len(r);a=i/3;b=(i+1)/3;d=0.10
        ts=[];vs=[]
        if a>0: ts.append(0);vs.append(0)
        for k in range(1,n+1):
            ts.append(a+d*(k-1)/n);vs.append(k)
        ts.append(1.0);vs.append(n)
        kt=";".join(f"{t:.4f}" for t in ts);vl=";".join(str(v) for v in vs)
        w=lambda v:v*CW
        cl=";".join(f"{w(v):.1f}" for v in vs)
        cx=";".join(f"{x+w(v):.1f}" for v in vs)
        ok=[0];ov=[0]
        if a>0: ok+= [a];ov+=[0]
        ok+=[a+0.003,b-0.03,b-0.005,1.0];ov+=[1,1,0,0]
        okt=";".join(f"{t:.4f}" for t in ok);ovl=";".join(str(v) for v in ov)
        if i==0:
            okt="0;0.30;0.3283;1";ovl="1;1;0;0"
        out.append(f'''<clipPath id="rc{i}"><rect x="{x}" y="{y-20}" width="{w(n):.1f}" height="28"><animate attributeName="width" calcMode="discrete" values="{cl}" keyTimes="{kt}" dur="{D}s" repeatCount="indefinite"/></rect></clipPath>
<g opacity="{1 if i==0 else 0}"><animate attributeName="opacity" values="{ovl}" keyTimes="{okt}" dur="{D}s" repeatCount="indefinite"/>
<text x="{x}" y="{y}" font-size="18" font-weight="700" fill="{T['accent_text']}" clip-path="url(#rc{i})">{E(r)}</text>
<rect x="{x+w(n):.1f}" y="{y-15}" width="8" height="18" fill="{T['a2']}"><animate attributeName="x" calcMode="discrete" values="{cx}" keyTimes="{kt}" dur="{D}s" repeatCount="indefinite"/><animate attributeName="opacity" values="1;0;1" dur="1s" repeatCount="indefinite"/></rect></g>''')
    return "\n".join(out)

def build(name):
    T=THEMES[name]
    s=[]
    A=s.append
    label="Gujjula Pragnya - Computer Science student and full-stack developer. Skills: Java, Python, React.js, Node.js, MongoDB, Supabase. Projects: Focus Room and EduCampus."
    A(f'<svg xmlns="http://www.w3.org/2000/svg" width="1180" height="610" viewBox="0 0 1180 610" role="img" aria-label="{E(label)}">')
    A(f'<title>Gujjula Pragnya - GitHub profile</title><desc>{E(label)}</desc>')
    A(f'''<defs>
<linearGradient id="bgg" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="{T['bg1']}"/><stop offset="1" stop-color="{T['bg2']}"/></linearGradient>
<radialGradient id="g1" cx=".15" cy=".1" r=".6"><stop offset="0" stop-color="{T['glow1']}" stop-opacity="{'.28' if name=='dark' else '.14'}"/><stop offset="1" stop-color="{T['glow1']}" stop-opacity="0"/><animate attributeName="cx" values=".15;.3;.15" dur="16s" repeatCount="indefinite"/></radialGradient>
<radialGradient id="g2" cx=".9" cy=".95" r=".6"><stop offset="0" stop-color="{T['glow2']}" stop-opacity="{'.22' if name=='dark' else '.14'}"/><stop offset="1" stop-color="{T['glow2']}" stop-opacity="0"/><animate attributeName="cx" values=".9;.75;.9" dur="18s" repeatCount="indefinite"/></radialGradient>
<linearGradient id="bd" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="{T['a1']}"/><stop offset=".5" stop-color="{T['a2']}"/><stop offset="1" stop-color="{T['a3']}"/><animateTransform attributeName="gradientTransform" type="rotate" from="0 .5 .5" to="360 .5 .5" dur="14s" repeatCount="indefinite"/></linearGradient>
<linearGradient id="asc" gradientUnits="userSpaceOnUse" x1="0" y1="112" x2="0" y2="400"><stop offset="0" stop-color="{T['ascii1']}"/><stop offset="1" stop-color="{T['ascii2']}"/></linearGradient>
<linearGradient id="asc2" gradientUnits="userSpaceOnUse" x1="0" y1="112" x2="0" y2="400"><stop offset="0" stop-color="{T['bright1']}"/><stop offset="1" stop-color="{T['bright2']}"/></linearGradient>
<linearGradient id="scan" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="{T['scan']}" stop-opacity="0"/><stop offset=".5" stop-color="{T['scan']}" stop-opacity=".35"/><stop offset="1" stop-color="{T['scan']}" stop-opacity="0"/></linearGradient>
<pattern id="grid" width="32" height="32" patternUnits="userSpaceOnUse"><path d="M32 0H0V32" fill="none" stroke="{T['grid']}" stroke-opacity="{T['gridop']}"/></pattern>
<pattern id="lines" width="4" height="4" patternUnits="userSpaceOnUse"><rect width="4" height="1" fill="{T['grid']}" fill-opacity="{'.05' if name=='dark' else '.04'}"/></pattern>
<clipPath id="lp"><rect x="32" y="64" width="408" height="514" rx="16"/></clipPath>
<clipPath id="frame"><rect x="1" y="1" width="1178" height="608" rx="24"/></clipPath>
<filter id="glow" x="-20%" y="-20%" width="140%" height="140%"><feGaussianBlur stdDeviation="{'3' if name=='dark' else '1.5'}" result="b"/><feMerge><feMergeNode in="b"/><feMergeNode in="SourceGraphic"/></feMerge></filter>
</defs>''')
    A('<g font-family="ui-monospace,SFMono-Regular,Menlo,Monaco,Consolas,monospace">')
    A('<g clip-path="url(#frame)">')
    A('<rect width="1180" height="610" fill="url(#bgg)"/><rect width="1180" height="610" fill="url(#g1)"/><rect width="1180" height="610" fill="url(#g2)"/><rect width="1180" height="610" fill="url(#grid)"/><rect width="1180" height="610" fill="url(#lines)"/>')
    rr=random.Random(3)
    for i in range(10):
        px=rr.randint(40,1140);py=rr.randint(80,560);du=rr.randint(9,16)
        A(f'<circle cx="{px}" cy="{py}" r="1.6" fill="{T["a2"]}" opacity=".5"><animate attributeName="cy" values="{py};{py-40};{py}" dur="{du}s" repeatCount="indefinite"/><animate attributeName="opacity" values=".15;.6;.15" dur="{du}s" repeatCount="indefinite"/></circle>')
    A('</g>')
    A('<rect x="1" y="1" width="1178" height="608" rx="24" fill="none" stroke="url(#bd)" stroke-width="1.5" stroke-opacity=".8"/>')
    A(f'<g>{reveal(0.1,.4)}<circle cx="42" cy="34" r="6" fill="#FF5F56"/><circle cx="62" cy="34" r="6" fill="#FFBD2E"/><circle cx="82" cy="34" r="6" fill="#27C93F"/>')
    A(f'<text x="110" y="38" font-size="13" fill="{T["muted"]}">pragnya@developer:~</text>')
    A(f'<circle cx="1036" cy="34" r="4" fill="{T["a3"]}"><animate attributeName="opacity" values="1;.3;1" dur="2s" repeatCount="indefinite"/></circle><text x="1146" y="38" text-anchor="end" font-size="12" letter-spacing="2" fill="{T["a3"]}">[ ONLINE ]</text></g>')
    for x,w in((32,408),(464,684)):
        A(f'<rect x="{x}" y="64" width="{w}" height="514" rx="16" fill="{T["panel"]}" fill-opacity="{T["pa"]}" stroke="{T["a2"]}" stroke-opacity=".35"/>')
        A(f'<rect x="{x+1}" y="65" width="{w-2}" height="40" rx="15" fill="#FFFFFF" fill-opacity="{".03" if name=="dark" else ".35"}"/>')
    A(f'<g>{reveal(0.3,.4)}<text x="236" y="92" text-anchor="middle" font-size="12" letter-spacing="4" fill="{T["label"]}">VISUAL.MAP</text></g>')
    A('<g clip-path="url(#lp)">')
    A('<g><animateTransform attributeName="transform" type="translate" values="0 0;0 -3;0 0" dur="7s" repeatCount="indefinite"/>')
    A(f'<g><animate attributeName="opacity" values=".85;1;.85" dur="5s" repeatCount="indefinite"/>')
    for i in range(H):
        y=124+i*12;d=round(0.55+0.05*i,2)
        A(f'<g>{reveal(d,.25)}<text x="236" y="{y}" text-anchor="middle" font-size="11" fill="url(#asc)" opacity=".75" xml:space="preserve">{E(bg[i])}</text><text x="236" y="{y}" text-anchor="middle" font-size="11" font-weight="700" fill="url(#asc2)" filter="url(#glow)" xml:space="preserve">{E(fg[i])}</text></g>')
    A('</g></g>')
    A(f'<rect x="32" y="104" width="408" height="40" fill="url(#scan)"><animate attributeName="y" values="100;400;100" dur="7s" repeatCount="indefinite"/></rect>')
    A('</g>')
    A(f'<g>{reveal(2.0,.5)}<text x="236" y="440" text-anchor="middle" font-size="11" letter-spacing="3" fill="{T["muted"]}">[ PROFILE / ENGINEERING ]</text>')
    A(f'<text x="236" y="474" text-anchor="middle" font-size="20" font-weight="700" fill="{T["accent_text"]}">Full-Stack Developer</text>')
    A(f'<text x="236" y="502" text-anchor="middle" font-size="13" fill="{T["muted"]}">CS Undergrad · KITSW · Class of 2027</text>')
    A(f'<text x="236" y="548" text-anchor="middle" font-size="13" fill="{T["text"]}">~/profile $ build --ship<tspan fill="{T["a2"]}"> ▌<animate attributeName="opacity" values="1;0;1" dur="1s" repeatCount="indefinite"/></tspan></text></g>')
    A(f'<g>{reveal(0.4,.4)}<text x="806" y="92" text-anchor="middle" font-size="12" letter-spacing="4" fill="{T["label"]}">SYSTEM.INFO</text>')
    A(f'<text x="494" y="124" font-size="13" fill="{T["muted"]}"><tspan fill="{T["a3"]}">pragnya@developer</tspan>:~$ ./profile.sh</text></g>')
    LX,VX=600,620
    def row(lbl,y,d):
        return f'<text x="{LX}" y="{y}" text-anchor="end" font-size="12" letter-spacing="2" fill="{T["label"]}">&gt; {lbl}</text>'
    A(f'<g>{reveal(1.0)}{row("NAME",166,0)}<text x="{VX}" y="168" font-size="26" font-weight="800" fill="{T["text"]}">Gujjula Pragnya</text></g>')
    A(f'<g>{reveal(1.3)}{row("ROLE",206,0)}</g>')
    A(f'<g>{reveal(1.3)}{role_block(T,VX,207)}</g>')
    vals=[("LOCATION",238,"Telangana, India"),("EDUCATION",268,"B.Tech CSE · KITSW Warangal · CGPA 9.17"),("EXPERIENCE",298,"Full Stack Developer Intern · KITSW Startup"),("FOCUS",328,"Full-Stack · REST APIs · RAG / LLMs")]
    for i,(l,y,v) in enumerate(vals):
        A(f'<g>{reveal(1.6+i*.15)}{row(l,y,0)}<text x="{VX}" y="{y}" font-size="14" fill="{T["text"]}">{E(v)}</text></g>')
    A(f'<g>{reveal(2.3)}{row("STACK",364,0)}')
    rows=[["Java","Python","React.js","Node.js","Express.js"],["MongoDB","Supabase","MySQL","REST APIs","Git & GitHub"]]
    k=0
    for ri,rw in enumerate(rows):
        x=VX;y=346+ri*32
        for t in rw:
            w=len(t)*7.4+30
            A(f'<g><animateTransform attributeName="transform" type="translate" values="0 0;0 -1.5;0 0" dur="{5+k%3}s" begin="{k*.4}s" repeatCount="indefinite"/><rect x="{x:.1f}" y="{y}" width="{w:.1f}" height="24" rx="12" fill="{T["pill"]}" fill-opacity="{".7" if name=="dark" else ".9"}" stroke="{T["pills"]}"/><circle cx="{x+12:.1f}" cy="{y+12}" r="3" fill="{T["a3"]}"/><text x="{x+22:.1f}" y="{y+16}" font-size="12" fill="{T["text"]}">{E(t)}</text></g>')
            x+=w+8;k+=1
    A('</g>')
    A(f'<g>{reveal(2.7)}{row("PROJECTS",450,0)}')
    A(f'<text x="{VX}" y="450" font-size="14" fill="{T["text"]}"><tspan font-weight="700" fill="{T["accent_text"]}">Focus Room</tspan>  AI study assistant (RAG + LLMs)</text>')
    A(f'<text x="{VX}" y="480" font-size="14" fill="{T["text"]}"><tspan font-weight="700" fill="{T["accent_text"]}">EduCampus</tspan>  MERN college management portal</text></g>')
    A(f'<line x1="494" y1="508" x2="1118" y2="508" stroke="{T["a2"]}" stroke-opacity=".25"/>')
    A(f'<g>{reveal(3.1)}{row("LINKS",542,0)}<text x="{VX}" y="542" font-size="14" fill="{T["text"]}">GitHub · LinkedIn · pragnyarao8@gmail.com</text></g>')
    A('</g></svg>')
    return "\n".join(s)

for n in ("dark","light"):
    open(f"{n}.svg","w",encoding="utf-8").write(build(n))
print("Done: dark.svg and light.svg created")
