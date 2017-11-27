<h1>Development guidelines</h1>

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
    - [Microflows](#microflows)
        - [Microflow naming](#microflow-naming)
            - [Object specific microflows](#object-specific-microflows)
            - [Event microflows](#event-microflows)
        - [Microflow variables](#microflow-variables)
        - [Microflow references](#microflow-references)
- [Commit descriptions](#commit-descriptions)
- [SVN release strategy](#svn-release-strategy)
    - [Main line](#main-line)
    - [Release versioning](#release-versioning)
    - [Branch naming convention](#branch-naming-convention)

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


## Microflows

### Microflow naming
Microflows can have several purposes:
 * Microflow invoked by clicking a button
 * Sub microflow
 * Scheduled event
 * Datasource for a (template) grid / listview / dataview
 * On change/leave of an input widget
 * Any custom trigger in a custom widget

#### Object specific microflows
Microflows triggered from a specific object should start with the entity name. Ie for object TradingTerms this would result in something like the following:
 * TradingTerms_New
 * TradingTerms_Save
 * TradingTerms_Cancel
 * TradingTerms_Delete
 * TradingTerms_GetCounterParties

#### Event microflows
Microflows used as event handlers on a domain model entity are named as follows;

``` 
LegDetails_BeforeCommit

Deal_AfterCreate
```

An entity should have only one event handler per event (before/after – create/commit/delete/rollback) as there is no guarantee on the order in which event handler microflows for one event are executed. In this case the syntax advised will always be clear.

### Microflow variables
Variable names should be short yet meaningful – starting with lower case prefix var (or pvar for a variable used as an input parameter of a microflow)– followed by a name in mixed case with the first letter of each internal word capitalized. The choice of a variable name should be mnemonic- that is, designed to indicate to the casual observer the intent of its use. 
Important is that the name of a variable should be obvious enough to give a developer an idea on the type. There will always be some exceptions to this but some examples are given below.
| Variable name | Type logic |
| --- | --- |
| `varDealType` or `varDealStatus` | The name of an enumeration should be descriptive enough for a developer to know that it’s a variable of this type |
| `varTradeDate` or `varStartTime` | The name of a datetime type variable should descriptive enough to conclude that it contains a datetime, date or time value |
| `varUpdate` or `varSkip` | The name of a boolean type variable should be logical when a question mark is added to the variable name – like Update? Or Skip? |
| `varMessage` or `varShortName` | In the examples given a developer should be able to determine the variable type to be of string |
| `varNotional` or `varSomeAmount` | In case of referring to a calculated and/or currency based value the name is already self-explanatory |
| `varNumberOfDays` or `varRowNumber` | The name of an integer/long type variable should be descriptive enough to conclude that the variable contains a whole number – including the word Number of NumberOf can be helpful |

To differentiate between input variables and variables created during a flow an input variable name is prefix with the smaller case letter `p`.

### Microflow references
Reference objects in microflows are objects retrieved from the model. Naming convention for these object references is described below.

A reference name should always start with prefix ref (or pref for a reference used as an input parameter of a microflow). The prefix is followed by the entity name that its referring to. As described in entity names should be singular and as such the reference object is also always singular – even in case of a list of object references.

Because a microflow can contain multiple references pointing to the same entity, a postfix short description should be applied to the reference name preceded by an underscore `_`.

| Target | Syntax |
| --- | --- |
| Single object reference | `refEntityName` or `refEntityName_specifcName` |
| Single mf input object reference | `prefEntityName` or `prefEntityName_specificName` |
| List of object references | `lstEntityName` or `lstEntityName_specificName` |
| List of mf input object references | `plstEntityName` or `plstEntityName_specificName` |

In some cases specific to the TM – ie `Party` is a `Company` or a `Counterparty` we can use these specific names, but preferably the entity name is always included.


# Commit descriptions
All changes made to the TM Mendix model are committed to the Mendix teamserver svn. Most of the time commits are related to stories that are part of a sprint. Usually one story consists of several commits. To make it easier to identify individual changes a convention for commit messages is required.

The syntax for a commit message is as follows:

```
304 – Some descriptive message 
```
So the number is the actual story number that is being worked on. As a ground rule every change (commit) to the model or project filesystem should be related to a story number. This is important for audit purposes whereas every change to the application needs to have a registered assignment (story, hotfix etc, feedback).
After the story number a space followed by a dash followed by a space is added. After the dash a descriptive message (starting with a capital letter) is included for a developer to be able to identify the changes made in that specific commit. There’s no sense in including just the story description unless its the complete story. For small changes including the actual technical change can be helpful. For larger stories including the functional description is a good practice.
Some examples:
```
TM0127 - Added the ability to add a collateral overview confirmation template + generate report button in collateral overview, enabled for FAM and Admin.

272 - Added DealTypeLabelEN attribute to be able to sort properly (Option tehnically is FX Option captioned)

490 – HOTFIX – Added module role DealView to Documents tab in all deal forms
```

# SVN release strategy
There are a few different strategies possible on how to use SVN combined with a release structure.
The strategy (to be) used for the TM is described in the following chapters.

## Main line
The TM is developed in an agile way using sprints. A sprint resembles a new release or version of the TM. 
All development is done on the mainline. Only after a sprint is finished, fully tested and approved for production will a specific release branch be created and will the release be tagged with the new version. Any changes made to that tagged release (ie hotfixes) are merged back into the mainline.

## Release versioning
Every sprint that is worked through for the TM is deployed to production as a release. A release is versioned and this reflects in the svn using tagging. Tagging in Mendix is done when creating a versioned deployment locally or in the cloud.

The release version consists of 3 numeric characters separated by periods like 2.3.0 where in this example:
 * 2 resembles the major version
 * 3 resembles the minor version
 * 0 resembles the patch version

Major versions are upped when major changes are made to the application which are major to the users of the platform.
Minor versions are upped with regular releases.
The patch version is only upped when hotfixes are applied to releases already deployed to production.

## Branch naming convention
Every sprint is deployed to production as a release. Every release is created as a new branch on svn. The syntax for a new release is as follows:

```
TM_MX6_10_10_R2_3_0
```