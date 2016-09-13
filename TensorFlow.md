# TensorFlow

[TOC]

---

### constant

```py
tf.constant(
    value,
    dtype=None,
    shape=None,
    name='Const'
)
# returnes a constant Tensor

tf.constant(2)
# <tf.Tensor 'Const_1:0' shape=() dtype=int32>

tf.constant(2, dtype=tf.float32)
# <tf.Tensor 'Const_2:0' shape=() dtype=float32>

tf.constant(2, dtype=tf.float32, shape=[1, 3])
# <tf.Tensor 'Const_3:0' shape=(1, 3) dtype=float32>
sess.run(tf.constant(2, shape=[1, 3])) == np.full([1, 3], 2)
# array([[ True,  True,  True]], dtype=bool)
```

---

### Tensor generators

These generators return constant tensors. To make them modifiable - wrep them into tf.Variable

```py
tf.zeros(
    shape,
    dtype=tf.float32,
    name=None
)
# tf.zeros([3, 4], int32) ==> [[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]

tf.zeros_like(
    tensor,
    dtype=None,
    name=None
)

# `tensor` is [[1, 2, 3], [4, 5, 6]]
# tf.zeros_like(tensor) ==> [[0, 0, 0], [0, 0, 0]]

tf.ones()
tf.ones_like()
# same logic, as for `zeros`

tf.fill(dims, value, name=None)
# fill([2, 3], 9) ==> [[9, 9, 9], [9, 9, 9]]
```

---

### Sequences

```py
tf.linspace(
    start, 
    stop, 
    num, 
    name=None
)
# tf.linspace(10.0, 12.0, 3, name="linspace") => [ 10.0  11.0  12.0]

tf.range(
    start, 
    limit=None, 
    delta=1, 
    name='range'
)
# tf.range(start, limit, delta) ==> [3, 6, 9, 12, 15]
# tf.range(limit) ==> [0, 1, 2, 3, 4]

```

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
1. **seq_lengths** -- vector of lengths of subsets of each vector inside the chosen dimension 
1. **seq_dim** -- the dimension, which is being reversed
1. **batch_dim** -- the dimension, for each element (from 1 till len(seq_dim)) the reverse-operation will be applied

Example:
**input** - change the array "input" (**x**, **y**, **z** axis)
**seq_lengths** - vector of int values, specifying how many items in each element of **seq_dim** dimension will be reversed
**seq_dim** - revert **seq_lengths[i]** elements in each **i** item of this dimension (choosing between those, which are not in **batch_dim**)
**batch_dim** - iterate through this dimension (for example - **z**)

---

### TensorBoard

To run **TensorBoard** you need to run `tensorboard --logdir=tensor_log_dir` in command line

```py
# Log all the values, which you want to see on TensorBoard
for value in [x, w, y, y_, loss]:
    tf.scalar_summary(value.op.name, value)

# Collect the under one name
summaries = tf.merge_all_summaries()

# Define the summary writer
summary_writer = tf.train.SummaryWriter('tensor_log_dir', sess.graph)

# Write information every time you need (for example in the training loop)
summary_writer.add_summary(sess.run(summaries), i)

# Everything is on the TensorBoard, enjoy
```