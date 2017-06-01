# TensorFlow Mechanics

## 1.Inputs and Placeholders

`tf.placeholder`: define the shape of the **inputs or label**, including the `batch_size`
```
images_placeholder = tf.placeholder(tf.float32, shape=(batch_size, mnist.IMAGE_PIXELS))
labels_placeholder = tf.placeholder(tf.int32, shape=(batch_size))
```

In training loop, the full image and label datasets are sliced to fit the `batch_size`, and then passed into the sess.run() function using the `feed_dict` parameter.

## 2.Bulid the Graph
- `inference()` running the network forward, like `Y = f(...f(WX))`

    Each layer can be created beneath a unique `tf.name_scope` that acts as a prefix to the items created within that scope
    ```
    with tf.name_scope('hidden1') # first hidden layer  # the name of weights variable will be "hidden1/weights" 
      weights = tf.Variable(tf.truncated_normal([IMAGE_PIXELS, hidden1_units],
                        stddev=1.0 / math.sqrt(float(IMAGE_PIXELS))), name='weights')
      biases = tf.Variable(tf.zeros([hidden1_units]), name='biases')
    ..//
    ..//
    
    hidden1 = tf.nn.relu(tf.matmul(images, weights) + biases)
    ..//
    hidden2 = tf.nn.relu(tf.matmul(hidden1, weights) + biases)
    ..//
    logits = tf.matmul(hidden2, weights) + biases
    
   ```

- `loss()` adds the inference graph the ops required to generate loss

    We can construct our own loss function, or using its built-in loss function like `tf.nn.sparse_softmax_cross_entropy_with_logits`
    ```
    labels = tf.to_int64(labels)
    cross_entropy = tf.nn.sparse_softmax_cross_entropy_with_logits(labels=labels, logits=logits, name='xentropy')
    loss = tf.reduce_mean(cross_entropy, name='xentropy_mean')
   ```
    `tf.summary.scalar('loss', loss)` and `tf.summary.FileWriter(..)` to print the summary or loss value
    
- `training()` add the loss graph the ops required to compute and apply gradients 
    First, choose an `optimizer`, like ` tf.train.GradientDescentOptimizer`
    `optimizer = tf.train.GradientDescentOptimizer(learning_rate)`
    `train_op = optimizer.minimize(loss, [some other parameter])`
    
    we need to run training repeatedly. (Basically, we put above three function into the same python file)

## 3.Train the Model

    We'd better start a new file to control the training procedures.
    **Session**: `tf.Session()` is created for running the graph
    Alternately, a Session may be generated into a `with` block for scoping:
    `with tf.Session() as sess:`
    
    After creating the session, all of the `tf.Variable()` instances are initialized by calling:
    `sess.run(tf.global_variables_initializer)`
    
    `tf.Session.run(ops)` will run the complete subset of the graph that corresponds to the `ops`(parameter)
    
    **Training loop:** repeatedly run the `train_op` which is built in the above. For example:
    ```
    for step in xrange(FLAGS.max_steps):  # in each step, return the 'train_op' and 'loss' which can be printed
      feed_dict = fill_feed_dict(data_sets.train, images_placeholder, labels_placeholder)
      _, loss_value = sess.run([train_op, loss], feed_dict=feed_dict)

    ```
    
    
## 4.Visualize the status - [TensorBoard](https://www.tensorflow.org/get_started/summaries_and_tensorboard)
    
    summary = tf.summary.merge_all() // all the summaries are collected into a single Tensor during **graph building**
    
    And after session is created, a `tf.summary.FileWriter` may be instantiated to write the events files, which contain both the graph itself and the values of the summaries.
    `summary_writer = tf.summary.FileWriter(FLAGS.train_dir, sess.graph)`
    
    In case of being updated each time, output passes to the writer's `add_summary()` function.
    ```
    summary_str = sess.run(summary, feed_dict=feed_dict)
    summary_writer.add_summary(summary_str, step)
    ```
    
    ___
    
    Save a Checkpoint: `saver = tf.train.Saver()` will write a checkpoint file to the training directory with the current values of all the **trainable variables**.
    
    `saver.save(sess, FLAGS.train_dir, global_step=step)` // save the parameter
    `saver.restore(sess, FLAGS.train_dir)`  // reuse the stored parameter
    
    
 ## 5. Evaluate the Graph
     Basically, we recommend to start a new file to write **Evaluate Model**
     Before entering the training loop, we should build evaluate graph.
     
 

     
    
    
