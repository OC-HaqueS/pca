# pca

[![Python](https://img.shields.io/pypi/pyversions/pca)](https://img.shields.io/pypi/pyversions/pca)
[![PyPI Version](https://img.shields.io/pypi/v/pca)](https://pypi.org/project/pca/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](https://github.com/erdogant/pca/blob/master/LICENSE)

* pca is a python package that performs the principal component analysis and allows to make several plots.
* Biplot to plot the loadings
* Explained variance 
* Scatter plot with the loadings

## Method overview
* fit
model=pca.fit(X)
* fit and plot
model=pca.biplot(X)
* biplot plot
pca.explainedvarplot(model)
* scatterplot
pca.scatterplot(model)
* 3d scatterplot
pca.scatterplot3d(model)
* Normalize out components from your dataset
pca.norm(X)


## Contents
- [Installation](#-installation)
- [Requirements](#-Requirements)
- [Quick Start](#-quick-start)
- [Contribute](#-contribute)
- [Citation](#-citation)
- [Maintainers](#-maintainers)
- [License](#-copyright)

## Installation
* Install pca from PyPI (recommended). pca is compatible with Python 3.6+ and runs on Linux, MacOS X and Windows. 
* It is distributed under the MIT license.

## Requirements
* It is advisable to create a new environment. 
```python
conda create -n env_pca python=3.6
conda activate env_pca
pip install numpy matplotlib sklearn
```

## Quick Start
```
pip install pca
```

* Alternatively, install pca from the GitHub source:
```bash
git clone https://github.com/erdogant/pca.git
cd pca
python setup.py install
```  

## Import pca package
```python
import pca as pca
```

## Load example data
```python
import numpy as np
from sklearn.datasets import load_iris
X = load_iris().data
feat=iris.feature_names
labels=iris.target
```

#### X looks like this:
```
X=array([[5.1, 3.5, 1.4, 0.2],
         [4.9, 3. , 1.4, 0.2],
         [4.7, 3.2, 1.3, 0.2],
         [4.6, 3.1, 1.5, 0.2],
         ...
         [5. , 3.6, 1.4, 0.2],
         [5.4, 3.9, 1.7, 0.4],
         [4.6, 3.4, 1.4, 0.3],
         [5. , 3.4, 1.5, 0.2],

labels=[0, 0, 0, 0,...,2, 2, 2, 2, 2]
feat=['feat1','feat2','feat3','feat4']
```

## PCA reduce dimensions and plot explained variance
```python
# Fit
model = pca.fit(X)
# Plot the explained variance. The total of captured variance is 1 and PC1 captures more then 90% of it.
ax = pca.plot_explainedvar(model)
# Biplot in 2D with shows the directions of features and weights of influence
ax  = pca.biplot(model)
# Biplot in 3D
ax  = pca.biplot3d(model)
```
<p align="center">
  <img src="https://github.com/erdogant/pca/blob/master/docs/figs/fig_explvar.png" width="400" />
</p>
<p align="center">
  <img src="https://github.com/erdogant/pca/blob/master/docs/figs/fig_biplot.png" width="400" />
  <img src="https://github.com/erdogant/pca/blob/master/docs/figs/fig_biplot3d.png" width="400" />
</p>

## PCA reduce dimensions as above but now plot with labels and feature names
```python
model = pca.fit(X, labels=labels, feat=feat)
ax  = pca.biplot(model)
ax  = pca.biplot3d(model)
```
<p align="center">
  <img src="https://github.com/erdogant/pca/blob/master/docs/figs/fig1b.png" width="400" />
  <img src="https://github.com/erdogant/pca/blob/master/docs/figs/fig1c.png" width="400" />
</p>

## PCA reduce dimensions to the number of components that capture 95% of the explained variance
```python
# Fit model and determine the number of required components that captures 95% of the explained variance.
model = pca.fit(X, components=0.95)
# Plot the explained variance. The required number of components is 2 to capture 95% of the variance.
ax = pca.plot_explainedvar(model)
```
<p align="center">
  <img src="https://github.com/erdogant/pca/blob/master/docs/figs/fig_explvar_95.png" width="400" />
</p>

## PCA reduce dimensions to exactly 2d and 3d
```python
# Set components=2 to reduce to 2d
model = pca.fit(X, components=2)
# Set components=2 to reduce to 3d
model = pca.fit(X, components=3)
```

## PCA normalization. 
```python
# Normalizing out the 1st and more components from the data. 
# This is usefull if the data is seperated in its first component(s) by unwanted or biased variance. Such as sex or experiment location etc. 

print(X.shape)
(150, 4)

# Normalize out 1st component and return data
Xnorm = pca.norm(X, pcexclude=[1])

print(Xnorm.shape)
(150, 4)

# In this case, PC1 is "removed" and the PC2 has become PC1 etc
ax = pca.biplot(model)

```
<p align="center">
  <img src="https://github.com/erdogant/pca/blob/master/docs/figs/fig_norm.png" width="400" />
</p>

## Citation
Please cite pca in your publications if this is useful for your research. Here is an example BibTeX entry:
```BibTeX
@misc{erdogant2019pca,
  title={pca},
  author={Erdogan Taskesen},
  year={2019},
  howpublished={\url{https://github.com/erdogant/pca}},
}
```

## Maintainers
* Erdogan Taskesen, github: [erdogant](https://github.com/erdogant)

## Contribute
* Contributions are welcome.

## © Copyright
See [LICENSE](LICENSE) for details.