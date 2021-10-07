---
title: 'Docker-stacks'
disqus: hackmd
---

Docker-Stacks
===
## Table of Contents
[TOC]

## Images dependency
```mermaid
graph TD
 Jupyterlab_base -->Jupyter_general;
 Jupyter_general -->Jupyterlab_datascience;
 Jupyter_general -->Jupyterlab_tensorflow;
 Jupyter_general -->Jupyterlab_pyspark;
 Jupyterlab_datascience-->Jupyterlab_decisiontree;
```

Images details
---
<font face = 微軟雅黑>

|  Image name             | Install Packages                                                             |
|  ----                   | ----                                                                         |
| Jupyterlab_base         | Jupyterlab git extension, <br> Mssql driver, Pyodbc, <br> Pyarrow,  Turbodbc |
| Jupyterlab_general      | Airflow, BentoML, Pylint                                                     |
| Jupyterlab_datascience  | Julia, R                                                                     |
| Jupyterlab_decisiontree |  Xgboost, Lightgbm, <br> Tpot, Mlxtend                                       |
| Jupyterlab_tensorflow   | Tensorflow, <br> Datatransformer, <br> Modelbricks                           |
| Jupyterlab_pysprak      |  Spark                                                                       |

</font>