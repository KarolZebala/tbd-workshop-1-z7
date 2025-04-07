IMPORTANT ❗ ❗ ❗ Please remember to destroy all the resources after each work session. You can recreate infrastructure by creating new PR and merging it to master.
  
![img.png](doc/figures/destroy.png)

1. Authors:

   ***Zespół 7***

   ***https://github.com/KarolZebala/tbd-workshop-1-z7***
   
2. Follow all steps in README.md.

3. In boostrap/variables.tf add your emails to variable "budget_channels".

4. From avaialble Github Actions select and run destroy on main branch.
   
5. Create new git branch and:
    1. Modify tasks-phase1.md file.
    
    2. Create PR from this branch to **YOUR** master and merge it to make new release. 
    
    ***place the screenshot from GA after succesfull application of release***

    ![img.png](doc/deploy/successful_deploy.png)


6. Analyze terraform code. Play with terraform plan, terraform graph to investigate different modules.

    ***describe one selected module and put the output of terraform graph for this module here***
   
7. Reach YARN UI
   
   ***place the command you used for setting up the tunnel, the port and the screenshot of YARN UI here***
   
8. Draw an architecture diagram (e.g. in draw.io) that includes:
    1. VPC topology with service assignment to subnets
    2. Description of the components of service accounts
    3. List of buckets for disposal
    4. Description of network communication (ports, why it is necessary to specify the host for the driver) of Apache Spark running from Vertex AI Workbech
  
    ***place your diagram here***

9. Create a new PR and add costs by entering the expected consumption into Infracost
For all the resources of type: `google_artifact_registry`, `google_storage_bucket`, `google_service_networking_connection`
create a sample usage profiles and add it to the Infracost task in CI/CD pipeline. Usage file [example](https://github.com/infracost/infracost/blob/master/infracost-usage-example.yml) 

   ***place the expected consumption you entered here***
   Zmieniony config w infracost-usage.yml
   ![img.png](doc/figures/ingracost/infracost-config.png)
   ***place the screenshot from infracost output here***'
   Wyniki odpalenia lokalnie `infracost breakdown --path=. --usage-file=.github/workflows/infracost-usage.yml`
   ![img.png](doc/figures/ingracost/infracost-wynik.png)

   Dodano równie w cicd podsumowanie - trzeba było wskazać na plik infracost-usage.yml oraz na Githubie dodać klucz do api jako sekret `INFRACOST_API_KEY`
   ![img.png](doc/figures/ingracost/github-wynik.png)

10. Create a BigQuery dataset and an external table using SQL
    
    ***place the code and output here***
    
    ```sql
    --utworzenie schematu
    CREATE SCHEMA IF NOT EXISTS test OPTIONS(location = 'europe-west1');

    --utworzenie tabeli w formacie ORC, dane są w zasobie gs://tbd-2025l-9913-data/data/shakespeare/
    CREATE OR REPLACE EXTERNAL TABLE test.shakespeare
    OPTIONS (
    format = 'ORC',
    uris = ['gs://tbd-2025l-9913-data/data/shakespeare/*.orc']
    );

    --pobranie danych
    select * from test.shakespeare
    ```
   Przykładowy wynik zapytania
   ![img.png](doc/figures/big_query/big_query_results.png)

    ***why does ORC not require a table schema?***
    ORC nie wymaga zewnętrznego schematu, poniewaz zawiera plik zawiera metadane, w których znajdują się informacje
    odnośnie schematu
11. Find and correct the error in spark-job.py

    ***describe the cause and how to find the error***
    Problemem w pliku jest na sztywno wpisana wartość DATA_BUCKET. Po poprawieniu jej na ściezkę pasującą do naszego
    projektu wszystko działa w porządku. Problem został właściwie od razu zauwazony po otwarciu pliku
    
    ![img.png](doc/figures/big_query/corrected_data.png)



12. Add support for preemptible/spot instances in a Dataproc cluster

    ***place the link to the modified file and inserted terraform code***
    
    
