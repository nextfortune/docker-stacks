Docker-Stacks
===
## Table of Contents
- [Docker-Stacks](#Docker-Stacks)
  - [Table of Contents](#Table-of-Contents)
  - [Images Dependency](#Inages-Dependency)
  - [Images Details](#Images-Details)

## Images Dependency

<!DOCTYPE html>
<html lang="en">
   <head>
	 <script src="https://cdnjs.cloudflare.com/ajax/libs/mermaid/8.0.0/mermaid.min.js"></script>
    </head>
	 
<body>
 <pre><code class="language-mermaid">graph LR
A--&gt;B
</code></pre>

<div class="mermaid">graph LR
A--&gt;B
</div>
	
</body>
<script>
var config = {
    startOnLoad:true,
    theme: 'forest',
    flowchart:{
            useMaxWidth:false,
            htmlLabels:true
        }
};
mermaid.initialize(config);
window.mermaid.init(undefined, document.querySelectorAll('.language-mermaid'));
</script>

</html>

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
