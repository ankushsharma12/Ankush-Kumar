<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>GitHub Profile Generator – Professional</title>
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;600&family=IBM+Plex+Sans:wght@300;400;600;700&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #f4f6f9;
    --surface: #ffffff;
    --border: #d0d7de;
    --accent: #0969da;
    --accent2: #1a7f37;
    --text: #1f2328;
    --muted: #57606a;
    --card: #f6f8fa;
    --shadow: 0 1px 3px rgba(31,35,40,0.12), 0 8px 24px rgba(66,74,83,0.06);
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { background: var(--bg); color: var(--text); font-family: 'IBM Plex Sans', sans-serif; min-height: 100vh; padding: 28px 20px; }
  .header { text-align: center; margin-bottom: 32px; }
  .header-badge { display: inline-block; background: #dff7e9; color: var(--accent2); border: 1px solid #9be9a8; border-radius: 20px; padding: 3px 14px; font-size: 0.72rem; font-family: 'IBM Plex Mono', monospace; letter-spacing: 1px; text-transform: uppercase; margin-bottom: 12px; }
  h1 { font-size: clamp(1.4rem, 3.5vw, 2.2rem); font-weight: 700; color: var(--text); letter-spacing: -0.5px; }
  .header-sub { color: var(--muted); font-size: 0.9rem; margin-top: 6px; font-weight: 300; }
  .layout { display: grid; grid-template-columns: 420px 1fr; gap: 20px; max-width: 1300px; margin: 0 auto; }
  @media(max-width: 960px) { .layout { grid-template-columns: 1fr; } }
  .card { background: var(--surface); border: 1px solid var(--border); border-radius: 12px; padding: 24px; box-shadow: var(--shadow); }
  .section-label { font-size: 0.7rem; font-family: 'IBM Plex Mono', monospace; font-weight: 600; letter-spacing: 2px; text-transform: uppercase; color: var(--muted); margin-bottom: 16px; padding-bottom: 10px; border-bottom: 1px solid var(--border); display: flex; align-items: center; gap: 8px; }
  label { display: block; font-size: 0.78rem; font-weight: 600; color: var(--text); margin-bottom: 5px; margin-top: 14px; }
  label span { font-weight: 400; color: var(--muted); }
  input, textarea { width: 100%; background: var(--card); border: 1px solid var(--border); color: var(--text); padding: 9px 12px; border-radius: 8px; font-family: 'IBM Plex Sans', sans-serif; font-size: 0.85rem; outline: none; transition: border-color 0.15s, box-shadow 0.15s; }
  input:focus, textarea:focus { border-color: var(--accent); box-shadow: 0 0 0 3px rgba(9,105,218,0.12); background: #fff; }
  textarea { resize: vertical; min-height: 72px; line-height: 1.5; }
  .skills-grid { display: flex; flex-wrap: wrap; gap: 7px; margin-top: 8px; }
  .skill-chip { padding: 5px 13px; border-radius: 6px; border: 1px solid var(--border); font-size: 0.75rem; font-family: 'IBM Plex Mono', monospace; cursor: pointer; transition: all 0.15s; background: var(--card); color: var(--muted); user-select: none; }
  .skill-chip:hover { border-color: var(--accent); color: var(--accent); }
  .skill-chip.active { background: #dbeafe; border-color: var(--accent); color: var(--accent); font-weight: 600; }
  .generate-btn { margin-top: 22px; width: 100%; padding: 12px; background: var(--accent); border: none; border-radius: 8px; color: #fff; font-family: 'IBM Plex Sans', sans-serif; font-weight: 600; font-size: 0.95rem; cursor: pointer; transition: background 0.15s, transform 0.1s; }
  .generate-btn:hover { background: #0860c4; }
  .generate-btn:active { transform: scale(0.99); }
  .preview-header { display: flex; align-items: center; justify-content: space-between; margin-bottom: 16px; flex-wrap: wrap; gap: 10px; }
  .tabs { display: flex; gap: 6px; }
  .tab { padding: 5px 14px; border-radius: 6px; font-size: 0.78rem; font-family: 'IBM Plex Mono', monospace; cursor: pointer; border: 1px solid var(--border); background: transparent; color: var(--muted); transition: all 0.15s; }
  .tab.active { background: var(--accent); color: #fff; border-color: var(--accent); }
  .copy-btn { padding: 6px 16px; background: transparent; border: 1px solid var(--accent2); color: var(--accent2); border-radius: 6px; font-family: 'IBM Plex Mono', monospace; font-size: 0.75rem; font-weight: 600; cursor: pointer; transition: all 0.15s; }
  .copy-btn:hover { background: #dff7e9; }
  .copy-btn.copied { background: #dff7e9; }
  .preview-frame { border: 1px solid var(--border); border-radius: 10px; overflow: hidden; margin-bottom: 14px; }
  .gh-render { background: #ffffff; padding: 28px 32px; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif; color: #1f2328; font-size: 14px; line-height: 1.6; min-height: 340px; }
  .gh-render h1 { font-size: 1.7rem; font-weight: 700; border-bottom: 1px solid #d0d7de; padding-bottom: 10px; margin-bottom: 14px; }
  .gh-render h2 { font-size: 1.15rem; font-weight: 600; margin: 20px 0 8px; }
  .gh-render p { margin: 8px 0; }
  .gh-render hr { border: none; border-top: 1px solid #d0d7de; margin: 18px 0; }
  .gh-render ul { padding-left: 20px; margin: 6px 0; }
  .gh-render li { margin: 3px 0; }
  .gh-render a { color: #0969da; text-decoration: none; }
  .gh-render code { background: #f6f8fa; border: 1px solid #d0d7de; border-radius: 4px; padding: 1px 6px; font-size: 0.85em; font-family: 'IBM Plex Mono', monospace; }
  .gh-render .center { text-align: center; }
  .gh-render .badge { display: inline-block; height: 26px; margin: 2px; vertical-align: middle; }
  .gh-render .typing { font-family: 'IBM Plex Mono', monospace; font-size: 0.85rem; color: #0969da; min-height: 20px; margin: 6px 0; }
  .gh-render .views-badge { display: inline-block; background: #f6f8fa; border: 1px solid #d0d7de; border-radius: 4px; padding: 2px 8px; font-size: 0.78rem; color: #57606a; font-family: 'IBM Plex Mono', monospace; }
  .preview-markdown { background: #f6f8fa; padding: 18px 20px; font-family: 'IBM Plex Mono', monospace; font-size: 0.74rem; color: #444d56; min-height: 340px; white-space: pre-wrap; overflow-x: auto; line-height: 1.75; }
  .steps { background: #f6f8fa; border: 1px solid var(--border); border-radius: 10px; padding: 18px 20px; font-size: 0.82rem; color: var(--muted); line-height: 1.9; }
  .steps strong { color: var(--text); }
  .step { display: flex; gap: 12px; align-items: flex-start; margin: 8px 0; }
  .step-num { background: var(--accent); color: #fff; border-radius: 50%; width: 20px; height: 20px; min-width: 20px; display: flex; align-items: center; justify-content: center; font-size: 0.7rem; font-weight: 700; margin-top: 2px; }
</style>
</head>
<body>

<div class="header">
  <div class="header-badge">✦ Professional Edition</div>
  <h1>GitHub Profile README Builder</h1>
  <p class="header-sub">Crafted for students & early-career developers — clean, credible, professional.</p>
</div>

<div class="layout">
  <!-- LEFT: FORM -->
  <div class="card">
    <div class="section-label">① Your Details</div>

    <label>Full Name</label>
    <input id="fname" type="text" placeholder="e.g. Rahul Sharma" value="Rahul Sharma">

    <label>GitHub Username <span>(used for stats cards)</span></label>
    <input id="username" type="text" placeholder="e.g. rahulsharma" value="rahulsharma">

    <label>Degree / Course</label>
    <input id="degree" type="text" placeholder="e.g. B.Tech Computer Science" value="B.Tech Computer Science">

    <label>University / College</label>
    <input id="university" type="text" placeholder="e.g. IIT Delhi" value="IIT Delhi">

    <label>Expected Graduation Year</label>
    <input id="gradyear" type="text" placeholder="e.g. 2027" value="2027">

    <label>Short Bio <span>(keep it professional)</span></label>
    <textarea id="bio">Aspiring software engineer with a strong foundation in Python and C++. Passionate about building efficient algorithms and exploring data structures. Open to internships and collaborative projects.</textarea>

    <label>Location <span>(optional)</span></label>
    <input id="location" type="text" placeholder="e.g. New Delhi, India" value="New Delhi, India">

    <label>LinkedIn URL <span>(optional)</span></label>
    <input id="linkedin" type="text" placeholder="https://linkedin.com/in/yourname" value="">

    <label>Email <span>(optional)</span></label>
    <input id="email" type="text" placeholder="e.g. rahul@gmail.com" value="">

    <label>Currently Working On</label>
    <input id="working" type="text" placeholder="e.g. A CLI task manager in Python" value="A CLI task manager in Python">

    <label>Currently Learning</label>
    <input id="learning" type="text" placeholder="e.g. Data Structures & Algorithms, OOP" value="Data Structures & Algorithms, OOP">

    <div class="section-label" style="margin-top:22px">② Select Your Skills</div>
    <div class="skills-grid" id="skillsGrid"></div>

    <button class="generate-btn" onclick="generate()">⟳ Update Preview</button>
  </div>

  <!-- RIGHT: PREVIEW -->
  <div class="card" style="display:flex;flex-direction:column;gap:0">
    <div class="preview-header">
      <div class="tabs">
        <button class="tab active" onclick="switchTab(this,'rendered')">👁 Preview</button>
        <button class="tab" onclick="switchTab(this,'markdown')">📝 Markdown</button>
      </div>
      <button class="copy-btn" id="copyBtn" onclick="copyMd()">📋 Copy Markdown</button>
    </div>

    <div class="preview-frame">
      <div class="gh-render" id="previewRendered"></div>
      <div class="preview-markdown" id="previewMarkdown" style="display:none"></div>
    </div>

    <div class="steps">
      <strong>🚀 How to publish your GitHub profile README:</strong>
      <div class="step"><div class="step-num">1</div><div>Go to <strong>github.com</strong> → Click <strong>+</strong> → <strong>New repository</strong></div></div>
      <div class="step"><div class="step-num">2</div><div>Name the repo <strong>exactly your GitHub username</strong> (e.g. <code>rahulsharma</code>)</div></div>
      <div class="step"><div class="step-num">3</div><div>Tick <strong>"Add a README file"</strong> → Click <strong>Create repository</strong></div></div>
      <div class="step"><div class="step-num">4</div><div>Click the ✏️ pencil to edit → <strong>Paste your copied Markdown</strong> → Commit changes</div></div>
      <div class="step"><div class="step-num">5</div><div>Visit <strong>github.com/yourusername</strong> — your profile is live! 🎉</div></div>
    </div>
  </div>
</div>

<script>
const SKILLS = [
  { name: 'Python',      badge: 'Python-3776AB?logo=python&logoColor=white' },
  { name: 'Java',        badge: 'Java-ED8B00?logo=openjdk&logoColor=white' },
  { name: 'C++',         badge: 'C%2B%2B-00599C?logo=cplusplus&logoColor=white' },
  { name: 'C',           badge: 'C-A8B9CC?logo=c&logoColor=white' },
  { name: 'HTML',        badge: 'HTML5-E34F26?logo=html5&logoColor=white' },
  { name: 'CSS',         badge: 'CSS3-1572B6?logo=css3&logoColor=white' },
  { name: 'JavaScript',  badge: 'JavaScript-F7DF1E?logo=javascript&logoColor=black' },
  { name: 'SQL',         badge: 'MySQL-4479A1?logo=mysql&logoColor=white' },
  { name: 'Git',         badge: 'Git-F05032?logo=git&logoColor=white' },
  { name: 'Linux',       badge: 'Linux-FCC624?logo=linux&logoColor=black' },
  { name: 'VS Code',     badge: 'VS_Code-007ACC?logo=visualstudiocode&logoColor=white' },
  { name: 'NumPy',       badge: 'NumPy-013243?logo=numpy&logoColor=white' },
  { name: 'Pandas',      badge: 'Pandas-150458?logo=pandas&logoColor=white' },
  { name: 'Django',      badge: 'Django-092E20?logo=django&logoColor=white' },
  { name: 'Docker',      badge: 'Docker-2CA5E0?logo=docker&logoColor=white' },
  { name: 'GitHub',      badge: 'GitHub-181717?logo=github&logoColor=white' },
];

let selected = ['Python', 'Java', 'C++', 'Git'];
let mdOutput = '';

const grid = document.getElementById('skillsGrid');
SKILLS.forEach(s => {
  const c = document.createElement('div');
  c.className = 'skill-chip' + (selected.includes(s.name) ? ' active' : '');
  c.textContent = s.name;
  c.onclick = () => {
    if (selected.includes(s.name)) { selected = selected.filter(x => x !== s.name); c.classList.remove('active'); }
    else { selected.push(s.name); c.classList.add('active'); }
    generate();
  };
  grid.appendChild(c);
});

const v = id => document.getElementById(id).value.trim();

function badgeUrl(s) {
  const sk = SKILLS.find(x => x.name === s);
  return sk ? `https://img.shields.io/badge/${sk.badge}&style=for-the-badge` : null;
}

function generate() {
  const name     = v('fname')      || 'Your Name';
  const username = v('username')   || 'yourusername';
  const degree   = v('degree')     || 'Computer Science';
  const uni      = v('university') || 'University';
  const gradyear = v('gradyear')   || '2027';
  const bio      = v('bio')        || '';
  const location = v('location');
  const linkedin = v('linkedin');
  const email    = v('email');
  const working  = v('working');
  const learning = v('learning');

  // MARKDOWN
  let md = `<div align="center">\n\n`;
  md += `# 👋 Hi, I'm ${name}\n\n`;
  md += `### ${degree} Student | ${uni} (${gradyear})\n\n`;
  md += `<img src="https://komarev.com/ghpvc/?username=${username}&label=Profile+Views&color=0969da&style=flat" alt="Profile views" />\n\n`;
  md += `</div>\n\n---\n\n`;
  md += `## 🎓 About Me\n\n`;
  md += `${bio}\n\n`;
  md += `- 🎓 **Degree:** ${degree} — *${uni}* (Class of ${gradyear})\n`;
  if (location) md += `- 📍 **Location:** ${location}\n`;
  if (working)  md += `- 🔭 **Currently working on:** ${working}\n`;
  if (learning) md += `- 🌱 **Currently learning:** ${learning}\n`;
  if (email)    md += `- 📬 **Contact:** [${email}](mailto:${email})\n`;
  md += `- 💼 **Open to:** Internships, open-source collaborations & entry-level roles\n\n---\n\n`;
  md += `## 🛠️ Technical Skills\n\n`;
  selected.forEach(s => { const u = badgeUrl(s); if (u) md += `![${s}](${u}) `; });
  md += `\n\n---\n\n`;
  md += `## 📊 GitHub Statistics\n\n`;
  md += `<div align="center">\n\n`;
  md += `<img src="https://github-readme-stats.vercel.app/api?username=${username}&show_icons=true&theme=default&hide_border=true&count_private=true" height="165" />\n`;
  md += `<img src="https://github-readme-stats.vercel.app/api/top-langs/?username=${username}&layout=compact&theme=default&hide_border=true" height="165" />\n\n`;
  md += `</div>\n\n<div align="center">\n\n`;
  md += `<img src="https://github-readme-streak-stats.herokuapp.com/?user=${username}&theme=default&hide_border=true" />\n\n</div>\n\n---\n\n`;
  if (linkedin || email) {
    md += `## 🤝 Connect With Me\n\n<div align="center">\n\n`;
    if (linkedin) md += `[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?logo=linkedin&logoColor=white&style=for-the-badge)](${linkedin}) `;
    if (email)    md += `[![Email](https://img.shields.io/badge/Email-D14836?logo=gmail&logoColor=white&style=for-the-badge)](mailto:${email}) `;
    md += `\n\n</div>\n\n---\n\n`;
  }
  md += `<div align="center">\n\n*⭐ If you find my work useful, feel free to star a repository — it means a lot!*\n\n</div>\n`;

  mdOutput = md;
  document.getElementById('previewMarkdown').textContent = md;

  // RENDERED
  document.getElementById('previewRendered').innerHTML = `
    <div class="center">
      <h1>👋 Hi, I'm ${name}</h1>
      <p style="color:#57606a;font-size:0.9rem;margin-bottom:6px">${degree} Student &nbsp;|&nbsp; ${uni} &nbsp;|&nbsp; Class of ${gradyear}</p>
      <div class="typing" id="typingEl"></div>
      <span class="views-badge">👁 Profile Views: 142</span>
    </div>
    <hr>
    <h2>🎓 About Me</h2>
    <p>${bio}</p>
    <ul style="margin-top:10px">
      <li>🎓 <strong>${degree}</strong> — <em>${uni}</em> (Class of ${gradyear})</li>
      ${location ? `<li>📍 ${location}</li>` : ''}
      ${working  ? `<li>🔭 Currently working on: <strong>${working}</strong></li>` : ''}
      ${learning ? `<li>🌱 Currently learning: <strong>${learning}</strong></li>` : ''}
      ${email    ? `<li>📬 <a href="mailto:${email}">${email}</a></li>` : ''}
      <li>💼 Open to internships & collaborations</li>
    </ul>
    <hr>
    <h2>🛠️ Technical Skills</h2>
    <div>${selected.map(s => { const u = badgeUrl(s); return u ? `<img class="badge" src="${u}" alt="${s}">` : ''; }).join('')}</div>
    <hr>
    <h2>📊 GitHub Statistics</h2>
    <div style="display:flex;flex-wrap:wrap;gap:10px;margin:10px 0">
      <div style="background:#f6f8fa;border:1px solid #d0d7de;border-radius:8px;padding:10px 18px;font-size:0.83rem">⭐ Stars: <strong>18</strong> &nbsp; 🔀 Commits: <strong>94</strong> &nbsp; 🔥 Streak: <strong>5 days</strong></div>
    </div>
    <p style="font-size:0.7rem;color:#8c959f;font-style:italic">* Your real GitHub stats appear once deployed</p>
    ${linkedin || email ? `<hr><h2>🤝 Connect With Me</h2><div>
      ${linkedin ? `<img class="badge" src="https://img.shields.io/badge/LinkedIn-0A66C2?logo=linkedin&logoColor=white&style=for-the-badge" alt="LinkedIn">` : ''}
      ${email    ? `<img class="badge" src="https://img.shields.io/badge/Email-D14836?logo=gmail&logoColor=white&style=for-the-badge" alt="Email">` : ''}
    </div>` : ''}
    <hr>
    <p style="text-align:center;color:#57606a;font-style:italic;font-size:0.82rem">⭐ If you find my work useful, feel free to star a repository!</p>
  `;

  // Typing animation
  const phrases = [`${degree} Student`, 'Python & C++ Learner 🐍', 'Future Software Engineer 💼', 'Open Source Enthusiast 🌍'];
  let pi = 0, ci = 0, del = false;
  const tel = document.getElementById('typingEl');
  if (tel) {
    clearInterval(window._typeTimer);
    function type() {
      const p = phrases[pi];
      if (!del) { tel.textContent = p.substring(0, ci++); if (ci > p.length) { del = true; window._typeTimer = setTimeout(type, 1600); return; } }
      else { tel.textContent = p.substring(0, ci--); if (ci < 0) { del = false; pi = (pi + 1) % phrases.length; ci = 0; } }
      window._typeTimer = setTimeout(type, del ? 45 : 75);
    }
    type();
  }
}

function switchTab(btn, tab) {
  document.querySelectorAll('.tab').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  document.getElementById('previewRendered').style.display = tab === 'rendered' ? '' : 'none';
  document.getElementById('previewMarkdown').style.display = tab === 'markdown' ? '' : 'none';
}

function copyMd() {
  if (!mdOutput) return;
  navigator.clipboard.writeText(mdOutput).then(() => {
    const b = document.getElementById('copyBtn');
    b.textContent = '✅ Copied!';
    b.classList.add('copied');
    setTimeout(() => { b.textContent = '📋 Copy Markdown'; b.classList.remove('copied'); }, 2200);
  });
}

document.querySelectorAll('input, textarea').forEach(el => el.addEventListener('input', generate));
generate();
</script>
</body>
</html>
