# Model Card

## Model Description

**Input:** 
1 - LFP power spectrograms consisting in a series of LFP power spectra over a time window of +- 50 s relative to the time pont to be classified. 
2 - Movement magnitude time series over a time window of +- 50 s relative to the time pont to be classified.

**Output:** 
Brain state prediction, which can be one of four classes: 1 - "Wake", 2 - "Quiet Wake", 3 - "NREM" sleep 4 - "REM" sleep. 

**Model Architecture:** Bimodal Concolutional Neural Network. The 2 types of inputs pass though independent convolutional branches, each composed by 2 convolutional layers (2D for LFP spectrograms branch or 1D for movement branch), after which their output is concatenated and fed into 2 fully connected layers before reching the output layer.

## Performance

The overall accuracy of the model, assessed in a test set containing data not seen during training and validation, is close to 90%. The figure shows the breakdown of accuracy accross classes, in comparison with a Random Forest classifier.

![Screenshot](Model_selection.png)

## Limitations

It is still unclear how the model generalizes on data collected from rodents not used in the model training. It is possible that in those cases accuracy might be lower that what is reported here.
The imputs provided should be as close as possible to the ones used in model training. Namely, electrical activity just be recorded from the hippocampus and the movement signal should be recorded with an accelerometer located in the head of the animal. Deviations from this might negatively impact predictions.

## Trade-offs

The main performance bottleneck of this model is the distinction between the class "Quiet Wake" and "Wake" and "NREM" sleep. That is because usually the animals slowly transition from being active, to immobility until eventually falling asleep. Exact determination of the timepoint of transition from active to quiet wakefullness is somewhat ambiguous. Moreover, detection of the moment when animals fall asleep is not possible based solely on this dataset. 
