# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Python PyPI package called "gocheck" for barrel distortion correction in wide-angle images. The library provides FOV-based distortion correction functionality with a simple API for developers working with action cameras, drones, and wide-angle photography.

## Key Architecture

- **Main Module**: `image_distortion.py` - Contains the core distortion correction algorithms
- **Core Functions**:
  - `theoretical_k1_k2_calculation()` - Calculates theoretical distortion coefficients based on FOV
  - `undistortion_fov()` - Applies barrel distortion correction to images using OpenCV

## Dependencies

The project uses:
- OpenCV (cv2) for image processing operations
- NumPy for mathematical calculations
- Math module for trigonometric functions

## Development Commands

### Package Development
- **Install dependencies**: `pip install -r requirements.txt`
- **Install in development mode**: `pip install -e .`
- **Build package**: `python -m build` (requires: `pip install build`)
- **Check package**: `python -m twine check dist/*` (requires: `pip install twine`)

### PyPI Publishing Workflow
1. Update version in both `setup.py` and `pyproject.toml`
2. Clean previous builds: `rm -rf dist/ build/`
3. Build: `python -m build`
4. Check package: `python -m twine check dist/*`
5. Upload to TestPyPI: `python -m twine upload --repository testpypi dist/*`
6. Test install: `pip install --index-url https://test.pypi.org/simple/ gocheck`
7. Upload to PyPI: `python -m twine upload dist/*`

### Testing
- **Manual testing**: `python -c "import gocheck; print(gocheck.theoretical_k1_k2_calculation(120))"`
- No formal test framework configured

## Project Structure

```
gocheck/
├── image_distortion.py    # Main distortion correction module
├── __init__.py           # Package initialization
├── setup.py              # Legacy package configuration
├── pyproject.toml         # Modern package configuration
├── requirements.txt       # Dependencies (opencv-python, numpy)
├── README.md             # Package documentation for PyPI
├── LICENSE               # MIT license
├── MANIFEST.in           # Package inclusion rules
└── .claude/              # Claude Code settings
```

## Package Information

- **Package Name**: gocheck
- **Version**: 0.1.0
- **Author**: jujuspace (juseongparkai@gmail.com)
- **Python Support**: >=3.7
- **License**: MIT

## Technical Notes

- The distortion correction assumes barrel distortion with configurable k1, k2 coefficients
- Camera matrix is calculated based on image dimensions with center point assumption
- FOV input is expected in degrees and converted to radians internally
- Package provides two main functions: `theoretical_k1_k2_calculation()` and `undistortion_fov()`

## Important Files for Version Updates

When updating the package version, modify these files:
- `setup.py` (line 11: version="X.X.X")
- `pyproject.toml` (line 7: version = "X.X.X")