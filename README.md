# Classification

As of ArcGIS Enterprise 11.4, you can [assign your organization a classification schema](https://enterprise.arcgis.com/en/portal/latest/administer/windows/configure-classification-schema.htm) that allows your members to classify items based on their level of sensitivity. Item classification helps organization members understand the extent of security and safeguarding an item warrants and thus can play a crucial role in protecting confidential and proprietary information. The following are examples of when item classification would be useful:

* Government agencies can classify sensitive items that, by law or regulation, can only be accessed by individuals with proper security clearance and incur criminal penalties if mishandled.

* Corporations and non-government organizations can classify items to protect trade secrets or conform with laws and regulations governing various situations such as privacy, legal proceedings, and the timing of financial information releases.

Before you can assign a classification schema to your organization, you must create it by defining the configuration options for the classification in a valid JSON file. This repository hosts simple and intermediate classification schema samples that you can use as a reference to create a classification schema that meets your organization's needs.

## Instructions

To create a classification schema using a schema sample as a reference, follow these steps:

1. Navigate to [simple classification schemas](https://github.com/ArcGIS/classification/tree/main/simple%20classification%20schemas) or [intermediate classification schemas](https://github.com/ArcGIS/classification/tree/main/intermediate%20classification%20schemas).
2. Click on a schema sample to preview it.
3. Click **Download raw file** in the top-right corner of the preview window.
4. Open the file in a text editor of your choice.
5. Use the sample as a reference and review [Item classification reference](https://developers.arcgis.com/rest/users-groups-and-items/classification-reference/) to create your classification schema.

## Requirements

The following is a list of requirements for assigning a classification schema to your organization:

* ArcGIS Enterprise 11.4
* Be a member of the default Administrator role or a custom role that includes the Organization website privilege

## Issues

Find a bug or want to request a new feature?  Please let us know by submitting an issue.

## Contributing

Esri welcomes contributions from anyone and everyone. Please see our [guidelines for contributing](https://github.com/esri/contributing).

## Licensing

Copyright 2024 Esri

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

A copy of the license is available in the repository's [license.txt](https://github.com/ArcGIS/classification/blob/main/LICENSE.txt) file.
