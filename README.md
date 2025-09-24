# NFL Prediction System

## Overview

This project implements machine learning models to predict NFL game outcomes using advanced analytics and the high-performance `nflreadpy` library. The system supports both moneyline (win/loss) and spread predictions with proper temporal validation and risk management.

## Prerequisites

- **Python 3.12+** 
- **UV Package Manager** (this GOAT)

## Installation & Setup

### 1. Install UV Package Manager

If you don't have UV installed, install it using one of these methods:

**macOS/Linux:**
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**Windows:**
```bash
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
```

**Alternative (using pip):**
```bash
pip install uv
```

### 2. Clone and Setup Project

```bash
# Clone the repository
git clone <repository-url>
cd NFL-Final-Project

# Create virtual environment and install dependencies
uv sync

# Activate the virtual environment
source .venv/bin/activate  # macOS/Linux
# or
.venv\Scripts\activate     # Windows
```

### 3. Verify Installation

```bash
# Check Python version
python --version

# Verify nflreadpy installation
python -c "import nflreadpy; print('nflreadpy installed successfully')"

# Run basic data test
python -c "
import nflreadpy as nfl
df = nfl.load_schedules([2024])
print(f'Loaded {len(df)} games from 2024 season')
"
```

## Project Structure (Possibly)

```
NFL-Final-Project/
- src/                    # Main source code
-   - data/              # Data collection modules
-   - features/          # Feature engineering
-   - models/            # Model training and evaluation
-   - utils/             # Utility functions
- notebooks/             # Jupyter notebooks for exploration
-   - 01-data-exploration.ipynb
-   - 02-feature-engineering.ipynb
-   - 03-model-development.ipynb
- tests/                 # Unit tests
- config/                # Configuration files
- data/                  # Data storage
-   - raw/              # Raw downloaded data
-   - processed/        # Processed datasets
-   - models/           # Saved model artifacts
- main.py               # Main execution script
- pyproject.toml        # Project configuration and dependencies
- README.md             # This file
```

## Running the Project

### Quick Start

```bash
# Activate virtual environment (if not already active)
source .venv/bin/activate

# Run the main prediction pipeline
# TODO
```

### Development Workflow

1. **Data Exploration:**
   ```bash
   # Start Jupyter notebook server
   uv run jupyter lab

   # Open notebooks/01-data-exploration.ipynb
   ```

2. **Feature Engineering:**
   ```bash
   # Run feature engineering pipeline
   uv run python -m src.features.build_features
   ```

3. **Model Training:**
   ```bash
   # Train models with cross-validation
   uv run python -m src.models.train_model
   ```

4. **Generate Predictions:**
   ```bash
   # Generate predictions for upcoming games
   uv run python -m src.models.predict_model
   ```

## Key Features

- **High-Performance Data Access**: Uses `nflreadpy` with Polars DataFrames for 10-100x faster processing
- **Comprehensive NFL Data**: Access to play-by-play, team stats, player stats, and advanced metrics since 1999
- **Advanced Feature Engineering**: EPA-based metrics, opponent adjustments, rolling averages, and situational factors
- **Temporal Cross-Validation**: Proper time-series validation preventing data leakage
- **Ensemble Methods**: Combines XGBoost, Random Forest, and other algorithms for robust predictions
- **Validation Metrics**: Kelly Criterion implementation and confidence estimation

## Configuration

The project uses hierarchical configuration through YAML files in the `config/` directory:

- `config/data.yaml` - Data collection settings
- `config/features.yaml` - Feature engineering parameters
- `config/models.yaml` - Model hyperparameters
- `config/evaluation.yaml` - Cross-validation and evaluation settings

## Data Sources

The nflverse ecosystem has a ton of data:

- **Play-by-Play Data**: Every offensive play since 1999
- **Team Statistics**: Traditional and advanced analytics
- **Player Performance**: Individual game and season stats
- **Injury Reports**: Official injury designations
- **Weather Data**: Game-day conditions
- **Betting Lines**: Historical spreads and totals


## Testing

```bash
# Run all tests
uv run pytest

# Run with coverage
uv run pytest --cov=src

# Run specific test categories
uv run pytest tests/test_features.py
uv run pytest tests/test_models.py
```

## Contributing (DO NOT PUSH DIRECTLY TO MASTER)

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes following the project structure
4. Add tests for new functionality
5. Ensure all tests pass (`uv run pytest`)
6. Commit your changes (`git commit -m 'Add amazing feature'`)
7. Push to the branch (`git push origin feature/amazing-feature`)
8. Open a Pull Request

## Dependencies

Key dependencies managed by UV:

- `nflreadpy` - High-performance NFL data access
- `polars` - Fast DataFrame operations
- `scikit-learn` - Machine learning algorithms
- `xgboost` - Gradient boosting
- `pandas` - Data manipulation (compatibility)
- `jupyter` - Interactive development
- `pytest` - Testing framework
- `pydantic` - Data validation and settings


## Troubleshooting

### Common Issues

**UV not found:**
```bash
# Restart terminal or source your shell profile
source ~/.bashrc  # or ~/.zshrc

#Set python to your present working directory if you run with just 
# python .. 
# Instead of 
# uv python ..

# This will only work for Mac / unix machines
export PYTHONPATH=$(pwd)
```

**Virtual environment activation fails:**
```bash
# Recreate virtual environment
uv venv --python 3.12
source .venv/bin/activate
uv sync
```

**Import errors:**
```bash
# Ensure virtual environment is activated and dependencies installed
source .venv/bin/activate
uv sync --reinstall
```

To look more into the python package responsible for our data look at the following links
- The library is a middleware to the lower link
[https://pypi.org/project/nflreadpy/](https://pypi.org/project/nflreadpy/)
[https://nflreadr.nflverse.com/](Info on where the data is sourced from)