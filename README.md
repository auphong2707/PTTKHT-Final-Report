# PTTKHT-Final-Report

## LaTeX Setup Instructions

### Windows

#### Installation
1. **Install MiKTeX** (Recommended for Windows):
   - Download from: https://miktex.org/download
   - Run the installer and follow the setup wizard
   - Choose "Install missing packages automatically" during installation

2. **Alternative: Install TeX Live**:
   - Download from: https://tug.org/texlive/acquire-netinstall.html
   - Run `install-tl-windows.exe`
   - Follow the installation wizard

3. **Install a LaTeX Editor** (Optional):
   - TeXstudio: https://www.texstudio.org/
   - TeXmaker: https://www.xm1math.net/texmaker/
   - VS Code with LaTeX Workshop extension

#### Compiling LaTeX Files

Using Command Prompt or PowerShell:

```powershell
# Navigate to project directory
cd d:\Git\PTTKHT-Final-Report

# Compile main document
pdflatex main.tex

# If using bibliography or cross-references, run:
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex

# Compile sub document
pdflatex sub.tex
```

#### Clean Build Files (Windows)

```powershell
# Remove auxiliary files
del *.aux *.log *.out *.toc *.lof *.lot *.bbl *.blg
```

---

### Linux

#### Installation

**Ubuntu/Debian:**
```bash
# Update package list
sudo apt update

# Install TeX Live (full installation)
sudo apt install texlive-full

# Or minimal installation
sudo apt install texlive-latex-base texlive-latex-extra
```

**Fedora/RHEL/CentOS:**
```bash
# Install TeX Live
sudo dnf install texlive-scheme-full

# Or minimal installation
sudo dnf install texlive texlive-latex
```

**Arch Linux:**
```bash
# Install TeX Live
sudo pacman -S texlive-core texlive-latexextra

# Or full installation
sudo pacman -S texlive-most
```

#### Compiling LaTeX Files

```bash
# Navigate to project directory
cd /path/to/PTTKHT-Final-Report

# Compile main document
pdflatex main.tex

# If using bibliography or cross-references, run:
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex

# Compile sub document
pdflatex sub.tex
```

#### Clean Build Files (Linux)

```bash
# Remove auxiliary files
rm -f *.aux *.log *.out *.toc *.lof *.lot *.bbl *.blg
```

---

## Docker Method (No LaTeX Installation Required)

**Just install Docker - no LaTeX needed!**

> **Important:** Use the correct syntax for your OS:
> - Windows PowerShell: `${PWD}`
> - Linux/macOS: `$(pwd)`

**Windows (PowerShell):**
```powershell
# Pull LaTeX Docker image (only needed once)
docker pull texlive/texlive:latest

# Navigate to project directory
cd d:\Git\PTTKHT-Final-Report

# Compile main document
docker run --rm -v ${PWD}:/workdir -w /workdir texlive/texlive pdflatex main.tex

# For bibliography or cross-references, run:
docker run --rm -v ${PWD}:/workdir -w /workdir texlive/texlive sh -c "pdflatex main.tex && bibtex main && pdflatex main.tex && pdflatex main.tex"

# Compile sub document
docker run --rm -v ${PWD}:/workdir -w /workdir texlive/texlive pdflatex sub.tex

# Clean build files
docker run --rm -v ${PWD}:/workdir -w /workdir texlive/texlive sh -c "rm -f *.aux *.log *.out *.toc *.lof *.lot *.bbl *.blg"
```

**Linux (Bash):**
```bash
# Pull LaTeX Docker image (only needed once)
docker pull texlive/texlive:latest

# Compile main document
docker run --rm -v $(pwd):/workdir -w /workdir texlive/texlive pdflatex main.tex

# For bibliography or cross-references, run:
docker run --rm -v $(pwd):/workdir -w /workdir texlive/texlive sh -c "pdflatex main.tex && bibtex main && pdflatex main.tex && pdflatex main.tex"

# Compile sub document
docker run --rm -v $(pwd):/workdir -w /workdir texlive/texlive pdflatex sub.tex

# Clean build files
docker run --rm -v $(pwd):/workdir -w /workdir texlive/texlive sh -c "rm -f *.aux *.log *.out *.toc *.lof *.lot *.bbl *.blg"
```

**Docker Compose (Optional):**

Create `docker-compose.yml`:
```yaml
version: '3'
services:
  latex:
    image: texlive/texlive:latest
    volumes:
      - .:/workdir
    working_dir: /workdir
```

Then compile with shorter commands:
```bash
# Windows or Linux
docker-compose run --rm latex pdflatex main.tex
docker-compose run --rm latex pdflatex sub.tex
```

---

## Additional Tools

### Makefile (Optional)
Create a `Makefile` for easier compilation:

```makefile
all: main.pdf sub.pdf

main.pdf: main.tex
	pdflatex main.tex
	pdflatex main.tex

sub.pdf: sub.tex
	pdflatex sub.tex
	pdflatex sub.tex

clean:
	rm -f *.aux *.log *.out *.toc *.lof *.lot *.bbl *.blg
```

Then simply run:
- Windows: `make` (requires Make for Windows or WSL)
- Linux: `make`

### VS Code LaTeX Workshop Extension

If using VS Code:
1. Install the "LaTeX Workshop" extension
2. Open the `.tex` file
3. Use `Ctrl+Alt+B` (Windows/Linux) to build
4. Use `Ctrl+Alt+V` to view PDF

---

## Troubleshooting

### Missing Packages
- **Windows (MiKTeX)**: Packages will be installed automatically on first use
- **Linux**: Install missing packages with:
  ```bash
  sudo apt install texlive-<package-name>
  ```

### Compilation Errors
- Always compile multiple times when using cross-references or bibliography
- Check the `.log` file for detailed error messages
- Ensure all referenced images and files exist in the correct directories