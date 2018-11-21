# Site-Schema.org

![Draft](https://img.shields.io/badge/Draft-In%20progress-yellow.svg)

Site schemas are a description file used to validate and describe the file structures of websites. They may offer additional annotations for user interfaces and for enforcing permissions.

Links:

 - [Read the Specification](./draft-01.md)
 - [JSON-schema definition](./draft-01.json)

## Status

This spec is a proposal. It has not yet been adopted for Beaker's roadmap.

## Example

This is the example schema for a "user" site.

```json
{
  "$schema": "http://site-schema.org/draft-01.json",
  "$id": "http://example.com/user-site.json",
  "title": "Example User",
  "additionalFiles": true,
  "additionalFolders": false,
  "files": {
    "profile.json": {
      "title": "User profile information",
      "jsonSchema": "http://example.com/user-profile.json"
    }
  },
  "folders": {
    "posts": {
      "title": "Social feed posts",
      "extensions": ["json"],
      "jsonSchema": "http://example.com/post.json",
      "additionalFolders": false
    },
    "media": {
      "title": "Media",
      "additionalFiles": false,
      "additionalFolders": false,
      "folders": {
        "images": {
          "title": "Images",
          "extensions": ["png", "gif", "jpg", "jpeg"],
          "additionalFolders": false
        },
        "videos": {
          "title": "Videos",
          "extensions": ["mp4", "avi"],
          "additionalFolders": false
        }
      }
    }
  }
}
```

This schema will validate correctly against a site with the following files & folder structure:

```
/profile.json
/posts
/media/images
/media/videos
```

Additionally, the schema will enforce the following JSON schemas:

 - `/profile.json` file must pass the `http://example.com/user-profile.json` schema validation.
 - `/posts/*.json` files must pass the `http://example.com/post.json` schema validation.

## Specification draft

[Read the draft-01 specification here](./draft-01.md).

## Motivation

Site schemas are used by [Beaker browser](https://beakerbrowser.com) applications to publish user data in [dat](https://datproject.org) websites. They provide the following features:

|Feature|Description|
|-|-|
|**Descriptions**|Site schemas give us the metadata we need to describe files and folders to the user. This is useful in permission prompts.|
|**Semantic&nbsp;knowledge**|In the same way that file-extensions describe the content of a file, site schema URLs identify the content of a site.|
|**Organization**|Site schemas help organize data by setting a predefined structure which can not be altered. The browser ensures that files and folders declared by the schema are present.|
|**Automated&nbsp;validation**|Site schemas help avoid errors by automatically validating data before it is written to the site.|
|**Advanced&nbsp;permissions**|Site schemas can describe advanced permissions such as "protected" folders.|

## Background

Site schema was created to explore an alternative to [Object-store folders (OSFs)](https://github.com/beakerbrowser/specs/blob/master/object-store-folder.md). It was created due to concerns that OSFs and the UI/UX flows around them were too complex. It addresses the following concerns:

### Concern: Dataset conflicts

It's possible for OSFs to have multiple variations of a similar dataset. For instance, you could have multiple "Social Media Post" datasets with no way to discern between them. Site schemas solve this by creating a single coordinated schema for the site's data.

### Concern: Conceptual simplicitiy

Site schemas create a schema for the entire site. This is conceptually simpler than multiple definitions which describe datasets within a site.

### Concern: Mechanical simplicity

The mechanics of a site-schema are relatively easy to explain. OSFs require more background reading and involve somewhat unusual and novel mechanics.

### Concern: Rigidity

OSFs force developers into a predefined file structure and can only enforce rules around JSON files. Site schemas are relatively free-form in comparison. They can be used to manage all kinds of files, folders, and mounts.

### Concern: Backwards compatibility

Site schemas can be introduced to an existing site without breaking backwards compatibility, making them easier to introduce progressively.

### Concern: Less abstraction

OSFs try to treat a folder in the filesystem like a database, which is a leaky abstraction. Site schemas stay more connected to the filesystem as a collection of files.
