Below is general structure of directories and fields within Salesforce Forms repository. Directories has been marked with - character.

```
 - fields
	 - overrides
	     - SITE_CODE
		 _nonApiFieldName.yaml        
	         objectNameFieldName.yaml
	 _nonApiFieldName.yaml
	 objectNameFieldName.yaml
 - forms
     - form_id
         - overrides
             - SITE_CODE
                 _nonApiFieldName.yaml
                 objectNameFieldName.yaml
         settings.yaml
   submitStructure.yaml
 README.md
```

 - `fields` dir - is a collection of all base definitions of fields used across different forms
	 - `overrides` dir - allows to override specific field per `SITE_CODE`, this means if the field is used in several different forms across single site then overriding field in this place will impact all the definitions of this field in all forms per single country
	 - `_noneApiFieldName.yaml` file - this is the definition of a field which is not part of Salesforce API and should not be sent to API endpoint. Usage example: there's a requirement which should allow to select one of two options on the form and based on the selected value other parts of form behave respectively. So, all and all this field is just a trigger to setup a specific structure which is going to be send to API, but the non API field is just a bridge to do it.
	 - `objectNameFieldName.yaml` file - this is the definition of Salesforce API field which is going to be part of payload of the API POST request.
 - `forms` dir - is a collection of Salesforce forms. Each directory inside this dir represents a single form.
	 - `form_id` dir - this is the representation of the single form, eg. `account_maintenance`. Every dir of this type MUST contain a `settings.yaml` file contains the structure of the form itself.
		 - `settings.yaml` file - this file represents the structure of a form which is going to be rendered on Drupal site.
		 - `overrides` dir - this directory is optional and contains list of overrides per SITE_CODE. Each overriden BU is represented as a single directory with its sitecode, eg. `SE` or `DKINGO`.
			 - `SITE_CODE` dir - this dir represents a single BU by its sitecode value. This dir needs to be provided with uppercase. For example: `PL`, `SE`, `SEINGO`, etc. It contains list of yaml files, each representing single field which is going to override it's base definition for this specific form and this specific BU.
				 - `_noneApiFieldName.yaml` file - here you can override specific properties of the base definition of the field or field already overriden in `fields` dir. There is no need to specify all the properties from the start but include only these which should be changed. This field required to have an ID of the field defined in the first line, for example: `id: orderCaseDescription`
				 - `objectNameFieldName.yaml`  file - similar to `_noneApiFieldName.yaml` definition, but this field is going to be part of API payload during API POST request (with exception of `not_submittable` flag, more about this here: XXX).
	 - `submitStructure.yaml` file - this file provides structure of objects for API submission. So it defines how objects needs to be nested for specific API call. This file delivers all the structures for all existing API endpoints eg. `genericCase` or `cardApplicationCase`.
 - `README.md` file - a read me file.
