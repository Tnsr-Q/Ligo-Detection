tensorq-darwinian-gateway/
├─ README.md
├─ LICENSE
├─ .gitignore
├─ .editorconfig
├─ go.work
│
├─ docs/
│  ├─ architecture/
│  │  ├─ 00-overview.md
│  │  ├─ 10-stream-simulation.md
│  │  ├─ 20-route-mutation-firewall.md      # invariants, two-phase commit, rollback rules
│  │  ├─ 30-swarm-integration.md            # brain/muscle boundary, failure modes
│  │  ├─ 40-cilium-mode-matrix.md           # native routing vs encap vs kube-proxy-free
│  │  └─ 50-observability.md
│  ├─ adr/
│  │  ├─ ADR-0001-bridge-over-uds.md
│  │  ├─ ADR-0002-firewall-owns-mac-resolution.md
│  │  ├─ ADR-0003-two-phase-map-commit.md
│  │  └─ ADR-0004-python-swarm-fault-isolation.md
│  └─ runbooks/
│     ├─ incident-route-flap.md
│     ├─ incident-map-pressure.md
│     ├─ incident-pyro-partition.md
│     └─ rollback.md
│
├─ proto/
│  ├─ buf.yaml
│  ├─ buf.gen.yaml
│  └─ tensorq/darwinian/v1/darwinian_gateway.proto
│
├─ gen/
│  └─ go/tensorq/darwinian/v1/
│
├─ cmd/
│  ├─ gatewayd/
│  │  └─ main.go                 # StreamSimulation, metrics ingestion
│  ├─ mutation-firewalld/
│  │  └─ main.go                 # admission + staging + probe + rollback + audit
│  ├─ ebpf-loaderd/
│  │  └─ main.go                 # load/pin programs+maps, attach tc/xdp
│  ├─ overseer-coordinatord/
│  │  └─ main.go                 # collects metrics, talks to swarm local bridge
│  └─ prober/
│     └─ main.go                 # synthetic probes, health confirmations
│
├─ internal/
│  ├─ gateway/
│  │  ├─ stream/
│  │  ├─ templates/
│  │  └─ server/
│  │
│  ├─ firewall/
│  │  ├─ admission/              # validation, quotas, auth, invariants
│  │  ├─ staging/                # A/B map staging, active index swap
│  │  ├─ probe/                  # reachability+backend confirmation logic
│  │  ├─ rollback/
│  │  ├─ audit/
│  │  └─ server/
│  │
│  ├─ ebpf/
│  │  ├─ maps/
│  │  ├─ programs/
│  │  ├─ pin/
│  │  └─ compat/                 # kernel feature detection matrix
│  │
│  ├─ swarmbridge/               # Go client to local Python bridge (NOT Pyro protocol)
│  │  ├─ client/
│  │  ├─ types/                  # intent schemas for leader/alpha/proposals
│  │  ├─ codec/                  # stable serialization + versioning
│  │  └─ health/
│  │
│  ├─ resolver/                  # owns neighbor/MAC/next-hop resolution
│  │  ├─ netlink/
│  │  ├─ cache/
│  │  └─ policies/
│  │
│  └─ obs/
│     ├─ metrics/
│     ├─ tracing/
│     └─ hubble/
│
├─ swarm/                         # Python Pyro5 swarm (Brain)
│  ├─ README.md
│  ├─ pyproject.toml              # prefer this over requirements.txt for reproducibility
│  ├─ poetry.lock / uv.lock       # pick one for deterministic deps
│  ├─ src/
│  │  ├─ modern_meta/
│  │  │  ├─ node.py               # leader election + membership
│  │  │  ├─ consensus.py          # agreement on alpha candidates
│  │  │  ├─ darwinian.py          # GA/selection logic
│  │  │  ├─ telemetry.py          # accepts metrics from overseer
│  │  │  └─ storage.py            # persistence for last-known-good
│  │  ├─ bridge/
│  │  │  ├─ server.py             # local-only UDS/localhost server for Go
│  │  │  ├─ schemas.py            # versioned request/response schemas
│  │  │  └─ auth.py               # local capability token / filesystem perms
│  │  └─ utils/
│  │     ├─ serialization.py
│  │     └─ time.py
│  ├─ Dockerfile
│  └─ tests/
│
├─ bpf/
│  ├─ README.md
│  ├─ include/
│  │  ├─ route_entry.h            # single source of truth for struct layout
│  │  └─ maps.h
│  ├─ tc/
│  ├─ xdp/
│  ├─ maps/
│  └─ build/
│
├─ deploy/
│  ├─ helm/
│  │  ├─ gateway/
│  │  ├─ swarm/
│  │  └─ monitoring/
│  ├─ k8s/
│  │  ├─ rbac/
│  │  ├─ services/
│  │  │  ├─ gatewayd.yaml
│  │  │  ├─ mutation-firewalld.yaml
│  │  │  ├─ ebpf-loaderd-daemonset.yaml
│  │  │  ├─ overseer-coordinatord.yaml
│  │  │  └─ swarm-statefulset.yaml
│  │  └─ gateway-api/
│  └─ terraform/
│
├─ test/
│  ├─ integration/
│  │  ├─ kind/
│  │  ├─ scenarios/
│  │  │  ├─ swarm-partition/
│  │  │  ├─ alpha-rollout/
│  │  │  ├─ rollback/
│  │  │  └─ route-flap/
│  │  └─ harness/
│  └─ fixtures/
│
└─ tools/
   ├─ proto/
   ├─ loadtest/
   └─ release/








GW150914-analysis/
│
├── .gitignore                       
├── README.md                      # Project documentation
├── LICENSE                        # License
├── environment.yml                # Environment config
├── requirements.txt               # Python requirements
│
├── echo_search/                      
│   ├── __init__.py                
│   ├── core/                      
│   │   ├── __init__.py
│   │   ├── schwarzschild_reflection.py
│   │   ├── wkb_phase_calculation.py
│   │   ├── parametric_rs.py
│   │   └── echo_detectability.py
│   │
│   ├── detectors/                 # LIGO/Virgo specifics
│   │   ├── __init__.py
│   │   ├── noise_psd.py         
│   │   └── antenna_pattern.py     
│   │
│   ├── templates/                 # Template generation
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
