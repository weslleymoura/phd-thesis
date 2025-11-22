# Density-Based Clustering for Vehicle Routing Problems

## About This Research

This repository contains the implementation and experiments for a PhD research project focused on **reducing vehicle routing problem complexity through density-aware clustering in urban logistics**.

### Research Overview

Urban last-mile delivery presents significant optimization challenges, with logistics companies needing to efficiently route vehicles to deliver thousands of parcels daily. This work proposes a novel hierarchical clustering approach that combines:

- **Kernel Density Estimation (KDE)** to identify high-density delivery regions
- **KMeans clustering** for macro-level spatial partitioning
- **DBSCAN** for fine-grained density-based sub-clustering
- **Spatial sequencing** of clusters to simplify vehicle allocation

The method is evaluated using the **LoggiBUD dataset** (Loggi Benchmark for Urban Deliveries), which provides real-world delivery data from major Brazilian cities, including street networks, travel distances, and historical delivery records.

### Key Innovation

Unlike traditional VRP segmentation methods, this approach:
1. Separates high-density urban cores from sparse peripheral areas using contour-based density thresholding
2. Applies different clustering strategies based on local density patterns
3. Sequences sub-regions spatially to reduce inter-route distances and improve route coherence

### Repository Structure

```
├── data/                    # LoggiBUD dataset (CVRP instances)
├── loggibud/               # Core library for data handling and evaluation
├── notebooks/              # Jupyter notebooks with experiments and analysis
├── osrm/                   # OSRM routing engine data files
├── phd-thesis/             # LaTeX papers and thesis materials
└── requirements.txt        # Python dependencies
```

## Environment Setup

### 1. Create Python Virtual Environment

Create and activate a conda environment with Python 3.13:

```bash
conda create -n phd-util-env python=3.13
conda activate phd-util-env
```

### 2. Install Dependencies

Install required Python packages:

```bash
python -m pip install -r requirements.txt
```

### 3. Configure OSRM Server

The project uses OSRM (Open Source Routing Machine) for calculating real-world road distances. Start the OSRM server with Docker:

```bash
docker run -t -i -p 5001:5000 -v "${PWD}:/data" \
  osrm/osrm-backend:v5.24.0 osrm-routed \
  --algorithm ch /data/osrm/brazil-201110.osrm \
  --max-table-size 10000
```

**OSRM Configuration Details:**
- Maps container port 5000 to host port 5001
- Uses Contraction Hierarchies algorithm for fast routing
- Supports distance matrix calculations for up to 10,000 points
- Brazil map data file: `osrm/brazil-201110.osrm`

### 4. Environment Management

**Deactivate environment:**
```bash
conda deactivate
```

**Remove environment (if needed):**
```bash
conda remove --name phd-util-env --all
```

## Getting Started

1. Ensure OSRM server is running (see step 3 above)
2. Activate the conda environment: `conda activate phd-util-env`
3. Open Jupyter notebooks in the `notebooks/` directory
4. Start with the baseline notebooks to understand the approach

## Dataset

This project uses the **LoggiBUD** (Loggi Benchmark for Urban Deliveries) dataset, which provides:
- Real delivery instances from Brazilian cities
- Street network data
- Historical delivery records
- Training and testing splits for evaluation

The dataset is organized in `data/cvrp-instances-1.0/` with separate `train/` and `dev/` directories.

## License

See the [LICENSE](LICENSE) file for details.

## Contact

**Weslley Moura**  
Email: weslleymoura@gmail.com



