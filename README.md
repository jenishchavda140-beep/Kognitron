#kognitron
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kognitron | Premium AI Directory</title>
    <style>
        :root {
            --accent: #7c4dff;
            --accent-glow: rgba(124, 77, 255, 0.3);
            --bg: #030508;
            --card-bg: #0f121a;
            --text: #ffffff;
            --text-dim: #94a3b8;
            --kyuri-bg: #131620;
        }

        * { 
            margin: 0; padding: 0; box-sizing: border-box; 
            font-family: 'Plus Jakarta Sans', sans-serif;
            user-select: none; 
        }

        body { background-color: var(--bg); color: var(--text); overflow-x: hidden; }

        .glow {
            position: fixed; width: 600px; height: 600px;
            background: radial-gradient(circle, var(--accent-glow) 0%, transparent 70%);
            top: -200px; right: -200px; z-index: -1;
        }

        header {
            padding: 1.2rem 8%; display: flex; justify-content: space-between; align-items: center;
            background: rgba(3, 5, 8, 0.8); backdrop-filter: blur(20px);
            position: sticky; top: 0; z-index: 1000; border-bottom: 1px solid rgba(255,255,255,0.05);
        }

        /* Professional Website Logo */
        .logo-wrapper { display: flex; align-items: center; gap: 10px; cursor: pointer; }
        .main-logo-svg { width: 32px; height: 32px; fill: var(--accent); filter: drop-shadow(0 0 5px var(--accent-glow)); }
        .logo { font-size: 1.6rem; font-weight: 800; letter-spacing: -1px; }
        .logo span { color: var(--accent); }

        .nav-links { display: flex; gap: 20px; align-items: center; }
        .nav-link { cursor: pointer; font-weight: 600; font-size: 0.9rem; color: var(--text-dim); transition: 0.3s; }
        .nav-link:hover { color: var(--accent); }

        #homeView { padding: 40px 8%; max-width: 1400px; margin: 0 auto; }
        
        .hero-section { text-align: center; margin-bottom: 50px; padding-top: 20px; }
        .hero-section h1 { font-size: clamp(2.2rem, 5vw, 3.5rem); line-height: 1.2; margin-bottom: 30px; }
        .hero-section span { color: var(--accent); }

        .search-wrapper { max-width: 600px; margin: 0 auto 30px; position: relative; }
        #searchInput {
            width: 100%; padding: 18px 25px; border-radius: 100px;
            background: var(--card-bg); border: 1px solid rgba(255,255,255,0.1);
            color: white; font-size: 1rem; outline: none; transition: 0.3s;
        }
        #searchInput:focus { border-color: var(--accent); box-shadow: 0 0 25px var(--accent-glow); }

        .filter-container {
            display: flex; gap: 10px; justify-content: center; flex-wrap: wrap; margin-bottom: 40px;
        }
        .filter-btn {
            background: var(--card-bg); color: var(--text-dim); padding: 8px 18px;
            border-radius: 50px; border: 1px solid rgba(255,255,255,0.1);
            cursor: pointer; font-size: 0.85rem; font-weight: 600; transition: 0.3s;
        }
        .filter-btn:hover, .filter-btn.active {
            background: var(--accent); color: white; border-color: var(--accent);
            box-shadow: 0 0 15px var(--accent-glow);
        }

        .grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 20px; }
        .cat-card {
            background: var(--card-bg); padding: 25px; border-radius: 20px;
            border: 1px solid rgba(255,255,255,0.03); cursor: pointer; transition: 0.4s;
        }
        .cat-card:hover { transform: translateY(-5px); border-color: var(--accent); background: #161b26; }

        #detailView, #contactView { display: none; padding: 60px 8%; max-width: 1000px; margin: 0 auto; }
        .back-link { color: var(--accent); cursor: pointer; margin-bottom: 30px; display: block; font-weight: 700; }

        #kyuriPage {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: var(--bg); z-index: 2000; display: none; flex-direction: column;
            animation: slideUp 0.4s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .kyuri-header {
            padding: 20px 8%; display: flex; justify-content: space-between; align-items: center;
            border-bottom: 1px solid rgba(255,255,255,0.05); background: rgba(19, 22, 32, 0.9);
        }
        .kyuri-logo-box { display: flex; align-items: center; gap: 12px; }
        .kyuri-svg-logo { width: 40px; height: 40px; background: linear-gradient(135deg, var(--accent), #a29bfe); border-radius: 10px; padding: 8px; fill: white; }
        
        .exit-btn {
            background: rgba(255,255,255,0.05); color: white; padding: 10px 20px;
            border-radius: 10px; cursor: pointer; font-weight: 600; transition: 0.3s;
        }
        .exit-btn:hover { background: #ff4757; }

        .chat-area { flex: 1; padding: 40px 8%; overflow-y: auto; display: flex; flex-direction: column; gap: 25px; }
        .msg { max-width: 800px; line-height: 1.6; }
        .bot-msg { align-self: flex-start; color: #e2e8f0; }
        .user-msg { align-self: flex-end; background: var(--accent); padding: 12px 20px; border-radius: 18px; border-bottom-right-radius: 2px; }
        
        .input-container { padding: 25px 8%; background: var(--kyuri-bg); display: flex; gap: 15px; }
        #kyuriInput { flex: 1; background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.1); padding: 15px; border-radius: 15px; color: white; outline: none; }

        .kyuri-float {
            position: fixed; bottom: 30px; right: 30px; width: 65px; height: 65px;
            background: var(--accent); border-radius: 20px; display: flex;
            align-items: center; justify-content: center; cursor: pointer; z-index: 1000;
            box-shadow: 0 10px 25px var(--accent-glow);
        }

        .go-btn {
            display: inline-block; text-decoration: none; background: var(--accent); color: white; 
            padding: 16px 45px; border-radius: 14px; font-weight: 800; margin-bottom: 40px; 
            box-shadow: 0 10px 20px var(--accent-glow); transition: 0.3s;
        }
        .go-btn:hover { transform: scale(1.03); filter: brightness(1.1); }

        @keyframes slideUp { from { transform: translateY(100%); } to { transform: translateY(0); } }
    </style>
</head>
<body oncontextmenu="return false;">

    <div class="glow"></div>

    <header>
        <div class="logo-wrapper" onclick="showHome()">
            <svg class="main-logo-svg" viewBox="0 0 24 24"><path d="M12 2L4.5 20.29L5.21 21L12 18L18.79 21L19.5 20.29L12 2Z"/></svg>
            <div class="logo">Kogni<span>tron</span></div>
        </div>
        <div class="nav-links">
            <span class="nav-link" onclick="showContact()">Suggest Tool</span>
        </div>
    </header>

    <div id="homeView">
        <div class="hero-section">
            <h1>Master the <span>AI Frontier</span><br>with Kognitron Intelligence.</h1>
            <div class="search-wrapper">
                <input type="text" id="searchInput" onkeyup="filterContent()" placeholder="Search 100+ AI tools...">
            </div>
            <div class="filter-container" id="filterBar">
                <button class="filter-btn active" onclick="filterGroup('All', this)">All</button>
                <button class="filter-btn" onclick="filterGroup('Creative', this)">Creative</button>
                <button class="filter-btn" onclick="filterGroup('Tech', this)">Tech</button>
                <button class="filter-btn" onclick="filterGroup('Business', this)">Business</button>
                <button class="filter-btn" onclick="filterGroup('Lifestyle', this)">Lifestyle</button>
            </div>
        </div>
        <div class="grid" id="categoryGrid"></div>
    </div>

    <div id="detailView">
        <div id="toolDetailContent"></div>
    </div>

    <div id="contactView">
        <span class="back-link" onclick="showHome()">&larr; Back to Directory</span>
        <h2 style="font-size: 2.5rem; margin-bottom: 10px;">Developer <span>Portal</span></h2>
        
        <div style="background: linear-gradient(135deg, var(--card-bg), #161b26); padding: 30px; border-radius: 20px; border: 1px solid var(--accent-glow); margin-bottom: 40px; display: flex; align-items: center; gap: 20px;">
            <div style="background: var(--accent); width: 50px; height: 50px; border-radius: 12px; display: flex; align-items: center; justify-content: center; font-size: 1.5rem;">✉</div>
            <div>
                <p style="color: var(--text-dim); font-size: 0.8rem; text-transform: uppercase;">Direct Inquiry</p>
                <a href="mailto:jenishchavda140@gmail.com" style="color: white; text-decoration: none; font-size: 1.2rem; font-weight: 700;">jenishchavda140@gmail.com</a>
            </div>
        </div>

        <div style="background: var(--card-bg); padding: 40px; border-radius: 25px; border: 1px solid rgba(255,255,255,0.05);">
            <div style="margin-bottom: 20px;">
                <label style="display:block; margin-bottom:10px;">Tool Name</label>
                <input type="text" id="toolName" placeholder="e.g. Sora" style="width:100%; background:rgba(255,255,255,0.03); border:1px solid rgba(255,255,255,0.1); padding:15px; border-radius:12px; color:white; outline:none;">
            </div>
            <button onclick="submitSuggestion()" style="width:100%; background:var(--accent); color:white; border:none; padding:18px; border-radius:12px; font-weight:700; cursor:pointer;">Submit to Kognitron</button>
        </div>
    </div>

    <div id="kyuriPage">
        <div class="kyuri-header">
            <div class="kyuri-logo-box">
                <svg class="kyuri-svg-logo" viewBox="0 0 24 24"><path d="M12 2L4.5 20.29L5.21 21L12 18L18.79 21L19.5 20.29L12 2Z"/></svg>
                <div><div style="font-weight:800;">Kyuri AI</div><div style="font-size:0.7rem; color:#4cd137;">● Kognitron Core</div></div>
            </div>
            <div class="exit-btn" onclick="closeKyuri()">Exit Assistant</div>
        </div>
        <div class="chat-area" id="kyuriFlow">
            <div class="msg bot-msg"><b>Interface Ready</b><br>I am Kyuri. I've mapped the Kognitron directory for you. How can I assist with Jenish's project today?</div>
        </div>
        <div class="input-container">
            <input type="text" id="kyuriInput" placeholder="Query Kognitron..." onkeypress="if(event.key=='Enter') sendToKyuri()">
            <button onclick="sendToKyuri()" style="background:var(--accent); color:white; border:none; padding:0 20px; border-radius:12px; cursor:pointer;">Send</button>
        </div>
    </div>

    <div class="kyuri-float" onclick="openKyuri()">
        <svg style="width:30px; height:30px; fill:white;" viewBox="0 0 24 24"><path d="M12 2L4.5 20.29L5.21 21L12 18L18.79 21L19.5 20.29L12 2Z"/></svg>
    </div>

    <script>
        const db = {
            "Art & Illustration": [
                {n: "Midjourney", d: "Leading high-end art generation specializing in realism and aesthetic textures.", l: "https://www.midjourney.com"}, 
                {n: "DALL-E 3", d: "OpenAI's precise image generator known for following complex instructions.", l: "https://openai.com/dall-e-3"}
            ],
            "Video Editing": [
                {n: "Runway Gen-3", d: "Next-gen cinematic video synthesis for professional workflows.", l: "https://runwayml.com"}, 
                {n: "Luma Dream Machine", d: "High-fidelity AI video that understands physics and movement.", l: "https://lumalabs.ai"}
            ],
            "Coding": [
                {n: "GitHub Copilot", d: "The global industry standard for AI-assisted programming.", l: "https://github.com/features/copilot"}, 
                {n: "Cursor", d: "An AI-native code editor that manages entire folders of code efficiently.", l: "https://cursor.sh"}
            ],
            "Music Production": [
                {n: "Suno AI", d: "Generate complete songs with lyrics and vocals from text prompts.", l: "https://suno.com"},
                {n: "Udio", d: "Professional-grade music synthesis with emotional depth.", l: "https://www.udio.com"}
            ],
            "Voice Synthesis": [
                {n: "ElevenLabs", d: "Top-tier realistic voice cloning and text-to-speech engine.", l: "https://elevenlabs.io"},
                {n: "Murf AI", d: "High-quality voiceover studio for marketing and narration.", l: "https://murf.ai"}
            ],
            "Cybersecurity": [
                {n: "Darktrace", d: "Autonomous AI system for real-time threat detection and response.", l: "https://darktrace.com"},
                {n: "Snyk", d: "Scans code and containers to fix security vulnerabilities instantly.", l: "https://snyk.io"}
            ]
        };

        const niches = ["Logo Design", "3D Modeling", "Copywriting", "UI/UX Design", "Animation", "Photography", "Web Development", "Data Science", "DevOps", "Blockchain", "Cloud Computing", "Legal", "Project Management", "CRM", "Accounting", "HR & Recruiting", "SEO", "Language Learning", "Fitness", "Travel", "Healthcare", "E-commerce", "Real Estate", "Logistics"];
        
        niches.forEach(name => {
            if(!db[name]) {
                db[name] = [{n: `${name} Pro`, d: `Automated AI solution for the ${name.toLowerCase()} sector.`, l: "https://google.com"}];
            }
        });

        const groups = {
            "Creative": ["Art & Illustration", "Video Editing", "Logo Design", "Music Production", "Voice Synthesis", "3D Modeling", "Copywriting", "UI/UX Design", "Animation", "Photography"],
            "Tech": ["Coding", "Web Development", "Cybersecurity", "Data Science", "DevOps", "Blockchain", "Cloud Computing"],
            "Business": ["Legal", "Project Management", "CRM", "Accounting", "HR & Recruiting", "SEO", "E-commerce", "Real Estate", "Logistics"],
            "Lifestyle": ["Research", "Language Learning", "Fitness", "Travel", "Healthcare"]
        };

        function displayCats(filterList = null) {
            const grid = document.getElementById('categoryGrid');
            grid.innerHTML = '';
            Object.keys(db).sort().forEach(key => {
                if (filterList && !filterList.includes(key)) return;
                const card = document.createElement('div');
                card.className = 'cat-card';
                card.onclick = () => openCat(key);
                card.innerHTML = `<span style="color:var(--accent); font-size:0.7rem; font-weight:800;">CORE</span><h3 style="margin-top:5px;">${key}</h3>`;
                grid.appendChild(card);
            });
        }

        function openCat(key) {
            hideAll();
            document.getElementById('detailView').style.display = 'block';
            const content = document.getElementById('toolDetailContent');
            content.innerHTML = `
                <span class="back-link" onclick="showHome()">&larr; Back to Home</span>
                <h2 style="font-size: 2.5rem; margin-bottom: 30px;">${key}</h2>
                <div id="toolsList"></div>
            `;
            const list = document.getElementById('toolsList');
            db[key].forEach((t, index) => {
                const toolCard = document.createElement('div');
                toolCard.style = "background:#161b26; padding:25px; border-radius:15px; margin-bottom:15px; border-left:4px solid var(--accent); cursor:pointer;";
                toolCard.onclick = () => openToolPage(key, index);
                toolCard.innerHTML = `<h3>${t.n}</h3><p style="color:var(--text-dim); margin-top:10px;">${t.d.substring(0, 100)}...</p>`;
                list.appendChild(toolCard);
            });
        }

        function openToolPage(catKey, toolIndex) {
            const tool = db[catKey][toolIndex];
            const content = document.getElementById('toolDetailContent');
            content.innerHTML = `
                <span class="back-link" onclick="openCat('${catKey}')">&larr; Back to ${catKey}</span>
                <div style="background: var(--card-bg); padding: 40px; border-radius: 25px; border: 1px solid var(--accent-glow);">
                    <h1 style="font-size: 3rem; margin-bottom: 10px;">${tool.n}</h1>
                    <p style="color: var(--accent); font-weight: 700; margin-bottom: 30px;">KOGNITRON VERIFIED TOOL</p>
                    
                    <a href="${tool.l}" target="_blank" class="go-btn">GO TO AI TOOL</a>

                    <div style="border-top: 1px solid rgba(255,255,255,0.1); padding-top: 30px;">
                        <h3 style="margin-bottom: 15px; color: var(--text);">About this Tool</h3>
                        <p style="color: var(--text-dim); line-height: 1.8; font-size: 1.1rem;">${tool.d}</p>
                    </div>
                </div>
            `;
        }

        function filterGroup(groupName, btn) {
            document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
            btn.classList.add('active');
            displayCats(groupName === 'All' ? null : groups[groupName]);
        }

        function filterContent() {
            const val = document.getElementById('searchInput').value.toLowerCase();
            const cards = document.getElementsByClassName('cat-card');
            for(let card of cards) {
                card.style.display = card.innerText.toLowerCase().includes(val) ? "" : "none";
            }
        }

        function hideAll() {
            document.getElementById('homeView').style.display = 'none';
            document.getElementById('detailView').style.display = 'none';
            document.getElementById('contactView').style.display = 'none';
        }

        function showHome() {
            hideAll();
            document.getElementById('homeView').style.display = 'block';
        }

        function showContact() {
            hideAll();
            document.getElementById('contactView').style.display = 'block';
        }

        function openKyuri() { document.getElementById('kyuriPage').style.display = 'flex'; }
        function closeKyuri() { document.getElementById('kyuriPage').style.display = 'none'; }

        function sendToKyuri() {
            const el = document.getElementById('kyuriInput');
            if(!el.value) return;
            appendMsg(el.value, 'user-msg');
            el.value = '';
            setTimeout(() => appendMsg("Analyzing Kognitron index... I've found the best tool match for Jenish's project.", 'bot-msg'), 700);
        }

        function appendMsg(t, c) {
            const f = document.getElementById('kyuriFlow');
            const d = document.createElement('div');
            d.className = `msg ${c}`;
            d.innerHTML = t;
            f.appendChild(d);
            f.scrollTop = f.scrollHeight;
        }

        function submitSuggestion() {
            alert("Sent to jenishchavda140@gmail.com for review.");
            showHome();
        }

        displayCats();
    </script>
</body>
</html>
