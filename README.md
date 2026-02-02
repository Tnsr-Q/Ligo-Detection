
GW150914-analysis/
│
├── .gitignore                     # Git ignore rules
├── README.md                      # Project documentation
├── LICENSE                        # MIT License
├── environment.yml                # Conda environment
├── requirements.txt               # Pip requirements
│
├── echo_search/                   # Main echo search module
│   ├── __init__.py               # Module exports
│   ├── core/                     # Physics core modules
│   │   ├── __init__.py
│   │   ├── schwarzschild_reflection.py
│   │   ├── wkb_phase_calculation.py
│   │   ├── parametric_rs.py
│   │   └── echo_detectability.py
│   │
│   ├── detectors/                # LIGO/Virgo specifics
│   │   ├── __init__.py
│   │   ├── noise_psd.py         # PSD models
│   │   └── antenna_pattern.py   # Detector responses
│   │
│   ├── templates/                # Template generation
│   │   ├── __init__.py
│   │   ├── waveform_generator.py
│   │   └── template_bank.py
│   │
│   ├── analysis/                 # Analysis methods
│   │   ├── __init__.py
│   │   ├── matched_filter.py
│   │   ├── bayesian_inference.py
│   │   └── statistics.py
│   │
│   ├── utils/                    # Utilities
│   │   ├── __init__.py
│   │   ├── plotting.py
│   │   └── file_io.py
│   │
│   └── pipeline.py               # Main pipeline orchestrator
│
├── notebooks/                    # Interactive analysis
│   ├── 01_data_exploration.ipynb
│   ├── 02_echo_detectability.ipynb
│   ├── 03_bayesian_analysis.ipynb
│   └── 04_results_visualization.ipynb
│
├── scripts/                      # Command-line tools
│   ├── run_gw150914_analysis.py
│   ├── generate_templates.py
│   ├── run_matched_filter.py
│   └── compute_upper_limits.py
│
├── data/                         # Data storage
│   ├── raw/                      # Raw GWOSC data (.gitignore)
│   ├── processed/                # Processed data (.gitignore)
│   └── README.md                 # Data documentation
│
├── results/                      # Analysis outputs (.gitignore)
│   ├── templates/
│   ├── mcmc_chains/
│   ├── upper_limits/
│   └── figures/
│
├── tests/                        # Unit tests
│   ├── __init__.py
│   ├── test_schwarzschild.py
│   ├── test_wkb.py
│   └── test_pipeline.py
│
└── docs/                         # Documentation
    ├── index.md
    ├── physics_background.md
    ├── installation.md
    └── api_reference.md
