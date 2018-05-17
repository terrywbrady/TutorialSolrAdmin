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
  - Only for testing - be careful in production production
- https://github.com/DSpace/DSpace/blob/dspace-6_x/dspace-solr/src/main/webapp/WEB-INF/web.xml#L52-L56

+++

Comment out the following for testing

    <!-- Any path (name) registered in solrconfig.xml will be sent to that filter -->
    <filter>
      <filter-name>LocalHostRestrictionFilter</filter-name>
      <filter-class>org.dspace.solr.filters.LocalHostRestrictionFilter</filter-class>
    </filter>


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

- [Sample Stats Records](sample-data/stats.csv)
- This data was pulled from a DSpace 5 test instance
- Numeric identifiers for item/community/collection are instance specific
- IP data has been masked

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

---

### Adding a Date Facet

- Use the Raw Query Parameters Field for search parameters that do not appear on the form
- Urlencode special characters
- In the following example `+` becomes `%2B`

+++

### Analyze year (By DATE Facet)

|name|value|
|---|---|
|q          | `*:*` |   
|start      | `0` |
|rows       | `0` |
|facet      | `true` |
|Raw Query Parameters|See following slides|

+++

### Last 5 Years (Raw Query Params)

|name|value|
|---|---|
|facet.date|time|
|facet.date.start|NOW/YEAR/DAY-5YEARS|
|facet.date.end|NOW/YEAR/DAY+1YEAR|
|facet.date.gap|+1YEAR|

    &facet.date=time&facet.date.start=NOW/YEAR/DAY-5YEARS&facet.date.end=NOW/YEAR/DAY%2B1YEAR&facet.date.gap=%2B1YEAR

+++

### Last 12 Months (Raw Query Params)

|name|value|
|---|---|
|facet.date|time|
|facet.date.start|NOW/MONTH/DAY-12MONTHS|
|facet.date.end|NOW/MONTH/DAY+1MONTH|
|facet.date.gap|+1MONTH|

    &facet.date=time&facet.date.start=NOW/MONTH/DAY-12MONTHS&facet.date.end=NOW/MONTH/DAY%2B1MONTH&facet.date.gap=%2B1MONTH

+++

### Last 6 Quarters (Raw Query Params)

|name|value|
|---|---|
|facet.date|time|
|facet.date.start|NOW/MONTH/DAY-18MONTHS|
|facet.date.end|NOW/MONTH/DAY+3MONTHS|
|facet.date.gap|+3MONTHS|

    &facet.date=time&facet.date.start=NOW/MONTH/DAY-18MONTHS&facet.date.end=NOW/MONTH/DAY%2B3MONTHS&facet.date.gap=%2B3MONTHS

+++

### Last 7 Days (Raw Query Params)

|name|value|
|---|---|
|facet.date|time|
|facet.date.start|NOW/DAY-7DAYS|
|facet.date.end|NOW/DAY+1DAY|
|facet.date.gap|+1DAY|

    &facet.date=time&facet.date.start=NOW/DAY-7DAYS&facet.date.end=NOW/DAY%2B1DAY&facet.date.gap=%2B1DAY

---

### Combining Search with a Date Facet

|name|value|
|---|---|
|q          | `statistics_type:search` |   
|start      | `0` |
|rows       | `0` |
|facet      | `true` |

    &facet.date=time&facet.date.start=NOW/MONTH/DAY-12MONTHS&facet.date.end=NOW/MONTH/DAY%2B1MONTH&facet.date.gap=%2B1MONTH

+++

### Combining Search with a Date Facet

|name|value|
|---|---|
|q          | `statistics_type:view` |   
|start      | `0` |
|rows       | `0` |
|facet      | `true` |

    &facet.date=time&facet.date.start=NOW/MONTH/DAY-12MONTHS&facet.date.end=NOW/MONTH/DAY%2B1MONTH&facet.date.gap=%2B1MONTH

+++

### Complex Queries - NOT Syntax

|name|value|
|---|---|
|q | `NOT(statistics_type:*)` |   

+++

### Complex Queries - NOT Syntax

|name|value|
|---|---|
|q | `NOT(type:*)` |   

+++

### Complex Queries - AND Clause

|name|value|
|---|---|
|q | `NOT(type:*) AND scopeType:3` |   

+++

### Complex Queries - RANGE Query

|name|value|
|---|---|
|q | `NOT(type:*) AND scopeType:[3 TO 4]` |   

+++

### Complex Queries - DATE RANGE QUERY

|name|value|
|---|---|
|q | `NOT(type:*) AND time:[NOW-7MONTHS TO NOW]` |   

---

### Our Custom Solr App

- DigitalGeorgetown
  - DSpace has collected 12 million records over the past 7 years
  - Stats Queries are relatively fast considering the volume

+++

### Sample Application Built With Solr Queries

- Statistics Reporting Tool
  - PHP Application for Repository Admins
  - Supplements statistics reports in DSpace
  - Additional bot filtering via Solr queries
  
+++  
### Demo: DigitalGeorgetown Statistics Reporting Tool   

![DigitalGeorgetown Statistics Reporting Tool](https://www.youtube.com/embed/VL3S2BmvXSU)

+++?code=https://raw.githubusercontent.com/Georgetown-University-Libraries/batch-tools/master/web/stats/solrFacets.php&lang=php
@[16-20](Date Query Construction)
@[21-25](Date Query Construction)
@[44-55](Queries based on DSpace Hierarchical Levels)
@[64-71](Distinguishing Downloads from Thumbnail Views)
@[72-83](Distinguishing full text and faceted searches)

---
### Working with a different Solr Repository





---
### Schema Browser
Each DSpace instance contains at least 3-4 separate Solr instances.  The presentation will take a brief tour of the DSpace "search" repository illustrating how the lessons learned from the statistics repository could be applied to a Solr repository with a different schema.
