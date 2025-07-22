
## ❓ Frequently Asked Questions

This section provides answers to common questions about the modeling strategy, data sources, and forecasting pipeline used in our Bhutan flood risk prediction project. It is intended to help both new team members and external collaborators quickly understand key concepts, design decisions, and system capabilities.


Q: What exactly does it mean to train a model? Why is training necessary?
A: Training a model means teaching it to learn patterns and relationships between input features (e.g., rainfall, temperature) and the target outcome (e.g., flood risk). During training, the model learns optimal parameters and how to process or transform features to improve accuracy. Without this training phase, model predictions would be essentially random and unreliable.

Q: Do you use actual flood events as training labels?
A: No, we use surface runoff from ERA5 as a proxy for flood events in model training. This is a commonly used approach in flood prediction research, especially when ground-truth flood event data are limited or unavailable. If reliable flood event records become available, they can be incorporated to fine-tune and validate the model further.

Q: What variables do you use as predictive features (X) for model training?
A: We use selected meteorological variables from ERA5—such as rainfall, temperature, and humidity—as predictive features. In addition, we can incorporate variables that are specifically relevant to Glacial Lake Outburst Floods (GLOFs), including lake location, lake size and growth over time, proximity to settlements or rivers, and dam type (e.g., moraine or ice). The model training process will learn how to best integrate and weigh these diverse features to predict flood risk effectively.

Q: How do you evaluate whether the model works well?
A: We split the dataset into training and validation subsets. The model is trained on one part and tested on another to evaluate its predictive accuracy. This validation step helps us understand the model’s generalizability and guides how much we can trust the predictions when deployed. Performance metrics will also be reported to end users.

Q: Why are you using GraphCast instead of other weather forecasts or building your own forecast system?
A: GraphCast (https://deepmind.google/discover/blog/graphcast-ai-model-for-faster-and-more-accurate-global-weather-forecasting/) outperforms traditional ECMWF forecasts on approximately 90% of key variables and generates predictions in under a minute. It's also open-source, making it ideal for integration and deployment within our system.

Q: What is the temporal resolution of the model?
A: The model operates on 6-hour intervals, aligned with the temporal resolution of GraphCast output.

Q: How far into the future can the model predict?
A: The model can forecast up to 10 days ahead, matching GraphCast’s prediction horizon.

