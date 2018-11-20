# Site-Schema.org

![Draft](https://img.shields.io/badge/Draft-In%20progress-yellow.svg)

Site schemas are a machine-readable description format used to validate and describe the file structures of websites. They may offer additional annotations for user interfaces and for enforcing permissions.

Links:

 - [Specification](./draft-01.md)
 - [JSON-schema definition](./draft-01.json)

## Motivation

Site schemas are a tool for [Beaker browser](https://beakerbrowser.com) applications which want to publish user data in [dat](https://datproject.org) websites. By encoding a site schema, applications can define the semantics of their data, enforce schemas and file-structures, and provide user-friendly metadata about their data.

### Permissions

When applications request access to a file or folder in a site, the browser needs to describe the data being accessed. It's not sufficient to ask `"Allow foo.com to read and write your /data/bookmarks?"` We ideally want to ask, `"Allow foo.com to read and write your Bookmarks?"`

Site schemas give us the metadata we need to describe files and folders to the user.

### Semantic knowledge

In the same way that file-extensions describe the content of a file, site schema URLs identify the content of a site.

### Organization

Site schemas help organize data by setting a predefined structure which can not be altered. The browser ensures that files and folders declared by the schema are present.

### Automated validation

Site schemas help avoid errors by automatically validating data before it is written to the site.

## Background

Site schemas were created to explore an alternative to [Object-store folders (OSFs)](https://github.com/beakerbrowser/specs/blob/master/object-store-folder.md). They were created due to concerns that OSFs and the UI/UX flows around them were too complex.

### Dataset conflicts

There are multiple datasets in an OSF. They can be created at an app's request. Because there's no coordination between those datasets, it's possible to have multiple variations of a similar dataset. For instance, you could have multiple "Social Media Post" datasets with no way to discern between them. This has a strong potential to confuse users.

Site schemas solve this by creating a single coordinated schema for the site's data.

### Conceptual simplicitiy

Site schemas create a schema for the entire site rather than creating a set of schemas for multiple datasets. This is easier to understand on two levels:

 - Mechanics: the mechanics of a site-schema are relatively easy to explain (it's a predefined structure for the sites' files and folders) whereas OSFs require more background reading and involve somewhat unusual and novel mechanics.
 - "Grain": a site-schema is a single definition which describes the entire site, which is conceptually simpler than a set of definitions which describe datasets within a site.

### Rigidity

OSFs force developers into a predefined file & folder structure, and can only enforce rules around JSON files. Site schemas are relatively free-form in comparison. They can be used to manage all kinds of files, folders, and mounts.

Site schemas can also be introduced to an existing site without breaking backwards compatibility, making them easier to introduce progressively.

### Less abstraction

OSFs try to treat a folder in the filesystem like a database, which is a leaky abstraction. Site schemas stay more connected to the filesystem as a collection of files.

## Status

This spec is a work-in-progress proposal. It has not yet been adopted for Beaker's roadmap.