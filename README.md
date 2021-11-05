Docker-Stacks
===
## Table of Contents
- [Docker-Stacks](#Docker-Stacks)
  - [Table of Contents](#Table-of-Contents)
  - [Images Dependency](#Images-Dependency)
  - [Images Details](#Images-Details)

## Images Dependency
![images](https://github.com/nextfortune/docker-stacks/blob/main/images/Images%20Dependency.PNG)

Images Details
---

|  Image name             | Install Packages                                                             |
|  ----                   | ----                                                                         |
| Jupyterlab_base         | Jupyterlab git extension, <br> Mssql driver, Pyodbc, <br> Pyarrow,  Turbodbc |
| Jupyterlab_general      | Airflow, BentoML, Pylint                                                     |
| Jupyterlab_datascience  | Julia, R                                                                     |
| Jupyterlab_decisiontree |  Xgboost, Lightgbm, <br> Tpot, Mlxtend                                       |
| Jupyterlab_tensorflow   | Tensorflow, <br> Datatransformer, <br> Modelbricks                           |
| Jupyterlab_pysprak      |  Spark                                                                       |
