# Dataplex

Dataplex is Google Cloud's intelligent data fabric that unifies distributed data across data lakes, data warehouses, and data marts. It provides centralized data management, governance, and discovery without moving or duplicating data.

Key capabilities:

🏗️ Organize data using Lakes → Zones → Assets hierarchy

🔍 Automatic metadata discovery and cataloging

✅ Data quality monitoring and validation

🔗 Data lineage tracking across BigQuery and Cloud Storage

🔐 Unified security and access control

This tutorial will guide you through setting up and using Dataplex to manage your data estate on GCP.

I am using the same BQ table as in the previous tutorial [bq-data-masking-example](https://github.com/janaom/bq-data-masking-example).

- [Data Catalog](https://github.com/janaom/dataplex-tutorial/blob/main/README.md#data-catalog)

- [Entry details](https://github.com/janaom/dataplex-tutorial/blob/main/README.md#entry-details)

- [Data Profile](https://github.com/janaom/dataplex-tutorial/blob/main/README.md#data-profile)

- [Data Lineage](https://github.com/janaom/dataplex-tutorial/blob/main/README.md#data-lineage)

- [Glossaries](https://github.com/janaom/dataplex-tutorial/blob/main/README.md#glossaries)

- [Dataplex Lake/Zone Concept](https://github.com/janaom/dataplex-tutorial/blob/main/README.md#dataplex-lakezone-concept)

- [Data Quality](https://github.com/janaom/dataplex-tutorial/blob/main/README.md#data-quality)

- [Custom Aspect Types](https://github.com/janaom/dataplex-tutorial/blob/main/README.md#custom-aspect-types)

- [Example: Glossaries, Aspects, Terms](https://github.com/janaom/dataplex-tutorial/blob/main/README.md#example-glossaries-aspects-terms)

- [Example: Lakes, Zones](https://github.com/janaom/dataplex-tutorial/blob/main/README.md#example-lakes-zones)


# Data Catalog

Data Catalog in Dataplex provides a unified discovery platform that helps both technical and non-technical users quickly find and access data across the organization through searchable metadata. It ensures data quality consistency and regulatory compliance while reducing unnecessary costs, and enables organizations to trace data lineage to understand where data originated, how it was transformed, and who used it. Users can add rich text table descriptions, assign data stewards for metadata management, and establish clear ownership to improve trust and confidence in data assets. Additionally, Data Catalog integrates with Sensitive Data Protection to automatically identify and tag sensitive data using tag templates, centralizing governance and reducing search friction across the organization.

# Entry details
Here you can find all info about your data: Entry type; Platform; System; Creation time; Last modification time; Labels; Description; Contacts; Fully Qualified Name. Here is an example of the table users under dataset bq_data_masking_demo.

<img width="1903" height="828" alt="image" src="https://github.com/user-attachments/assets/a43e5cba-f53c-4d34-b330-e0f16b3698b5" />

Overview lets you provide additional description for the entry. Usage lets you see usage of the entry. Aspects lets you attach metadata to an entry.

<img width="1888" height="882" alt="image" src="https://github.com/user-attachments/assets/799608e0-af3a-406d-845c-fa4fc37d7c1e" />

The number of tags shows tags associated with columns in the table. In our case this table has 4 tags masking sensitive data.

<img width="1891" height="862" alt="image" src="https://github.com/user-attachments/assets/f65ec61d-57bc-4521-b9ae-445c4093ee65" />

# Data Profile

Dataplex Universal Catalog makes it easier to understand and analyze your data by automatically profiling your BigQuery tables.

Profiling is like getting a detailed health report for your data. It gives you key statistics, such as common values, how the data is spread out (distribution), and how many entries are missing (null counts). This information speeds up your analysis.

Data profiling automatically detects sensitive information and lets you set access control policies. It recommends data quality check rules to ensure your data stays reliable.

Here is an example of Data Profile of users table.

<img width="1886" height="890" alt="image" src="https://github.com/user-attachments/assets/62b991b6-b447-4992-9dbd-ae18a9da4ad1" />

# Data Lineage 

Data Lineage in Dataplex provides automated tracking of data flows across your Google Cloud environment. It visualizes how data moves between BigQuery tables, Cloud Storage buckets, and other GCP services, showing upstream sources and downstream consumers. This enables teams to understand data dependencies, assess the impact of schema changes, ensure compliance, and troubleshoot data quality issues by tracing data back to its origin.

![20260202_173055](https://github.com/user-attachments/assets/0a17f706-3bc1-4e62-ade0-fc0a2616942a)


In this example, I created additional tables and joined them to demonstrate data lineage and trace data origins. On the right, you can see the BigQuery queries used to join these tables. Here is an example:

```sql
CREATE OR REPLACE TABLE `elt-project-482220.bq_data_masking_demo.users_with_purchases` AS
SELECT 
  u.id, 
  u.first_name, 
  u.last_name, 
  p.item, 
  p.amount, 
  p.purchase_date
FROM `elt-project-482220.bq_data_masking_demo.users` AS u
INNER JOIN `elt-project-482220.bq_data_masking_demo.user_purchases` AS p 
  ON u.id = p.user_id;
```

You can also view detailed information about each table, filter connections by column name, and use upstream/downstream directions with time range filters.

# Glossaries

Use a business glossary to establish a standardized vocabulary for your data assets, which reduces ambiguity and improves data discovery and governance across your organization. By creating a common language for data using Dataplex Universal Catalog business glossary, you can achieve the following:

Define a clear hierarchy of business categories and terms.

Link concepts using synonyms and show relationships between terms.

Search for data resources based on business concepts, not just technical names.

Dataplex Universal Catalog business glossary helps streamline data discovery and reduce ambiguity, resulting in better governance, more accurate analysis, and faster insights.

Here is an example of 'Customer Transaction Data Glossary'.

<img width="1868" height="943" alt="image" src="https://github.com/user-attachments/assets/828e8973-79a8-44b2-9508-93972420e9b9" />

When you connect terms to the tables, they appear in Related entries.

<img width="1889" height="913" alt="image" src="https://github.com/user-attachments/assets/935e67cd-d4c9-400b-9fc1-a91e611a3fea" />

And in Glossary Terms in table Details in Dataplex.

<img width="1875" height="849" alt="image" src="https://github.com/user-attachments/assets/3e2b8741-d4c8-46b0-b6b4-7ee68d5cd8a7" />

Business terms can also be connected under the table schema in Dataplex.

<img width="1898" height="728" alt="image" src="https://github.com/user-attachments/assets/a11a8826-ed46-4b41-a5c1-8157a491c539" />

# Dataplex Lake/Zone Concept

Dataplex organizes data using a hierarchical structure: Lakes contain Zones, and Zones contain Assets (data stored in BigQuery or Cloud Storage).

Lake: A lake is a logical domain that groups related data together based on business function, department, or data domain (e.g., "Customer Data Lake", "Finance Lake", "Marketing Lake"). Lakes provide:

    High-level organizational boundaries
    Centralized governance and access control
    A way to manage related datasets as a unified domain
    
Zone: Zones are subdivisions within a lake that organize data by processing stage, data quality level, or functional area. Common zone patterns include:

    Raw Zone - Ingested data in original format, unprocessed
    Curated Zone - Cleaned, validated, and transformed data
    Processed/Analytics Zone - Business-ready data for analytics and reporting

Zones can be either:

    Raw zones - contain unstructured or semi-structured data (typically Cloud Storage)
    Curated zones - contain structured, quality-controlled data (typically BigQuery tables)
    
Asset: Assets are the actual data resources (BigQuery datasets/tables or Cloud Storage buckets) attached to zones.

Benefits:

    Clear data lifecycle management (raw → curated → analytics)
    Consistent governance policies applied at lake or zone level
    Better data discovery and organization
    Simplified access control management

Lake `My data mesh` was created here as an example.

<img width="1791" height="317" alt="image" src="https://github.com/user-attachments/assets/e71ddb88-486c-49e3-a58b-76c3f5e79227" />

And then 2 Zones: Curated Zone for BQ dataset and Raw Zone for GCS bucket.

<img width="1852" height="783" alt="image" src="https://github.com/user-attachments/assets/c48b9d4a-9ead-4df5-9f70-e464c15b3171" />

There are options to see the details of the Zone and send alerts based on specific rules.

<img width="1873" height="880" alt="image" src="https://github.com/user-attachments/assets/0cd66b95-a08b-4904-84a5-2df5cd9f968b" />

# Data Quality

Dataplex Universal Catalog lets you define and measure the quality of the data in your BigQuery tables. You can automate the data scanning, validate data against defined rules, and log alerts if your data doesn't meet quality requirements. Auto data quality lets you manage data quality rules and deployments as code, improving the integrity of data production pipelines.

You can use predefined quality rules or build custom rules.

Dataplex Universal Catalog provides monitoring, troubleshooting, and Cloud Logging alerting that's integrated with auto data quality. More about Data Quality scans here.

Creating and using a data quality scan consists of the following steps:

    Define data quality rules
    Configure rule execution
    Analyze data quality scan results
    Set up monitoring and alerting
    Troubleshoot data quality failures
Here is an example where we scan users table. First, there is an option to schedule the scans.

<img width="1606" height="868" alt="image" src="https://github.com/user-attachments/assets/e4d764c5-cae6-4ae9-aa6c-8bfbc211118e" />

Then we have to configure validation rules. Use SQL to create your own rules or use built-in rule types.

<img width="1877" height="640" alt="image" src="https://github.com/user-attachments/assets/8fe46c4b-e461-44b2-bfaf-588d8de11b41" />

Here is an example of built-in rules.

<img width="1909" height="735" alt="image" src="https://github.com/user-attachments/assets/b3f1cd3b-19d6-4659-9c9d-2048e3b7a4ec" />

It is possible to export scan results to a BigQuery table, as well as receive notification reports via email.

<img width="1868" height="839" alt="image" src="https://github.com/user-attachments/assets/1c82c342-e0e1-44a8-8ad3-556d46f25ab2" />

All details and rules are visible inside the scan.

<img width="1899" height="902" alt="image" src="https://github.com/user-attachments/assets/c4c4c4c5-eb21-4330-a7b7-c2d6233fc9d6" />

Each scan is visible in Dataplex.

<img width="1889" height="543" alt="image" src="https://github.com/user-attachments/assets/723610ce-ef2b-4335-a917-169480f79cb7" />

Each job provides detailed results.

<img width="1892" height="935" alt="image" src="https://github.com/user-attachments/assets/28c32a40-9c58-4aba-8951-499cf3bc1ceb" />

Each scan is visible in the Dataplex Data Quality view for the table.

<img width="1876" height="838" alt="image" src="https://github.com/user-attachments/assets/ef42516c-a5bb-47a2-8e34-6e1a22566c07" />

Results are published in a BQ table as well.

<img width="789" height="775" alt="image" src="https://github.com/user-attachments/assets/27fa2796-0de6-4da9-bf71-f89c278940cc" />

And here is AutoDQ Email Report.

<img width="1475" height="767" alt="image" src="https://github.com/user-attachments/assets/95145d78-13a5-4e5b-89f7-06161e0dd097" />

# Custom Aspect Types

To create custom Aspects types, run these commands in your Cloud Shell terminal:

```
ACCESS_TOKEN=$(gcloud auth print-access-token)

curl --request POST \
  "https://dataplex.googleapis.com/v1/projects/your-project-id/locations/your-location/aspectTypes?aspectTypeId=data-stewardship-info" \   #e.g. location: europe-west1
  --header "Authorization: Bearer $ACCESS_TOKEN" \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --data '{
    "displayName": "Data Stewardship Information",
    "description": "Metadata related to data ownership and stewardship.",
    "metadataTemplate": {
      "name": "DataStewardshipTemplate",
      "type": "record",
      "recordFields": [
        {
          "name": "data_owner_email",
          "type": "string",
          "annotations": {
            "displayName": "Data Owner Email",
            "description": "Email address of the data owner."
          },
          "index": 1,
          "constraints": { "required": true }
        },
        {
          "name": "steward_team",
          "type": "string",
          "annotations": {
            "displayName": "Stewardship Team",
            "description": "Team responsible for data stewardship."
          },
          "index": 2
        },
        {
          "name": "last_reviewed_date",
          "type": "datetime",
          "annotations": {
            "displayName": "Last Reviewed Date",
            "description": "Date when the data asset was last reviewed for governance."
          },
          "index": 3
        }
      ]
    }
  }' \
  --compressed
```

You will create a new Aspect type.

<img width="1903" height="676" alt="Screenshot 2026-02-19 171807" src="https://github.com/user-attachments/assets/27fa0d90-81fa-48a7-9fb4-5cbd20d369ed" />

Check Template inside the details.

<img width="1912" height="779" alt="Screenshot 2026-02-19 171821" src="https://github.com/user-attachments/assets/3439095d-234c-449e-a5b7-73937e1942a5" />

# Example: Glossaries, Aspects, Terms

Here is an example demonstrating how elements connect within Dataplex.

![20260219_213521](https://github.com/user-attachments/assets/db808f8c-d3a9-4f78-bf88-eb17f7e01ccd)

Within the Dataplex Business Glossary, we have established the 'Financial Transaction Data Glossary'. This glossary is organized into two primary categories (or sub-glossaries):

    'Raw Financial Transaction Data - Source System Layer'
    'Transformed Financial Transaction Data - Analytics Layer'

<img width="1906" height="849" alt="Screenshot (183)" src="https://github.com/user-attachments/assets/87b322ad-00b4-4dbd-9757-af61cfefa884" />

<img width="1896" height="860" alt="Screenshot (184)" src="https://github.com/user-attachments/assets/72b7f3dd-7bf4-417a-a6d5-957dafaedb69" />

The first one focuses on the raw data. You can see all the fields (terms) pulled directly from that source table, like ID1 and String1.

<img width="1898" height="844" alt="Screenshot (185)" src="https://github.com/user-attachments/assets/f01d1bac-8d90-4ad6-8a1f-fdf5e95ccd7d" />

We use dbt for data transformation. Following this process, the second category reflects a new table created from the raw data.

<img width="1898" height="847" alt="Screenshot (186)" src="https://github.com/user-attachments/assets/5b061139-160b-4468-9a64-86defd559d45" />

When examining any specific term, you will find detailed information: a description, an overview, attached Aspects (like my 'Data Stewardship Info'), related entries, and related terms. For example, a term in the transformed layer is linked as a 'Related Term' to its corresponding field, such as ID1, in the raw data.

<img width="1899" height="852" alt="Screenshot (187)" src="https://github.com/user-attachments/assets/fa8eeada-e13c-4a40-93e1-db3d6a0583f1" />

Next, we will see the transformed data table.

<img width="1898" height="751" alt="Screenshot (188)1" src="https://github.com/user-attachments/assets/9d14d63a-e996-44a6-8fb8-fbc1f60f51b7" />

As you can see here, the asset is enriched with critical governance information. Here you can see who is data governor, business owner, data classification, data lifecycle, if it's encrypted, has PII, data owner email, etc.

<img width="1889" height="848" alt="Screenshot (189)1" src="https://github.com/user-attachments/assets/b0b5dc5b-b280-4865-91ba-6783ca14441a" />

Additionally, the Glossary Terms panel illustrates the direct semantic connections, showing exactly which business terms are mapped to this particular table.

<img width="1884" height="719" alt="Screenshot (190)1" src="https://github.com/user-attachments/assets/af1ceb1d-0dc7-42d2-9305-6622a62a3edf" />

# Example: Lakes, Zones

![20260219_223005](https://github.com/user-attachments/assets/6916d852-023a-4714-887f-ccc1b30b2a56)

Under the Manage tab in Dataplex, I have configured one Data Lake containing two distinct assets.

<img width="1905" height="304" alt="Screenshot (191)1" src="https://github.com/user-attachments/assets/d91f3a3b-eae5-45c6-81a5-32367a86a721" />

This Data Lake is segmented into two Zones:

    bq-data-prod: A curated zone designed for a BigQuery dataset.
    raw-data-gcs: A raw zone designated for a Cloud Storage (GCS) bucket.

<img width="1901" height="699" alt="Screenshot (192)1" src="https://github.com/user-attachments/assets/dcf89a9f-9bd2-4491-844b-c0620534626c" />

The details view aggregates metrics from both zones, such as the total discovered file size.

<img width="1895" height="761" alt="Screenshot (193)1" src="https://github.com/user-attachments/assets/e05884aa-8cfd-439e-93c4-2ebe0955218d" />

Within each zone, specific assets are registered. For example, the bq-data-prod curated zone contains the BigQuery dataset named fin-data-prod.

<img width="1904" height="709" alt="Screenshot (194)1" src="https://github.com/user-attachments/assets/e6257a2b-9b03-4e27-a29b-1c6cdae72ca5" />

This view also displays the discovery configuration and status, showing that 10,000 rows have been discovered in this asset.

<img width="1827" height="788" alt="Screenshot (195)1" src="https://github.com/user-attachments/assets/08798254-7ce4-42c3-8565-6ec587e5c38c" />

Inside raw-data-gcs zone we have GCS bucket elt-prod.

<img width="1895" height="713" alt="Screenshot (196)1" src="https://github.com/user-attachments/assets/29f063fd-d007-47d5-b9b4-3eec3d77375f" />

Similarly, the raw-data-gcs zone contains the GCS bucket elt-prod, with a discovered data size of 718.72KiB.

<img width="1718" height="789" alt="Screenshot (197)1" src="https://github.com/user-attachments/assets/40e6d254-6e04-4db8-be81-bf296a48e1c6" />

**Important Requirement**: All components of a Dataplex, including the Data Lake, its Zones, and the underlying data assets, must share the same  location. Discovery will fail if you attempt to link an asset from a different region; for example, a Data Lake set to europe-west1 cannot ingest or discover data from a bucket residing in a different EU location.

