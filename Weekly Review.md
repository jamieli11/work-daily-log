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
- The variability in elongation may be caused by instability in the ML detect model's output results. https://github.com/jamieli11/work-daily-log/issues/2#issuecomment-3197335872
- The existing code generates segmentation masks for markers using the releases-3.0.9 codebase, but release 3.0.9 cannot handle halo scenarios effectively. This leads to inaccurate input data for the ML model, resulting in a "garbage in, garbage out" situation. https://github.com/jamieli11/work-daily-log/issues/3#issue-3331144047
https://github.com/jamieli11/work-daily-log/issues/4#issue-3331196391
- The current documentation and data generation code do not separate training and test sets, creating a risk of data leakage. 
- The ML detect model is missing the model weights file (only onnx and trt engine models), making it unable to fine-tune (needs pth or pt file) and requiring retraining from scratch.
- Two possible optimization approaches for improving detection accuracy in halo scenarios: 1) Optimize existing data generation code; 2) Use alternative ML models with appropriate data generators. Currently focusing on approach 1, as modifying the existing code effectively optimizes release 3.0.9, which can benefit both production code and the ML model. 
- Tested the following optimization methods: boundary clearance, morphological operations, and partial contrast adjustments, but no significant improvements have been observed yet. Further exploration is needed.

### Next Week Plan
- Continue optimizing detection for halo scenarios
- Complete learning the calibration code section
-------------------------
## Aug 18,2025 - Aug 22, 2025
### Work Overview
- Enhanced data generation algorithm with multi-resolution pyramid support, utilizing higher resolution inputs and leveraging known left_mark and right_mark position information to create ROI constraints for precise halo edge detection using Sobel operators and marker contour generation. https://github.com/jamieli11/work-daily-log/issues/4#issuecomment-3221187020
- Finish reading the calibration code section.

### Results & Findings
- Successfully reduced halo interference and improved data quality. Some minor halo fragments still appear in challenging scenarios, but the algorithm is ready for large-scale data generation and model training.

### Next Week Plan
- Planned to deliver an initial model trained on small dataset this week, followed by full-scale dataset model delivery in the future.
-------------------------
## Aug 25,2025 - Aug 29, 2025
## Work Overview
- Implemented edge-detector-based halo removal method into the data generation pipeline
- Applied SAM2 as an alternative data cleaning approach
- Cleaned chevron data (8988 frames total) and fine-tuned the detection model
- Wrote [inference code](https://github.com/LabsCubed-Inc/ML_marker_detect/blob/dev/jamie/inference.py) for the detection model, enabling it to run on unlabeled data
- Evaluated the updated model performances using labsvision code

## Results & Findings
- The edge-detector-based halo removal method shows inconsistent performance. Halos are not effectively removed in some cases, and hallowed regions in the mark mask occur frequently (particularly in the brightest area of the mark). https://github.com/jamieli11/work-daily-log/issues/4#issuecomment-3246076352
- SAM2 demonstrates strong performance in cleaning haloed data, though it occasionally failed. https://github.com/jamieli11/work-daily-log/issues/3#issuecomment-3246152768
- Completed model training for 40 epochs in total. The model achieved optimal performance at epoch 40 (based on visualized inference results on the test set), with significant improvement in halo-related issues. https://github.com/jamieli11/work-daily-log/issues/4#issuecomment-3246208941

## Next Week Plan
- Build TensorRT engine and test it on chip
- Generate additional training data to further fine-tune the ML detection model.
- Refactor ML detection code for improved modularity and scalability
- Implement comprehensive evaluation metrics for the ML detector and develop more detailed user documentation
