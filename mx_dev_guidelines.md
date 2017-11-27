- [Naming conventions](#naming-conventions)
    - [Modules](#modules)
    - [Module roles](#module-roles)
    - [Folders](#folders)
        - [Process Related Sources](#process-related-sources)
        - [Entity Related Sources](#entity-related-sources)
    - [Forms](#forms)
    - [Domain model](#domain-model)
        - [Entities](#entities)
        - [Entity attributes](#entity-attributes)
        - [Enumeration attributes](#enumeration-attributes)
        - [Associations](#associations)

# Naming conventions
While developing a Mendix application several different naming conventions should be used to improve readability of flows, make it easier to logically find re-usable functions (ie microflows) and speed up analysis of bugs.

## Modules
Modules should be treated like standalone replaceable services if possible, for example, the email module should function as a standalone email system as much as possible, replaceable by a different email system. Module names should have camel case names that identify the responsibility of the module.

## Module roles
The module roles should have logical names that reflect the access they should have within a module.

## Folders
The structure for your documents starts with a clear separation of folders. When using a decent folder structure you will improve the maintainability of your application and will be able to find required documents faster and therefore will be able to develop and fix faster. The optimal grouping of your documents into folders depends on the circumstances and on the functional setup of your application. We recommend combining the guidelines below in a way that fits your project.

### Process Related Sources
Every project has processes that are developed, so structure your documents for this process into folders that reflect those processes and their steps.

### Entity Related Sources
Every project has documents that are needed for specific entities. Think of overview pages for maintenance, validation microflows that prevent commits, or other event triggers. Those type of documents should be structured into one folder that is named after the entity where optional sub-folders could be applied to order for, example, events and pages.

## Forms
Forms can have several purposes:
 * Module landing page
 * Entity management
 * Selection popup dialog
 * Edit dialog

If a form is used to manage a specific object for example the TradingTerms – the name of the form should start with the entity name, followed by an underscore and a target use. The most common usages are `_NewEdit`, `_View`, `_Select` and `_MultiSelect`.
In some cases you might need to create specific `_Select`/`_MultiSelect` dialogs for the same type of selectable entity object, but with different filters (or root dataview object). In these cases use another underscore followed by the specific use – ie `Account_NewEdit`.


## Domain model
A domain model consists of the following:
 * Entities
 * Entity attributes
 * Enumerations
 * Associations

### Entities
Entity names should be nouns, in mixed case with the first letter of each internal word capitalized. Try to keep your entity names simple and descriptive. Use whole words-avoid acronyms and abbreviations (unless the abbreviation is much more widely used than the long form, such as URL or HTML). Also use the singular form, so `DealType` instead of `DealTypes`.

### Entity attributes
Attribute names should be short yet meaningful in mixed case with the first letter of each internal word capitalized. The choice of a variable name should be mnemonic- that is, designed to indicate to the casual observer the intent of its use.

### Enumeration attributes
Entity names should be nouns, in mixed case with the first letter of each internal word capitalized. Try to keep your entity names simple and descriptive. Use whole words-avoid acronyms and abbreviations (unless the abbreviation is much more widely used than the long form, such as URL or HTML). Also use the singular form, so `Day` instead of `Days`.

### Associations
Association names should consist of both entity names involved in the association. For a typical association a simple underscore in between suffices.
`Deal_Document`.
In case multiple associations between the same entity types are required the convention is to include a specific meaning in between the entity names keeping the related entity type names, ie:
`Deal_pay_LegDetails`
`Deal_receive_LegDetails`
