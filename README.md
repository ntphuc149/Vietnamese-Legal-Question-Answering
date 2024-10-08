# Vietnamese Legal Question Answering: An Experimental Study [paper]

This paper investigates the legal question-answering (QA) task in Vietnamese. Different from prior studies that only report results on the task of machine reading comprehension (MRC), we compare the strong QA models in two scenarios: MRC (span extraction) and answer generation (AG) (text generation). To do that, we first created a new dataset, namely ViBidLQA, using the bidding law. The dataset is synthesized by using a large language model (LLM) and corrected by two domain experts. After that, we train a set of robust MRC and AG models on the ViBidLQA dataset and predict on both ALQAC and the test set of ViBidLQA. Experimental results show that for the MRC scenario, vi-mrc-large achieves the best scores while for the AG scenario, ViT5 obtains good performance. The results also indicate that the
new ViBidLQA dataset contributes to improving the performance of MRC models for domain adaptation on ALQAC

<figure>
  <p align="center">
    <img src="images/What is QA.png" alt="Fig.1">
  </p>
  <p align="center"><normal>Fig.1: An example of Question Answering</strong></p>
</figure>

## Problem Formulation
### 1. Machine Reading Comprehension (MRC)

QA is formulated as an MRC problem. Given a context $C = {w_1, ..., w_n}$ and question $Q$, the goal is to determine start $(s)$ and end $(e)$ token of the answer $A$, which form a span within $C$. From the start token $s$ and end token $e$, the start position and end position are obtained.
MRC models transform $C$ and $Q$ into contextual representations $H_C$ and $H_Q$, apply attention:

$$
A = \text{softmax}(H_Q \cdot H_C^T)
$$

Then the model predicts answer span positions as:

<div align="center">

![Equation](https://latex.codecogs.com/gif.latex?(s^*,%20e^*)%20=%20\arg\max_{(s,%20e)}%20\text{logits}_{\text{start}}(s)%20\cdot%20\text{logits}_{\text{end}}(e))

</div>

### 2. Answer Generation (AG)

Answer generation models produce a suitable answer $A$ by extracting tokens from the context $C$.

The training process uses the contextual vector $\boldsymbol{h}$ from the encoder to generate output tokens $y_t$ by the softmax function.

<div align="center">

![Equation](https://latex.codecogs.com/gif.latex?p_t%20=%20\text{softmax}(f(\boldsymbol{h},%20y_{<t},%20\theta)))

</div>

where $\theta$ is the weight matrix, the objective is to minimize the negative likelihood of the conditional probability between the predicted outputs and the gold answer $A$.

<div align="center">

![Equation](https://latex.codecogs.com/gif.latex?\mathcal{L}%20=%20-\frac{1}{k}%20\sum_{t=1}^{k}%20\log%20\left(%20p_t%20\mid%20A_{<k},%20\theta%20\right))

</div>

where $k$ is the number of tokens in $A$, for inference, given an input context with the question, the trained AG models generate the corresponding question.

For more details, access the repo: https://github.com/Shaun-le/ViQAG. In this repo, I'll dive deeply into the Machine Reading Comprehension (MRC) approach.

## Installation Guide

### 1.1. Clone the repository:

```python
git clone https://github.com/ntphuc149/ViLQA.git
cd ViLQA
```

### 1.2. Create a virtual environment (recommended):

```python
python3 -m venv venv
source venv/bin/activate
```

### 1.3. Install the dependencies:

```python
pip install -r requirements.txt
```

## Usage Instructions
### 2.1. Configure the project:

Update the parameters in config.py to suit your dataset and requirements.

### 2.2. Fine-tune and evaluate the model:

Run the following command to start fine-tuning and evaluate the model:

```python
python train.py
```

## Contribution
We welcome contributions to this project. Please create a pull request or open an issue to discuss your ideas for improvement.

## ViBidLawQA
We introduce a demo application system ViBidLawQA at [here](https://ntphuc149-vibidlawqa.hf.space/). The brief introduction of the system was also shown in a video ↓↓↓
<p align="center">
  <a href="https://youtu.be/wfmGcs50sWI" onclick="window.open(this.href); return false;"><img src="https://img.youtube.com/vi/wfmGcs50sWI/0.jpg" alt="Alt Text" /></a>
</p>

## License
This project is licensed under the MIT License. See the LICENSE file for details.

## Access our new dataset ViBidLQA
To access our data, please take the survey at: https://forms.gle/Ti4d31xKoa78Hud69

## Citation
Coming soon
