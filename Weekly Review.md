## Aug 4,2025 - Aug 8, 2025
### Work Overview
Conducted in-depth investigation and analysis of distance measurement variability issues observed in SN0035 samples during the initial 30 seconds of tensile testing.
https://github.com/jamieli11/work-daily-log/issues/2

### Key Findings
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

**Critical Insight**

Through detailed comparison of left and right edges, discovered that edge point selection algorithms are directly related to measurement variability. The centerline-based approach did not resolve the variability issue, indicating the root cause lies in the edge point extraction algorithm limitations.

### Next Week Plan ###
- Continue analyzing edge point extraction algorithm improvement strategies
- Implement detection strategy optimization for marker deformation scenarios
- Validate impact of improved solutions on measurement stability
