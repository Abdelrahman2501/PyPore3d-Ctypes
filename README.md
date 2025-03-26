# PyPore3D (ctypes version)

A Python wrapper for the PyPore3D image processing tool using `ctypes`, replacing the original SWIG interface. This tool supports geological and porous media analysis using various filters, skeletonization, and blob analysis techniques on 3D volumetric data.

Developed as part of a Bachelor Thesis by **Abdelrahman Mohamed Rashwan**, supervised by **Dr. John Zaki** and **Dr. Amal Aboulhassan**.

## 🔧 Features

- Filtering Techniques
- Blob (Connected Component) Analysis  
- Skeletonization  
- Anisotropy & Basic Component Analysis  
- Raw Image (.raw) file reader  
- ctypes-based DLL loading  
- GCC Command Generator (semi-automated)(Not Filled with all paths yet)
- High performance with low overhead  

## 📚 Background

PyPore3D is an open-source software for the analysis of 3D/4D tomographic data, originally using SWIG to bridge Python and C. While powerful, SWIG suffers from:

- High overhead in wrapper generation  
- Complex debugging  
- Platform-specific configuration  
- Time-consuming setup process  

This project replaces SWIG with Python’s built-in `ctypes`, a lightweight and direct interface to C libraries, simplifying the integration process while boosting performance.

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/Abdelrahman2501/PyPore3d-Ctypes.git
cd pypore3d-ctypes
```

### 2. Install Python Dependencies

Make sure you have Python 3.x installed, then install dependencies:

```bash
pip install -r requirements.txt
```

Contents of `requirements.txt`:

```
numpy
matplotlib
scikit-image
jupyter
```

### 3. Prepare DLLs

Ensure all required DLLs (e.g., `P3D_Filt.dll`, `p3d_blob.dll`, etc.) are located in the `dlls/` directory.

Use the `dll_path_generator` tool to generate the full path references:

U Can find the dlls at the dlls folder or in the pypore3d tool folder insidie like filters dlls will be found in the filters folder while the skeltonization dll is found in its respesctive folder.

Each Python wrapper (like `otsu.py`, `median.py`, etc.) loads its specific DLL using the generated path.

### 4. Load and Process a .raw Image

You can load a 3D image using the provided utility:

```python
from pypore3d.utils import read_raw_image
image = read_raw_image("data/SC1_700x700x700.raw", (700, 700, 700))
```

Then apply a filter, for example Otsu thresholding:

```python
from pypore3d.otsu import apply_otsu
result = apply_otsu(image)
```

### 5. Run Example Notebook

Launch Jupyter Notebook and open the demo:

```bash
jupyter notebook notebooks/example_usage.ipynb
```

This notebook shows how to use all ctypes-based functions including filtering, blob detection, and skeletonization.

## 🧠 Methodology Overview

Comparison between SWIG and ctypes:

- SWIG: Requires `.i` files, slow execution, complex debugging  
- ctypes: No wrappers needed, faster execution, easier debugging  

Example GCC command to compile C files into DLLs:

```bash
gcc -shared -o P3D_Filt.dll P3D_Filt.c
```

## 🧪 Experimental Setup

- Dataset: Geological raw image (700x700x700)  
- Operations tested:  
  - Otsu Thresholding  
  - Median Filtering  
  - Blob Analysis  
  - Skeletonization  

## ⏱ Performance Summary

| Operation         | SWIG Time | ctypes Time | Improvement |
|------------------|-----------|-------------|-------------|
| Otsu Thresholding| 5.10 sec  | 2.37 sec    | 54% faster  |
| Median Filtering | 134 sec   | 78 sec      | 42% faster  |
| Blob Analysis    | 492.87 sec| 490 sec     | Slightly faster |
| Skeletonization  | 390.36 sec| 173.66 sec  | 56% faster  |

All outputs were visually and numerically identical. This was validated using pixel-by-pixel subtraction (resulting in black difference images).

## ✅ Results & Insights

- Faster execution across all filters and analysis  
- Reliable and consistent outputs  
- Easier to integrate and debug  
- ctypes is a practical and scalable alternative to SWIG  

## 🔭 Future Work

- Enhance error handling during C function execution  
- Add Mac/Linux DLL support  
- Complete the GCC Command Generator into a full tool  
- Benchmark with larger datasets and new filters  

## 👨‍🎓 Author

**Abdelrahman Mohamed Rashwan**  


## 📜 License

This project is licensed under the MIT License.


