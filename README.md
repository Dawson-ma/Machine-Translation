# Machine Translation (Sequence to Sequence)

This project focuses on English to Chinese machine translation, achieving a notable BLEU (bilingual evaluation understudy) score of **29.36**.

## Data Preprocessing

### Data Cleaning and Normalization

The sentences underwent cleaning and normalization, removing excessively long or short sentences and normalizing punctuation. Subsequently, tokenization was performed. The [training](https://drive.google.com/file/d/1-y2Y9Mh3PjAAc4rJA-DS6IxDGgtZQawY/view?usp=sharing), [test](https://drive.google.com/file/d/1xwh5Wd2jJiDu9y6VGHndYrElc0eomMQB/view?usp=sharing), and [monolingual](https://drive.google.com/file/d/1nRoFkwf97rd-iagx3Pu9FZKFZVsv3yKY/view?usp=sharing) datasets were stored.

### Subword Units

To address out-of-vocabulary issues, subword units were employed:
- Utilization of the 'sentencepiece' package
- Selection of either 'unigram' or 'byte-pair encoding (BPE)' algorithm

The data was binarized after subword tokenization.

## Model Architecture

- **Encoder**: Employed either a RNN or Transformer Encoder.
- **Decoder**: Utilized either a RNN or Transformer Decoder.
- **Attention**:
  - Addressing long input sequences, attention mechanisms provided the Decoder with more comprehensive information.
  - Correlation between **Decoder embeddings** of the current timestep and **Encoder outputs** was determined, followed by weighted summation of the Encoder outputs as input to the **Decoder** RNN.
  - Common attention implementations utilized neural networks/dot product for correlation determination between **query** (decoder embeddings) and **key** (Encoder outputs). This was followed by **softmax** to obtain a distribution, with subsequent **weighted sum** of **values** (Encoder outputs) based on this distribution.

## Training Techniques

- **Label Smoothing Regularization**: Reserved probability for incorrect labels to prevent overfitting.
- **Learning Rate Scheduling**: Linearly increased learning rate, followed by decay via inverse square root of steps to stabilize transformer training in early stages.
- **Back-Translation**: Leveraged monolingual data for synthetic translation data:
  1. Trained a translation system in the opposite direction.
  2. Collected monolingual data on the target side and applied machine translation.
  3. Utilized translated and original monolingual data as additional parallel data for training stronger translation systems.

## Dataset

The Ted2020 dataset served as the primary data source for this project:
- Raw: 398,066 sentences
- Processed: 393,980 sentences

For detailed implementation and usage instructions, please refer to the provided [code](https://github.com/Dawson-ma/Machine-Translation/blob/main/Machine_translation.ipynb).
