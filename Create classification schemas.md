# Create classification schemas

Before you can assign a classification schema to your organization, you must create it by defining the configuration options for the classification in a valid JSON file. The classification schema you create must adhere to the classification grammar, a JSON schema included with Portal for ArcGIS that describes and validates classification schemas.  

Depending on your organization’s needs, you can create a simple schema that, at minimum, defines only the required properties or a complex schema that uses [Arcade expressions](https://developers.arcgis.com/arcade/) for highly detailed classification of items. See a complete example of a classification schema or download a sample schema from this repo

<br>

When creating a classification schema, start by defining the following properties: 

> ![Note](https://user-images.githubusercontent.com/31771293/225783213-2d4e69a4-035e-4126-b2aa-d2a864fa59b6.png)
>
> A property is optional unless specified otherwise.

> ![Note](https://user-images.githubusercontent.com/31771293/225783213-2d4e69a4-035e-4126-b2aa-d2a864fa59b6.png)
>
> Arcade expressions do not support **&lt;** and **&gt;** characters. 

<br>

- **name**—A required property that identifies the name of the classification schema. 
  
- **version**—A required property that identifies the version of the classification schema. 
 
- **grammarVersion**—A required property that specifies the version of the classification grammar the schema adheres to. You can access the classification grammar version using the URL <span>https://</span>webadaptorhost<span>.domain</span><span>.com/webadaptorname/sharing/rest/portals/&lt;org Id&gt;/classification</span>.
  
- **helpToolTip**—The help text that appears when you hover over **Information** <img src="https://github.com/user-attachments/assets/9be797f3-580f-4407-a068-5ded7e540642" width=20 /> at the top of the classification form. 
  
- **helpURL**—The URL of the schema help document that opens in a new tab when you click **Information** <img src="https://github.com/user-attachments/assets/9be797f3-580f-4407-a068-5ded7e540642" width=20 /> at the top of the classification form. 

- **bannerExpression**—The classification information that appears under **Classification** on the item details page. You can use Arcade expressions to create banner texts or set the value to an empty string to implement generic encoding logic defined for **uiElements** in the classification form (for example, bannerOrder, bannerLabel, labelDelimiter).

  > ![Note](https://user-images.githubusercontent.com/31771293/225783213-2d4e69a4-035e-4126-b2aa-d2a864fa59b6.png)
  >
  > If you omit this property or define it as an empty string, you must have at least one attribute with **bannerOrder** defined to implement generic encoding logic.

- **selectionTextExpression**—The classification information that appears on the **Edit Classification** dialog box. You can use Arcade expressions to create banner texts or set the value to an empty string to implement generic encoding logic defined for **uiElements** in the classification form (for example, selectionDisplayOrder, selectionDisplayLabel, labelDelimiter).

    > ![Note](https://user-images.githubusercontent.com/31771293/225783213-2d4e69a4-035e-4126-b2aa-d2a864fa59b6.png)
    >
    > If you omit this property or define it as an empty string, you must have at least one attribute with **selectionDisplayOrder** defined to implement generic encoding logic.
    
- **attributeCategories**—The list of attribute categories that appear as sections or tabs in the classification form.

    > ![Note](https://user-images.githubusercontent.com/31771293/225783213-2d4e69a4-035e-4126-b2aa-d2a864fa59b6.png)
    >
    > "Default” is a reserved keyword and cannot be used as an attribute category.

<br>

<br>

```
{ 
  "name": "academic-institution-classification-schema", 
  "version": "2.0", 
  "grammarVersion": "2.0", 
  "helpURL": "https://ansible.hynes.com/portal/home/schema_help.pdf", 
  "helpTooltip": "Click to open the schema help document", 
  "bannerExpression": "", 
  "selectionTextExpression": "", 
  "attributeCategories": [] 
} 

```

<br>

<br>

## Define classificationMetadata 

The required **classificationMetadata** object can include the following properties: 

- **primaryAttribute**—A required property that identifies the attribute that appears as the primary classification field in the classification form. 
 
- **defaultValue**—A required property that specifies the default value for the **primaryAttribute**. 
 
- **classificationValueProperties**—A required array of objects, where each object represents a classification option of the attribute identified as the **primaryAttribute** and defines specific properties for the option. The following properties can be defined for each classification option: 
 
  - **value**—A required property that specifies the label for the option used in the classification form. 
 
  - **acronym**—The acronym for the option. 
 
  - **textColor**—When the option is selected, its label will appear in this color under **Current Selections** in the classification form. Color can be specified with predefined color names, or with RGB and HEX values. 

  - **backgroundColor**—When the option is selected, its label will be highlighted in this color under **Current Selections** in the classification form. Color can be specified with predefined color names, or with RGB and HEX values.

<br>

<br>

```
{ 
... 
 
"classificationMetadata": { 
    "primaryAttribute": "classification", 
    "defaultValue": "Public Data", 
    "classificationValueProperties": [ 
      { 
        "value": "Public Data", 
        "acronym": "Public Data", 
        "backgroundColor": "Green", 
        "textColor": "Black" 
      }, 
      { 
        "value": "Restricted", 
        "acronym": "Restricted", 
        "backgroundColor": "Yellow", 
        "textColor": "Black" 
      }, 
      { 
        "value": "Confidential", 
        "acronym": "Confidential", 
        "backgroundColor": "Red", 
        "textColor": "Black" 
      } 
    ] 
  } 
} 

```

<br>

<br>

## Define attributes

Each attribute defined in the required **attributes** object corresponds to an input field in the classification form. The following properties can be defined for each attribute:

- **label**— A required property that specifies the label for the attribute used in the classification form. 
 
- **description**—The description used as a placeholder in the input field. 
  
- **type**—A required property that identifies the attribute's data type. Supported data types are string, date, integer, float, and Boolean. 
  
- **isRequired**—A Boolean (true or false) value that specifies if the attribute is considered a required attribute. It cannot be defined as an empty string. 
 
- **uiElement**—A required property that identifies the attribute’s UI element type in the classification form. The six possible values are: 
 
  - **text**— A single-line text box. 
  - **checkbox**— A standard checkbox. 
  - **date**— A date picker that lets you select a date from the calendar in the format DD/MM/YYYY. 
  - **single-select**—A dropdown menu that lets you select a single option. 
  - **multi-select**—A dropdown menu that lets you select multiple options. 
  - **multi-grouped-select**— A dropdown menu that lets you select individual options from groups of related options but not the top-level groups themselves. 
  - **multi-grouped-select-nested**—A dropdown menu that lets you select groups of related options or individual options from those groups. 

- **defaultValue**—The default value assigned for the attribute. This property can only be set for single-select, multi-select, multi-grouped-select, multi-grouped-select-nested **uiElement** types. 
  
- **defaultDateTimeline**—Used in combination with defaultDateTimelineUnits to set the default date for the attribute. This property can only be set for date **uiElement** type. 
 
- **defaultDateTimelineUnits**—Used in combination with defaultDateTimeline to set the default date for the attribute. The three possible values are **years**, **months**, and **days**. This property can only be set for date **uiElement** type. 
 
- **validValues**—The list of options that appear in single-select or multi-select **uiElement** type dropdowns in the classification form. It can be defined as an empty string if the options are generated by the Arcade expression for **valueExpression**.  
 
- **validValuesMap**—The map of options that appear in multi-grouped-select or multi-grouped-select-nested **uiElement** type dropdowns in the classification form. It can be defined as an empty string if the options are generated by the Arcade expression for **valueExpression**. 

- **valueExpression**—An Arcade expression that returns a list of options when **validValues** and **validValuesMap** are not defined or defined as an empty string. 
 
- **isAttributeEnabled**—An Arcade expression that returns a Boolean value that specifies if the attribute will appear or be hidden in the classification form. 
  
- **attributeValidation**—An Arcade expression that returns either an empty string or an error message based on the value selected for the attribute in the classification 

- **arcadeResultLookup**—A map of keys and values that lets the Arcade expression defined for valueExpression generate the list. 
  
- **attributeCategory**—The attributeCategories section or tab under which the attribute appears in the classification form. 

- **selectionDisplayOrder**—The order in which the attribute appears in the selectionTextExpression text.  
 
  > ![Note](https://user-images.githubusercontent.com/31771293/225783213-2d4e69a4-035e-4126-b2aa-d2a864fa59b6.png)
  >
  > You must define this property for at least one attribute in your classification if you omit **selectionTextExpression** or define it as an empty string. 
 
- **selectionDisplayLabel**—The label for the attribute used in the selectionTextExpression text. 

- **bannerOrder**—The order in which the attribute appears in the bannerExpression text.  
  
  > ![Note](https://user-images.githubusercontent.com/31771293/225783213-2d4e69a4-035e-4126-b2aa-d2a864fa59b6.png)
  >
  > You must define this property for at least one attribute in your classification if you omit **bannerExpression** or define it as an empty string.

- **bannerLabel**—The label for the attribute used in the **bannerExpression** text. 

- **labelDelimiter**—The delimiter that separates the attribute’s label and value in the **selectionTextExpression** and **bannerExpression** texts. 

- **valueDelimiter**—The delimiter that separates the values selected in a multi-select **uiElement** type when they appear in the **selectionTextExpression** and **bannerExpression** texts. 
 
- **attributeDelimiter**—The delimiter separates the attribute and its preceding attribute in the **selectionTextExpression** and **bannerExpression** texts. 
 
- **labelTooltip**—The help text that appears when you hover over **Information** <img src="https://github.com/user-attachments/assets/9be797f3-580f-4407-a068-5ded7e540642" width=20 /> next to the attribute’s label. 

<br>

<br>

```
{ 
... 
 
"attributes": { 
    "classification": { 
      "label": "Classification", 
      "description": "Classification", 
      "type": "string", 
      "uiElement": "single-select", 
      "validValues": [{"label": "Public Data", "value": "Public Data"}, {"label": "Restricted", "value": "Restricted"}, {"label": "Confidential", "value": "Confidential"}], 
      "selectionDisplayOrder": 1, 
      "bannerOrder": 1, 
      "labelDelimiter": "", 
      "valueDelimiter": "-", 
      "attributeDelimiter": ";" 
    }, 
    "program": { 
      "label": "Program", 
      "description": "Program", 
      "type": "string", 
      "uiElement": "single-select", 
      "valueExpression": "function getProgramValidValues(schemaJsonString, valueJsonString, attributeId) {\n    var valueJson = Dictionary(valueJsonString)\n    var schemaJson = Dictionary(schemaJsonString)\n    if (!HasKey(valueJson, \"classification\"))\n        return null;\n    if (valueJson.classification == \"Public Data\")\n        return schemaJson.attributes[attributeId].arcadeResultLookup[\"Public_Data_List\"];\n    if (valueJson.classification == \"Restricted\")\n        return schemaJson.attributes[attributeId].arcadeResultLookup[\"Restricted_List\"];\n    if (valueJson.classification == \"Confidential\")\n        return schemaJson.attributes[attributeId].arcadeResultLookup[\"Confidential_List\"];\n    return null;\n}\ngetProgramValidValues(schemaJsonString, valueJsonString, attributeId)", 
      "arcadeResultLookup": { 
        "Public_Data_List": [{"label": "Intra-agency", "value": "Intra-agency"}, {"label": "Marketing", "value": "Marketing"}, {"label": "Promotional", "value": "Promotional"}], 
        "Restricted_List": [{"label": "Compliance", "value": "Compliance"}, {"label": "Financial", "value": "Financial"}, {"label": "Human Resources", "value": "Human Resources"}, {"label": "Market Data", "value": "Market Data"}, {"label": "PII", "value": "PII"}, {"label": "Proprietary", "value": "Proprietary"}], 
        "Confidential_List": [{"label": "Intellectual Property", "value": "Intellectual Property"}, {"label": "Legal", "value": "Legal"}, {"label": "Security", "value": "Security"}] 
      }, 
      "selectionDisplayOrder": 2, 
      "bannerOrder": 2, 
      "labelDelimiter": "", 
      "valueDelimiter": "-", 
      "attributeDelimiter": ";" 
    } 
  } 
} 

```
<br>

<br>

## Define layouts

The required **layouts** object specifies the order in which attributes appear in the classification form. It can include the following:

- **default**—The object that includes the details of a specific layout. You can define the following property within the object. 
 
  - **layoutElements**—A required object that maps attributes and their order in the classification form. The following property can be defined for each attribute in the object: 
 
    - **formDisplayOrder**—A required integer that identifies the order in which the attribute appears in the classification form. 

<br>

<br>

```
{ 
... 
 
"layouts": { 
    "default": { 
      "layoutElements": { 
        "classification": { 
          "formDisplayOrder": 1 
        }, 
        "program": { 
          "formDisplayOrder": 2 
        } 
      } 
    } 
  } 
} 

```

<br>

<br>

The following is a complete example of a classification schema: 

<br>

```
{  
  "name": "academic-institution-classification-schema",  
  "version": "2.0",  
  "grammarVersion": "2.0",  
  "helpURL": "https://ansible.hynes.com/portal/home/schema_help.pdf",  
  "helpTooltip": "Click to open the schema help document",  
  "bannerExpression": "",  
  "selectionTextExpression": "",  
  "attributeCategories": [], 
  "classificationMetadata": {  
    "primaryAttribute": "classification",  
    "defaultValue": "Public Data",  
    "classificationValueProperties": [  
      {  
        "value": "Public Data",  
        "acronym": "Public Data",  
        "backgroundColor": "Green",  
        "textColor": "Black"  
      },  
      {  
        "value": "Restricted",  
        "acronym": "Restricted",  
        "backgroundColor": "Yellow",  
        "textColor": "Black"  
      },  
      {  
        "value": "Confidential",  
        "acronym": "Confidential",  
        "backgroundColor": "Red",  
        "textColor": "Black"  
      }  
    ]  
  }, 
  "attributes": {  
    "classification": {  
      "label": "Classification",  
      "description": "Classification",  
      "type": "string",  
      "uiElement": "single-select",  
      "validValues": [{"label": "Public Data", "value": "Public Data"}, {"label": "Restricted", "value": "Restricted"}, {"label": "Confidential", "value": "Confidential"}],  
      "selectionDisplayOrder": 1,  
      "bannerOrder": 1,  
      "labelDelimiter": "",  
      "valueDelimiter": "-",  
      "attributeDelimiter": ";"  
    },  
    "program": {  
      "label": "Program",  
      "description": "Program",  
      "type": "string",  
      "uiElement": "single-select",  
      "valueExpression": "function getProgramValidValues(schemaJsonString, valueJsonString, attributeId) {\n    var valueJson = Dictionary(valueJsonString)\n    var schemaJson = Dictionary(schemaJsonString)\n    if (!HasKey(valueJson, \"classification\"))\n        return null;\n    if (valueJson.classification == \"Public Data\")\n        return schemaJson.attributes[attributeId].arcadeResultLookup[\"Public_Data_List\"];\n    if (valueJson.classification == \"Restricted\")\n        return schemaJson.attributes[attributeId].arcadeResultLookup[\"Restricted_List\"];\n    if (valueJson.classification == \"Confidential\")\n        return schemaJson.attributes[attributeId].arcadeResultLookup[\"Confidential_List\"];\n    return null;\n}\ngetProgramValidValues(schemaJsonString, valueJsonString, attributeId)",  
      "arcadeResultLookup": {  
        "Public_Data_List": [{"label": "Intra-agency", "value": "Intra-agency"}, {"label": "Marketing", "value": "Marketing"}, {"label": "Promotional", "value": "Promotional"}],  
        "Restricted_List": [{"label": "Compliance", "value": "Compliance"}, {"label": "Financial", "value": "Financial"}, {"label": "Human Resources", "value": "Human Resources"}, {"label": "Market Data", "value": "Market Data"}, {"label": "PII", "value": "PII"}, {"label": "Proprietary", "value": "Proprietary"}],  
        "Confidential_List": [{"label": "Intellectual Property", "value": "Intellectual Property"}, {"label": "Legal", "value": "Legal"}, {"label": "Security", "value": "Security"}]  
      },  
      "selectionDisplayOrder": 2,  
      "bannerOrder": 2,  
      "labelDelimiter": "",  
      "valueDelimiter": "-",  
      "attributeDelimiter": ";"  
    }  
  }, 
  "layouts": {  
    "default": {  
      "layoutElements": {  
        "classification": {  
          "formDisplayOrder": 1  
        },  
        "program": {  
          "formDisplayOrder": 2  
        }  
      }  
    }  
  } 
} 

```
