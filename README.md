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

<!-- <style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-lboi{border-color:inherit;text-align:left;vertical-align:middle}
.tg .tg-9wq8{border-color:inherit;text-align:center;vertical-align:middle}
.tg .tg-0pky{border-color:inherit;text-align:left;vertical-align:top}
.tg .tg-dvpl{border-color:inherit;text-align:right;vertical-align:top}
</style> -->
<table class="tg">
<thead>
  <tr>
    <th class="tg-0pky"><span style="font-weight:bold">Image Name</span></th>
    <th class="tg-0pky"><span style="font-weight:bold">Install Packages</span></th>
    <th class="tg-0pky"><span style="font-weight:bold">Version</span></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-9wq8" rowspan="6">Jupyterlab_base</td>
    <td class="tg-0pky">Jupyterlab git extension</td>
    <td class="tg-dvpl">0.33.0</td>
  </tr>
  <tr>
    <td class="tg-0pky">Mssql driver</td>
    <td class="tg-dvpl">17.8.1.1-1</td>
  </tr>
  <tr>
    <td class="tg-0pky">pyodbc</td>
    <td class="tg-dvpl">4.0.0</td>
  </tr>
  <tr>
    <td class="tg-0pky">Pyarrow</td>
    <td class="tg-dvpl">3.0.0</td>
  </tr>
  <tr>
    <td class="tg-0pky">Pycrypto</td>
    <td class="tg-dvpl">2.6.1</td>
  </tr>
  <tr>
    <td class="tg-0pky">Turbodbc</td>
    <td class="tg-dvpl">4.2.1</td>
  </tr>
  <tr>
    <td class="tg-lboi" rowspan="3">Jupyterlab_general</td>
    <td class="tg-0pky">Airflow</td>
    <td class="tg-dvpl">2.1.0</td>
  </tr>
  <tr>
    <td class="tg-0pky">BentoML</td>
    <td class="tg-dvpl">0.13.1</td>
  </tr>
  <tr>
    <td class="tg-0pky">Pylint</td>
    <td class="tg-dvpl">2.11.1</td>
  </tr>
  <tr>
    <td class="tg-lboi" rowspan="3">Jupyterlab_pyspark</td>
    <td class="tg-0pky">Spark</td>
    <td class="tg-dvpl">3.1.1</td>
  </tr>
  <tr>
    <td class="tg-0pky">Hadoop</td>
    <td class="tg-dvpl">3.2</td>
  </tr>
  <tr>
    <td class="tg-0pky">Pyspark</td>
    <td class="tg-dvpl">3.1.1</td>
  </tr>
  <tr>
    <td class="tg-lboi" rowspan="3">Jupyterlab_tensorflow</td>
    <td class="tg-0pky">Tensorflow</td>
    <td class="tg-dvpl">2.7.0</td>
  </tr>
  <tr>
    <td class="tg-0pky">Datatransformer</td>
    <td class="tg-dvpl">0.1.7</td>
  </tr>
  <tr>
    <td class="tg-0pky">Modelbricks</td>
    <td class="tg-dvpl">0.1.1</td>
  </tr>
  <tr>
    <td class="tg-lboi" rowspan="2">Jupyterlab_datascience</td>
    <td class="tg-0pky">Julia</td>
    <td class="tg-dvpl">1.6.0</td>
  </tr>
  <tr>
    <td class="tg-0pky">R</td>
    <td class="tg-dvpl">4.0.3</td>
  </tr>
  <tr>
    <td class="tg-lboi" rowspan="4">Jupyterlab_decisiontree</td>
    <td class="tg-0pky">Xgboost</td>
    <td class="tg-dvpl">1.5.2</td>
  </tr>
  <tr>
    <td class="tg-0pky">Lightgbm</td>
    <td class="tg-dvpl">3.3.2</td>
  </tr>
  <tr>
    <td class="tg-0pky">Tpot</td>
    <td class="tg-dvpl">0.11.7</td>
  </tr>
  <tr>
    <td class="tg-0pky">Mlxtend</td>
    <td class="tg-dvpl">0.18.0</td>
  </tr>
</tbody>
</table>