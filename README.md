# Traffic-Volume-Prediction-Model-and-Visualisation-
A data analytics pipeline transforming unstructured TfNSW telemetry APIs into optimised spatial predictive models to deliver actionable city planning infrastructure metrics

## Project Architecture & Workflow

```

┌──────────────────────────┐      ┌──────────────────────────┐
│  1. DATA PROTOTYPING     ├─────►│  2. MACHINE LEARNING     │
│ Google Colab Exploration │      │ Train Predictive Trees   │
└──────────────────────────┘      └──────────────────────────┘
│
┌──────────────────────────┐      ┌─────────────▼────────────┐
│  4. USER INTERFACE (.EXE)│◄─────┤  3. PYINSTALLER BUILD    │
│ Color-Coded Live Maps    │      │ Package Code + Datasets  │
└──────────────────────────┘      └──────────────────────────┘

```

---

## 1. Machine Learning Core (Google Colab)
The predictive backbone of the project was developed and validated within Google Colab, utilising historical traffic logs to train **Supervised Machine Learning Regression models**. 

* **Feature Engineering:** The models process structural traffic variables, including:
  * Spatial details (Station Key, Traffic/Cardinal Direction Sequence)
  * Temporal details (Month, Day of the Week, Prediction Hour, School Holiday Status)
  * Lag features (Average traffic volume from the previous 3 hours, and the previous day's baseline).
* **Model Objective:** To intercept real time traffic attributes and immediately output a highly precise, estimated vehicle volume count.

## 2. The Interactive Desktop Application Engine
The deployment phase wraps the trained ML models into an interactive Windows executable application (`map_display.exe`). Upon launching, users see a **Welcome Interface** featuring a fully interactive command ecosystem:

### Core CLI Features:
* **`Basic` (Geospatial Mapping):** Feeds geographic coordinate points into a core map engine to overlay active Sydney tracking stations with directional arrows showing traffic flow.
* **`StationList` (Data Directory):** Outputs an indexed table of all active traffic monitoring stations and their corresponding identifier keys for easy lookup.
* **`Predict` (Live Machine Learning Inference):** Prompts the user through a guided question sequence to input current contextual variables. It passes these straight to the ML model backend to generate a real time traffic volume prediction.
* **`Overall` (Advanced Congestion Mapping):** A dynamic macromapping feature. Users enter a subset of target stations along with global variables (Hour, Day, Public Holiday Status). The application computes predictions for all points simultaneously and renders a **geographical map with colour coded arrows representing traffic congestion severity**.
* **`Help` & `Quit`:** Features dedicated diagnostic modules for formatting support and clean system termination.

### Fail-Safe Input Validation:
To guarantee production level application stability, robust error handling mechanisms shield the engine from crashes. The interface actively intercepts user typos such as incorrect capitalisation, accidental trailing spaces, or invalid commands safely rejecting the input and prompting a re entry without breaking the program runtime.

---
## Production Packaging & Deployment
1. **Python Script Migration:** The finalised mapping code and model weights were exported from Google Colab into modular Python (`.py`) scripts.
2. **PyInstaller Compiling:** The executable was compiled into a single file portable utility containing both the internal mapping engine and the core database:
   ```bash
   pyinstaller --onefile map_display.py

```
