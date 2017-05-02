an open data playbook
========================================================
author: ursula kaczmarek
font-import: https://fonts.googleapis.com/css?family=NTR
font-family: 'NTR', sans-serif
css: simple.css
width: 1440
height: 900
<p>twitter <span style='color:#4f5d75;'>@ukacz</span>
  <br/>
  github <span style='color:#4f5d75;'>ursulakaczmarek</span>
</p>

so you want to work with open data
========================================================

- there are government sources and private (e.g. Kaggle, Quandl) sources of open data. we'll focus on the government sources.
- open data catalogues are geographically siloed, although the feds do host some state and local datasets <https://catalog.data.gov/dataset?groups=local>  
- open data catalogues vary in quality and depth. check out <http://us-city.census.okfn.org> for a crowdsourced census of cities' open data catalogues

so you want to work with open data
========================================================
open data is truly open when it's:
- openly licensed: free to use, reuse, and distribute at no cost
- machine readable: csv, json, xml, etc.  **NOT**  PDF, HTML, DOC, JPEG
- available in bulk: not record-by-record, although APIs can allow for selective data pulls

although not open by default, there is public gov data lurking around
- data released through Federal and State Freedom of Information Act/Law requests compended here: <https://www.muckrock.com>
- get scraping!

identifying the right source
========================================================
it's not always clear where to start looking, so ask:
what's the subject matter? 
- the feds cover well: 
  * demographics and mapping <https://census.gov/data.html> 
  * housing <https://huduser.gov>
  * environmental topics <https://www.data.gov/ecosystems/ecoinforma/>
- states cover well: 
  * elections 
  * transportation 
  * budgets
- citites/localities cover well: 
  * public safety/crime
  * zoning/construction/properties 
  * local services

identifying the right source
========================================================
what's the level of detail i need?
-the more granular the geography you're interested in, the more local the catalogue you need

what kind of data do i need?
- GIS? (more available for larger cities than smaller)
- structured datasets? (most widely available)
- can I tolerate some quality issues? (quality is a bigger concern with locally hosted datasets)


bulk data or API?
========================================================
- bulk datasets are manageable as a single flat file
- APIs are best for getting smaller bits of large (American Community Survey) or rapidly changing (stock tickers) datasets
- bulk datasets are more stable and readily available through file download
- APIs rely on servers and are less predictable and less open in that they may require registration or limiting parameters to accommodate traffic


get local: NYS/NYC data with the Socrata API
========================================================
- with R


```r
> library(RSocrata)
> #Socrata Query Language filter built into the API endpoint
> #pull data on transportation projects in the Capital District 
> transpo.url <- "https://data.ny.gov/resource/
+               eazj-exh7.json?region=01 CAPITAL DISTRICT"
> transpo.data <- read.socrata(transpo.url)
```
- with Python (Requests package)

```python
import requests
#pull data on public wifi locations the the borough of Manhattan
transpourl = "https://data.cityofnewyork.us
            /resource/3ktt-gd74.json?boro=Manhattan"
response = requests.get(transpourl)
if response.status_code == 200:
    data = response.json()
print(data)
```

want to learn more?
========================================================
- u.s. city open data census <http://us-city.census.okfn.org/>
- open prism: search tool across aggregated open data catalogues <http://openprism.thomaslevine.com/>
- open data policies in your neighborhood: <http://www.opendatapolicies.org/browse/>
