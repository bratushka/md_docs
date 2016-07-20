# TensorFlow

[TOC]

---

### reverse_sequence

```py
tf.reverse_sequence(
    input,
    seq_lengths,
    seq_dim,
    batch_dim=None,
    name=None
)

##############################

import tensorflow as tf
import numpy as np


cat = tf.Variable(np.array([[1,2,3],[4,5,6]]))
init = tf.initialize_all_variables()

with tf.Session() as sess:
    height, width = map(lambda x: x.value, cat.get_shape())
    sess.run(init)
    crazy_cat = tf.reverse_sequence(
        cat,
        np.full((width,), height),
        seq_dim=0,
        batch_dim=1
    )
    print(sess.run(cat))
    print(sess.run(crazy_cat))

# [[1 2 3]
#  [4 5 6]]

# [[4 5 6]
#  [1 2 3]]

```
where:

1. **input** -- array, which is being reversed
1. **seq_lengths** -- vector of lengths of subsets of each vector inside the chosen dimention 
1. seq_dim -- the dimention, for each element (from 1 till len(seq_dim)) the reverse-operation will be applied
1. batch_dim -- the dimention, which is being reversed
