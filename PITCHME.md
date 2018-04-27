## Examining Your Repository under the Hood from the Solr Admin Console

Terry Brady

Georgetown University Library

https://github.com/terrywbrady/info

![](https://www.library.georgetown.edu/sites/default/files/library-logo.png)

---
### Tour of the Admin Console
The Solr Admin Console can be intimidating to a new user.  Some actions available in the console could be destructive to a repository.  The presentation will provide a tour of the admin console and highlight the user-friendly components.  The majority of the presentation will focus on the Query tab of the console.
---
###Document Counts
The first step of the tutorial will be to query for all documents in the Solr repository (q=*:*).  We will review the documents that are returned and note the count of objects that are returned.  We will also note the named fields in each resulting document.  We will manipulate the start index and result count to vary the number of documents returned.  We will manipulate the field list parameter to alter the amount of data that is returned from the query.  We will also manipulate the output format for the query illustrating how to return JSON, XML, or CSV from the query.
---
###Query Construction
The next step of the tutorial will be construct a query on a text field, on a numeric field, and on a date field.  Once we have studied how to query on a single field, we will construct queries with AND, OR, and NOT.  Lastly, we will alter the sort options to change the order of the results.
---
###Result Faceting
The next step of the tutorial will be manipulate facet parameters to analyze the contents of the Solr repository.  In the example of the DSpace statistics repository, we will demonstrate how search facets can help to identify new bots and web crawlers. 
Solr provides powerful capabilities to facet values by date.  Using the sample repository data, we will analyze user activity over various time ranges.  The presentation will then demonstrate a DSpace statistics reporting dashboard constructed from numerous individual Solr queries.
---
###Schema Browser
The Solr Schema browser can also provide insight about the fields within a Solr repository.  We will take a brief look at this tab of the console and show how it can confirm some of our previous discoveries.
Looking at another Solr Repo
Each DSpace instance contains at least 3-4 separate Solr instances.  The presentation will take a brief tour of the DSpace “search” repository illustrating how the lessons learned from the statistics repository could be applied to a Solr repository with a different schema.
