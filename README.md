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


## 4. Contribution and Usage Guidelines (if applicable)

Include any guidelines for contributions, dataset usage, or instructions for running the code.
