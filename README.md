# Dataplex

Dataplex is Google Cloud's intelligent data fabric that unifies distributed data across data lakes, data warehouses, and data marts. It provides centralized data management, governance, and discovery without moving or duplicating data.
Key capabilities:

🏗️ Organize data using Lakes → Zones → Assets hierarchy

🔍 Automatic metadata discovery and cataloging

✅ Data quality monitoring and validation

🔗 Data lineage tracking across BigQuery and Cloud Storage

🔐 Unified security and access control

This tutorial will guide you through setting up and using Dataplex to manage your data estate on GCP.

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















