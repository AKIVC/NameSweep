# NameSweep  
### Multi‑Engine OSINT Sweep Tool with Encrypted Config, Archive Mode, and Parallel Execution

NameSweep is a powerful, single‑file OSINT aggregation tool that performs wide‑spectrum searches across multiple engines, enriches results with Archive.org, and stores configuration securely using AES‑256 encryption with a Windows registry‑stored key.

This tool is designed for researchers, analysts, journalists, and anyone who needs fast, reproducible, multi‑source OSINT sweeps.

---

## Features

- **Multi‑engine OSINT sweep** (Brave, Yandex, Google CSE, Wikipedia, Reddit, YouTube, GNews, GeoNames, GDELT, DuckDuckGo, Wikidata)
- **AES‑256 encrypted config file** (`config.cfg`)
- **Encryption key stored in Windows Registry**
- **Config mode** with full interactive setup
- **Parallel engine execution** (`--threads`)
- **Colored terminal output**
- **Per‑engine timing metrics**
- **Timestamped JSON/CSV outputs**
- **SQLite logging option**
- **Archive mode** (Archive.org lookup for every URL)
- **Engine activation system** (enable/disable engines)
- **Selective engine execution** (`--only`, `--skip`)
- **Verbose/quiet modes**
- **Custom output directory** (`--output-dir`)

---

## Quickstart

### 1. Install dependencies

```
pip install -r requirements.txt
```

### 2. Run config mode (first‑time setup)

```
python name_sweep.py --mode config
```

You will be prompted for:
- API keys  
- Target name  
- Context terms  
- Engine activation  
- Request delay  
- Max results  

All values are encrypted and stored securely.

### 3. Run a sweep

```
python name_sweep.py "John Doe"
```

### 4. Run a sweep with parallel engines

```
python name_sweep.py "John Doe" --threads 5
```

### 5. Archive mode

```
python name_sweep.py --mode archive --input results.json
```

---

## Usage Examples

### Only run Brave + Reddit

```
python name_sweep.py "John Doe" --only brave reddit
```

### Skip YouTube + GNews

```
python name_sweep.py "John Doe" --skip youtube gnews
```

### Save results to a custom folder

```
python name_sweep.py "John Doe" --output-dir ./results/
```

### Log results to SQLite

```
python name_sweep.py "John Doe" --db sweep.db
```

---

## Security Model

- All configuration is stored in `config.cfg`
- The file is **AES‑256‑CBC encrypted**
- The encryption key is stored in:
  ```
  HKCU\Software\NameSweep\ConfigKey
  ```
- No plaintext API keys are ever written to disk
- The tool never transmits your config or keys anywhere

---

## Supported Engines

| Engine       | Type        | API Key Required |
|--------------|-------------|------------------|
| Brave        | HTML        | No               |
| Yandex       | HTML        | No               |
| Wikipedia    | API         | No               |
| NewsAPI      | API         | Yes              |
| Google CSE   | API         | Yes              |
| Wikidata     | SPARQL      | No               |
| GDELT        | API         | No               |
| YouTube      | API         | Yes              |
| DuckDuckGo   | API         | No               |
| Reddit       | API         | No               |
| GeoNames     | API         | Yes              |
| GNews        | API         | Yes              |

---

## Requirements

```
requests
beautifulsoup4
pycryptodome
colorama
```

---


## License

MIT License — see `LICENSE` file.

---

## Contributing

Pull requests are welcome!  
Feel free to submit:
- new engines  
- bug fixes  
- performance improvements  
- documentation updates  

---

## Roadmap

- HTML report generation  
- Plugin system for custom engines  
- Web UI wrapper  
- API mode for automation  

---

## Author

Created by **Rhys Edwards**  
GitHub: *AKIVC*
