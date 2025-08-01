# Work Daily  
## Jul 2025, Week 4

**Jul 28** 
- Completed onboarding 
- Started setting up LabsVision development environment (installation guide missing; encountered errors during Docker image build)

TODO: 
- Complete environment setup 
- Begin reading LabsVision code 

---

**Jul 29** 
- Finished environment setup. LabsVision runs successfully on laptop #env #docker 
- Drafted installation guide #doc 
- Read `elongation_thread` module and identified main procedure 

TODO: 
- Continue reading code related to marker detection and extensometer 

---

**Jul 30** 
- Reviewed `release-3.0.9` branch and git logs 
- Started dev environment setup for `release-4.0.0`. Encountered issues with OpenCV 4.6 image build, Dockerfile customization needed #env #docker 
- Pushed installation guide to Git (`dev/jamie/release-3.0.9` branch) #gitadd #doc 

TODO:
- Complete and run `release-4.0.0` build 
- Read `ML_marker_detect` repo

**Jul 31** 
- Reviewed the `ML_marker_detect` repo
- Ran the code successfully on the laptop

TODO:
- Evaluate model performance


**Aug 1**
- Wrote and ran visualization code for `ML_marker_detect` repo. Issues discovered: 1) Model evaluation metrics need improvement — some samples classified as poor by the test code are actually performing well. 2) False positive segmentations were observed, possibly due to preprocessing steps that amplify the effect of noisy pixels. #model #metrics
- Started reviewing the 'dev/ddarolfi/chevron-cubeten-ml-experimental' code branch. This branch is currently pending customer feedback. More attention should be given to the first 30 seconds of the pull when the sample begins moving. There's increased variability in the initial slope region, which may be unexpected. #customer 


TODO:
- Review the 'dev/ddarolfi/chevron-cubeten-ml-experimental' code branch and investigate the cause of the variability in the first 30 seconds.
