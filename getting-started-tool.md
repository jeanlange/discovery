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

# Getting started with the tooling

In this short tutorial, we introduce the {{site.data.keyword.discoveryshort}} tooling and go through the process of creating a private data collection and searching it.
{: shortdesc}

## Before you begin

Before beginning with the {{site.data.keyword.discoveryshort}} service, you will need:

- Content to upload - Don't have any? Download the four documents here:

    <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>,
    <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>,
    <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>,
    <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>.

- A document that is representative of the ones you are going to upload to the service. You can use <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a> if you're using the provided example documents.

- To create an instance of the {{site.data.keyword.discoveryshort}} service:

  You create your {{site.data.keyword.watson}} services through {{site.data.keyword.Bluemix}}, so you need a free {{site.data.keyword.Bluemix_notm}} account to get started. ({{site.data.keyword.Bluemix_notm}} is IBM's cloud platform. For details, see [What is Bluemix?](https://console.ng.bluemix.net/docs/overview/whatisbluemix.html){: new_window})

  1.  Go to the [{{site.data.keyword.discoveryshort}} service ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window} on {{site.data.keyword.Bluemix_notm}} and either sign up for a free account or log into your {{site.data.keyword.Bluemix_notm}} account.

  1.  Choose your plan (Lite, Standard, or Advanced). See the [{{site.data.keyword.discoveryshort}} service ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window} for details. (Your original source files do not count against your file size limit.) To start, you could choose the free `Lite` plan. You can create a paid instance later.

  1.  Type `discovery-tutorial` in the **Service name** field, click **Create**.      

## Step 1: Launch the tooling

After you create the service instance, you'll land on the dashboard for the instance. Launch the {{site.data.keyword.discoveryshort}} tooling from here.

Click **Manage**, then **Launch Tool**.

![Launch the tooling](images/bm-launch-tool.png)

## Step 2: Create a collection
Your first step in the {{site.data.keyword.discoveryshort}} tool is to create a data collection.

A collection is a set of your documents. *Why would I want more than one collection?* There are a few reasons, including:

  -   You may want multiple collections in order to separate results for different audiences
  -   The data may be so different that it doesn't make sense for it all to be queried at the same time

The public, pre-enriched {{site.data.keyword.discoverynewsshort}} data collection is also available for your use. It is ready-to-query and you can begin to create queries on it immediately. You cannot adjust its configuration or add documents to {{site.data.keyword.discoverynewsshort}}.

1.  Click the icon on the upper right ![Cog](images/icon_settings.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> and choose **Create environment**. The environment is created based on the Bluemix plan you selected earlier. The status of your environment is always available from this drop-down.

1.  Once your environment is ready, the **Name your new collection** dialog appears. Name your collection and choose **Default Configuration** from the **Select a configuration to apply** drop-down (we can change the configuration later).

## Step 3: Create a custom configuration

1.  After your collection has been created, you could immediately start uploading content using the upload area at the right of the screen, but we want to create and test a custom configuration. To do so, click **Switch** next to the collection name and choose **Create a new configuration**. Name your configuration and click **Create**.

1.  Once you have created your configuration, you will be able to customize it. Before you start changing settings, you should upload the sample document that you identified at the start of this task (<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a> if you are using the examples and don't feel like scrolling back up). Use the **Upload Sample Documents** panel on the right side of the screen to upload the example document. Click on the document name link that appears after the example document has been uploaded to view the current transformation.

1.  Now it's time to adjust the configuration. For this task, you will change the enrichment that are applied to each document.

    *  Click on the **Enrich** section of the configuration. Look at the generated JSON to the right of the screen. Scroll down to the *enriched_text* section and notice that it contains many *concepts*.
    *  Next, remove the text enrichment named *concept* by clicking the **X** next to it and then click **Apply & Save**.
    *  Finally, look at the JSON again. Notice how the output has changed and no longer includes *concepts*.

    Repeat this process to customize the conversion to your exact requirements.

## Step 4: Upload your documents

Once you are happy with the custom conversion of your sample document it's time to actually ingest the real content into your collection.

1.  Click on the file icon ![File icon](images/icon_yourData.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> in the top left of your screen and select your collection.

1.  Make sure the custom configuration you created is listed next to **Configuration**. If it isn't, click **Switch** next to the configuration name and select it.

1.  Go to **Add data to this collection** at the right of the screen and start uploading your documents.

    The document(s) that you uploaded as samples are not automatically uploaded. If you want them in your collection, you must upload them to here as well.

    If you are using the provided examples, upload: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>. Wait for them to upload. The **Documents available**, **Documents processing**, and **Documents failed** fields will let you know their status.

    The API information for this collection is listed on the left. You can use it to quickly build an application using the {{site.data.keyword.discoveryshort}} API. For more information, see the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/watson/developercloud/discovery/api/v1){: new_window}.

## Step 5: Build a query

1.  Once you have uploaded all your documents, you are ready to begin searching them. Click on the magnifying glass icon ![Query icon](images/icon_queryBuilder.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> to open the query page. Select your collection and click **Get started**.

1.  The **My data insights** screen will open. This screen displays the insights Watson discovered in your enriched documents. Each card displays the results of one enrichment. If you applied the default configuration to your collection, the following cards will display:

    -  **General sentiments** displays the percentage breakdown of documents tagged as positive, neutral, and negative discovered by the Sentiment Analysis enrichment.
    -  **Top entities** displays persons, places, and organizations discovered in your documents by the Entity Extraction enrichment.
    -  **Content hierarchy** displays the hierarchical taxonomies discovered in your documents by the Category Classification enrichment.
    -  **Related concepts** displays the concepts discovered in your documents by the Concept Tagging enrichment.

    **Note:** Starting on **18 July, 2017** {{site.data.keyword.discoveryfull}} introduced a new enrichment technology, named {{site.data.keyword.nlushort}} (NLU). See [Adding enrichments](/docs/services/discovery/building.html#adding-enrichments) for details. If you applied the **Default Configuration** to a collection prior to this date, that collection was enriched with the {{site.data.keyword.alchemylanguageshort}} enrichments. The insight cards in collections enriched with {{site.data.keyword.alchemylanguageshort}} enrichments will not update automatically.

    You can fine-tune the default insights by filtering on the **Type of enrichment** and **Term** in the **Filtering my data insights** panel on the left.

    To learn more about each enrichment see [Adding Enrichments](/docs/services/discovery/building.html#adding-enrichments).

    The **Top entities** and **Related concepts** insight cards display the number of documents each entity or concept can be found in. When you review the insight cards for the example documents, you will notice (among other things) that 75% of the documents in that collection have a positive sentiment, 25% have a negative sentiment; and that the top keywords are GMT, Oct, URL, APIs, and Celgene Corporation.

    These queries are ready-to-use as-is, or you can use them as a starting point for building your own queries. Click the **More options** icon on the top right of any card for two options:

    -  **Copy query URL** - Click here and you will copy the generated query. You can then use the query in your application.
    -  **Edit query** - Click here and you will open the **Build your own query** screen. The generated query will be displayed for editing. (If you want to return to the **My data insights** screen, click the **Close** button at the bottom.

1.  Click the **Build your own query** button to build and test queries. Under **Search for Documents**, click **Use the {{site.data.keyword.discoveryshort}} Query Language**, then:

    -  To search for results with entities named "IBM", enter `enriched_text.entities.text:IBM` in the **Enter query here** field, then click **Run Query**. - The query will return 4 results.
    -  To search for results with entities named "Watson", enter `enriched_text.entities.text:watson` in the **Enter query here** field, then click **Run Query**. - The query will return 3 results.
    -  To search for results with both entities named "Watson" and "Slack", enter `enriched_text.entities.text:watson,enriched_text.entities.text:Slack` in the **Enter query here** field, then click **Run Query** - The query will return 1 result.

    The results of your query will display in the **Results** section on the right. This section has two tabs - the **Summary** tab provides an overview of the query results; while the **JSON** tab displays the full JSON results. For the queries listed, the **Summary** will display the document passages (in order of relevance) first, followed by the names of the documents found, then the results by enrichment. **Passages** are short, relevant excerpts extracted from the full documents returned by your query.

    The **Query URL** link provided under the **JSON** tab is ready-to-use in your application.

    To learn more about the {{site.data.keyword.discoveryshort}} Query Language see [Building a Basic Query](/docs/services/discovery/using.html#building-a-basic-query). In addition, you can click on the **?** icons next to any of the **Enter query here** fields for more examples. Both filters (**Limit which documents you query**) and aggregations (**Include analysis of your results**) must be written in the {{site.data.keyword.discoveryshort}} Query Language.

    You can also click on the **Use natural language** button and write a natural language query, such as "IBM Watson partnerships". To learn more about natural language queries, see [Search parameters](/docs/services/discovery/query-reference.html#search-parameters).

    Watson can be trained to improve the results of natural language queries, see [Improving result relevance with the tooling](/docs/services/discovery/train-tooling.html).

## Next steps

Now you have a functioning and populated {{site.data.keyword.discoveryshort}} service instance. You can now begin customizing your collection by adding more documents and enrichments, and customizing conversion settings.
