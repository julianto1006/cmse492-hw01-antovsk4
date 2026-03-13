1. **Overview**  
   This project repo analyzes sales data to figure out which regions and prodcut categories are bringing in the most revenue. It takes two CSV files (sales and customer). It will show a summary table as a CSV file and a bar chart as a PNG file in the outputs folder when its done. 

2. **Data**  
   The data is already in the repo so no downloading is needed. Two CSV files live in datafiles/raw,
   - sals_jan.csv: sales transactions(order_id,date,customer_id,category,units,unit_price)
   - customer_lookup.csv: customer info (customer_id,customer_name,region,segment)

   There is also a datafiles/random that has weather_small.csv (date,city,temp_f,precip_in) this is not needed for the repo. 

3. **Environment Setup**  
   - venv + requirements.txt:
    - python -m venv venv (copy and paste)
    - source venv/vin/activate (copy and paste)
    - pip install pandas matplotlib numpy (copy and paste)
    - pip freeze > requirements.txt (copy and paste)
   - Inside the requiremtents.txt it should look like:      matplotlib==3.10.8 (your version)
   numpy==2.4.3 (your version)
   pandas==3.0.1 (your version)

   - to deactivate: deactivate 
   - to reactivate: source venv/vin/activate

   - conda + environment.yml:
    - touch environment.yml  (copy and paste)
    - conda env create -f environment.yml (copy and paste)
    - conda activate hw01-env (copy and paste)
   - Inside the environment.yml it should look like(copy and paste): 
     - name: hw01-env  
      channels:
        - conda-forge
        - defaults
      dependencies:
        - python=3.13.5 (your version)
        - numpy
        - pandas
        - matplotlib

    - to deactivate: conda deactivate
    - to reactivate: conda activate hw01-env 

4. **Reproduce a Result**  
  In the terminal to see if the environments are working run
  - python scripts/analysis.py 
  once the environment is activated this command will be used for venv and conda. Deactivate the environment before trying the next environment. Only one environment should be active at a time (look at enviorment setup above on how to reactivate and deactivate enviorments). 

  Expected output in the outputs folder: 
  - summary_by_region.csv: 12 row summary tables (region category,total_units,total_revenue,orders,avg_revenue_per_order)
  - revenue_by_region.png: bar chart of total revenue by region  

  To verify open quick_run_demo.ipynb and output_examples.ipynb and run all the cells with no errors. 


5. **Troubleshooting**  
   - For windows computers if there is an issue on setting up enviroments google the right command that will be needed sometimes they are different. 
   - If there is an error when running the .ipynb files make sure in the analysis.py that all the paths are correct 
   - Another error that may happen when running the .ipynb files is that its not outputing in the correct place so make sure that is going into outputs. 
   - if you move any of the files around or change names make sure you update the paths 

6. **Personal Analysis**
   I added a second plot that shows total units sold broken down by product category (hardware, software, office). This uses the same summary data that's already being generated, just visualized differently. The new chart gets saved to outputs folder as units_by_category.png when you run analysis.py.

   Before this change the only output plot was revenue by region. Now you can also see which product categories are moving the most units, which is a different visual on the same data (a category could have low revenue but high unit volume or vice versa), so it adds something the original plot didn't show.

7. **Containerized Run**
   - Check if docker is installed with docker --version 
   - if installed continue below, if not go to install docker part 
   - touch Dockerfile (copy and paste)
   - open the dockerfile created and add:

     FROM python:3.13-slim (your version)

     ENV PYTHONDONTWRITEBYTECODE=1 \
        PYTHONUNBUFFERED=1

      WORKDIR /app

      COPY requirements.txt .

      RUN pip install -r requirements.txt

      COPY . .

      CMD ["python", "scripts/analysis.py"]

    - docker build -t hw01-analysis .  (copy and paste)
    - docker run --rm -v $(pwd)/outputs:/app/outputs hw01-analysis (copy and paste)
    - output that it ran correctly: 
      Analysis complete.

      Rows in summary: 12

      Summary written to: /app/outputs/summary_by_region.csv

      Plot written to: /app/outputs/revenue_by_region.png

      Category plot written to: /app/outputs/units_by_category.png

   - INSTALL DOCKER:
        - go to webiste and pick the right installer https://www.docker.com/products/docker-desktop/

   - Windows: 
        - Download and run the installer
        - Accept the default options unless you have a specific reason not to
        - If prompted about WSL2, accept the recommended settings 

  - macOS:
        - Download and run the installer, then follow the on-screen instructions