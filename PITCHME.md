## Examining Your Repository under the Hood from the Solr Admin Console

Terry Brady

Georgetown University Library

https://github.com/terrywbrady/info

![](https://www.library.georgetown.edu/sites/default/files/library-logo.png)

---
### SOLR in DSpace

- Search / Discovery
- OAI Harvest Index
- Statistics 
- Authority Index (Optional)

+++

### Accessing SOLR

- In DSpace, SOLR Admin access is generally restricted to local server
- Overriding localhost restriction
  - Essential for production
- https://github.com/DSpace/DSpace/blob/dspace-6_x/dspace-solr/src/main/webapp/WEB-INF/web.xml#L52-L56

+++?code=https://raw.githubusercontent.com/DSpace/DSpace/blob/dspace-6_x/dspace-solr/src/main/webapp/WEB-INF/web.xml
@[52-56](Uncomment these lines to remove the local restriction)

---
### Tour of the Admin Console

- Caution - The Solr Admin Console has some options that are destructive
- Presentation will focus on safe operations

+++
### Core Selector
![](images/core.png)

+++
### Core Overview 
![](images/tOver.png)

+++
### Core Query
![](images/tQuery.png)

+++
### Schema Browser
![](images/tSchema.png)

+++
### Document Add (for testing)
![](images/tDoc.png)

---

### Load Sample Statistics Data (if needed)

(Link to be added)

---

### Query All Items

|name|value|
|---|---|
|q     | `*:*` |   

Note that Only 10 items are listed

+++

### Query All, View Only Item 1

|name|value|
|---|---|
|q     | `*:*` |   
|rows  | `1` |

+++

### Query All, View Only Item 2

|name|value|
|---|---|
|q     | `*:*` |   
|start | `1` |
|rows  | `1` |

+++

### Change Output Format

- XML
- CSV
- JSON

+++

### List specific fields

|name|value|
|---|---|
|q     | `*:*` |   
|start | `1` |
|rows  | `1` |
|fl    | `statistics_type, type, time` |

+++

### List 20 items

|name|value|
|---|---|
|q     | `*:*` |   
|start | `0` |
|rows  | `20` |
|fl    | `statistics_type, type, time` |
    
---

### Analyze Fields (Schema Browser)

- statistics_type
- type    
    
+++

### Analyze statistics_type (By Facet)

|name|value|
|---|---|
|q          | `*:*` |   
|start      | `0` |
|rows       | `0` |
|facet      | `true` |
|facet.field| `statistics_type` |

+++

### Analyze type (By Facet)

|name|value|
|---|---|
|q          | `*:*` |   
|start      | `0` |
|rows       | `0` |
|facet      | `true` |
|facet.field| `type` |

+++

### Analyze time (By Facet)

|name|value|
|---|---|
|q          | `*:*` |   
|start      | `0` |
|rows       | `0` |
|facet      | `true` |
|facet.field| `time` |

+++

### Analyze year (By Facet)

|name|value|
|---|---|
|q          | `*:*` |   
|start      | `0` |
|rows       | `0` |
|facet      | `true` |

    &facet.date=time&facet.date.start=NOW/YEAR/DAY-5YEARS&facet.date.end=NOW/YEAR/DAY%2B1YEAR&facet.date.gap=%2B1YEAR

---
### Document Counts
The first step of the tutorial will be to query for all documents in the Solr repository (q=*:*).  We will review the documents that are returned and note the count of objects that are returned.  We will also note the named fields in each resulting document.  We will manipulate the start index and result count to vary the number of documents returned.  We will manipulate the field list parameter to alter the amount of data that is returned from the query.  We will also manipulate the output format for the query illustrating how to return JSON, XML, or CSV from the query.
---
### Query Construction
The next step of the tutorial will be construct a query on a text field, on a numeric field, and on a date field.  Once we have studied how to query on a single field, we will construct queries with AND, OR, and NOT.  Lastly, we will alter the sort options to change the order of the results.
---
### Result Faceting
The next step of the tutorial will be manipulate facet parameters to analyze the contents of the Solr repository.  In the example of the DSpace statistics repository, we will demonstrate how search facets can help to identify new bots and web crawlers. 
Solr provides powerful capabilities to facet values by date.  Using the sample repository data, we will analyze user activity over various time ranges.  The presentation will then demonstrate a DSpace statistics reporting dashboard constructed from numerous individual Solr queries.
---
### Schema Browser
The Solr Schema browser can also provide insight about the fields within a Solr repository.  We will take a brief look at this tab of the console and show how it can confirm some of our previous discoveries.
Looking at another Solr Repo
Each DSpace instance contains at least 3-4 separate Solr instances.  The presentation will take a brief tour of the DSpace â€œsearchâ€� repository illustrating how the lessons learned from the statistics repository could be applied to a Solr repository with a different schema.
