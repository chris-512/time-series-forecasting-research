# Are Transformers Effective for Time Series Forecasting?
- URL: https://arxiv.org/pdf/2205.13504.pdf


FEDformer achieves competitive forecasting accuracy on ETTh1. This is because FEDformer employees classical time series analysis techniques such as frequency processing, which brings in time series inductive bias and benefits the ability of temporal feature extraction. In summary, these results reveal that existing complex Transformer-based LTSF solutions are not seemingly effective on the existing nine benchmarks while LSTF-Linear can be a powerful baseline.

In contrast, the performances of all TSF-Linear are significantly boosted with the increase of look-back window size. Thus, existing solutions tend to overfit temporal noises instead of extracting temporal information if given a longer sequence, and the input size 96 is exactly suitable for most Transformers. 

Are the self-attention scheme effective for LTSF?
Finally we simplify the model to one linear layer. Surprisingly, the performance of Informer grows with the gradual simplification, indicating the unnecessary of the self-attention scheme and other complex modules at least for existing LTSF benchmarks. 

Can existing LTSF-Transformers preserve temporal order well?
Self-attention is inherently permutation invariant, i.e., regardless of the order. However, in time-series forecasting, the sequence order often plays a crucial role. 

Interestingly,  compared with the original setting on the Exchange Rate, the performance of all Transformer-based methods does not fluctuate even when the input sequence is randomly shuffled. By contrary, the performance of LTSF-Linear is damaged significantly. These indicate that LTSF-Transformers with different temporal relations and are prone to overfit on noisy financial data, while the LTSF-Linear can model the order naturally and avoid overfitting with fewer parameters. 
Overall, the average drops of LTSF-Linear are larger than Transformer-based methods for all cases, indicating the existing Transformers do not preserve temporal order well.

→ 모델을 망가뜨리는 방법들을 실험해봄으로써 모델의 성질을 파악해볼 수 있다.

The forecasting errors of Informer largely increase without positional embeddings (wo/Pos). Without timestamp embeddings (wo/Temp.) will gradually damage the performance of Informer as the forecasting lengths increase. Since Informer uses a single time step for each token, it is necessary to introduce temporal information in tokens.

Rather than using a single time step in each token, FEDformer and Autoformer input a sequence of timestamps to embed the temporal information. Hence, they can achieve comparable or even better performance without fixed positional embeddings. Instead, thanks to the frequency-enhanced module proposed in FEDformer to introduce temporal inductive bias, it suffers less from removing any positional/timestamp embeddings.

Is training data size a limiting factor for existing LTSF-Transformers?
Some may argue that the poor performance of Transformer-based solutions is due to the small sizes of the benchmark datasets. Unexpectedly, the prediction errors with reduced training data are lower in most cases. This might because the whole-year data maintains more clear temporal features than a longer but incomplete data size. While we cannot conclude that we should use less data for training, it demonstrates that the training data scale is not the limiting reason for the performances of Autoformer and FEDformer. 

RNN-based TSF methods belong to IMS forecasting techniques. Depending on whether the decoder is implemented in an autoregressive manner, there are either IMS or DMS forecasting techniques for CNN-based TSF methods.

RNNs for Time Series Forecasting
https://arxiv.org/pdf/1901.00069.pdf
