---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Building queries and delivering content

The {{site.data.keyword.discoveryfull}} service offers powerful content search capabilities. Once your content is uploaded and enriched by the {{site.data.keyword.discoveryshort}} service, you can build queries, then integrate {{site.data.keyword.discoveryshort}} into your own projects, or create a custom application by using the {{site.data.keyword.watson}} Explorer Application Builder.
{: shortdesc}

  The queries you write will vary by collection, because all collections contain unique content. The examples given here will return results from the example {{site.data.keyword.IBM_notm}} Press Release collection and the {{site.data.keyword.discoverynewsshort}} collection. These queries should help you get started building your own queries.
  {: tip}

When you create a query or filter, {{site.data.keyword.discoveryshort}} looks at each result and tries to match the paths you have defined. When matches occur, they are added to the results set. When creating a query, you can be as vague or as specific as you want. The more specific the query, the more targeted the results. You have the option to turn on passage retrieval with the **Include relevant passages** radio button (found under **Customize display options**). Passages are short, relevant excerpts extracted from the full documents returned by your query. These targeted passages are extracted from the `text` fields of the documents in your collection. A maximum of three passages of no more than 2,000 characters each will be returned per relevant document, and no more than 10 passages total will be returned (the number of passages returned cannot be changed). The `passages` parameter is only available for private collections; it is not available in the {{site.data.keyword.discoverynewsshort}} collection.

These example queries are built using the {{site.data.keyword.discoveryshort}} tooling. If you'd like to use the API instead, add the query parameters to your API call. For more information and examples, see the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}.

## Before you begin

**Complete the steps in [Getting started](/docs/services/discovery/getting-started-tool.html).** If you haven't completed the **Getting started**, go to the **Your data** screen, create a new collection, and add these four documents to it (use the **Default Configuration**): <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>

## Building a basic query

Start out by getting to know the {{site.data.keyword.discoveryshort}} JSON. To understand how to build a query using the {{site.data.keyword.discoveryshort}} Query Language, you need to be familiar with the JSON produced by {{site.data.keyword.discoveryshort}} after it enriches the documents in your collection.

You can also write natural language queries (such as "IBM Watson partnerships") in the {{site.data.keyword.discoveryshort}} tooling. This tutorial focuses on how to write structured queries because even if you write your document query in natural language, both filters and aggregations must be written in the {{site.data.keyword.discoveryshort}} Query Language. To learn more about natural language queries, see [Search parameters](/docs/services/discovery/query-reference.html#search-parameters).
{: tip}

1.  On the **Your data** screen, choose the collection that contains the {{site.data.keyword.IBM_notm}} Press Releases.

1.  Click **Query this collection**. The **My data insights** screen will display some of the insights Watson discovered in your enriched documents. You can review them to get an overview of the insights in this collection.

    -  **Top keywords** displays the most important topics in your documents, discovered by the Keyword Extraction enrichment.
    -  **General sentiments** displays the percentage breakdown of documents tagged as positive, neutral, and negative discovered by the Sentiment Analysis enrichment.
    -  **Top entities** displays persons, places, and organizations discovered in your documents by the Entity Extraction enrichment.
    -  **Content hierarchy** displays the hierarchical taxonomies discovered in your documents by the Category Classification enrichment.
    -  **Related concepts** displays the concepts discovered in your documents by the Concept Tagging enrichment.

       **Note:** Starting on **18 July, 2017** {{site.data.keyword.discoveryfull}} introduced a new enrichment technology, named {{site.data.keyword.nlushort}} (NLU). See [Adding enrichments](/docs/services/discovery/building.html#adding-enrichments) for details. If you applied the **Default Configuration** to a collection prior to this date, that collection was enriched with the {{site.data.keyword.alchemylanguageshort}} enrichments. The insight cards in collections enriched with {{site.data.keyword.alchemylanguageshort}} enrichments will not update automatically.

       You can learn more about each insight by clicking on it, or click **More options** icon on the top right of any card to look at the query that returned those results, but now we want to look at the JSON.

1.  Now run an "empty" query. Click the **Build your own query** button, then **Run Query**. You can now see how each of the four documents was enriched with Watson insights. The results will be displayed on the right, under two tabs, **Summary** (an overview of the query results) and **JSON**. Start by opening the **JSON** tab.
    -  Each of the four documents will be proceeded by an `id` number.
    -  Scroll down to the `enriched_text` field. All of the enrichments applied to your documents with the **Default Configuration** file can be found here. Examine each enrichment to learn about the JSON fields you can query on.

       ![Default configuration fields](images/JSON.png)

    -  **entities** - Start by finding the `text` field, and examine the other enrichment information.
    -  **sentiment** - Start by finding the `label` field, and examine the other enrichment information.
    -  **concepts** - Start by finding the `text` field, and examine the other enrichment information.
    -  **categories** - Start by finding the `document` field, and examine the other enrichment information.

After you have examined the insights in the first document, you can look at the other three documents if you wish.

Once you are familiar with the JSON it will be easier to write queries in the {{site.data.keyword.discoveryshort}} Query Language.

### How to structure a basic query

As you have noticed, the JSON is hierarchical, so queries need to be written using that same hierarchy. So if your JSON looks like this:

```json
"enriched_text": {
  "concepts": [
    {
    "text": "Cloud computing",
    "relevance": 0.610029}
    ]
  }
```
{: codeblock}

Your query would be structured like this:

![Example query structure](images/query_structure2.png)

So to find the concept `Cloud computing` in your collection:

1.  Under **Search for Documents** click **Use the {{site.data.keyword.discoveryshort}} Query Language**. Enter `enriched_text.concepts.text:Cloud computing` into the **Enter query here** field. The delimiter in this query is `.` and the operator is `:`, see [Operators](/docs/services/discovery/query-reference.html#operators) to learn about other operators available in the {{site.data.keyword.discoveryshort}} Query Language.

1.  Click **Run query**. There should be one match (`"matching_results": 1`). Copy the **Query URL** at the top of the **JSON** tab to use in your application.

#### Additional example queries

-   `enriched_text.sentiment.document.label:positive` - Will return all documents that have a `positive` sentiment.

-   `enriched_text.entities.type:company` - Will return all documents that contain an entity of the type `company`

-   `enriched_text.categories.label::"health and fitness"` - Will return all documents in the `health and fitness` category. (The operator `::` specifies an exact match.)

-   `enriched_text.entities.text::Watson` - Will return all documents that contain the entity `Watson`. (The operator `::` specifies an exact match. By using an exact match we don't get false positives on similar entities, for example `Watson Health` and `Dr. Watson` would be ignored.)

-   `enriched_text.entities.text:IBM,enriched_text.entities.text:!Watson` - Will return all documents that contain the entity `IBM`, but not the entity `Watson` (The operator `:!` specifies "does not contain".)

Not sure when to query on an entity, concept, or keyword? See [Understanding the difference between Entities, Concepts, and Keywords](/docs/services/discovery/building.html#udbeck).

**Note:** When using the query builder, query highlighting is turned on by default. This will add a `highlight` field to your query results. Within the `highlight` field, the words that match your query will be wrapped in HTML `<em>` (emphasis) tags. See the [Query building reference](/docs/services/discovery/query-reference.html) for details.

Under **Customize display options**, you have the option to turn on passage retrieval with the **Include relevant passages** radio button. Passages are short, relevant excerpts extracted from the full documents returned by your query. These targeted passages are extracted from the `text` fields of the documents in your collection. A maximum of three passages of no more than 2,000 characters each will be returned per relevant document, and no more than 10 passages total will be returned (the number of passages returned cannot be changed). The `passages` parameter is only available for private collections; it is not available in the {{site.data.keyword.discoverynewsshort}} collection. See the [Query building reference](/docs/services/discovery/query-reference.html) for details.

## Building combined queries

You can combine query parameters together to build more targeted queries. This example uses both the `filter` and `query` parameters to return documents about {{site.data.keyword.IBM_notm}} acquisitions. In this example, the filter parameter will narrow down the results to only documents that mention `IBM`, and then the query parameter will return all results about `acquisitions`,in order of relevance. For more information about filtering vs. querying, see [Parameter descriptions and examples](/docs/services/discovery/query-reference.html#parameter-descriptions).

1.  On the **Your data** screen, choose the collection that contains the {{site.data.keyword.IBM_notm}} Press Releases.

1.  Click **Query this collection**, then **Build your own query**.

1.  Under **Limit which documents you query**, enter `enriched_text.entities.text:IBM` into the **Write a filter to narrow down your document set using the {{site.data.keyword.discoveryshort}} Query Language** field. This will narrow down the documents to only those that mention the entity `IBM`.

1.  Under **Search for Documents** click **Use the {{site.data.keyword.discoveryshort}} Query Language**. Enter `enriched_text.concepts.text:world wide web` into the **Enter query here** field. This will return all documents that include the concept of `world wide web`, and those documents will be ranked in order of relevance.

1.  Click **Customize display options**, then **Fields to return** and choose **Specify**. Select `text`. This will limit the response to the text of the relevant articles and exclude everything else.

1.  Click **Run query**. There will be one matching document: `"matching_results": 1`

### Additional example filters

When used in tandem with queries, filters execute first to narrow down the document set and speed up the query. Adding these filters in the **Write a filter to narrow down your document set using the {{site.data.keyword.discoveryshort}} Query Language** field will return unranked documents, and after that the accompanying query will run and return the results of that query ranked by relevance.

-   `enriched_text.sentiment.document.label:positive` - Will return only the documents in the collection with the `sentiment` of `positive`.

-   `enriched_text.entities::(relevance>0.8,text::IBM)` - Will return only the documents that contain the entity `IBM` with a relevance score above 80% for that entity.

## Building aggregations

Aggregation queries return a set of data values; for example, top keywords, overall sentiment of entities, and more. For the full list of aggregation options, see the [Aggregations table](/docs/services/discovery/query-reference.html#aggregations).

If you'd like to check out a few pre-built aggregations, all of the queries on the insight cards are aggregation queries. Click the **More options** icon on the top right of any card to view the query.
{: tip}

### How to structure an aggregation

![Example aggregation query structure](images/aggregation_structure.png)

This example aggregation will find all of the `concepts` in your collection.
The delimiter in this query is `.` and the operator is `()`, see [Operators](/docs/services/discovery/query-reference.html#operators) to learn about other operators available in the {{site.data.keyword.discoveryshort}} Query Language.

This example aggregation query will return the top 10 concepts in the collection of {{site.data.keyword.IBM_notm}} press releases.

1.  On the **Your data** screen, choose the collection that contains the {{site.data.keyword.IBM_notm}} Press Releases.

1.  Click **Query this collection**, then **Build your own query**.

1.  Under **Include analysis of your results**, enter `term(enriched_text.concepts.text,count:10)` into the **Write an aggregation query using the {{site.data.keyword.discoveryshort}} Query Language** field. `Term` will return the most common values for the `concepts` `text` field. `Count` specifies the number of results that you want returned.

1.  Click **Customize display options**, then enter `0` in the `Number of documents to return` field.

1.  Click **Run query**. The top 10 concepts will be displayed.

```json
{
    "matching_results": 4,
    "aggregations": [
        {
            "type": "term",
            "field": "enriched_text.concepts.text",
            "count": 10,
            "results": [
                {
                    "key": "Lotus Software",
                    "matching_results": 2
                },
                {
                    "key": "Power",
                    "matching_results": 2
                },
                {
                    "key": "Thomas J. Watson",
                    "matching_results": 2
                },
                {
                    "key": "Thomas J. Watson Research Center",
                    "matching_results": 2
                },
                {
                    "key": "2000 albums",
                    "matching_results": 1
                },
                {
                    "key": "Adverse drug reaction",
                    "matching_results": 1
                },
                {
                    "key": "Automobile",
                    "matching_results": 1
                },
                {
                    "key": "Business continuity planning",
                    "matching_results": 1
                },
                {
                    "key": "Chevrolet",
                    "matching_results": 1
                },
                {
                    "key": "Cloud computing",
                    "matching_results": 1
                }
            ]
        }
```
{: codeblock}

## Querying Watson Discovery News

{{site.data.keyword.discoverynewsshort}}, a public data set that has been pre-enriched with cognitive insights, is also included with {{site.data.keyword.discoveryshort}}. See [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html#watson-discovery-news) for more information about this collection.

You can query this collection using natural language queries, for example "IBM Watson partnerships", or the {{site.data.keyword.discoveryshort}} Query Language. On the **Build your own query** screen, under **Search for documents** choose either **Use natural language** or **Use the {{site.data.keyword.discoveryshort}} Query Language**. To learn more about natural language queries, see [Search parameters](/docs/services/discovery/query-reference.html#search-parameters).

- To learn more about natural language queries, see [Search parameters](/docs/services/discovery/query-reference.html#search-parameters).
- To learn more about the {{site.data.keyword.discoveryshort}} Query Language, see [Building queries and delivering content](/docs/services/discovery/using.html#building-queries-and-delivering-content)

The following example query returns the top 10 articles in {{site.data.keyword.discoverynewsfull}} about the Pittsburgh Steelers that have a positive sentiment.

1.  On the **Your data** screen, choose the {{site.data.keyword.discoverynewsshort}} collection.
1.  Click **Query this collection**, then **Build your own query**.
1.  Under **Search for documents**, click **Use the {{site.data.keyword.discoveryshort}} Query Language**, then enter `text:Pittsburgh Steelers, enriched_text.sentiment.document.label:positive` into the **Enter query here** field.
1.  Click **Customize display options**, then enter `10` (this is the default) in the `Number of documents to return` field.
1.  Click **Run query**. The top 10 articles about the Pittsburgh Steelers with a positive sentiment will be displayed.

### Additional example Watson Discovery News queries

-  `enriched_text.concepts.text:"Health care"` - Under **Search for documents**, click **Use the {{site.data.keyword.discoveryshort}} Query Language**, then enter this query. It will return all articles that include the concept of `health care`. If you specify a count, such as 50, in the **Number of documents to return** field you will receive the top 50 most relevant articles.

### Example Watson Discovery News aggregation

The following example aggregation returns the number of articles found in {{site.data.keyword.discoverynewsshort}} about the Pittsburgh Steelers by sentiment.

1.  On the **Your data** screen, choose the {{site.data.keyword.discoverynewsshort}} collection.
1.  Click **Query this collection**, then **Build your own query**.
1.  Under **Include analysis of your results**, enter `filter(text:"Pittsburgh Steelers").term(enriched_text.sentiment.document.label,count:3)` in the **Write an aggregation query using the {{site.data.keyword.discoveryshort}} Query Language** field.
1.  Click **Customize display options**, then enter `0` in the **Number of documents to return** field.
1.  Click **Run query**. The results will show the number of documents about the Pittsburgh Steelers and how many of those results have a `positive`, `negative`, or `neutral` sentiment.

### Additional example Watson Discovery News aggregation

```
filter(enriched_text.entities.text:twitter).term(enriched_text.sentiment.document.label,count:3)
```
{: codeblock}

If you enter this aggregation in the **Write an aggregation query using the {{site.data.keyword.discoveryshort}} Query Language** field, it will first narrow down (filter) the set of articles to only the ones that include the entities text of twitter, then divide those articles by the document sentiment types. Only the top 3 document sentiment types (`positive`, `negative`, `neutral`) will be returned.

Adding `nested` before an aggregation query restricts the aggregation to the area of the results specified. For example: `nested(text.entities)` means that only the `text.entities` components of any result are used to aggregate against. This effect can be seen easily by looking at the differences between the following two queries: `filter(text.entities.type::City)` - the aggregation counts the number of *Results* that contain one or more `entity` with the type `City` and `nested(text.entities).filter(text.entities.type::City)` - the aggregation counts the number of instances of an `entity` with the type `City` in the results.  Additionally, any subsequent operation will further restrict the result set that can be aggregated against. For example `nested(text.entities).filter(text.entities.type::City)` means that any only entities of `type::City` will be aggregated. For example: `nested(text.entities).filter(text.entities.type::City).term(text.entities.text,count:3)` will aggregate the top 3 entities of type `City`, Where as: `filter(text.entities.type::City).term(text.entities.text,count:3)` will return the top 3 entities where the result contains at least one entity of type `City`.

You cannot adjust the {{site.data.keyword.discoverynewsshort}} configuration, train, or add documents to {{site.data.keyword.discoverynewsshort}} collection. See a demo of what you can build with {{site.data.keyword.discoverynewsshort}} [here ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://discovery-news-demo.mybluemix.net/){: new_window}.
