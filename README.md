# DATE:
# EXPNO:2 Fitting Poisson  distribution
# Aim : 

To fit poisson distribution for the arrival of objects per minute from the feeder

# Software required :  

Python and Visual component tool

# Theory:

The Poisson distribution is the discrete probability distribution of the number of events occurring in a given time period, given the average number of times the event occurs over that time period.

![image](https://user-images.githubusercontent.com/104613195/166248326-fd042076-8b0b-40c4-8b11-1d8e8fcb74db.png)

 Conditions for Poisson Distribution:

1. An event can occur any number of times during a time period.
2. Events occur independently. I
3. The rate of occurrence is constant.
4. The probability of an event occurring is proportional to the length of the time period. 
 
# Procedure :

![image](https://user-images.githubusercontent.com/104613195/166251988-d0c53205-6080-4f7b-ae4c-398178586637.png)

# Experiment :

![image](https://user-images.githubusercontent.com/103921593/230282876-f4a5afbf-cac1-4648-a1b0-c78840638a8e.png)

# Program :
```
import numpy as np
import math
import scipy.stats
data = [int(i) for i in input().split()]
n = len(data)
max_val = max(data)
values = list()
frequencies = list()

for val in range(max_val + 1):
    count = 0
    for j in range(n):
        if data[j] == val:
            count += 1
    frequencies.append(count)
    values.append(val)
total_freq = np.sum(frequencies)
probabilities = list()
for i in range(max_val + 1):
    probabilities.append(frequencies[i] / total_freq)
mean_val = np.inner(values, probabilities)
poisson_probs = list()
expected_freqs = list()
chi_square_terms = list()
print("X P(X=x) Obs.Fr Exp.Fr xi")
print("--------------------------")
for x in range(max_val + 1):
    poisson_prob = math.exp(-mean_val) * mean_val**x / math.factorial(x)
    expected = poisson_prob * total_freq
    chi_term = (frequencies[x] - expected) ** 2 / expected
    poisson_probs.append(poisson_prob)
    expected_freqs.append(expected)
    chi_square_terms.append(chi_term)
    print("%2.2f %2.3f %4.2f %3.2f %3.2f" % (x, poisson_prob, frequencies[x], expected, chi_term))
print("--------------------------")
calculated_chi2 = np.sum(chi_square_terms)
print("Calculated value of Chi square is %4.2f" % calculated_chi2)
chi2_critical = scipy.stats.chi2.ppf(1 - 0.01, df=max_val)
print("Table value of chi square at 1 level is %4.2f" % chi2_critical)
if calculated_chi2 < chi2_critical:
    print("The given data can be fitted in Poisson Distribution at 1% LOS")
else:
    print("The given data cannot be fitted in Poisson Distribution at 1% LOS")
 ```
 

# Output : 

![Screenshot 2025-05-02 141245](https://github.com/user-attachments/assets/3dd3d352-eba1-4602-bd17-4a821cc2f7dc)


# Results

The Poisson distribution is fitted for the objects arrived from feeder per minute and the data is tested using Chi-square test. 
 
