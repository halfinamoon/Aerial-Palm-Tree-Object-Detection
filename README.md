# Proposal of SCOPE Analysis: Aerial Palm Tree Counting Project

Notes: In this project exploratory analysis i use terms of _"projected"_ as the indication for synthetization of data or rough assumptions, only for the project exploratory simulations purposes (contextual awareness and objective alignment), the actual facts and validity might actually far from accurate representative of company

## S: Stakeholder Requirements & Success Criteria

### Primary Stakeholders:

- **Primary Stakeholders**: Company
- **Plantation Manager**: Requires automated palm tree plantation quantity data for harvest planning (_projected_)
- **Agricultural Officers**: Track and Monitor plantation's growth or decline
- **Financial Department**: Require the data for asset analysis and valuation (_projected_)

### Business Success Definition:

- AI Model of Aerial Tree Counter accuracy reach at least 80% of Coverage (_projected_)
- Automated track of changes of specific landscape of plantation growth and disposal over certain period of times
- Generating automated aerial distribution maps for palm tree plantation management

### Error Tolerance:

- **Type I errors (False Positives)**: Medium tolerance
  - _Business Impact_: Over-Preparation of harvesting operation
  - Business Mitigation: Abundance of cost is still recoverable and reallocate-able (_projected_)
- **Type II errors (False Negatives)**: High tolerance
  - _Business Impact_: Losing full potential of plantation harvesting
- \*\*Conclusion:
  - Recall (Coverage) over Precision (Quality)
  - Over-Preparation < Under-Preparation (_projected_)

### Interpretability Requirements:

- Requires Image visualizations and quantity result for further validation
- Providing confidence scores for least ambiguous detection

```
Conclusion of Success Criteria (projected):
1. Maximize coverage of detected palm trees
2. Keep Maintaining Quality of detection
3. Develop robust AI model for better generalization on highly heterogenous condition of nature
4. Identify obscure area that hardly to yields accurate automatic detection
```

## C: Constraints & Context

### Computational Resources:

- **Training**:
  - Low-performance GPU cluster at Engineer compute station (_projected_)
- **Inference**:
  - Mid or Edge Device at plantation unit probably in remote locations with limited connectivity
  - Not requires of object tracking system as palm tree is a still object, which requires quality of coverage detection rather than fastest inference speed
- **Field Use**: For Laptop or Mobile device that processing aerial images from drone (_projected_)

### Deployment Environment:

- Primary: Cloud-based processing pipeline
- Secondary: Laptop or Mobile Devices for offline processing
- Future consideration:
  - Hybrid Cloud-based for main inference and local Model for backup inference mitigation
  - Drone as Computational Edge device

### Response Time Requirements:

- Job Processing or minimum delayed inference is still acceptable
- Inference Speed at least of 1 FPS on all target machines

### Data Constraints:

- Palm Tree Object Characteristic
  - Palms Tree Overlapping nature due to dense plantation setup
  - Non-Complex nature of pattern from palm tree especially from top angle
  - Various size or scale of the palm tree
- Environment Characteristic
  - Aerial imagery from drones or helicopter
  - Variation of Scale and Resolution of images
  - Natural illumination, bush, foliage, similar plant and other object
  - Palm Tree Occlusion with shadows or other similar Trees
  - Potentially Mixed with other plants or vegetation
- Contextual Consideration
  - Limited training data (~500 manually annotated images) that sourced from public object detection dataset from _Roboflow_

## O: Objectives & Optimization Targets

### Primary Metric:

- Recall (AR) across different tree densities (IOU overlapping: 0.5, 0.7, 0.9)

### Secondary Metrics:

- Average Precision (AP) at high recall point (> 0.9) finding best coverage with best quality
- F1 score for tree detection (balancing precision and recall) since the detection consist of single class target
- Inference time per image

### Performance Thresholds:

- **Minimum Acceptable**:
  - R > 80%
  - AP > 70%
- **Target**: F1 > 0.7
- **Stretch Goal**: F1 > 0.85

### Acceptable Trade-offs:

- Recall > Precision (Precision can be sacrifice reasonably)
- Quality > Speed (Inference time can be sacrifice at extend)
- Small Model Size < Large Model Size (The Model needs to be deploy on mid to edge devices)
- Low computational Limit resulting long duration span of training process due to hardware constraint (_projected_)

```
Optimization Priority Order:
1. Recall (Detection Coverage)
2. Precision (Detection Quality)
3. Model size efficiency
4. Inference speed
```

## P: Problem Characteristics

### Problem Type:

- Object detection of palm tree in aerial imagery with counting capability
- Monitoring plantation changes over time (_predicted_)

### Data Characteristics:

- **Volume**: aerial images covering more than 1 hectares
- **Dimensions**: High-resolution 5954 x 6978 from 41.5 MP camera source
- **Distribution**:
  - Manual Human Counting approximately 615 trees relatively in the center of the image and 105 trees spread across the border of the image in total of 720
  - Imbalanced tree density in certain area
  - Variable tree size and scale
  - Significant tree overlapping across plantation
  - Some irregular pattern or blank spot (adjacent with river pond, flat ground, etc.)
  - Some occlusion with other species of trees or bush

### Special Considerations:

- Seasonal variations (rain and sunny) affecting natural color and shade significantly between different season (predicted)

### Domain-Specific Factors:

- Knowledge Seasonal behaviors of trees different growth
- Plantation layout management approach and their impact on tree occlusion

## E: Evaluation Strategy

### Validation Approach:

### A. Dataset Splitting

- **Training Set**: 90% of the data for training
- **Validation Set**: 5% of the data for hyperparameters tuning.
- **Test Set**: 5% of the data for final evaluation

### B. Cross-Validation

- **K-Fold Cross-Validation**: If the dataset is large enough, use k-fold cross-validation

### Testing Methodology:

### A. A/B Testing

- **Implementation**: Compare the baseline model against alternative model
- **Metrics to Compare**: Use F1, AR, and AP to evaluate performance gap.

### B. Validation

- **Validation**: Conduct manual labeling of palm tree number to validate model predictions

### Monitoring Plan:

### A. Performance Monitoring

- **Real-Time Monitoring**: Set up dashboards to monitor performance metrics in training progress

### B. Feedback Collection

- **User Feedback**: Gather input from Plantation Manager regarding of model reliability.
- **Iterative Improvements**: Use monitoring metric to refine the model and retrain with new dataset improvement.

### Maintenance Strategy:

- **Retraining Schedule**: Schedule the regular model updates to incorporate new data and model improvement regarding to computational power

## AI Model Development Approach Selection Framework

## Project Requirements:

1. **Time Constraints**: < 1 Week
2. **Team Expertise**: Software Engineers with some ML or General Developers
3. **Use Case Complexity**: Standard Object Detection (Not for research purpose)
4. **Data Availability**: Medium Dataset (500-1000 images)
5. **Deployment Environment**: Edge Devices, Mobile Applications, Cloud Services

**Balance development speed vs. performance needs**:

- MMDetection Model Toolbox
- Model API Frameworks (Ultralytics)

## Detailed Analysis by Confidence Threshold

| Threshold | Precision | Recall | F1 Score | mAP50 | Analysis                                     |
| --------- | --------- | ------ | -------- | ----- | -------------------------------------------- |
| 0.1       | 0.939     | 0.878  | 0.908    | 0.931 | Highest recall, highest F1, highest mAP50    |
| 0.2       | 0.939     | 0.868  | 0.902    | 0.924 | Slight decrease in recall and F1             |
| 0.3-0.4   | 0.953     | 0.849  | 0.898    | 0.915 | Improved precision, further decreased recall |
| 0.5       | 0.957     | 0.849  | 0.900    | 0.917 | Slight improvement in F1 over 0.3-0.4        |
| 0.6       | 0.976     | 0.774  | 0.863    | 0.883 | Significant drop in recall and F1            |
| 0.7       | 1.000     | 0.717  | 0.835    | 0.858 | Perfect precision but lowest recall and F1   |
|           |           |        |          |       |                                              |
|           |           |        |          |       |                                              |
|           |           |        |          |       |                                              |

Model Tuning Result:

1. Recall: 0.878
2. Precision: 0.939
3. F1 Score: 0.908
4. MAP-50: 0.931
5. mAP50-95: 0.699
6. Model size efficiency
7. Inference speed:
   1. 55.73ms on Small 640x640 image
   2. 2.66 s/im on Huge Aerial Stitched Image with Sliding Windows
8. Real Case Detection: Found 654 Tree Out of 720 (Human Count)
