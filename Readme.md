from pathlib import Path
import shutil, zipfile

base = Path("/mnt/data/VHugoASouza_Profile_V6")
base.mkdir(parents=True, exist_ok=True)

# Usa exatamente a imagem que você enviou.
source_image = Path("/mnt/data/image(20261019-190406).png")
target_image = base / "guts.png"
shutil.copy2(source_image, target_image)

readme = r'''<table>
<tr>
<td width="62%" valign="top">

<h1>Victor Hugo</h1>

<p><code>Matemática • Astronomia • Design • Tecnologia</code></p>

<blockquote>
building useful things — learning how they work — improving them until they don't break
</blockquote>

<h3><code>&gt; about_me</code></h3>

<p>
Sou <strong>Victor Hugo</strong>. Gosto de transformar ideias em projetos e aprender enquanto construo cada parte.
</p>

<p>
Meu foco passa por <strong>matemática, astronomia, design, tecnologia, economia e empreendedorismo</strong> — áreas diferentes, mas com algo em comum: resolver problemas e criar coisas melhores.
</p>

<pre>
mode      = curious
approach  = learn_by_building
current   = StudyBox
next      = ...
</pre>

<h3><code>&gt; current_project</code></h3>

<h4>📦 StudyBox</h4>

<p><strong>Tudo para estudar. Do seu jeito.</strong></p>

<p>
Projeto de empreendedorismo voltado para caixas de materiais escolares prontas e personalizáveis, com organização por ano escolar e montagem personalizada.
</p>

<p>
<code>HTML</code>
<code>CSS</code>
<code>JavaScript</code>
<code>Git</code>
<code>GitHub</code>
</p>

<p>
🌐 <a href="https://studybx.neocities.org/">studybx.neocities.org</a>
</p>

</td>

<td width="38%" valign="top" align="center">

<img src="./guts.png" width="300" alt="Guts"/>

</td>
</tr>
</table>

---

## `> interests`

<p>
<img src="https://img.shields.io/badge/Matemática-0D1117?style=for-the-badge&logo=wolfram&logoColor=00E5FF" alt="Matemática">
<img src="https://img.shields.io/badge/Astronomia-0D1117?style=for-the-badge&logo=starship&logoColor=8B5CF6" alt="Astronomia">
<img src="https://img.shields.io/badge/Design-0D1117?style=for-the-badge&logo=figma&logoColor=2F81F7" alt="Design">
<img src="https://img.shields.io/badge/Tecnologia-0D1117?style=for-the-badge&logo=github&logoColor=FFFFFF" alt="Tecnologia">
<img src="https://img.shields.io/badge/Economia-0D1117?style=for-the-badge&logo=googleanalytics&logoColor=F9D423" alt="Economia">
</p>

---

## `> achievements`

<table>
<tr>
<td align="center" width="33%">
<strong>🥇 Ouro Regional</strong><br>
<sub>Mathématiques sans Frontières</sub>
</td>

<td align="center" width="33%">
<strong>🥈 Prata Nacional</strong><br>
<sub>Mathématiques sans Frontières</sub>
</td>

<td align="center" width="33%">
<strong>🥈 Prata</strong><br>
<sub>Olimpíada Brasileira de Astronomia (OBA)</sub>
</td>
</tr>
</table>

---

## `> toolbox`

<p>
<img src="https://skillicons.dev/icons?i=html,css,js,git,github,vscode,windows&theme=dark" alt="Ferramentas">
</p>

<sub>Ferramentas que uso ou estou aprendendo.</sub>

---

## `> github`

<p align="center">
<img height="165" src="https://github-readme-stats.vercel.app/api?username=VHugoASouza&show_icons=true&hide_border=true&bg_color=0D1117&title_color=00E5FF&text_color=C9D1D9&icon_color=2F81F7&ring_color=00E5FF" alt="GitHub stats">
<img height="165" src="https://github-readme-stats.vercel.app/api/top-langs/?username=VHugoASouza&layout=compact&hide_border=true&bg_color=0D1117&title_color=00E5FF&text_color=C9D1D9" alt="Top languages">
</p>

<p align="center">
<img width="92%" src="https://github-readme-activity-graph.vercel.app/graph?username=VHugoASouza&bg_color=0D1117&color=C9D1D9&line=00E5FF&point=2F81F7&area=true&hide_border=true" alt="Contribution graph">
</p>

---

<div align="center">

### `BUILD / LEARN / IMPROVE`

`VHugoASouza`

</div>
'''

readme_path = base / "README.md"
readme_path.write_text(readme, encoding="utf-8")

# Validações para não repetir o erro.
assert readme.startswith("<table>")
assert "from pathlib" not in readme
assert "shutil" not in readme
assert 'src="./guts.png"' in readme
assert target_image.exists() and target_image.stat().st_size > 0

zip_path = Path("/mnt/data/VHugoASouza_Profile_V6_LIMPO.zip")
with zipfile.ZipFile(zip_path, "w", zipfile.ZIP_DEFLATED) as z:
    z.write(readme_path, "README.md")
    z.write(target_image, "guts.png")

print("OK — pacote validado.")
print("Arquivos no ZIP: README.md + guts.png")
print(zip_path)
