# plot_data() - Line-by-Line Breakdown with Data Examples

## Setup: Sample Data
```python
# Assume we have this dataset:
X_sample = torch.tensor([
    [1.0],   # sample 0
    [2.5],   # sample 1
    [5.0],   # sample 2
    [7.5],   # sample 3
    [3.0]    # sample 4
])  # shape: (5, 1)

Y_sample = torch.tensor([0, 0, 1, 2, 0])  # shape: (5,)

data_set = (X_sample, Y_sample)
```

---

## Line-by-Line Execution

### **Line 1: Function Definition**
```python
def plot_data(data_set, model=None, n=1, color=False):
```
**What it does:**
- `data_set`: tuple of (X, Y) tensors
- `model`: trained neural network (optional)
- `n`: not used in this function
- `color`: whether to shade decision regions

---

### **Line 2: Extract Features**
```python
X = data_set[:][0]
```

**What it does:**
- `data_set[:]` returns the tuple `(X_sample, Y_sample)`
- `[0]` gets the first element

**After execution:**
```
X = torch.tensor([
    [1.0],
    [2.5],
    [5.0],
    [7.5],
    [3.0]
])  # shape: (5, 1)
```

---

### **Line 3: Extract Labels**
```python
Y = data_set[:][1]
```

**What it does:**
- `data_set[:]` returns the tuple
- `[1]` gets the second element

**After execution:**
```
Y = torch.tensor([0, 0, 1, 2, 0])  # shape: (5,)
```

---

### **Line 4: Comment** ✓ (No execution)

---

### **Line 5: Plot Class 0 (Blue Dots)**
```python
plt.plot(X[Y == 0, 0].numpy(), Y[Y == 0].numpy(), 'bo', label='y = 0')
```

**Breaking it down:**

**Step 1: `Y == 0`**
```
Y == 0 produces:
torch.tensor([True, True, False, False, True])
# samples 0, 1, 4 belong to class 0
```

**Step 2: `X[Y == 0, 0]`**
```
X[Y == 0] selects rows where Y == 0:
torch.tensor([
    [1.0],
    [2.5],
    [3.0]
])  # shape: (3, 1)

X[Y == 0, 0] selects column 0 (the single feature):
torch.tensor([1.0, 2.5, 3.0])  # shape: (3,)
```

**Step 3: `Y[Y == 0]`**
```
Y[Y == 0] selects labels where Y == 0:
torch.tensor([0, 0, 0])  # shape: (3,)
```

**Step 4: `.numpy()`**
```
Converts tensors to numpy arrays:
X_vals = array([1.0, 2.5, 3.0])
Y_vals = array([0, 0, 0])
```

**Step 5: `plt.plot(..., 'bo', label='y = 0')`**
```
'bo' = blue circle markers (no line)
Plots points at:
  (1.0, 0)
  (2.5, 0)
  (3.0, 0)
```

**Visual Result:**
```
y-axis
2 |
1 |
0 | ●      ●    ●     <- blue dots at y=0
  |___|____|____|___
    0   2   4   6   x-axis
    (1.0)(2.5)(3.0)
```

---

### **Line 6: Plot Class 1 (Red Dots)**
```python
plt.plot(X[Y == 1, 0].numpy(), Y[Y == 1].numpy(), 'ro', label='y = 1')
```

**Same logic as Line 5:**

**Step 1: `Y == 1`**
```
torch.tensor([False, False, True, False, False])
# only sample 2 belongs to class 1
```

**Step 2: `X[Y == 1, 0]`**
```
torch.tensor([5.0])  # shape: (1,)
```

**Step 3: `Y[Y == 1]`**
```
torch.tensor([1])  # shape: (1,)
```

**Step 4: `.numpy()`**
```
X_vals = array([5.0])
Y_vals = array([1])
```

**Step 5: Plot**
```
Plots point at (5.0, 1)
'ro' = red circle

y-axis
2 |
1 |              ●     <- red dot at y=1
0 | ●      ●    ●
  |___|____|____|___
    0   2   4   6   x-axis
                (5.0)
```

---

### **Line 7: Plot Class 2 (Green Dots)**
```python
plt.plot(X[Y == 2, 0].numpy(), Y[Y == 2].numpy(), 'go', label='y = 2')
```

**Same logic:**

**Step 1: `Y == 2`**
```
torch.tensor([False, False, False, True, False])
# only sample 3 belongs to class 2
```

**Step 2-5: Extract and Plot**
```
X_vals = array([7.5])
Y_vals = array([2])
Plots point at (7.5, 2)
'go' = green circle

y-axis
2 |                  ●   <- green dot at y=2
1 |              ●
0 | ●      ●    ●
  |___|____|____|___
    0   2   4   6   8  x-axis
```

---

### **Line 8: Set Y-Axis Limits**
```python
plt.ylim((-0.1, 2.5))
```

**What it does:**
- Sets y-axis to show from -0.1 to 2.5
- Leaves space above class 2 (at y=2)

**Visual Result:**
```
y-axis
2.5 |__________ <- upper limit
2   |        ●
1   |      ●
0   |●  ●  ●
-0.1|__________ <- lower limit
```

---

### **Line 9: Add Legend**
```python
plt.legend()
```

**What it does:**
- Displays a box showing:
  ```
  ● y = 0
  ● y = 1
  ● y = 2
  ```

---

### **Line 10: Check if Model Exists**
```python
if model is not None:
```

**What it does:**
- Only runs the next block if you passed a trained model
- If `model=None`, skips everything inside and goes to `plt.show()`

---

## [IF MODEL IS PROVIDED]

### **Line 11: Extract Weights**
```python
weights = model.state_dict()['0.weight']
```

**What it does:**
- `model.state_dict()` returns all trained parameters as a dict
- `['0.weight']` gets the weight matrix from layer 0

**Assume our model learned:**
```
weights = torch.tensor([
    [0.5],    # weight for class 0
    [-0.2],   # weight for class 1
    [0.1]     # weight for class 2
])  # shape: (3, 1)
```

**Why (3, 1)?**
- 3 output classes
- 1 input feature

---

### **Line 12: Extract Biases**
```python
biases = model.state_dict()['0.bias']
```

**What it does:**
- Gets the bias vector from the same layer

**Assume our model learned:**
```
biases = torch.tensor([1.0, 2.0, 0.5])  # shape: (3,)
```

**What it means:**
- Class 0 bias: 1.0
- Class 1 bias: 2.0
- Class 2 bias: 0.5

---

### **Line 13: Setup Colors**
```python
colors = ['b', 'r', 'g']
```

**What it does:**
- 'b' = blue, 'r' = red, 'g' = green
- One color per class

---

### **Line 14: Setup Labels**
```python
labels = ['yhat=0', 'yhat=1', 'yhat=2']
```

**What it does:**
- Labels for the legend
- 'yhat' = predicted y (model's output)

---

### **Line 15: Loop Over Classes**
```python
for i, (w, b) in enumerate(zip(weights, biases)):
```

**What it does:**
- `zip(weights, biases)` pairs up weights with biases
- `enumerate()` adds a counter

**First iteration (i=0):**
```
i = 0
w = 0.5   (weight for class 0)
b = 1.0   (bias for class 0)
```

**Second iteration (i=1):**
```
i = 1
w = -0.2  (weight for class 1)
b = 2.0   (bias for class 1)
```

**Third iteration (i=2):**
```
i = 2
w = 0.1   (weight for class 2)
b = 0.5   (bias for class 2)
```

---

### **Line 16: Calculate Logits**
```python
y_logit = (w * X + b).numpy().flatten()
```

**ITERATION 1 (Class 0: w=0.5, b=1.0):**
```
w * X =
0.5 * torch.tensor([[1.0], [2.5], [5.0], [7.5], [3.0]])
= torch.tensor([[0.5], [1.25], [2.5], [3.75], [1.5]])

w * X + b =
[[0.5], [1.25], [2.5], [3.75], [1.5]] + 1.0
= [[1.5], [2.25], [3.5], [4.75], [2.5]]

.flatten() removes the column dimension:
torch.tensor([1.5, 2.25, 3.5, 4.75, 2.5])

.numpy() converts to array:
array([1.5, 2.25, 3.5, 4.75, 2.5])
```

**ITERATION 2 (Class 1: w=-0.2, b=2.0):**
```
w * X + b =
[-0.2, -0.5, -1.0, -1.5, -0.6] + 2.0
= [1.8, 1.5, 1.0, 0.5, 1.4]
```

**ITERATION 3 (Class 2: w=0.1, b=0.5):**
```
w * X + b =
[0.1, 0.25, 0.5, 0.75, 0.3] + 0.5
= [0.6, 0.75, 1.0, 1.25, 0.8]
```

---

### **Line 17: Plot the Logit Line**
```python
plt.plot(X.numpy().flatten(), y_logit, colors[i], label=labels[i])
```

**ITERATION 1 (i=0, color='b', label='yhat=0'):**
```
x_vals = X.numpy().flatten() = [1.0, 2.5, 5.0, 7.5, 3.0]
y_vals = [1.5, 2.25, 3.5, 4.75, 2.5]

Plots line connecting:
  (1.0, 1.5)
  (2.5, 2.25)
  (5.0, 3.5)
  (7.5, 4.75)
  (3.0, 2.5)
```

**ITERATION 2 (i=1, color='r', label='yhat=1'):**
```
Plots line for class 1:
  (1.0, 1.8)
  (2.5, 1.5)
  (5.0, 1.0)
  (7.5, 0.5)
  (3.0, 1.4)
```

**ITERATION 3 (i=2, color='g', label='yhat=2'):**
```
Plots line for class 2:
  (1.0, 0.6)
  (2.5, 0.75)
  (5.0, 1.0)
  (7.5, 1.25)
  (3.0, 0.8)
```

**Visual Result (all 3 lines + dots):**
```
y-axis
4.5 |        ●
4.0 |       /● <- blue line rising
3.5 |      /  ●
3.0 |    ●/
2.5 |   /●        ← y=2 ●
2.0 |  / ●●●●     ← y=1 ●
1.5 | ●            ← y=0 ●●●
1.0 |             (logits intersect here)
0.5 |
0.0 |___|____|____|_____
    0   2   4   6   8   x-axis
```

---

### **Line 18: Check if Color Shading Enabled**
```python
if color == True:
```

**What it does:**
- Only shade regions if `color=True`
- Otherwise skip to `plt.show()`

---

## [IF COLOR = TRUE]

### **Line 19: Calculate All Logits**
```python
logits = X @ weights.T + biases
```

**Breaking it down:**

**Step 1: `weights.T` (transpose)**
```
weights = [[0.5], [-0.2], [0.1]]   shape: (3, 1)
weights.T = [[0.5, -0.2, 0.1]]     shape: (1, 3)
```

**Step 2: `X @ weights.T`**
```
Matrix multiplication (X is 5x1, weights.T is 1x3):
X @ weights.T =

[[1.0], [2.5], [5.0], [7.5], [3.0]] @ [[0.5, -0.2, 0.1]]

= [[1.0*0.5,    1.0*-0.2,   1.0*0.1],
   [2.5*0.5,    2.5*-0.2,   2.5*0.1],
   [5.0*0.5,    5.0*-0.2,   5.0*0.1],
   [7.5*0.5,    7.5*-0.2,   7.5*0.1],
   [3.0*0.5,    3.0*-0.2,   3.0*0.1]]

= [[0.5,   -0.2,   0.1],
   [1.25,  -0.5,   0.25],
   [2.5,   -1.0,   0.5],
   [3.75,  -1.5,   0.75],
   [1.5,   -0.6,   0.3]]

shape: (5, 3) — one logit per class for each sample
```

**Step 3: `+ biases`**
```
biases = [1.0, 2.0, 0.5]

logits = [[0.5,   -0.2,   0.1],      + [1.0, 2.0, 0.5]
          [1.25,  -0.5,   0.25],
          [2.5,   -1.0,   0.5],
          [3.75,  -1.5,   0.75],
          [1.5,   -0.6,   0.3]]

       = [[1.5,   1.8,   0.6],
          [2.25,  1.5,   0.75],
          [3.5,   1.0,   1.0],
          [4.75,  0.5,   1.25],
          [2.5,   1.4,   0.8]]

shape: (5, 3)
```

**Interpretation:**
- Row 0: Sample 1.0 → logits [1.5, 1.8, 0.6]
  - Class 0: 1.5
  - Class 1: 1.8 ← highest
  - Class 2: 0.6

---

### **Line 20: Find Predicted Class**
```python
pred_class = logits.argmax(dim=1).numpy()
```

**What it does:**
- `argmax(dim=1)` finds the class with highest logit for each sample

**For each row, which class wins?**
```
Row 0: [1.5,   1.8,   0.6]  → argmax = 1 (class 1 has 1.8)
Row 1: [2.25,  1.5,   0.75] → argmax = 0 (class 0 has 2.25)
Row 2: [3.5,   1.0,   1.0]  → argmax = 0 (class 0 has 3.5)
Row 3: [4.75,  0.5,   1.25] → argmax = 0 (class 0 has 4.75)
Row 4: [2.5,   1.4,   0.8]  → argmax = 0 (class 0 has 2.5)

pred_class = [1, 0, 0, 0, 0]  (numpy array, shape: (5,))
```

---

### **Line 21: Flatten X Values**
```python
x_vals = X.numpy().flatten()
```

**What it does:**
- Converts X (5x1) to 1D array

```
X = [[1.0], [2.5], [5.0], [7.5], [3.0]]
x_vals = [1.0, 2.5, 5.0, 7.5, 3.0]
```

---

### **Line 22: Loop Over Colors**
```python
for c, col in enumerate(['blue', 'red', 'green']):
```

**What it does:**
- c = class index (0, 1, 2)
- col = color name

**Iteration 1:** c=0, col='blue'
**Iteration 2:** c=1, col='red'
**Iteration 3:** c=2, col='green'

---

### **Line 23: Create Boolean Mask**
```python
mask = (pred_class == c)
```

**ITERATION 1 (c=0, looking for class 0 predictions):**
```
pred_class = [1, 0, 0, 0, 0]
pred_class == 0 = [False, True, True, True, True]

mask = [False, True, True, True, True]
```

This means: samples at indices 1, 2, 3, 4 are predicted as class 0.

**ITERATION 2 (c=1, looking for class 1 predictions):**
```
pred_class == 1 = [True, False, False, False, False]

mask = [True, False, False, False, False]
```

Only sample 0 is predicted as class 1.

**ITERATION 3 (c=2, looking for class 2 predictions):**
```
pred_class == 2 = [False, False, False, False, False]

mask = [False, False, False, False, False]
```

No samples predicted as class 2.

---

### **Line 24: Check if Any Matches**
```python
if mask.any():
```

**What it does:**
- Only plot shading if at least one sample belongs to this class

**ITERATION 1:** mask.any() = True → proceed to fill
**ITERATION 2:** mask.any() = True → proceed to fill
**ITERATION 3:** mask.any() = False → skip (no class 2 predictions)

---

### **Line 25-26: Fill Regions**
```python
plt.fill_between(x_vals, 0, 1, where=mask, 
                 alpha=0.3, color=col, transform=plt.gca().get_xaxis_transform())
```

**ITERATION 1 (c=0, col='blue', mask=[F,T,T,T,T]):**
```
x_vals = [1.0, 2.5, 5.0, 7.5, 3.0]
mask =   [F,   T,   T,   T,   T]

Fill blue shading between y=0 and y=1 for x values where mask=True:
  From x=2.5 to x=7.5 (indices where True)
  
alpha=0.3 makes it semi-transparent (30% opaque)
transform=... keeps it aligned with x-axis (not affected by y-zoom)
```

**ITERATION 2 (c=1, col='red', mask=[T,F,F,F,F]):**
```
Fill red shading for x=1.0 (only index where True)
  Just a thin vertical band at x=1.0
```

**ITERATION 3 (c=2, col='green', mask=[F,F,F,F,F]):**
```
Skip (no green regions)
```

**Visual Result:**
```
y-axis
2.5 |
2   |█ ← green dot
1   |█   ← red dot
0   |█ █████████ ← blue region (semi-transparent)
    |___|____|____|_____|___
    0   2   4   6   8   10   x-axis

Legend:
█ = shaded region (semi-transparent)
●= actual data points
```

---

### **Line 27: Show Plot**
```python
plt.show()
```

**What it does:**
- Displays the complete plot with all dots, lines, and shading

---

## Summary of Data Flow

```
Input: data_set = (X_tensor, Y_tensor)

↓

Extract: X shape (5,1), Y shape (5,)

↓

Plot dots: 3 separate plots (one per class)

↓

If model provided:
  └─ Extract weights (3,1) and biases (3,)
  └─ Calculate logit line for each class
  └─ Plot 3 lines
  └─ If color=True:
     └─ Calculate all logits (5,3)
     └─ Find argmax → pred_class (5,)
     └─ Create mask for each class
     └─ Fill regions with color

↓

Display: plt.show()
```

---

## Quick Reference: Shapes at Each Step

| Variable | Shape | Content |
|----------|-------|---------|
| X | (5, 1) | Features (1 per sample) |
| Y | (5,) | Class labels (0, 1, or 2) |
| weights | (3, 1) | One weight per class |
| biases | (3,) | One bias per class |
| y_logit (per class) | (5,) | Logit scores for 1 class |
| logits | (5, 3) | All logit scores |
| pred_class | (5,) | Predicted class per sample |
| mask (per class) | (5,) | Boolean: which samples match class |
| x_vals | (5,) | Flattened X coordinates |

