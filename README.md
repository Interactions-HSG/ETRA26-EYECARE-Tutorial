# ETRA26-EYECARE-Tutorial

This repository contains the notebooks for the ETRA 2026 tutorial 
**EYE-CARE: Eye Tracking for Context-Adaptive Systems Based on Activity and Cognitive Load Prediction**. 
Date: June 1st, 13:30 - 17:00 (Marrakech, Morocco local time)

## 📄 Abstract
With the growing amount of digital data, the importance of systems that allow humans to exploit such data to obtain insightful interpretations has skyrocketed. Recent context-adaptive systems can provide users with assistance by proactively sensing, tracking, and interacting with them in a seamless, user friendly, and privacy preserving manner. For example, in an industrial or educational setting, such a system can detect when a user is challenged and provide adequate support (e.g., by highlighting task-relevant information that remains beyond the user’s attention). To maintain such adaptations, a real-time assessment of the user’s cognitive state and behavior are required. Such assessments can be addressed in multiple ways. One particular way to understand user behavior is to assess their visual perception through gaze-enabled systems. This half day tutorial will enable participants to analyze an existing human-activity recognition pipeline that is trained with an exiting eye movement dataset. The participants will be encouraged to build groups and discuss how this pipeline (as a proxy environment) can be extended (e.g., with multi-modal interaction or large language models) towards providing users with feedback that is potentially useful in a broad spectrum of personal and professional activities.


The notebooks that we provide in this repository show a compact pipeline from raw HoloLens 2 gaze data to gaze features, activity prediction, and task-adaptive AI support.

![Pipeline overview](Docs/pipeline_overview.png)

The pipeline starts with raw eye-tracking logs collected from the Microsoft HoloLens 2 through ARETT. The data is visualized and converted into gaze features. These features are then used to train an SVM classifier for activity recognition. The predicted activity can be forwarded to an intervention service that selects an activity-specific prompt and demo image, then returns AI-generated support for the detected task.

## Notebooks

- [`ReadAndVisualizeRawHL2GazeData.ipynb`](ReadAndVisualizeRawHL2GazeData.ipynb): Loads raw HoloLens 2 gaze CSV files, inspects columns, and visualizes different gaze metrics.
- [`FeatureCalculation.ipynb`](FeatureCalculation.ipynb): Implements I-DT-based fixation detection and computes a set of gaze features.
- [`AnSVMClassifierForHL2GazeFeatures.ipynb`](AnSVMClassifierForHL2GazeFeatures.ipynb): Reads the generated feature CSV, trains and evaluates SVM classifiers with different kernels, and predicts activity labels for new feature windows.
- [`InterventionExample.ipynb`](InterventionExample.ipynb): Uses the detected activity to select a demo image and prompt, generates AI support, and can expose the intervention as a small local HTTP service.

## Data and Assets

- `Data/RawGazeData/`: raw gaze recordings used by the visualization and feature calculation notebooks.
- `Data/FeatureFiles/`: feature CSV files used by the SVM classifier notebook.
- `DemoImages/`: example images used by the intervention notebook.
- `Docs/pipeline_overview.png`: overview figure shown above.

## Running in VS Code

1. Open this folder in VS Code.
2. Install the VS Code **Python** and **Jupyter** extensions if they are not already installed.
3. Select a Python kernel for the notebooks. A local virtual environment is recommended.
4. Open each notebook and run the install cell at the top once. The notebooks install their own basic dependencies with `%pip install ...`.
5. Run the notebooks in this order for the full flow:
   1. `ReadAndVisualizeRawHL2GazeData.ipynb`
   2. `FeatureCalculation.ipynb`
   3. `AnSVMClassifierForHL2GazeFeatures.ipynb`
   4. `InterventionExample.ipynb`
6. If you want the classifier in `AnSVMClassifierForHL2GazeFeatures.ipynb` to call the intervention service, first run the service cell in `InterventionExample.ipynb`. It starts a local endpoint at `http://127.0.0.1:5020/intervention`. Then run the classifier cell that calls that endpoint.

## 📚 Reference

*This tutorial contains supplementary material (e.g., the eye movement recordings in the Data folder) of the follwing publication. If you use/modify this material please add a reference to our publication:*
Kenan Bektaş, Jannis Strecker, Simon Mayer, and Kimberly Garcia. 2024. Gaze-enabled activity recognition for augmented reality feedback. Computers & Graphics (March 2024), 103909. https://doi.org/10.1016/j.cag.2024.103909

```bibtex
@article{bektasetalCG24,
title = {Gaze-enabled activity recognition for augmented reality feedback},
journal = {Computers & Graphics},
volume = {119},
pages = {103909},
year = {2024},
issn = {0097-8493},
doi = {https://doi.org/10.1016/j.cag.2024.103909},
url = {https://www.sciencedirect.com/science/article/pii/S009784932400044X},
author = {Kenan Bektaş and Jannis Strecker and Simon Mayer and Kimberly Garcia},
keywords = {Pervasive eye tracking, Augmented reality, Attention, Human activity recognition, Context-awareness, Ubiquitous computing},
abstract = {Head-mounted Augmented Reality (AR) displays overlay digital information on physical objects. Through eye tracking, they provide insights into user attention, intentions, and activities, and allow novel interaction methods based on this information. However, in physical environments, the implications of using gaze-enabled AR for human activity recognition have not been explored in detail. In an experimental study with the Microsoft HoloLens 2, we collected gaze data from 20 users while they performed three activities: Reading a text, Inspecting a device, and Searching for an object. We trained machine learning models (SVM, Random Forest, Extremely Randomized Trees) with extracted features and achieved up to 89.6% activity-recognition accuracy. Based on the recognized activity, our system—GEAR—then provides users with relevant AR feedback. Due to the sensitivity of the personal (gaze) data GEAR collects, the system further incorporates a novel solution based on the Solid specification for giving users fine-grained control over the sharing of their data. The provided code and anonymized datasets may be used to reproduce and extend our findings, and as teaching material.}
}
```
