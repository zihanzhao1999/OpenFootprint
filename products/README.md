[Footprint Builder](/io/template) and [Open Data Panels](../)
# Product Comparisons

**BuildingTransparency.org API**
Environmental Product Declarations (EPD)

[Feed View - Static EPD json](/feed/view/#feed=epd)
[Product Feed API](/io/template/feed)
[View parsed YAML-TO-JSON-TO-HTML](/io/template/parser/)
<!--[View as Markdown](/io/template/product/product-concrete.html)-->


## Fetch Product Data

[Our EPD Pull on GitHub](https://github.com/ModelEarth/OpenFootprint/tree/main/products/) - [Resulting Data](https://github.com/ModelEarth/OpenFootprint/tree/main/products/US)
Python resides in prep/product-footprints.py

June 3, 2024 - <!--Loren -->Copied product-footprints.py into [Product Footprints Colab](https://colab.research.google.com/drive/1TJ1fn0-_8EBryN3ih5hZiKLISomOrWDW?usp=sharing)
Haven't run as CoLab yet.

TO DO: Activate Helper.py to save username and password since it expires


## Get API Key for Product Profile YAML

The [Central Concrete EPD data](https://github.com/modelearth/io/blob/master/template/product/product-concrete.yaml) was pulled from the BuildingTransparency.org API using the following steps:  

**STEP 1:** Create an account at [buildingtransparency.org](https://www.buildingtransparency.org/)

**STEP 2:** Use your name and password to get your bearer "key" here in Swagger: [openepd.buildingtransparency.org](https://openepd.buildingtransparency.org) - Click Authorize.

NOTE: Your BuildingTransparency API Key will expire after 3 days. Our python process automatically refreshes the key.

**STEP 3:** Open a command terminal, and get the "Bearer" secret key for your username

curl -X POST "https://etl-api.cqd.io/api/rest-auth/login" -H "accept: application/json" -H "Content-Type: application/json" -d "{\"username\":\"YOUR_USERNAME_EMAIL\",\"password\":\"YOUR PASSWORD\"}"


**RETURNS**

~~~
{"key":"xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx","last_login":"2021-08-12T02:49:09.850397Z"}%   
~~~

Which you'll append as:

~~~
-H "Authorization: Bearer xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
~~~

**Example:**

~~~
curl -X 'GET' \
 'https://openepd.buildingtransparency.org/api/epds?page_number=1&page_size=100' \
 -H 'accept: application/json' \
 -H 'filter: {"epds.name":"ASTM International"}' \
 -H 'Authorization: Bearer xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
~~~

**Tip:** Use the [EC3 frontend](https://buildingtransparency.org/ec3/material-search) of the tool and watch the commands it issues in the dev inspector's network tab. 

Georgia Mass Timber:

https://buildingtransparency.org/api/materials?page_number=1&page_size=25&soft_search_terms=true&category=b03dba1dca5b49acb1a5aa4daab546b4&jurisdiction=US-FL&epd__date_validity_ends__gt=2021-08-24


~~~
curl -X 'GET' \
  'https://openepd.buildingtransparency.org/api/epds?page_number=1&page_size=1' \
  -H 'accept: application/json' \
  -H "Authorization: Bearer xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
~~~

<div id="postman"></div>

To convert to yaml, the json can be pasted in either: [json2yaml.com](https://www.json2yaml.com/) or [editor.swagger.io](https://editor.swagger.io)

<br>

# View API in Postman

1. Click on "import" tab on the upper left side.
2. Select the Raw Text option and paste your cURL command.
3. Hit import and you will have the command in your Postman builder!
4. Click Send to post the command.

[How to use Curl with Postman](https://www.google.com/search?q=how+to+use+Curl+with+Postman&oq=how+to+use+Curl+with+Postman&aqs=chrome..69i57.18359j0j9&sourceid=chrome&ie=UTF-8) - [YouTube](https://www.google.com/search?q=how+to+use+Curl+with+Postman&sxsrf=APq-WBtPCQSW52ZIvoJZxIvspDVdEJ_G0g:1648670885549&source=lnms&tbm=vid&sa=X&ved=2ahUKEwio-u_T0e72AhXWmGoFHSTLB6sQ_AUoAXoECAEQAw&biw=1513&bih=819&dpr=1)
<br>

# Get YAML for IO Template

[For IO Template](../) - Use OpenEPD swagger

<!-- https://etl-api.cqd.io/ No longer works -->

BuildingTransparency OpenEPD API
[https://openepd.buildingtransparency.org/#/epds/get_epds_id](openepd.buildingtransparency.org/#/epds/get_epds_id)


Inside Postman, you can load the swagger.yaml file [exported from Swagger](https://stackoverflow.com/questions/48525546/how-to-export-swagger-json-or-yaml) which will import the schemas into Postman.


