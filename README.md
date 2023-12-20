# 🚀 Object Detection Project

## 3. Techniques and Challenges

### 3.1 Objects

Objects can be categorized as:
- Small Objects: <32x32 Pixels
- Medium Objects: 32x32-96x96 Pixels
- Large Objects: >96x96 Pixels

Rare objects refer to items that are infrequently observed and have limited representation in datasets, making them less commonly encountered or documented.

### 3.2 Techniques to Improve Object Detection

#### 📊 Dataset Generation and Training

Create specialized datasets with a mix of variations, encompassing different weather conditions and, notably, night vision visuals. This approach ensures the model becomes adept at object detection across a diverse set of environmental scenarios, enhancing its overall robustness.

#### 🛠️ Architectural Modifications

Modifying the architecture involves adjusting the structure, layers, or parameters of the model. This could include adding more layers, changing activation functions, or incorporating attention mechanisms to improve object detection performance.

Right now, I am concentrating on creating datasets for the initial phase. This means we’re putting our efforts into making a diverse and comprehensive set of examples for the model to learn from.

### 3.3 Challenges

- 🌐 Data Acquisition
- 🌧️ Limited Datasets: Only limited to very good weather conditions
- 🌈 Need diversified samples in the dataset for better detection
- ⚖️ Class Imbalance

### 3.4 Overcoming Datasets Limitations

Getting datasets of rare objects is tough because of privacy issues, making them not widely accessible. Yet, there’s a silver lining – videos naturally show lots of different things, providing a chance to train models for real-life situations. But here’s the catch – annotating the data is a real pain, it takes a lot of time and effort. To tackle this, a smart idea is using trackers that can follow any object. This way, the datasets can annotate themselves. And to make sure we get a good mix of examples, we use special methods to pick diverse samples. It’s a cool way to handle the challenges when data is scarce and annotations are a headache.

### 3.5 Annotating Datasets with a Tracker

Drone objects in the first frame are localized in a drone video, and provided to the state-of-the-art single-object trackers. These trackers were then used to determine the object’s location in subsequent frames of any drone video.
<img width="837" alt="sent1" src="https://github.com/VijayRajIITP/Multi-Drone-Detection/assets/149241319/61e127a4-7fef-4136-a740-18fee5fe8d42">

# 3.6 Dataset Details

In this section, we present an overview of vision-based drone detection and tracking resources, including details about our generated dataset.

We utilized Fredrik’s Svanstrom et al. (2020) dataset, comprising real-time video clips captured in day and night scenarios. From this dataset, we carefully selected 13,801 annotated training samples and 3,451 annotated test samples for our experimental purposes. Additionally, we generated 459 effective samples using Custom web data, forming the Custom Web Drone Video Tracks (CWDVT) dataset.

## Experimental Setup

### Training Samples

| Dataset | No. of Training Samples |
|---------|--------------------------|
| ICPR    | 13,801                   |
| LaSOT   | 40,748                   |
| CLDT    | 1,708                    |

### Testing Samples

| Dataset | No. of Testing Samples |
|---------|------------------------|
| ICPR    | 3,451                  |
| DUT     | 2,208                  |
| CWDVT   | 419                    |

Both CWDVT and DUT datasets are exclusively reserved for testing, categorizing them as unseen datasets in our experiments. We compare synthetic drone samples generated from tracks in LaSOT (CLDTs) and Custom web videos (CWDVT) with samples from well-established datasets like ICPR and DUT. The diversity observed in the generated synthetic drone samples validates the effectiveness of our proposed approach.
# 🌐 Multi-Drone Tracking Dataset Details

## 3.6.1 Multi-Drone Tracking Dataset

Our multi-drone tracking dataset is a unique creation, merging ICPR drone data and LaSOT videos. Leveraging SiamMask Wang et al. (2019), a mask-based tracker, we manually annotated the first frame of single drone videos. Pseudo-labeled masks were then extracted from ICPR drone videos, and the center of each track in the video sequence was calculated.

### Dataset Generation Process

With the obtained pseudo-labeled masks and their corresponding center coordinates, we composited drones into the LaSOT background drone video using our proposed image composition method (see Figure 2). The composited drones were assigned relevant tracker IDs for labeling. This approach demonstrates the effectiveness of our framework, resulting in the creation of the Multi-Drone Tracking (MDT) dataset.

### Dataset Challenges

The MDT dataset encompasses various challenges, including:
- Drones of varying sizes, from small drones as tiny as 10x10 pixels
- Significant drift in drone movement from frame to frame, reflecting very fast drone motion
- A background cluttered with various elements

### MDT Dataset Parameters

| Parameter          | Value           |
|--------------------|-----------------|
| No. of Videos      | 20              |
| No. of Frames      | 21,818          |
| Min Width x Height | 10x10 pixels    |
| Max Width x Height | 310x252 pixels  |
| Backgrounds        | Night, Sky, Cloudy |

**Table 3.2: Details of the Multi-Drone Tracking (MDT) dataset.**

This dataset showcases the complexities of tracking multiple drones in various scenarios. The challenges posed by drones of different sizes and rapid movements, along with diverse backgrounds, make the MDT dataset an excellent testbed for evaluating the robustness of object tracking models. if you see carefully now we hyave two drones in Single Image
![fig7](https://github.com/VijayRajIITP/Multi-Drone-Detection/assets/149241319/be8f5674-d13e-4a3d-ba4d-cd7d6daa42f2)


# 🚀 Evaluation and Results

To assess the effectiveness of the generated datasets, we employed the YoloV8 object detection model, known for its speed and superior accuracy. Fine-tuning was conducted on the Yolov8n model pretrained on the COCO dataset using the Adam optimizer for 50 epochs, with a batch size of 16 and hyperparameters aligned with Yolov8n's foundational paper.

## Object Detection Precision Results with YOLO V8 Model

| Training Dataset        | ICPR | DUT (Unseen) | LDT  | CWDT | CMD  |
|-------------------------|------|--------------|------|------|------|
| ICPR                    | 0.954| 0.107        | 0.123| 0.505| 0.108|
| LDT                     | 0.148| 0.826        | 0.984| 0.911| 0.304|
| ICPR plus CLDT          | 0.964| 0.719        | 0.965| 0.901| 0.325|
| ICPR, CLDT, MDT         | 0.939| 0.629        | 0.952| 0.898| 0.99 |

**Table 4.1: Precision Results with YOLO V8 model**

## Multi-Object Tracking Performance with YOLO V8n Trained Model

| Detector           | MOTA (BT) | MOTA (SS) | MOTP (BT) | MOTP (SS) |
|--------------------|-----------|-----------|-----------|-----------|
| ICPR               | 0.07      | -1.23     | 0.721     | 0.709     |
| LaSOT              | 0.697     | 0.756     | 0.683     | 0.658     |
| ICPR and CLDT      | 0.6601    | 0.686     | 0.651     | 0.650     |
| ICPR, LaSOT, MDT   | 0.93      | 0.931     | 0.213     | 0.198     |

**Table 4.2: MOT Performance with YOLO V8n Trained Model.**

From the precision results in Table 4.1, it's evident that the model trained solely on ICPR real data struggles on unseen datasets such as LaSOT Drone data and DUT-Test data. However, when trained with the self-annotated LDT dataset, the model performs effectively on both seen and unseen datasets.

We also assessed state-of-the-art trackers Byte-Track (BT) Zhang et al. (2022) and Strong-SORT (SS) Du et al. (2023) on our Multi-Drone Tracking (MDT) dataset, showcasing their capabilities.

The detector trained with a combination of existing and generated synthetic datasets outperforms other datasets in tracker performance. This improvement is evident in Table 4.2, indicating the potential for further developments and highlighting the challenging nature of the generated datasets.



## 4. Contribution and Usage Guidelines (if applicable)

Include any guidelines for contributions, dataset usage, or instructions for running the code.
