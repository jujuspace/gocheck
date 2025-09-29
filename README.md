# GoCheck

A Python library for barrel distortion correction in wide-angle images using field of view (FOV) calculations.

## Features

- **Theoretical Distortion Calculation**: Calculate distortion coefficients (k1, k2) based on field of view
- **Barrel Distortion Correction**: Remove barrel distortion from wide-angle images
- **OpenCV Integration**: Built on top of OpenCV for efficient image processing
- **Simple API**: Easy-to-use functions for quick distortion correction

## Installation

```bash
pip install gocheck
```

## Quick Start

```python
import gocheck

# Correct barrel distortion using field of view
corrected_image = gocheck.undistortion_fov('input_image.jpg', fov=120)

# Calculate theoretical distortion coefficients
k1, k2 = gocheck.theoretical_k1_k2_calculation(fov_degrees=120, image_width=500)
print(f"Distortion coefficients: k1={k1}, k2={k2}")
```

## API Reference

### `undistortion_fov(image_path, fov)`

Corrects barrel distortion in an image based on the field of view.

**Parameters:**
- `image_path` (str): Path to the input image
- `fov` (float): Field of view in degrees

**Returns:**
- `numpy.ndarray`: Corrected image as NumPy array

### `theoretical_k1_k2_calculation(fov_degrees, image_width=500)`

Calculates theoretical distortion coefficients based on field of view.

**Parameters:**
- `fov_degrees` (float): Field of view in degrees
- `image_width` (int, optional): Image width in pixels (default: 500)

**Returns:**
- `tuple`: (k1, k2) distortion coefficients

## Dependencies

- OpenCV (opencv-python >= 4.5.0)
- NumPy (numpy >= 1.19.0)

## Use Cases

- Action camera footage correction
- Wide-angle lens distortion removal
- Drone camera image processing
- Security camera footage enhancement
- VR/AR content preprocessing

## Example

```python
import cv2
import matplotlib.pyplot as plt
import gocheck

# Load and correct an image with 150° FOV
corrected = gocheck.undistortion_fov('wide_angle_photo.jpg', fov=150)

# Save the corrected image (BGR format)
cv2.imwrite('corrected_photo.jpg', corrected)

# For matplotlib display, convert to RGB
corrected_rgb = cv2.cvtColor(corrected, cv2.COLOR_BGR2RGB)
plt.imshow(corrected_rgb)
plt.show()

# For OpenCV display (BGR format)
cv2.imshow('Corrected', corrected)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Changelog

- **v0.1.3**: Reverted to BGR output format to maintain OpenCV ecosystem consistency - use `cv2.cvtColor(result, cv2.COLOR_BGR2RGB)` for matplotlib display
- **v0.1.2**: Fixed color display issue - function now returns RGB format compatible with matplotlib (no more cv2.cvtColor needed)
- **v0.1.1**: Added direct import support - now you can use `gocheck.undistortion_fov()` instead of `gocheck.image_distortion.undistortion_fov()`
- **v0.1.0**: Initial release with barrel distortion correction functionality

## Author

jujuspace