### 📚 Table of Contents

* [Dataset Description](#dataset-description)
* [Dataset Descriptions](#dataset-descriptions)
  * [Public Training Datasets](#public-training-datasets)
  * [Validation Datasets](#validation-datasets)
  * [Testing Datasets](#testing-datasets)
* [Data Structure and File Organization](#data-structure-and-file-organization)
  * [Reference Contents](#reference-contents)
* [Downloads](#downloads)
* [Examples](#examples)



# Datasets and Technical Details

## Dataset Description
<table>
  <tr>
    <td align="center">
      <img
        src="https://raw.githubusercontent.com/aislabunimi/IAS_IRIM_AIS_dataset/refs/heads/main/images/ias_lab.JPG"
        alt="IAS Lab Overview"
        height="250"
      /><br>
      <sub><strong>Figure 1.</strong> IAS Lab Overview</sub>
    </td>
    <td align="center">
      <img
        src="https://raw.githubusercontent.com/aislabunimi/IAS_IRIM_AIS_dataset/refs/heads/main/images/put_lab.jpg"
        alt="PUT Lab Overview"
        height="250"
      /><br>
      <sub><strong>Figure 2.</strong> PUT Lab Overview</sub>
    </td>
  </tr>
</table>



*Dataset are collected in two different environments (IAS and IRIM lab), one empty and one cluttered environment.*

The datasets consist of multiple recorded loops obtained in real-world indoor environment with low-cost quadrupeds equipped with low-end sensors.
The same setting of the robot has been used in both environments.

- **IAS LAB** trajectories are simpler and collected in an empty environment (Figure 1).
- **IRIM Lab** are more complex as they have been collected in a cluttered environment (Figure 2).

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

## Examples

We provide a reference SLAM pipeline which is described [in this repository](https://github.com/dyumanaditya/quad-stack). It contains a simulated navigation stack for the same robot setting that can be deployed in two virtual environments. Full description of the setup can be found [here](https://sites.google.com/view/low-cost-quadruped-slam).
![IASLabel](https://github.com/aislabunimi/IAS_IRIM_AIS_dataset/blob/main/images/legend_14font.png?raw=true)
*Example of IAS Lab Data*
![IAS_traj](https://github.com/aislabunimi/IAS_IRIM_AIS_dataset/blob/main/images/combined_traj_ias.png?raw=true)
*Example of IRIM Lab Data
![RIM_traj](https://github.com/aislabunimi/IAS_IRIM_AIS_dataset/blob/main/images/sb_irim_trajs.png?raw=true)

