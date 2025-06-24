### 📚 Table of Contents

* [Dataset Description](#dataset-description)
* [Dataset Descriptions](#dataset-descriptions)
  * [Public Training Datasets](#public-training-datasets)
  * [Validation Datasets](#validation-datasets)
  * [Testing Datasets](#testing-datasets)
* [Data Structure and File Organization](#data-structure-and-file-organization)
  * [Reference Contents](#reference-contents)
* [Downloads](#downloads)
* [Examples and Teasers](#examples-and-teasers)

  * [Video Teasers](#video-teasers)

# Datasets and Technical Details

## Dataset Description
![Dataset overview](https://lh4.googleusercontent.com/b1hIjRfaMLGZJNZ62ZLkU3p7J_dA10PzSscAiQMnESTr9JpWI7GCiE4nSdMbaz36LeJ9oPfwruqZwfXWlwpopoRpHXj83EftUzoDb9tVSXiVj3p1byOTb-9oRbGnEyqXDqh3jaW0jYLHxEG_D7Eq4_5EpqWtNlNuBl92fLxFUARmDxDVeb79YA=w1280)
![Dataset overview](https://lh4.googleusercontent.com/rH5nzNJbMmamNz2kdl1Tx4UcJ0qSwq14_Zxpx0KsKX5SnlGhG3sdV9PV7dO5F7JnzPxo5_lKMASPw3slXC1xYSI0MW3tgqj8nzcAfw2gu0V78d4Y2gPP_k6kTwixG0dA6_8svcJI6MW8AnlQoGx3SfkRy5zr3oGvKvcjQgFelUc7LGmnEL5zGQ=w1280)
*Dataset are collected in two different environments (IAS and IRIM lab), one empty and one cluttered environment.*

The datasets consist of multiple recorded loops obtained in real-world indoor environment with low-cost quadrupeds equipped with low-end sensors. 
The dataset are recorded in two real-world environment. The the same setting of the robot has been used in both environments.
**IAS LAB** trajectories are simpler and collected in an empty environment (first figure).
**IRIM Lab** are more complex as they have been collected in a cluttered environment (second figure).

The robot used for testing is a [MAB robotics](https://www.mabrobotics.pl/) Silver Badger, which is a versatile quadruped robot with a flexible spine.

The dataset contain also millimeter-precision ground truth robot position obtained with an Optitrack recording device. 

In this setting SLAM is particularly challenging due to the fast and jerky motion of quadruped robots, combined with the complex nature of the environment and of the availability cheap low-end sensors to cope.

![silver](https://www.ias.informatik.tu-darmstadt.de/uploads/Research/Robots/sbg.png)

**Data contain both proprioceptive and exteroceptive sensor readings. SLAM should be performed using a low-end RBGD Camera (Intel RealSense D435i).**



---

## Dataset Descriptions

<span style="color:red">TODO: update here this, we can use a few good IAS Run for Training and the IRIM ones and the one where there is some loss of data for testing,</span>
### Public Training Datasets

* **shellby-0225-train-loop1** (451 m)
  Loop in an open field used for training, moving further from trees.

* **shellby-0225-train-lab**
  Short indoor recording from **CTU Computational Robotics Lab** for initial testing.
  Uses **Total Station** instead of GNSS.

### Validation Datasets

* **shellby-0225-validation-loop1** (313 m)
  Small loop primarily for testing submissions. The **forest remains in LiDAR range**.

### Testing Datasets


* **shellby-0225-test-loop1** (1892 m)
  Long loop with both field and forest. Includes a **30-second LiDAR outage** due to power loss.

* **shellby-0225-test-loop2** (667 m)
  Similar to the training loop but with **less smooth trajectory**.
  Evaluated using **Total Station** data. Basler camera slightly overexposed.

---

## Data Structure and File Organization
<span style="color:red">TODO: we can provide here a description of what there is in the bag. for the parameters we can also refer to the repository i think...</span>
```
data/
├── calibration
│   ├── extrinsics
│   │   ├── extrinsics.txt
│   │   ├── static_tf.launch
│   │   └── static_tf.urdf
│   └── instrinsics
│       ├── basler.yaml
│       ├── flir_boson.yaml
│       ├── plantpix1.yaml
│       └── plantpix2.yaml
├── train
│   ├── calibration
│   ├── shellby-0225-train-lab
│   │   ├── reference
│   │   │   ├── shellby-0225-train-lab.txt
│   │   │   └── shellby-0225-train-lab_noisy.txt
│   │   └── shellby-0225-train-lab.bag
│   └── shellby-0225-train-loop1
├── validation
│   ├── calibration
│   └── shellby-0225-validation-loop1
├── test/...
```

* `<sequence>.bag` → Raw sensory data.
* `reference/` → Folder containing reference trajectories.
* `calibration/extrinsics/` → Transformations between sensor frames.
* `calibration/instrinsics/` → Intrinsic parameters for cameras.
* `static_tf.launch` → ROS static transform launch file.
* `static_tf.urdf` → URDF for static transform definitions.

### Reference Contents

<span style="color:red">TODO: also here we should describe how reference are used, and how we fed reference to the library we used for making the plots.</span>

Each dataset contains a `reference/` subdirectory with:

* `*.txt`: Ground-truth trajectory (TUM or Total Station format).
* `*_noisy.txt`: Unfiltered GNSS trajectory (may be degraded by environment).

---

## Downloads

* [Training data - IAS LAB](https://unimi2013-my.sharepoint.com/:f:/g/personal/matteo_luperto_unimi_it/EixVFC1xQKZLn9FxnvQvoYMBC6WyZAWBMWDr-w_-KOT67A?e=b9FqsE) (\~25 GB download)

---

## Examples and Teasers

We provide a reference SLAM pipeline which is described [in this repository](https://github.com/dyumanaditya/quad-stack). It contains a simulated navigation stack for the same robot setting that can be deployed in two virtual environments. Full description of the setup can be found [here](https://sites.google.com/view/low-cost-quadruped-slam).
![IASLabel](https://lh5.googleusercontent.com/b59i84zvyObRSNG6i7yxO5GKjMXqGchbsgyLxGC2noLueo6nMp-AqXL6htj6xY-dSz3jXOcpIMJq_xX_47WCWRzxf_MMhToN47iUP6nEGvMUBzieacdwNt_RQatpf4G09MXcW_B05Ng6q33M5yviduxTf3YyUw7-N_5jx-NDNNtOmS3BCYYYNQ=w1280)
*Example of IAS Lab Data*
![IAS_traj](https://lh3.googleusercontent.com/eiFiPLa-4O6cVSHXcW0VCTzKlCT_O3Jhn2WSB7oSa_Gr7zXZnDXvLHhRj968JJ4cud2ZYmEYt6ptQrBdHttbcUY2M0KZ1A7Hh-NDucOzgJ0xrkZ2LzbODDEx90cweF4Z-hujFj2GWuI80O8YRe9BS_E4fIUqOQKwDbeMyDJTIRFxAT_ghd-qDA=w1280)
*Example of IRIM Lab Data
![RIM_traj](https://lh5.googleusercontent.com/IG9eylizrzGqkP_WqGijEQEagay-b9-9lcZSWkzs2i4eTVK8ikEj3JRMgYnh5nXUb4yXNUUzq7YXuA53mTpgw5e4QiFgu5M7-aTgv6irrjP_HhY9GWRKcpj-eyu69BIca7ObbjzUVSFieiUm1SKg1nKFATEhnKBOF-bNAXnA2HLPUgCJb08PUQ=w1280)

### Video Teasers

#### Train Dataset

[![Train teaser](https://img.youtube.com/vi/dQw4w9WgXcQ/0.jpg)](https://comrob-ds.fel.cvut.cz:9000/cb-slam/media/videos/shellby-0225-train-loop1-teaser.mp4)

#### Test Datasets

[![Test loop 1](https://img.youtube.com/vi/dQw4w9WgXcQ/0.jpg)](https://comrob-ds.fel.cvut.cz:9000/cb-slam/media/videos/shellby-0225-test-loop1-teaser.mp4)

[![Test loop 2](https://img.youtube.com/vi/dQw4w9WgXcQ/0.jpg)](https://comrob-ds.fel.cvut.cz:9000/cb-slam/media/videos/shellby-0225-test-loop2-teaser.mp4)
