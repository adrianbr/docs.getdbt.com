---
title: "GraphQL"
id: sl-graphql
description: "Integrate and use the GraphQL API to query your metrics."
tags: [Semantic Layer, APIs]
---

<VersionBlock lastVersion="1.5">

import LegacyInfo from '/snippets/_legacy-sl-callout.md';

<LegacyInfo />

</VersionBlock>


[GraphQL](https://graphql.org/) (GQL) is an open-source query language for APIs. It offers a more efficient and flexible approach compared to traditional RESTful APIs. 

With GraphQL, users can request specific data using a single query, reducing the need for many server round trips. This improves performance and minimizes network overhead.

GraphQL has several advantages, such as self-documenting, having a strong typing system, supporting versioning and evolution, enabling rapid development, and having a robust ecosystem. These features make GraphQL a powerful choice for APIs that prioritize flexibility, performance, and developer productivity.

dbt Partners can use the Semantic Layer GraphQL API to build and integration with the dbt Semantic Layer.

## dbt Semantic Layer GraphQL API

The dbt Semantic Layer GraphQL API allows you to explore and query metrics and dimensions. Due to it's self-documenting nature, you can explore the calls conveniently through the [schema explorer](https://cloud.getdbt.com/semantic-layer/api/graphql). 

## Using the GraphQL API

If you are a dbt user or partner with access to dbt Cloud and the Semantic Layer, you can setup and test this API in your oown instance by configuring the Semantic Layer and obtaining the right GQL onnection parameters provided. (PROVIDE link to set up?) 

### Authentication 

Authentication uses a dbt Cloud Service token passed through a header as follows. To explore the schema, you can enter this information in the "header" section.

```
{"Authorization": "Bearer <SERVICE TOKEN>"}
```

Each GQL request also comes with a dbt Cloud Environment Id. Our API will use the combination of the Service Token in the header and Environment Id to authenticate.


### Metric metadata calls

Use the following example calls to provide you with an idea of the types of commands you can use:

**Fetch available metrics**

```graphql
metrics(environmentId: Int!): [Metric!]!
```

**Fetch available dimensions for metrics**

```graphql
dimensions(
environmentId: Int!
metrics: [String!]!
): [Dimension!]!
```

**Fetch available time granularities given metrics**

```graphql
queryableGranularities(
environmentId: Int!
metrics: [String!]!
): [TimeGranularity!]!
```

**Fetch available metrics given a set of a dimensions**

```graphql
metricsForDimensions(
environmentId: Int!
dimensions: [String!]!
): [Metric!]!
```

**Fetch dimension values for metrics and a given dimension**

```graphql
dimensionValues(
environmentId: Int!
metrics: [String!]!
dimension: String!
```

### Metric value query parameters

The mutation is `createQuery`. The parameters are as follows:

```graphql
createQuery(
environmentId: Int!
metrics: [String!]!
dimensions: [String!] = null
limit: Int = null
startTime: String = null
endTime: String = null
where: String = null
order: [String!] = null
): String
```
