### Keras
#### [Usage of callbacks](https://keras.io/callbacks/)
- Callback
Abstract base class used to build new callbacks.
- BaseLogger
accumulates epoch averages of metrics.
- TerminateOnNaN
terminates training when a NaN loss is encountered.
- ProgbarLoger
prints metrics to stdout
- History
records events into a History object.
- ModelCheckpoint
save the model after every epoch.
- EarlyStopping
stop training when a monitored quantity has stopped improving
- RemoteMonitor
used to stream events to a server
- LearningRateScheduler
args:
schedule: a function that takes an epoch index as input and current learning rate and returns a new learning rate as output.
verbos: 0:quiet, 1:update messages
- TensorBoard
- ReduceLROnPlateau
Reduce learning rate when a metric has stopped improving
- CSVLogger
streams epoch results to a .csv file
- LambdaCallback
creating simple, custom callbacks on-the-fly
