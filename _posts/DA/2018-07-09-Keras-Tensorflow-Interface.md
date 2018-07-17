---
layout: post
title: A complete guide to using Keras as part of a TensorFlow workflow
category: DA
tags: DA
keywords:
description:
---

> Keras(tensorflow backend), make life easier.

# Using Keras models with TensorFlow

## Exporting a model with TensorFlow-serving

Any Keras model can be exported with TensorFlow-serving(as long as it only has one input and one output, which is a limitation of TF-serving).

If your graph makes use of the Keras learning phase(different behavior at training time and test time), the very first thing to do before exporting your model is to hard-code the value of the learning phase(as 0, presumably, i.e. test mode) into your graph.

1. Registering a constant learning phase with the Keras backend.
2. Re-building your model afterwards.

```
from keras import backend as K
K.set_learning_phase(0)  # all new operations will be in test mode from now on

# serialize the model and get its weights, for quick re-building
config = previous_model.get_config()
weights = previous_model.get_weights()

# re-build a model where the learning phase is now hard-coded to 0
from keras.models import model_from_config
new_model = model_from_config(config)
new_model.set_weights(weights)
```

We can not use TensorFlow-serving to export the model, following the instructions found in [the official tutorial](https://github.com/tensorflow/serving/blob/master/tensorflow_serving/g3doc/serving_basic.md)

```
from tensorflow_serving.session_bundle import exporter

export_path = ... # where to save the exported graph
export_version = ... # version number (integer)

saver = tf.train.Saver(sharded=True)
model_exporter = exporter.Exporter(saver)
signature = exporter.classification_signature(input_tensor=model.input,
                                              scores_tensor=model.output)
model_exporter.init(sess.graph.as_graph_def(),
                    default_graph_signature=signature)
model_exporter.export(export_path, tf.constant(export_version), sess)
```
