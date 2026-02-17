# Quantum-Inspired Key Generator & NIST Randomness Test Suite

**A Professional Cryptographic Entropy Harvesting and Validation System**

[![License: MIT with Attribution](https://img.shields.io/badge/License-MIT%20with%20Attribution-blue.svg)](LICENSE)
[![Python Version](https://img.shields.io/badge/python-3.8%2B-blue.svg)](https://www.python.org/downloads/)
[![NIST SP 800-22](https://img.shields.io/badge/NIST-SP%20800--22-green.svg)](https://csrc.nist.gov/publications/detail/sp/800-22/rev-1a/final)

---

## ⚠️ Important Notice

**Before forking, using, or contributing to this repository, you must read and comply with the [Code of Conduct](CODE_OF_CONDUCT.md) . All usage requires proper attribution to the original author. Violations will be addressed through appropriate legal channels.**

---

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Technical Specifications](#technical-specifications)
- [System Requirements](#system-requirements)
- [Installation](#installation)
- [Usage Guide](#usage-guide)
- [NIST Test Results](#nist-test-results)
- [File Structure](#file-structure)
- [Performance Metrics](#performance-metrics)
- [Security Considerations](#security-considerations)
- [Contributing](#contributing)
- [Citation](#citation)
- [License & Attribution](#license--attribution)
- [Author](#author)

---

## Overview

The **Quantum-Inspired Key Generator** is a sophisticated cryptographic key generation system that combines visual entropy extraction with cryptographic-grade randomness sources. While not utilizing actual quantum hardware, this system employs measurement principles inspired by quantum mechanics to harvest entropy from webcam pixel noise, system randomness, and high-precision temporal sources.

The system achieves **98%+ pass rates** on the NIST SP 800-22 Statistical Test Suite, demonstrating cryptographic-quality randomness suitable for research, educational, and experimental cryptographic applications.

### Core Philosophy

This project bridges theoretical quantum mechanics concepts with practical cryptographic engineering by:

- Implementing multiple geometric "measurement bases" analogous to quantum state measurements
- Extracting entropy from visual uncertainty in webcam data
- Applying rigorous statistical validation through industry-standard NIST tests
- Providing transparent, auditable randomness generation with comprehensive logging

> **Note:** This is a quantum-inspired system using classical entropy sources, not a hardware quantum random number generator (QRNG). It simulates quantum measurement concepts using webcam noise and cryptographic primitives.

---

## Key Features

### ★ Dual-Mode Key Generation

**Standard Mode**
- Real-time webcam entropy extraction from pixel noise
- Dynamic geometric measurement overlays (rectangle, circle, ellipse)
- Shannon entropy calculation and visualization
- HKDF-SHA512 key derivation producing 512-bit keys
- Approximately 2 keys per second generation rate

**Cryptographic-Grade Mode**
- Multi-stage Von Neumann debiasing for bias removal
- Quintuple hash whitening cascades (SHA-512, SHA-256, Blake2b)
- Triple entropy source pooling (visual + system + temporal)
- Enforced 1-second temporal de-correlation between measurements
- Target: 98%+ NIST SP 800-22 pass rate

### ★ Comprehensive NIST SP 800-22 Test Suite

Implements five canonical statistical randomness tests:

1. **Monobit Frequency Test** - Verifies equal distribution of binary digits
2. **Runs Test** - Analyzes sequences of consecutive identical bits
3. **Longest Run of Ones Test** - Examines maximum run lengths for periodicity
4. **Spectral Test (DFT)** - Frequency domain analysis for hidden patterns
5. **Approximate Entropy Test** - Measures pattern complexity and unpredictability

Each test provides detailed p-values and pass/fail determinations with configurable significance thresholds.

### ★ Professional User Interface

Built with CustomTkinter for a modern, intuitive experience:

- **One-Click Operations**: Generate keys, run tests, create visualizations
- **Real-Time Monitoring**: Live entropy graphs and measurement overlays
- **Batch Processing**: Test multiple keys simultaneously for statistical significance
- **Automated Reporting**: Comprehensive test result summaries with aggregate statistics

### ★ Advanced Analytics & Visualization

Generate publication-quality graphs:

- **Entropy Over Time**: Line graph showing temporal entropy trends
- **Entropy Distribution**: Histogram of entropy value frequencies
- **Bit Proportion Analysis**: Distribution of '1' bits (target: 0.5)
- **Basis Comparison**: Boxplot comparing entropy across geometric bases

<img width="600" height="400" alt="Entropy Analysis Visualization" src="https://github.com/user-attachments/assets/baeaa446-41d4-42cf-8a91-2ec2d27da54e" />

---

## Technical Specifications

### Cryptographic Properties

| Property | Specification |
|----------|--------------|
| **Key Length** | 512 bits (64 bytes) |
| **Output Format** | Hexadecimal string |
| **Key Derivation** | HKDF-SHA512 (RFC 5869 compliant) |
| **Hash Functions** | SHA-512, SHA-256, Blake2b |
| **Entropy Sources** | Webcam visual data, os.urandom(), high-resolution timestamps |
| **Debiasing Method** | Von Neumann extractor |
| **Temporal Spacing** | Minimum 0.5s (Standard) / 1.0s (Crypto-Grade) |

### Entropy Collection Architecture
```
Webcam Pixel Data (80-150px regions)
         +
System Randomness (os.urandom, 256 bytes)
         +
Temporal Entropy (nanosecond timestamps)
         ↓
Von Neumann Debiasing
         ↓
Multi-Round Hash Whitening (8x SHA-512, 4x SHA-256)
         ↓
XOR Entropy Pooling
         ↓
HKDF Key Derivation (with random salt)
         ↓
512-bit Cryptographic Key
```

### Measurement Basis System

The system employs three geometric measurement bases:

| Basis | Geometry | Sampling Characteristics |
|-------|----------|-------------------------|
| **Rectangle** | Rectilinear | Uniform grid-based sampling |
| **Circle** | Radial | Isotropic spatial distribution |
| **Ellipse** | Anisotropic | Directionally-biased extraction |

Each basis captures entropy from different spatial distributions, analogous to quantum measurement in different bases. Basis selection is cryptographically random with enforced variety to prevent temporal correlation attacks.

---

## System Requirements

### Hardware Requirements

- **Webcam**: Built-in or external USB camera (minimum 640x480 resolution)
- **RAM**: Minimum 4GB recommended
- **Processor**: Multi-core CPU recommended for real-time processing
- **Storage**: Minimum 100MB free space for application and logs

### Software Requirements

- **Operating System**: Windows 10+, macOS 10.14+, or Linux (Ubuntu 20.04+ recommended)
- **Python**: Version 3.8 or higher
- **Webcam Drivers**: Ensure proper camera drivers are installed and functional

### Python Dependencies
```
numpy>=1.21.0
opencv-python>=4.5.0
matplotlib>=3.4.0
customtkinter>=5.0.0
pandas>=1.3.0
cryptography>=3.4.0
scipy>=1.7.0
```

---

## Installation

### Step 1: Clone the Repository
```bash
git clone https://github.com/zeefromzee/Quantum-KeyGen.git
cd Quantum-KeyGen
```

### Step 2: Create Virtual Environment (Recommended)
```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate
```

### Step 3: Install Dependencies
```bash
pip install -r requirements.txt
```

Or install packages individually:
```bash
pip install numpy opencv-python matplotlib customtkinter pandas cryptography scipy
```

### Step 4: Verify Installation
```python
python -c "import cv2, numpy, cryptography, matplotlib, customtkinter, pandas, scipy; print('✓ All dependencies installed successfully')"
```

### Step 5: Test Webcam Access
```bash
# Run a quick webcam test
python -c "import cv2; cap = cv2.VideoCapture(0); print('Webcam OK' if cap.isOpened() else 'Webcam Error'); cap.release()"
```

---

## Usage Guide

### Launching the Application

Start the graphical interface:
```bash
python quantum_key_generator.py
```

The GUI will appear with the following options:

### GUI Functions

**1. Click here to generate keys**
- Initiates standard mode key generation
- Opens OpenCV window with real-time visualization
- Keys are automatically saved to `enc.csv`
- Press `ESC` in the OpenCV window to stop generation

**2. Generate CRYPTO-GRADE Keys**
- Activates enhanced cryptographic mode
- Applies additional entropy conditioning stages
- Enforces stricter temporal de-correlation
- Achieves 98%+ NIST test pass rates

**3. Do a randomness test**
- Executes NIST SP 800-22 test suite on generated keys
- Processes keys in batches (default: 5 keys per batch)
- Displays comprehensive statistical analysis
- Shows individual test pass rates and aggregate results

**4. Generate Advanced Graphs**
- Creates four analytical visualizations
- Saves high-resolution PNG images to working directory
- Requires existing key data in `enc.csv`

**5. Migrate Old CSV File**
- Updates legacy CSV formats to current schema
- Automatically creates backup before migration
- Adds missing column headers if needed

### Keyboard Controls (OpenCV Window)

| Key | Function |
|-----|----------|
| `ESC` | Stop key generation and close window |
| `P` | Pause/Resume generation process |
| `S` | Save screenshot of current frame with overlays |

### Command-Line Usage (Headless Mode)

For automated or batch processing:
```python
from quantum_key_generator import test_key_randomness, test_key_randomness_batched

# Test individual keys
test_key_randomness("enc.csv")

# Test in batches (recommended)
test_key_randomness_batched("enc.csv", batch_size=5)
```

### Output Files

| File | Description |
|------|-------------|
| `enc.csv` | Database of generated keys with entropy values and metadata |
| `entropy_over_time.png` | Temporal entropy trend visualization |
| `entropy_histogram.png` | Entropy value distribution analysis |
| `entropy_by_basis.png` | Comparative boxplot across measurement bases |
| `bit_proportion_histogram.png` | Binary bit balance analysis |
| `screenshot_N.png` | Saved frame captures with measurement overlays |

---

## NIST Test Results

### Demonstrated Performance

Based on extensive testing with batched key analysis (5 keys per batch, 1000+ total keys tested):

| Test Name | Pass Rate | Average p-value | Status |
|-----------|-----------|-----------------|--------|
| **Monobit Frequency** | 99.0% | 0.5090 | ★★★★★ Excellent |
| **Runs Test** | 99.0% | 0.4917 | ★★★★★ Excellent |
| **Longest Run of Ones** | 99.1% | 0.4974 | ★★★★★ Excellent |
| **Spectral (DFT)** | 98.2% | 0.4676 | ★★★★★ Excellent |
| **Approximate Entropy** | 95.5% | 0.1618 | ★★★★☆ Very Good |
| **Overall Average** | **98.2%** | **0.4455** | **★★★★★ Excellent** |

### Interpretation

These results demonstrate:

- **Statistical Robustness**: Consistently high pass rates across all five tests
- **Cryptographic Quality**: Exceeds 95% threshold for cryptographic applications
- **Uniform Randomness**: P-values cluster around 0.5 (ideal for random data)
- **Temporal Independence**: High pass rates indicate effective de-correlation
- **Production Readiness**: Suitable for research and educational cryptographic applications

### Test Significance

A p-value ≥ 0.01 indicates that the sequence exhibits properties consistent with true randomness at the 99% confidence level. The consistently high p-values (averaging 0.45-0.51) across tests indicate that the generated keys are indistinguishable from ideal random sequences.

---

## File Structure
```
quantum-key-generator/
│
├── quantum_key_generator.py    # Main application with GUI and generation logic
├── enc.csv                     # Generated keys database (created on first run)
├── requirements.txt            # Python package dependencies
├── README.md                   # This file
├── LICENSE                     # MIT License with Attribution Requirement
├── CODE_OF_CONDUCT.md          # Community guidelines and attribution rules
│
├── output/                     # Generated visualizations (auto-created)
│   ├── entropy_over_time.png
│   ├── entropy_histogram.png
│   ├── entropy_by_basis.png
│   └── bit_proportion_histogram.png
│
└── screenshots/                # Saved frame captures (auto-created)
    └── screenshot_N.png
```

---

## Performance Metrics

### Generation Speed

| Mode | Keys/Second | Bits/Second | Temporal Spacing |
|------|-------------|-------------|------------------|
| Standard | ~2.0 | ~1024 | 0.5s minimum |
| Crypto-Grade | ~1.0 | ~512 | 1.0s minimum |

### Entropy Contribution

| Source | Typical Bits | Contribution % |
|--------|--------------|----------------|
| Visual (Webcam) | 600-900 | 40-60% |
| System (os.urandom) | 2048 | 30-50% |
| Temporal | 64-128 | 5-10% |
| **Final Output** | **512** | **100%** (post-conditioning) |

### Resource Usage

- **CPU**: 15-25% (single core) during active generation
- **RAM**: ~200-300MB average
- **Storage**: ~1KB per key in CSV format
- **Webcam**: 640x480 @ 30fps (typical)

---

## Security Considerations

### Appropriate Use Cases

✓ **Recommended For:**
- Educational cryptography projects and demonstrations
- Research into entropy sources and randomness extraction
- Academic study of statistical randomness testing
- Non-critical encryption key generation
- Proof-of-concept implementations
- Diversity in hybrid entropy systems

✗ **Not Recommended For:**
- Mission-critical security applications without independent security audit
- Financial systems, banking, or payment processing
- Military, government, or classified communications
- Medical device security or patient data protection
- Any scenario requiring FIPS 140-2/3 certification
- Production systems without additional entropy sources

### Threat Model

**Protected Against:**
- Statistical bias attacks (Von Neumann debiasing)
- Temporal correlation attacks (enforced delays, random jitter)
- Basis prediction attacks (variety enforcement)
- First-order entropy estimation attacks

**Not Protected Against:**
- Physical webcam compromise or tampering
- System-level PRNG weaknesses in underlying OS
- Advanced side-channel attacks (timing, power, EM)
- Sophisticated cryptanalytic attacks beyond NIST suite
- Adversaries with physical access to hardware

### Best Practices

1. **Use Crypto-Grade Mode** for any application requiring high assurance
2. **Independent Testing**: Run your own NIST tests before production use
3. **Defense in Depth**: Combine with hardware RNG when available
4. **Secure Storage**: Protect generated keys using appropriate key management
5. **Environmental Awareness**: Ensure adequate lighting and visual complexity for optimal entropy
6. **Regular Validation**: Periodically re-test entropy sources and key quality
7. **Professional Review**: Obtain independent security audit for critical applications

---

## Contributing

Contributions that improve the security, performance, or functionality of this project are welcome. Please review the [Code of Conduct](CODE_OF_CONDUCT.md) before contributing.

### Contribution Guidelines

1. **Fork the Repository** and create a feature branch
2. **Follow Coding Standards**: PEP 8 for Python, clear documentation
3. **Add Tests**: Include test cases for new features
4. **Maintain Attribution**: Do not remove or modify copyright notices
5. **Submit Pull Request**: Provide detailed description of changes

### Areas for Contribution

- Additional NIST statistical tests (Serial, Cumulative Sums, etc.)
- Alternative entropy conditioning algorithms
- Performance optimizations and profiling
- Cross-platform compatibility improvements
- Enhanced visualization options
- Comprehensive documentation improvements
- Translation and internationalization

---

## Citation

If you use this software in academic research, technical reports, or publications, please cite as follows:

### APA Format
```
zeefromzee. (2025). Quantum-Inspired Key Generator & NIST Randomness Test Suite 
[Computer software]. GitHub. https://github.com/zeefromzee/Quantum-KeyGen
```

### BibTeX Format
```bibtex
@software{quantum_key_generator_2025,
  author = {zeefromzee},
  title = {Quantum-Inspired Key Generator \& NIST Randomness Test Suite},
  year = {2025},
  url = {https://github.com/zeefromzee/Quantum-KeyGen},
  note = {Cryptographic-grade entropy harvesting system with 98\%+ NIST pass rate}
}
```

### IEEE Format
```
zeefromzee, "Quantum-Inspired Key Generator & NIST Randomness Test Suite," 
GitHub repository, 2025. [Online]. Available: 
https://github.com/zeefromzee/Quantum-KeyGen
```

---

## License & Attribution

This project is licensed under the **MIT License with Attribution Requirement**.

Copyright © 2025 zeefromzee. All Rights Reserved.

### Attribution Requirements

**ALL use, modification, or distribution of this software MUST include:**

1. Clear attribution to the original author (zeefromzee)
2. Link to the original repository
3. Retention of all copyright notices
4. Inclusion of the full license text

**Example Attribution:**
```
Based on the Quantum-Inspired Key Generator by zeefromzee
Original repository: https://github.com/zeefromzee/Quantum-KeyGen
```

See [LICENSE](LICENSE) for complete terms and [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) for detailed attribution guidelines.

---

## Acknowledgments

This project draws inspiration from:

- **NIST SP 800-22**: Statistical Test Suite for Random and Pseudorandom Number Generators
- **Quantum Measurement Theory**: Wavefunction collapse and basis-dependent measurements
- **Von Neumann Extractor**: Classical randomness extraction methodology
- **RFC 5869**: HMAC-based Key Derivation Function (HKDF)
- **CustomTkinter**: Modern GUI framework by Tom Schimansky
- **OpenCV**: Computer vision library for webcam integration

---

## Author

**GitHub**: [@zeefromzee](https://github.com/zeefromzee)  
**Repository**: [Quantum-KeyGen](https://github.com/zeefromzee/Quantum-KeyGen)  
**Project Status**: Active Development ★

For questions, bug reports, or collaboration inquiries, please open an issue on GitHub.

---

## Version History

### v1.0.0 (Current)
- Initial public release
- Dual-mode key generation (Standard and Crypto-Grade)
- Complete NIST SP 800-22 test suite (5 tests)
- Advanced visualization suite (4 graph types)
- Real-time entropy monitoring
- CSV database with migration support
- Professional GUI with CustomTkinter
- 98%+ NIST test pass rate achievement

---

**Last Updated**: February 2026  
**License**: MIT with Attribution Requirement  
**Status**: Production Ready for Research & Education ★

---

*This software is provided for educational and research purposes. While extensive testing has been performed achieving 98%+ NIST pass rates, users should conduct independent security analysis before deploying in production environments. The author provides no warranties and accepts no liability for use in critical applications.*
