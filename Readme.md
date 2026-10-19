from pathlib import Path
import shutil, zipfile

src = Path("/mnt/data/image(20261019-190406).png")
base = Path("/mnt/data/VHugoASouza_Profile_V5")
assets = base / "assets"
assets.mkdir(parents=True, exist_ok=True)

# Copy the exact image the user provided.
guts_path = assets / "guts.png"
shutil.copy2(src, guts_path)

readme = r'''<table>
<tr>
<td width="62%" valign="top">

# Victor Hugo

### `Matemática • Astronomia • Design • Tecnologia`

> building useful things — learning how they work — improving them until they don't break

<br>

### `> about_me`

Sou **Victor Hugo**. Gosto de transformar ideias em projetos e aprender enquanto construo cada parte.

Meu foco passa por **matemática, astronomia, design, tecnologia, economia e empreendedorismo** — áreas diferentes, mas com algo em comum: resolver problemas e criar coisas melhores.

```txt
mode        = curious
approach    = learn_by_building
current     = StudyBox
next        = ...
```

<br>

### `> current_project`

#### 📦 StudyBox

**Tudo para estudar. Do seu jeito.**

Projeto de empreendedorismo voltado para caixas de materiais escolares prontas e personalizáveis, com organização por ano escolar e montagem personalizada.

`HTML` `CSS` `JavaScript` `Git` `GitHub`

🌐 https://studybx.neocities.org/

</td>

<td width="38%" valign="top" align="center">

<img src="./assets/guts.png" width="290" alt="Guts dark artwork"/>

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

### 🥇 Ouro Regional
**Mathématiques sans Frontières**

</td>
<td align="center" width="33%">

### 🥈 Prata Nacional
**Mathématiques sans Frontières**

</td>
<td align="center" width="33%">

### 🥈 Prata
**Olimpíada Brasileira de Astronomia**

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

zip_path = Path("/mnt/data/VHugoASouza_Profile_V5.zip")
with zipfile.ZipFile(zip_path, "w", zipfile.ZIP_DEFLATED) as z:
    for p in base.rglob("*"):
        if p.is_file():
            z.write(p, p.relative_to(base))

print("Criado:")
print(readme_path)
print(guts_path)
print(zip_path)
