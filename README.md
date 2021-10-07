Docker-Stacks
===
## Table of Contents
- [Docker-Stacks](#Docker-Stacks)
  - [Table of Contents](#Table-of-Contents)
  - [Images Dependency](#Inages-Dependency)
  - [Images Details](#Images-Details)

## Images Dependency
```plantuml
@startdot
digraph G{
 Jupyterlab_base ->Jupyter_general
 Jupyter_general ->Jupyterlab_datascience
 Jupyter_general ->Jupyterlab_tensorflow
 Jupyter_general ->Jupyterlab_pyspark
 Jupyterlab_datascience->Jupyterlab_decisiontree
}
@enddot
```

```mermaid
graph TD
 Jupyterlab_base -->Jupyter_general
 Jupyter_general -->Jupyterlab_datascience
 Jupyter_general -->Jupyterlab_tensorflow
 Jupyter_general -->Jupyterlab_pyspark
 Jupyterlab_datascience-->Jupyterlab_decisiontree
```

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
