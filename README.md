# MCX-Trading-buy-sell-signal-update

MCX Trading Buy/Sell Signal Update is a Python-based trading application that provides entry and exit signals for MCX Natural Gas (NG) Futures trading. The application allows traders to monitor market conditions and receive trading signals based on predefined strategies.

## Features

- Real-time MCX Natural Gas Futures monitoring
- Buy and Sell signal generation
- Entry and Exit trade alerts
- Automated trade management
- Trading performance monitoring
- Voice and popup notifications

---

# Creating a Standalone Executable

To make the application independent of Python installation and distribute it as a standalone executable, use PyInstaller.

## Step 1: Install PyInstaller

```bash
pip install pyinstaller
```

## Step 2: Generate a Spec File

```bash
pyi-makespec MCX_AUTO_TRADING.py
```

This will create:

```text
MCX_AUTO_TRADING.spec
```

## Step 3: Update the Spec File

Add the following imports at the beginning of the file:

```python
from PyInstaller.utils.hooks import collect_all
import pkg_resources
```

Initialize the required variables:

```python
hiddenimports = []
datas = []
binaries = []
```

Collect all dependencies automatically:

```python
for pkg in pkg_resources.working_set:
    try:
        collected = collect_all(pkg.key)
        datas += collected[0]
        binaries += collected[1]
        hiddenimports += collected[2]
    except Exception:
        pass
```

Update the Analysis section:

```python
a = Analysis(
    ['MCX_AUTO_TRADING.py'],
    pathex=[],
    binaries=binaries,
    datas=datas,
    hiddenimports=hiddenimports,
    hookspath=[],
    runtime_hooks=[],
    excludes=[],
    noarchive=False,
)
```

## Step 4: Build the Executable

```bash
pyinstaller MCX_AUTO_TRADING.spec --clean
```

## Optional: Build a Single Executable File

```bash
pyinstaller --onefile MCX_AUTO_TRADING.py
```

## Optional: Build Without Console Window

```bash
pyinstaller --onefile --noconsole MCX_AUTO_TRADING.py
```

---

# Running the Application

Install project dependencies:

```bash
pip install -r requirements.txt
```

Launch the application:

```bash
python MCX_AUTO_TRADING.py
```

---

# Linux (Ubuntu 22.04) Prerequisites

Install required system packages:

```bash
sudo apt update

sudo apt install -y \
python3-tk \
python3-dev \
python3-venv \
build-essential \
espeak-ng \
libespeak1
```

For Linux environments, ensure that the voice engine (eSpeak NG) is installed if voice alerts are enabled.

---

# Disclaimer

This software is intended for educational and personal trading assistance purposes only. Users are responsible for validating signals and managing risk before placing any trades in live markets.
