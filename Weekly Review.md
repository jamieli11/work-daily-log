## Aug 4,2025 - Aug 8, 2025
### Work Overview
Conducted in-depth investigation and analysis of distance measurement variability issues observed in SN0035 samples during the initial 30 seconds of tensile testing.
https://github.com/jamieli11/work-daily-log/issues/2

### Results & Findings
**Problem Identification**:
- Fine-tuned labsvision ML branch exhibits poor tracking performance when plastic pull samples begin moving
- Significant elongation variability observed across different slots within the same run
- ML detection issues include vague boundary capture and inaccurate marker coordinates
- Late-stage marker deformation with stretching in x-direction forming irregular shapes

**Technical Analysis**:
- Completed distance vs. time analysis for 12 SN0035 datasets, confirming measurement variability
- Implemented ML model detection result visualization, revealing edge point extraction algorithm deficiencies

**Solution Attempts: Modified Distance Calculation Method**
- Approach: Changed measurement calculation from mean of all distances to measurements only near specimen centerline
- Results: No change in detected distance compared to original method
- Follow-up Analysis: Conducted 2D to 3D magnification study, finding 1mm 3D displacement corresponds to 16 pixels change

**Conclusion**

Through detailed comparison of left and right edges, discovered that edge point selection algorithms are related to measurement variability but only has limited impact on the final distance measurements.

### Next Week Plan ###
- Analyze edge point extraction algorithm improvement strategies
- Implement detection strategy optimization for marker deformation scenarios
-------------------------
## Aug 11,2025 - Aug 15, 2025
### Work Overview
- Conducted more detailed analysis of elongation differences across different slots within the same run during the 30 seconds after pulling begins (chevron-cubeten-ml-experimental branch).
- Successfully ran the ML detect model's data generation code and performed visual evaluation of the generated dataset.
- Attempted to optimize detection methods for samples with halos.

### Results & Findings
- The variability in elongation may be caused by instability in the ML detect model's output results.
The existing code generates segmentation masks for markers using the releases-3.0.9 codebase, but release 3.0.9 cannot handle halo scenarios effectively. This leads to inaccurate input data for the ML model, resulting in a "garbage in, garbage out" situation. 
- The current documentation and data generation code do not separate training and test sets, creating a risk of data leakage. 
- The ML detect model is missing the model weights file, making it unable to fine-tune and requiring retraining from scratch.
- Two possible optimization approaches for improving detection accuracy in halo scenarios: 1) Optimize existing data generation code; 2) Use alternative ML models with appropriate data generators. Currently focusing on approach 1, as modifying the existing code effectively optimizes release 3.0.9, which can benefit both production code and the ML model. 
- Tested the following optimization methods: boundary clearance, morphological operations, and partial contrast adjustments, but no significant improvements have been observed yet. Further exploration is needed.

### Next Week Plan
- Continue optimizing detection for halo scenarios
- Complete learning the calibration code section
