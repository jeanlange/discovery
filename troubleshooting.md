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

# Troubleshooting

Troubleshooting tips for using the {{site.data.keyword.discoveryshort}} service.

If you encounter problems when using the {{site.data.keyword.discoveryshort}} service, try one or more of the following troubleshooting tips.

-   A document can fail to be ingested because of a type mismatch between data in the current document and similar data in a previously ingested document. For example, a field might be typed as a **date** in one document and a **string** in a subsequent document, preventing the subsequent document from being indexed correctly.

    The preview operation cannot predict type mismatches because it tests only a single document and does not keep a record of the conversion results.
-   Rapid or large-scale indexing of documents can sometimes result in the back-end search service restarting. If this occurs, contact {{site.data.keyword.IBM}} support for assistance.
