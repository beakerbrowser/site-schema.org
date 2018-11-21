# Site Schema draft-01

Site schemas are a machine-readable description format used to validate the file and folder structures of websites. They may offer additional annotations for user interfaces and for enforcing permissions.

## Table of Contents

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Schema file location](#schema-file-location)
- [Definitions](#definitions)
  - [Privileged origins](#privileged-origins)
- [Schema description](#schema-description)
  - [Root object](#root-object)
    - [`$schema`](#schema)
    - [`$id`](#id)
    - [`title`](#title)
    - [`description`](#description)
    - [`files`](#files)
    - [`extensions`](#extensions)
    - [`jsonSchema`](#jsonschema)
    - [`additionalFiles`](#additionalfiles)
    - [`folders`](#folders)
    - [`additionalFolders`](#additionalfolders)
    - [`protected`](#protected)
  - [Folder object](#folder-object)
    - [`title`](#title-1)
    - [`description`](#description-1)
    - [`files`](#files-1)
    - [`extensions`](#extensions-1)
    - [`jsonSchema`](#jsonschema-1)
    - [`additionalFiles`](#additionalfiles-1)
    - [`folders`](#folders-1)
    - [`additionalFolders`](#additionalfolders-1)
    - [`protected`](#protected-1)
  - [File object](#file-object)
    - [`title`](#title-2)
    - [`description`](#description-2)
    - [`jsonSchema`](#jsonschema-2)
    - [`protected`](#protected-2)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Schema file location

The site schema-file MUST be located at `/schema.json` on the site.

 - The location is case-sensitive; it cannot be `/SCHEMA.json`.
 - The extension is required; it cannot be `/schema`.

## Definitions

### Privileged origins

"Priviliged origins" refer to applications which have full write-access to the site. They are typically defined in the following way: they are either the system (the browser) or the application that initially created the site.

## Schema description

[Full JSON Schema](./draft-01.json)

### Root object

#### `$schema`

The "$schema" keyword is both used as a Site Schema version identifier and the location of a resource which is a JSON Schema.

The value of this keyword MUST be a [URI](http://tools.ietf.org/html/rfc3986) (containing a scheme) and this URI MUST be normalized. The current schema MUST be valid against the meta-schema identified by this URI. 

#### `$id`

The "$id" keyword defines a URI for the schema, and the base URI that other URI references within the schema are resolved against.

If present, the value for this keyword MUST be a string, and MUST represent a valid [URI-reference](http://tools.ietf.org/html/rfc3986). This value SHOULD be normalized, and SHOULD NOT be an empty fragment `<#>` or an empty string `<>`. 

#### `title`

The value MUST be a string.

This keyword can be used to decorate a user interface with information about the site described by this schema. A title will preferably be short. 

Omitting this keyword has the same behavior as an empty string. 

#### `description`

The value MUST be a string.

This keyword can be used to decorate a user interface with information about the site described by this schema. A description will provide explanation about the purpose of the site described by this schema. 

Omitting this keyword has the same behavior as an empty string. 

#### `files`

The value MUST be an object.

This keyword determines how files in the folder validate.

Validation succeeds if, for each file name that appears in both the folder and as a name within this keyword's value, the file for that name successfully validates against the corresponding schema. The schema for file objects is described at ["File object"](#file-object).

Omitting this keyword has the same behavior as an empty object. 

#### `extensions`

The value of this keyword MUST be either null or an array. Elements of this array, if any, MUST be strings, and MUST be unique.

The folder is valid against this keyword if every file name has an extension which is represented in the array.

Omitting this keyword has the same behavior as a null. 

#### `jsonSchema`

The "jsonSchema" keyword defines a URI for the schema for all files in the folder with a `.json` schema.

If present, the value for this keyword MUST be a string, and MUST represent a valid [URI-reference](http://tools.ietf.org/html/rfc3986). This value SHOULD be normalized, and SHOULD NOT be an empty fragment `<#>` or an empty string `<>`. 

#### `additionalFiles`

The value MUST be a boolean.

This keyword determines if the folder is able to contain files which have not been specified in the [files](#files) keyword.

If the keyword value is false, then the folder is valid against this keyword if the files present are represented in the [files](#files) keyword or are standard system files (such as dat.json).

Omitting this keyword has the same behavior as a true value.

#### `folders`

The value MUST be an object.

This keyword determines how folders in the folder validate.

Validation succeeds if, for each folder name that appears in both the folder and as a name within this keyword's value, the folder for that name successfully validates against the corresponding schema. The schema for file objects is described at ["Folder object"](#folder-object).

Omitting this keyword has the same behavior as an empty object. 

#### `additionalFolders`

The value MUST be a boolean.

This keyword determines if the folder is able to contain folders which have not been specified in the [folders](#folders) keyword.

If the keyword value is false, then the folder is valid against this keyword if the folders present are represented in the [folders](#folders) keyword or are standard system folders.

Omitting this keyword has the same behavior as a true value.

#### `protected`

The value MUST be a boolean.

This keyword determines whether the folder may be modified by non-[privileged origins](#privileged-origins).

Omitting this keyword has the same behavior as a false value.

### Folder object

#### `title`

The value MUST be a string.

This keyword can be used to decorate a user interface with information about the folder described by this schema. A title will preferably be short. 

Omitting this keyword has the same behavior as an empty string. 

#### `description`

The value MUST be a string.

This keyword can be used to decorate a user interface with information about the folder described by this schema. A description will provide explanation about the purpose of the folder described by this schema. 

Omitting this keyword has the same behavior as an empty string. 

#### `files`

The value MUST be an object.

This keyword determines how files in the folder validate.

Validation succeeds if, for each file name that appears in both the folder and as a name within this keyword's value, the file for that name successfully validates against the corresponding schema. The schema for file objects is described at ["File object"](#file-object).

Omitting this keyword has the same behavior as an empty object. 

#### `extensions`

The value of this keyword MUST be either null or an array. Elements of this array, if any, MUST be strings, and MUST be unique.

The folder is valid against this keyword if every file name has an extension which is represented in the array.

Omitting this keyword has the same behavior as a null. 

#### `jsonSchema`

The "jsonSchema" keyword defines a URI for the schema for all files in the folder with a `.json` schema.

If present, the value for this keyword MUST be a string, and MUST represent a valid [URI-reference](http://tools.ietf.org/html/rfc3986). This value SHOULD be normalized, and SHOULD NOT be an empty fragment `<#>` or an empty string `<>`. 

#### `additionalFiles`

The value MUST be a boolean.

This keyword determines if the folder is able to contain files which have not been specified in the [files](#files-1) keyword.

If the keyword value is false, then the folder is valid against this keyword if the files present are represented in the [files](#files-1) keyword or are standard system files.

Omitting this keyword has the same behavior as a true value.

#### `folders`

The value MUST be an object.

This keyword determines how folders in the folder validate.

Validation succeeds if, for each folder name that appears in both the folder and as a name within this keyword's value, the folder for that name successfully validates against the corresponding schema. The schema for file objects is described at ["Folder object"](#folder-object).

Omitting this keyword has the same behavior as an empty object. 

#### `additionalFolders`

The value MUST be a boolean.

This keyword determines if the folder is able to contain folders which have not been specified in the [folders](#folders-1) keyword.

If the keyword value is false, then the folder is valid against this keyword if the folders present are represented in the [folders](#folders-1) keyword or are standard system folders.

Omitting this keyword has the same behavior as a true value.

#### `protected`

The value MUST be a boolean.

This keyword determines whether the folder may be modified by non-[privileged origins](#privileged-origins).

Omitting this keyword has the same behavior as a false value.

### File object

#### `title`

The value MUST be a string.

This keyword can be used to decorate a user interface with information about the title described by this schema. A title will preferably be short. 

Omitting this keyword has the same behavior as an empty string. 

#### `description`

The value MUST be a string.

This keyword can be used to decorate a user interface with information about the file described by this schema. A description will provide explanation about the purpose of the file described by this schema. 

Omitting this keyword has the same behavior as an empty string. 

#### `jsonSchema`

The "jsonSchema" keyword defines a URI for the schema for the file.

If present, the value for this keyword MUST be a string, and MUST represent a valid [URI-reference](http://tools.ietf.org/html/rfc3986). This value SHOULD be normalized, and SHOULD NOT be an empty fragment `<#>` or an empty string `<>`. 

#### `protected`

The value MUST be a boolean.

This keyword determines whether the file may be modified by non-[privileged origins](#privileged-origins).

Omitting this keyword has the same behavior as a false value.