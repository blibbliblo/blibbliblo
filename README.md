<h1>Hi, I'm Pattaradanai</h1>

 - This is my **mini-project** just only to experiement and observe how the famous **Collatz Conjecture** form in a chart.
 - Using Google Colab, I am able to achieve my goal by plotting the conjecture (in the range of 2^16) in a chart using pandas and altair framework.
 - By defining a function "collatz" with the parameter "number" :
```python3
#define collatz function with number
def collatz(number):
  is_valid = False
  step_count = 0
  initial = number

#collatz conjecture
  while number !=1:
    if number % 2 == 0:
      number = number / 2
    else:
      number = (3 * number) + 1
    step_count += 1
  #true means its not countered and is true by the hypothesis
  is_valid = True

  return initial, is_valid, step_count
```

 - After the values require to be plotted are created, I made three lists:
```
import altair as alt
import pandas as pd

#lists of values
initial_values = []
step_counts = []
is_valid_values = []
```
 To store these values which will later be plotted

 - Later we evaluate the values and put it in their corresponding lists:
```
#only 2**16 because 32 and 64 takes 7 hours to show output
for i in range(1, 2**16): #take data of the re-evaluation of collatz and append it in the coresponding list
  initial, is_valid, step_count = collatz(i)
  initial_values.append(initial)
  step_counts.append(step_count)
  is_valid_values.append(is_valid)
```
 - After that a dataset is made to store the value which we will put in the chart
```
#put the list as data
data = pd.DataFrame({
    "initial_x": initial_values,
    "step_y": step_counts,
    "is_valid": is_valid_values
})
```
 - An interactive chart is made using the data acquired:
 - X is the initial value before the application of Collatz
 - While Y is the steps required for the value to reach the final point: 1
```
#put the data in the chart
chart = alt.Chart(data).mark_circle().encode(
    x='initial_x',
    y='step_y',
    tooltip=['initial_x','step_y','is_valid']
).interactive()

#plotting and output
chart
```
 - After that the max and min value can be acquire using:
```
data.min()
```
```
data.max()
```
