# NHL Game Data Project Structure

## Directory Layout

```
nhlgamedata/                    # Project root
│
├── nhlgame.py                  # Main data collection script
├── pyproject.toml              # uv package configuration
├── README.md                   # Main project documentation
├── NHL_API_DOCUMENTATION.md    # API reference
│
├── nogames.json                # Log of 404 errors (games not found)
├── errors.json                 # Log of other API errors
│
├── 2025/                       # 2024-2025 season data
│   ├── shifts/
│   │   └── 2025020393.json
│   ├── plays/
│   │   └── 2025020393.json
│   ├── meta/
│   │   └── 2025020393.json
│   └── boxscores/
│       └── 2025020393.json
│
├── 2024/                       # 2023-2024 season data
│   ├── shifts/
│   ├── plays/
│   ├── meta/
│   └── boxscores/
│
├── 2023/                       # 2022-2023 season data
│   ├── shifts/
│   ├── plays/
│   ├── meta/
│   └── boxscores/
│
└── plays/                      # Play-by-play analysis tools
    ├── flatten_plays.py        # CSV conversion script
    ├── FLATTEN_PLAYS_README.md # Documentation
    └── output/                 # Generated CSV files (auto-created)
        ├── plays_2025020393.csv
        ├── plays_2025020394.csv
        └── ...
```

## Workflow

### 1. Data Collection (Project Root)
```bash
# Run from project root
python nhlgame.py 1 100
```
- Downloads game data for games 1-100
- Saves to `SEASON/[shifts|plays|meta|boxscores]/`
- Logs errors to `nogames.json` and `errors.json`

### 2. Data Analysis (plays/ subdirectory)
```bash
# Run from plays/ subdirectory
cd plays
python flatten_plays.py 393 2025
```
- Reads from `../2025/plays/2025020393.json`
- Outputs to `output/plays_2025020393.csv`
- Auto-creates `output/` directory if needed

## Path References

| Script Location | Input Data Location | Output Location |
|----------------|---------------------|-----------------|
| `nhlgame.py` (root) | NHL API | `SEASON/[endpoint]/` |
| `plays/flatten_plays.py` | `../SEASON/plays/` | `plays/output/` |

## Design Rationale

- **Season folders at root**: Easy to see all available data years
- **plays/ subfolder**: Keeps analysis tools separate from raw data
- **output/ subfolder**: Keeps generated files organized and separate from source code
- **Relative paths**: Scripts work regardless of where project is located