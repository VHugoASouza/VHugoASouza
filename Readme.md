from pathlib import Path
import textwrap, zipfile, os

base = Path("/mnt/data/VHugoASouza_Profile_V3")
assets = base / "assets"
assets.mkdir(parents=True, exist_ok=True)

banner = '''<svg xmlns="http://www.w3.org/2000/svg" width="1200" height="320" viewBox="0 0 1200 320">
  <defs>
    <linearGradient id="bg" x1="0" y1="0" x2="1" y2="1">
      <stop offset="0%" stop-color="#05070a"/>
      <stop offset="55%" stop-color="#0a0f16"/>
      <stop offset="100%" stop-color="#07111a"/>
    </linearGradient>
    <linearGradient id="line" x1="0" y1="0" x2="1" y2="0">
      <stop offset="0%" stop-color="#00e5ff" stop-opacity="0"/>
      <stop offset="45%" stop-color="#00e5ff" stop-opacity=".9"/>
      <stop offset="100%" stop-color="#2f81f7" stop-opacity="0"/>
    </linearGradient>
    <filter id="glow">
      <feGaussianBlur stdDeviation="5" result="blur"/>
      <feMerge><feMergeNode in="blur"/><feMergeNode in="SourceGraphic"/></feMerge>
    </filter>
  </defs>
  <rect width="1200" height="320" rx="28" fill="url(#bg)"/>
  <rect x="1" y="1" width="1198" height="318" rx="27" fill="none" stroke="#18202b"/>
  <g fill="#7d8590" opacity=".55">
    <circle cx="95" cy="66" r="2"/><circle cx="160" cy="210" r="1.4"/><circle cx="248" cy="83" r="1.5"/>
    <circle cx="1020" cy="66" r="1.6"/><circle cx="1120" cy="230" r="1.7"/><circle cx="906" cy="176" r="1.2"/>
    <circle cx="820" cy="55" r="1.2"/><circle cx="350" cy="248" r="1.3"/><circle cx="720" cy="255" r="1.6"/>
  </g>
  <path d="M845 226c48-55 107-93 202-109" fill="none" stroke="#17263a" stroke-width="2"/>
  <path d="M862 235c65-48 123-70 235-78" fill="none" stroke="#0e3d55" stroke-width="2"/>
  <circle cx="1018" cy="116" r="42" fill="none" stroke="#1b3550" stroke-width="2"/>
  <circle cx="1018" cy="116" r="4" fill="#00e5ff" filter="url(#glow)"/>
  <text x="70" y="115" font-family="Segoe UI, Arial, sans-serif" font-size="18" letter-spacing="4" fill="#00e5ff">PROFILE / VHUGOASOUZA</text>
  <text x="70" y="178" font-family="Segoe UI, Arial, sans-serif" font-size="54" font-weight="700" fill="#e6edf3">VICTOR HUGO</text>
  <text x="72" y="220" font-family="Segoe UI, Arial, sans-serif" font-size="22" fill="#9da7b3">matemática • astronomia • design • projetos</text>
  <rect x="70" y="255" width="560" height="2" fill="url(#line)"/>
  <text x="70" y="290" font-family="Consolas, monospace" font-size="15" fill="#7d8590">&gt; build. learn. improve. repeat.</text>
</svg>
'''

studybox = '''<svg xmlns="http://www.w3.org/2000/svg" width="760" height="220" viewBox="0 0 760 220">
  <defs>
    <linearGradient id="g" x1="0" y1="0" x2="1" y2="1">
      <stop offset="0%" stop-color="#0b0f14"/>
      <stop offset="100%" stop-color="#09131d"/>
    </linearGradient>
  </defs>
  <rect width="760" height="220" rx="22" fill="url(#g)"/>
  <rect x="1" y="1" width="758" height="218" rx="21" fill="none" stroke="#1b2b3a"/>
  <text x="34" y="48" font-family="Consolas, monospace" font-size="15" fill="#00e5ff">FEATURED PROJECT</text>
  <text x="34" y="92" font-family="Segoe UI, Arial" font-size="34" font-weight="700" fill="#e6edf3">StudyBox</text>
  <text x="34" y="124" font-family="Segoe UI, Arial" font-size="17" fill="#9da7b3">Tudo para estudar. Do seu jeito.</text>
  <text x="34" y="164" font-family="Segoe UI, Arial" font-size="15" fill="#c7d1db">HTML • CSS • JavaScript • GitHub Actions</text>
  <rect x="34" y="186" width="230" height="3" rx="2" fill="#00e5ff"/>
  <g transform="translate(592,48)">
    <rect x="0" y="30" width="105" height="78" rx="10" fill="#101923" stroke="#2f81f7"/>
    <path d="M15 45h75l-10 18H25z" fill="#172b3d" stroke="#00e5ff"/>
    <path d="M53 7v40M38 19l15-12 15 12" fill="none" stroke="#7dd3fc" stroke-width="4" stroke-linecap="round" stroke-linejoin="round"/>
    <circle cx="53" cy="123" r="6" fill="#00e5ff"/>
  </g>
</svg>
'''

focus = '''<svg xmlns="http://www.w3.org/2000/svg" width="760" height="190" viewBox="0 0 760 190">
  <rect width="760" height="190" rx="22" fill="#0b0f14"/>
  <rect x="1" y="1" width="758" height="188" rx="21" fill="none" stroke="#1b2b3a"/>
  <text x="34" y="45" font-family="Consolas, monospace" font-size="15" fill="#8b5cf6">CURRENT FOCUS</text>
  <text x="34" y="83" font-family="Segoe UI, Arial" font-size="24" font-weight="700" fill="#e6edf3">Aprender construindo.</text>
  <text x="34" y="116" font-family="Segoe UI, Arial" font-size="16" fill="#9da7b3">Web • UI/UX • Git • automação • inteligência artificial</text>
  <text x="34" y="151" font-family="Consolas, monospace" font-size="14" fill="#7d8590">&gt; curiosidade primeiro, ferramenta depois.</text>
</svg>
'''

readme = r'''<p align="center">
  <img src="./assets/banner.svg" width="100%" alt="Victor Hugo — profile banner"/>
</p>

<p align="center">
  <a href="https://studybx.neocities.org/">
    <img src="https://img.shields.io/badge/StudyBox-05070A?style=for-the-badge&logo=googlechrome&logoColor=00E5FF" alt="StudyBox"/>
  </a>
  <img src="https://img.shields.io/badge/Math-05070A?style=for-the-badge&logo=wolfram&logoColor=00E5FF" alt="Matemática"/>
  <img src="https://img.shields.io/badge/Astronomy-05070A?style=for-the-badge&logo=starship&logoColor=8B5CF6" alt="Astronomia"/>
  <img src="https://img.shields.io/badge/Design-05070A?style=for-the-badge&logo=figma&logoColor=2F81F7" alt="Design"/>
</p>

<br>

<table>
<tr>
<td width="52%" valign="top">

### `> about_me`

Sou **Victor Hugo**. Gosto de transformar ideias em projetos e aprender enquanto descubro como cada parte funciona.

Meu foco passa por **matemática, astronomia, design, tecnologia, economia e empreendedorismo** — áreas diferentes, mas que têm algo em comum: resolver problemas e criar coisas melhores.

```txt
mode        = curious
approach    = learn_by_building
current     = StudyBox
next        = ...
```

</td>
<td width="48%" valign="top">

### `> now`

- 📦 Evoluindo a **StudyBox**
- 🧠 Aprendendo desenvolvimento web
- 🎨 Explorando interface e identidade visual
- 🌌 Sempre voltando para astronomia e exatas
- 🛠️ Usando IA como ferramenta para aprender e construir

</td>
</tr>
</table>

<br>

<p align="center">
  <a href="https://studybx.neocities.org/">
    <img src="./assets/studybox.svg" width="92%" alt="StudyBox"/>
  </a>
</p>

<p align="center">
  <img src="./assets/focus.svg" width="92%" alt="Current focus"/>
</p>

<br>

## `> achievements`

<table>
<tr>
<td align="center" width="33%">
  <h3>🥇 Ouro Regional</h3>
  <sub>Mathématiques sans Frontières</sub>
</td>
<td align="center" width="33%">
  <h3>🥈 Prata Nacional</h3>
  <sub>Mathématiques sans Frontières</sub>
</td>
<td align="center" width="33%">
  <h3>🥈 Prata</h3>
  <sub>Olimpíada Brasileira de Astronomia</sub>
</td>
</tr>
</table>

<br>

## `> toolbox`

<p>
  <img src="https://skillicons.dev/icons?i=html,css,js,git,github,vscode,windows&theme=dark" alt="Ferramentas e tecnologias"/>
</p>

<sub>Ferramentas que uso ou estou aprendendo — não uma lista de “nível profissional”.</sub>

<br><br>

## `> github_activity`

<p align="center">
  <img width="49%" src="https://github-readme-stats.vercel.app/api?username=VHugoASouza&show_icons=true&hide_border=true&bg_color=0D1117&title_color=00E5FF&text_color=C9D1D9&icon_color=2F81F7&ring_color=00E5FF" alt="GitHub stats"/>
  <img width="41%" src="https://github-readme-stats.vercel.app/api/top-langs/?username=VHugoASouza&layout=compact&hide_border=true&bg_color=0D1117&title_color=00E5FF&text_color=C9D1D9" alt="Top languages"/>
</p>

<p align="center">
  <img src="https://github-readme-activity-graph.vercel.app/graph?username=VHugoASouza&bg_color=0D1117&color=C9D1D9&line=00E5FF&point=2F81F7&area=true&hide_border=true" width="92%" alt="Contribution graph"/>
</p>

<br>

<div align="center">

### `BUILD  /  LEARN  /  IMPROVE`

<sub>VHugoASouza</sub>

</div>
'''

(assets / "banner.svg").write_text(banner, encoding="utf-8")
(assets / "studybox.svg").write_text(studybox, encoding="utf-8")
(assets / "focus.svg").write_text(focus, encoding="utf-8")
(base / "README.md").write_text(readme, encoding="utf-8")

zip_path = Path("/mnt/data/VHugoASouza_Profile_V3.zip")
with zipfile.ZipFile(zip_path, "w", zipfile.ZIP_DEFLATED) as z:
    for p in base.rglob("*"):
        if p.is_file():
            z.write(p, p.relative_to(base))

print("README:", base / "README.md")
print("ZIP:", zip_path)
print("Files:", [str(p.relative_to(base)) for p in base.rglob("*") if p.is_file()])
