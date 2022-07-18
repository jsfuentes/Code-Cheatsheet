# MatplotLib

## Simplest 

```python
import matplotlib.pyplot as plt
plt.plot([1,4,9,16]) # y with x = [0, 1,2,3]
plt.plot([1,2,3,4], [1,4,9,16], 'ro') # x y color
plt.axis([0, 6, 0, 20]) #xmin xmax ymin ymax
plt.show()
```

## Simple Example

```python
import matplotlib.pyplot as plt
import numpy as np

# Data for plotting
t = np.arange(0.0, 2.0, 0.01)
s = 1 + np.sin(2 * np.pi * t)

# Note that using plt.subplots below is equivalent to using
# fig = plt.figure() and then ax = fig.add_subplot(111)
fig, ax = plt.subplots()
ax.plot(t, s)

ax.set(xlabel='time (s)', ylabel='voltage (mV)',
       title='About as simple as it gets, folks')
ax.grid()

fig.savefig("test.png")
plt.show()
```

