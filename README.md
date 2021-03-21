# Tech Challenge
This document objetive is to provide a detail explanation on the solution for the HellowFresh tech challenge explain on `README.md` file. The deliverables for the solution are:

- [X] A deployable Spark applicationm written in Python that can be submitted to a Spark cluster (or locally) using the 'spark-submit' command.
- [X] Proper documentation on the solution, that you can be find across the project and mostly within this file, `ETL_README.md`.
- [X] CSV outpout dataset `outpout/beef_recipes.csv`.

- [X] Method for logging and alerting using log4j.
- [X] Unit test for the etl components.
- [X] Data Quality validations.
- [X] Theoretical implementation scenarios:
    - [X] CI/CD implementation
    - [X] Performance tunning
    - [X] Scheduled pipelines

## Project Structure
```bash
root/
 |-- configs/
 |   |-- etl.json
 |-- dependencies/
 |   |-- logging.py
 |   |-- spark.py
 |-- jobs/
 |   |-- etl.py
 |-- tests/
 |   |-- test_data/
 |   |-- | -- beef_recipes/
 |   |-- test_etl.py
 |   make.sh
 |   packages.zip
 |   Pipfile
 |   Pipfile.lock
 |   requirements.txt
```

The main Python module is the ETL job, `jobs/etl.py`,  which is going to be send it to Spark. 
The source events of the recipes stored as json files, are located on, `input/*.json`. 
The persist dataset as CSV that only containts the recipes that have `beef` as one of the ingredients is located on, `output/beef_recipes.csv`. This file contains 2 columns: `difficulty,avg_total_cooking_time`.

```bash
    total_cook_time = cookTime + prepTime
    
    difficulty:
        easy < 30 min
        30 min < medium > 60 min
        hard > 60 min
```  

Criteria for levels based on total cook time duration:
- easy - less than 30 mins
- medium - between 30 and 60 mins
- hard - more than 60 mins.

The main Python module containing the ETL job (which will be sent to the Spark cluster), is `jobs/etl_job.py`. Any external configuration parameters required by `etl_job.py` are stored in JSON format in `configs/etl_config.json`. Additional modules that support this job can be kept in the `dependencies` folder (more on this later). In the project's root we include `build_dependencies.sh`, which is a bash script for building these dependencies into a zip-file to be sent to the cluster (`packages.zip`). Unit test modules are kept in the `tests` folder and small chunks of representative input and output data, to be used with the tests, are kept in `tests/test_data` folder.


## Assumptions / Considerations


## ETL approach

