# COSMIC Explorer

<p align="center">
  <img src="image.png" alt="COSMIC Logo" width="80">
</p>

<p align="center">
  <strong>CO₂ Solvent Materials Informatics Collection — Interactive Explorer</strong>
</p>

<p align="center">
  An interactive web application for browsing 3,200+ organic solvents with 3D molecular visualization<br>
  and comprehensive physical, thermodynamic, electronic, and CO₂ capture properties.
</p>

---

## Live Demo

Open `index.html` via a local HTTP server:

```bash
cd COSMIC
python -m http.server 8080
# Then visit http://localhost:8080
```

> **Note:** A local server is required because the app loads CSV and XYZ data files via `fetch()`.

---

## Features

- **3D Molecular Viewer** — Interactive ball-and-stick models rendered with Three.js. Rotate, zoom, and fullscreen support. Bond connectivity is computed in real-time from DFT-optimized XYZ geometries using covalent radii.
- **3,200+ Solvents** — Searchable and sortable list with pagination. Filter by solvent ID or SMILES.
- **Multi-Source Data Integration** — Properties merged from three independent computational pipelines:
  - COSMO-RS thermodynamic predictions (24 properties)
  - DFT quantum-mechanical calculations (13 properties)
  - CO₂ solubility predictions
- **Materials Project–Inspired UI** — Three-column detail view with left navigation, central content sections, and a right-hand property summary sidebar.

---

## Data Sources

| File | Records | Description |
|------|---------|-------------|
| `COSMO-RS/pure_solvent_properties_data.csv` | 3,203 | Viscosity, density, boiling/melting/flash point, dielectric constant, vapor pressure, critical constants, enthalpies, Gibbs energy, vdW area/volume, solubility parameter, synthetic accessibility |
| `Quantum_mechanics_DFT/DFT_Computed_Properties.csv` | 3,019 | SCF energy, dipole moment, HOMO/LUMO/gap, polarizability, partial charges, vibrational frequencies |
| `COSMO-RS/solubility_co2.csv` | 3,015 | Predicted CO₂ solubility (mol/L) from COSMO-RS |
| `xyz_files/Optimized_Geometry_xyz/` | ~2,600 | DFT-optimized molecular geometries in XYZ format |

---

## Project Structure

```
COSMIC/
├── index.html                              # Web application (single-file)
├── image.png                               # Logo
├── COSMO-RS/
│   ├── pure_solvent_properties_data.csv    # Physical & thermodynamic properties
│   └── solubility_co2.csv                  # CO₂ solubility data
├── Quantum_mechanics_DFT/
│   └── DFT_Computed_Properties.csv         # Electronic structure properties
└── xyz_files/
    └── Optimized_Geometry_xyz/             # ~2,600 XYZ geometry files
```

---

## Detail View Sections

| Section | Source | Properties Shown |
|---------|--------|-----------------|
| **Summary** | All | Key properties overview (boiling point, density, viscosity, HOMO-LUMO gap, CO₂ solubility) |
| **Physical Properties** | COSMO-RS | Viscosity, density, boiling/melting/flash point, dielectric constant, vapor pressure, molar volume, solubility parameter |
| **Thermodynamics** | COSMO-RS | Ideal gas entropy, enthalpies of formation/combustion/fusion/sublimation, Gibbs energy |
| **Critical Constants** | COSMO-RS | Critical temperature, pressure, volume; triple point temperature |
| **Molecular Descriptors** | COSMO-RS | van der Waals area & volume, parachor, synthetic accessibility |
| **Electronic Structure** | DFT | SCF energy, HOMO, LUMO, gap, dipole moment, polarizability, partial charges, vibrational frequencies |
| **Bonding** | XYZ | Bond types, average distances, and counts (computed from geometry) |
| **CO₂ Solubility** | COSMO-RS | Solubility value and capture rating (High / Moderate / Low) |

---

## Technology

- **Three.js** (v0.160.0) — WebGL-based 3D molecular rendering
- **OrbitControls** — Camera interaction (rotate, zoom, pan)
- **Vanilla JavaScript** — No build tools or frameworks required
- **Single HTML file** — Zero dependencies to install

---

## How Bonds Are Computed

XYZ files contain only atomic coordinates. Bonds are determined at runtime using covalent radii:

```
For each atom pair (i, j):
    d = Euclidean distance between atoms i and j
    threshold = (covalent_radius_i + covalent_radius_j) × 1.3
    minimum   = (covalent_radius_i + covalent_radius_j) × 0.4
    if minimum ≤ d ≤ threshold → bond exists
```

This is a standard approach in computational chemistry visualization tools.

---

## Licensing

This repository is released under the [MIT License](LICENSE).

---

## Acknowledgments

The COSMIC database was developed as part of research on organic solvents for electrochemical CO₂ reduction (CO₂ER). Data spans quantum chemical (DFT), thermodynamic (COSMO-RS), and classical molecular dynamics (MD) calculations covering solvents from 11 chemical classes.

---

## Contact

**Ruiqi Luo**
[GitHub: @RuiqiLuo](https://github.com/RuiqiLuo)
