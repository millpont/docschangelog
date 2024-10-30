---
description: V1.0 July 2, 2024
---

# QC Requirements & Protocol

## 1. **Introduction**

This document outlines the requirements to be considered a Qualified Custodian (QC) for METI Originate. It also details the protocol for transferring environmental attribute data from participating QCs to METI for the purposes of requesting Spatiotemporal Claim Identifiers (SCIDs) and generating Environmental Attribute Certificates (EACs).&#x20;

## **2. Qualified Custodian Entity Guidelines**

As a Qualified Custodian, the custodial party will adhere to the following guidelines:

* **Account Creation**: A Qualified Custodian requests, and upon METI Administrator approval, creates an account in METI Originate. The METI Administrator will validate all information submitted during registration.
* **Detailed Reporting**: Reported data should be detailed enough to (i) identify the amount, type and methods for underwriting the environmental benefits generated by the project or activities overseen and or administered by the QC. And (ii) establish a clear, non-repudiated chain of custody and legal entitlement to the environmental claims affiliated with project or activities. &#x20;
* **Data Reliability**: Reported data should be inherently reliable and fully auditable, down to field-level for agricultural land management-based projects.
* **Data Quality**: Reported data should be financial settlement quality, adhering to highest industry standards such as those specified by ISO, PCF, GHGP, VCI, and SBTi.&#x20;
* **Data Submission**: QCs should submit data to METI as agreed upon in Terms of Use, and or, on behalf of METI Account Holder that designated them as the QC for their registered projects or activities.
* **Data Aggregation**: Aggregation is allowed if the projects share the same characteristics as long as QC maintains a robust identification program that contains reasonable procedures to verify the identity of any individuals and common ownership down to field-level. Relevant records should be maintained and made available to Administrator upon request.&#x20;
* **Independent Functioning**: If the QC also functions in other capacities, it must demonstrate independence in its custodial functions in accordance with the [International Chamber of Commerce Guidelines on Conflicts of Interest in Enterprises](https://iccwbo.org/wp-content/uploads/sites/3/2018/08/icc-conflicts-of-interest-guidelines-july-2018.pdf).&#x20;
* **Validation and Verification**: Projects will adhere to regular internal and external validation and verification procedures, which may include:
  * Third Party Verification and Validation
  * Digital Measuring, Monitoring, and Verification audit trails&#x20;
* **Audit and Verification Reports**: Upon request, QCs will provide METI Administrators, and or a mutually agreed upon and qualified independent third party, with audit and verification reports, which may include:
  * Contractual Documentation
  * Environmental Benefit Quantification & Calibration Protocols
  * Data System Integrity Validation
  * Internal Audit Process
  * Third Party Reports
  * Annual Audit Results from Relevant Authorities

## **3. Qualified Custodian Entity Candidates**

Candidates for QC in METI may include but are not limited to:

* Project Developers&#x20;
* Conservation Program Administrators (pay for practices or outcomes)
* NGOs
* MRV Providers&#x20;
* Carbon Management Platforms or Marketplaces
* Registries&#x20;
* Commodity Traders and Cooperatives&#x20;
* Climate-Smart Commodity Merchandisers or Certifiers&#x20;
* Biofuel Certification Bodies&#x20;
* Vertically Integrated Food, Fuel and Fiber Companies&#x20;
* Sustainability Solution Providers&#x20;

## **4. Data Protocol**&#x20;

#### Basic SCID Request Data Elements&#x20;

| Field Name      | Type   | Description                                                        | Example Value                                                                                                                                                                                                        |
| --------------- | ------ | ------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type            | string | The type of the claim, must be "Feature".                          | "Feature"                                                                                                                                                                                                            |
| properties      | object | Detailed properties of the claim.                                  | See below                                                                                                                                                                                                            |
| geometry        | object | Geographical information in GeoJSON format.                        | See below                                                                                                                                                                                                            |
| contractStart   | string | The start date and time of the contract.                           | "2019-10-14T15:30:00Z"                                                                                                                                                                                               |
| contractEnd     | string | The end date and time of the contract.                             | "2025-10-14T15:30:00Z"                                                                                                                                                                                               |
| attribute       | string | The type of environmental attribute (e.g., carbon).                | "carbon"                                                                                                                                                                                                             |
| type (geometry) | string | The type of GeoJSON object, must be "Polygon".                     | "Polygon"                                                                                                                                                                                                            |
| coordinates     | array  | Coordinates defining the polygon in \[longitude, latitude] format. | \[\[\[-96.27745937013486,45.152922799410504], \[-96.27745937013486,45.14703051688835], \[-96.26748864422862,45.14703051688835], \[-96.26748864422862,45.152922799410504], \[-96.27745937013486,45.152922799410504]]] |

#### Example JSON

Here is how the example JSON would look:

```json
{
  "type": "Feature",
  "properties": {
    "contractStart": "2019-10-14T15:30:00Z",
    "contractEnd": "2025-10-14T15:30:00Z",
    "attribute": "carbon"
  },
  "geometry": {
    "type": "Polygon",
    "coordinates": [
      [
        [-96.27745937013486, 45.152922799410504],
        [-96.27745937013486, 45.14703051688835],
        [-96.26748864422862, 45.14703051688835],
        [-96.26748864422862, 45.152922799410504],
        [-96.27745937013486, 45.152922799410504]
      ]
    ]
  }
}
```

#### Explanation:

* **type**: The type of the claim, must be "Feature".
* **properties**: Detailed properties of the claim.
* **geometry**: Geographical information in GeoJSON format.
* **contractStart**: The start date and time of the contract.
* **contractEnd**: The end date and time of the contract.
* **attribute**: The type of environmental attribute (e.g., carbon).
* **type**: The type of GeoJSON object, must be "Polygon" following the [IETF specification](https://datatracker.ietf.org/doc/html/rfc7946).
* **coordinates**: Coordinates defining the polygon in \[longitude, latitude] format.

#### Basic EAC Issuance & Distribution Data Table

<table><thead><tr><th width="247">Field Name</th><th width="154">Type</th><th>Description</th><th>Example Value</th></tr></thead><tbody><tr><td><code>SCID</code></td><td><code>string</code></td><td>Unique Spatiotemporal Claim ID or IDs for the EAC</td><td><code>"YOUR SCID HERE"</code></td></tr><tr><td><code>commodityCode</code></td><td><code>string</code></td><td>Code representing the type of commodity. </td><td><code>"ZC"</code></td></tr><tr><td><code>allocableBenefit</code></td><td><code>number</code></td><td>Total benefit that can be allocated, expressed as a numerical value.</td><td><code>1250.5</code></td></tr><tr><td><code>vintage</code></td><td><code>integer</code></td><td>Year of issuance or validity of the benefit.</td><td><code>2023</code></td></tr><tr><td><code>verifiedBenefit</code></td><td><code>boolean</code></td><td>Indicates whether the benefit has been verified.</td><td><code>true</code></td></tr><tr><td><code>allocations</code></td><td><code>array</code></td><td>List of allocations detailing how the benefit is distributed among beneficiaries.</td><td>See sub-table below</td></tr><tr><td><strong>Sub-fields in <code>Distributions</code></strong></td><td></td><td></td><td></td></tr><tr><td><code>beneficiary</code></td><td><code>string</code></td><td>Identifier for the beneficiary receiving the allocation.</td><td><code>"beneficiary-corp-001"</code></td></tr><tr><td><code>proportionAllocated</code></td><td><code>number</code></td><td>Proportion of the total benefit allocated to this beneficiary, expressed as a decimal.</td><td><code>0.75</code></td></tr></tbody></table>

#### Example of `allocations` Sub-Table

| **Beneficiary**          | **Proportion Allocated** |
| ------------------------ | ------------------------ |
| `"beneficiary-corp-001"` | `0.75`                   |
| `"beneficiary-corp-002"` | `0.25`                   |

#### Complete Example JSON

```json
{
  "allocableBenefit": 1250.5,
  "allocations": [
    {
      "beneficiary": "beneficiary-corp-001",
      "proportionAllocated": 0.75
    },
    {
      "beneficiary": "beneficiary-corp-002",
      "proportionAllocated": 0.25
    }
  ],
  "claimId": "YOUR CLAIM ID HERE",
  "commodityCode": "ZC",
  "verifiedBenefit": true,
  "vintage": 2023
}
```

#### Explanation:

* **claimId**: This is a unique identifier for the claim, which is used to reference the specific benefit being issued.
* **commodityCode**: This represents the type of commodity, such as "ZC" for a specific type of environmental attribute.&#x20;
* **allocableBenefit**: This indicates the total benefit amount available for allocation.
* **vintage**: This is the year when the benefit is issued or becomes valid.
* **verifiedBenefit**: A boolean field indicating whether the benefit has been verified (true) or not (false).
* **allocations**: This is an array of objects detailing how the benefit is distributed among various beneficiaries. Each allocation specifies a beneficiary and the proportion of the total benefit they receive.

## **5. Data Integration**

Data will be integrated with METI via APIs or via front-end using a valid QC login and password. Only QCs and the Administrator can integrate environmental attribute datasets to METI.

**SCID Certificate Request Procedure**:

1. Log into METI Originate.
2. Locate the SCID Request module, and or navigate to API documentation tab for automated and programmatic bulk requests workflows.
3. Select the “Request SCID Certificate” button to upload one or more GeoJSON (other shapefiles will be converted to GeoJSON upon ingestion) and input temporal and attribute specific data.
4. Select the “Request” button to request SCIDs and initiate the review process.&#x20;
5. METI's proprietary algorithms evaluate SCID requests for conflict across existing SCIDs and data platform integrations. Routine conflict analysis is conducted for continual monitoring of SCID integrity and status.&#x20;
6. Administrators issue eligible SCID Certificates to QC's account.&#x20;

**EAC Issuance and Distribution Procedure:**

1. Log into METI Originate&#x20;
2. Locate the EAC Issuance module, and or navigate to the API documentation tab for automated and programmatic bulk issuance workflows.
3. Select the "EAC Issuance" button to select on or more SCIDs to include in the issuance tranche.
4. Then, select and input the affiliated environmental attribute data to convey claim rights of specific environmental benefits to the EAC.&#x20;
5. Issue the EAC to a holding account, and or transfer and allocate to one or more Beneficiaries via 1 of 3 (or a combination thereof) distribution models described in the METI Originate Fact Sheet.&#x20;

Data can be reloaded/updated multiple times, following specific rules regarding data status and validation. Validation ensures data accuracy before it is written to the METI database. Notifications will be sent to QC Account Holders regarding the status of their data.

**Validation Checks**:

* **Entity Validation**: Ensures the custodial entity is authorized to report data for the project.
* **Data Format Validation**: Validates the data formats for consistency, efficiency and scalability of METI Services.
* **Spatial, Temporal and Attribute Check**: Ensures no gaps or overlaps in custodial claims.
* **Aggregation Handling**: Processes data for units sharing common ownership appropriately.

If validation fails, the reporting entity receives a warning but may proceed with data submission, which will remain in a pending state until reviewed, approved and or rejected by the METI Administrator.