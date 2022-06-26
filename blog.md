---
layout: default
---

## 1. Initial Goals
*Posted 26 June 2022*

At our first meeting, my mentors and I discussed the options we have for implementing new interfaces to PySAL's model and exploratory statistic classes. We discussed using multiple dispatch or ducktyping from `scikit-learn` and chose to begin with ducktyping `scikit-learn` as multiple dispatch has been deemed non-Pythonic. While developing functionality for Wilkinson formulas is an ancillary goal of this project, we are keeping it in mind as we make interface edits as those structural changes affect the formula implementation.

My first two goals are as follows:
1. Choose an unsupervised statistic (`Moran_Local`) and a supervised statistic (`GM_Lag`) and implement them using the `scikit-learn` paradigm. This will give us two concrete, minimal working examples that we can share to package leads.
2. Start issues in relevant packages to fill out the cells in the table below. We want to know what must be done for each package to switch to a `scikit-learn` interface and to extend it to Wilkinson formulas.

| Package | Requirements for ducktyping `scikit-learn` | Requirements for extending to Wilkinson formulas |
| :-----: | ------------------------------------------ | ------------------------------------------------ |
| `spreg` | | |
| `gwr`   | | |
| `esda`  | | |
| `spopt` | | |
|`weights`| | |
| `spglm` | | |
| ...     | | |

Finally, we aim to include automatic attribution tools to all the new interfaces so that users may easily generate the proper citations for the code they are using.
