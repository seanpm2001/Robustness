Qrobustness
===

Robustness Verification of Quantum Classifiers (Binary implementation)

### Requirements
---
Our tool relies on [CVXPY](https://www.cvxpy.org/). 

Its installation requires BLAS and LAPACK. Cmake and pip3 are also needed.
###### Unix, Linux (Example for Ubuntu 18.04)
```sh
sudo apt install -y libblas-dev liblapack-dev cmake python3-pip
```
Because the default version of Python in Ubuntu 18.04 is Python3.6, we should install Numpy first.
```sh
pip3 install numpy
```
Then, install CVXPY.
```sh
pip3 install cvxpy
```
In addition, our demostration file `batch_check.py` uses a Python library PrettyTable for printing a format table.
```sh
pip3 install prettytable
```

### Usage
---
We provide two functions for robustness verification `RobustnessVerifier` and `PureRobustnessVerifier` that aim to mixed quantum state and pure quantum state, respectively. See the following example for usage.
```python
from Qrobustness import RobustnessVerifier, PureRobustnessVerifier

# MIXED STATE VERIFICATION

# E: 3-dimensional narray
# Kraus representaion for a quantum classifier A
# A(rho) = sum (E[i,:,:] @ rho @ E[i,:,:].conj().T )

# O: 2-dimensional narray
# Final observable, for binary classification
# p1 = trace( O @ A(rho))

# data: 3-dimensional narray
# data needed for verification
# input state rho = data[i,:,:] 
# label: 1-dimensional narray
# data label, 0 or 1
# data[i,:,:] is labeled by label[i]

# e: a small real positive number
# check for e-robustness (fidelity)

robust_accuray, verification_time = RobustnessVerifier(
    E, O, data, label, e
)

# robust_accuracy[1] is robust accuracy
# verification_time[1] is the total verification time
# robust_accuracy[0] and verfication_time[0] is the corresponding outcome for our robust bound

# PURE STATE VERIFICATION

# data: 2-dimensional narray
# pure input state, psi = data[:,i]

robust_accuray, verification_time = PureRobustnessVerifier(
    E, O, data, label, e
)
```

### CAV Artifact Evaluation
---
Try follwing command in bash.
```sh
python3 batch_check.py binary_cav.mat 1e-4 4 mixed
```
