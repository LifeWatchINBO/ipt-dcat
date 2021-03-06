# Mapping of RDF DCAT to IPT concepts

namespace prefix | base URIs
----:|:----
dct:| `http://purl.org/dc/terms/`
dcat:| `http://www.w3.org/ns/dcat#`
xsd:| `http://www.w3.org/2001/XMLSchema#`
skos:| `http://www.w3.org/2004/02/skos/core#`
rdfs:| `http://www.w3.org/2000/01/rdf-schema#`
foaf:| `http://xmlns.com/foaf/0.1/`
schema:| `http://schema.org/`
adms:| `http://www.w3.org/ns/adms#`

## dcat:Catalog

### URI

The URI for the IPT catalog will be `http://homepage-of-ipt#Catalog` (e.g. http://data.inbo.be/ipt#Catalog). The URI will become dereferenceable using RDFa. In RDFa, a `rdfs:seeAlso` link will be given to a document which contains the entire DCAT feed.
Only public published resources with a license are added to the DCAT feed.

### Concepts

Mandatory concepts are indicated in bold.

predicate | resource or literal | type | # | IPT concept | example
---:|:---:|:---:|:---:|:---|:---
**dcat:dataset**|resource|dcat:Dataset|M|`dcat:Dataset URI` we create (see below)|`http://data.inbo.be/ipt/resource?r=bird-tracking-gull-occurrences#Dataset`
**dct:description**|literal|xsd:string|1|[Host#Description](https://github.com/gbif/ipt/blob/acb9ed2a57bda3bbebacd48c0eb777dfdba8437a/src/main/java/org/gbif/ipt/model/AgentBase.java#L41)|`The INBO IPT is hosted at the Research Institute for Nature and Forest (INBO) in Brussels, Belgium.`
**dct:publisher**|resource|foaf:Agent|1|`http://www.gbif.org/publisher/` + [Host#Organization:Key](https://github.com/gbif/ipt/blob/acb9ed2a57bda3bbebacd48c0eb777dfdba8437a/src/main/java/org/gbif/ipt/model/AgentBase.java#L57) with foaf:name [Host#Organization:Name](https://github.com/gbif/ipt/blob/acb9ed2a57bda3bbebacd48c0eb777dfdba8437a/src/main/java/org/gbif/ipt/model/AgentBase.java#L65) and [Host#Homepage](https://github.com/gbif/ipt/blob/master/src/main/java/org/gbif/ipt/model/AgentBase.java#L49)|`http://www.gbif.org/publisher/1cd669d0-80ea-11de-a9d0-f1765f95f18b#Organization` with foaf:name `Research Institute for Nature and Forest (INBO)` and foaf:homepage `http://data.inbo.be/ipt`
**dct:title**|literal|xsd:string|1|[Host#Name](https://github.com/gbif/ipt/blob/acb9ed2a57bda3bbebacd48c0eb777dfdba8437a/src/main/java/org/gbif/ipt/model/AgentBase.java#L65)|`INBO IPT`
foaf:homepage|resource||1|[baseURL](https://github.com/gbif/ipt/blob/master/src/main/java/org/gbif/ipt/config/AppConfig.java#L134)|`baseURL`
dct:issued|literal|xsd:DateTime|1|First [Resource#Created](https://github.com/gbif/ipt/blob/23c2648cb738fbd5ee69d5244ce41e20983f9ae8/src/main/java/org/gbif/ipt/model/Resource.java#L339)|`2012-05-04`
dct:modified|literal|xsd:DateTime|1|Latest [Resource#LastPublished](https://github.com/gbif/ipt/blob/23c2648cb738fbd5ee69d5244ce41e20983f9ae8/src/main/java/org/gbif/ipt/model/Resource.java#L449)|`2015-05-07`
dct:license|resource||1|static|`https://creativecommons.org/publicdomain/zero/1.0/`
dct:spatial|resource|dct:Location|1|[IPT#Latitude](https://github.com/gbif/ipt/blob/89172698ee7bd3934ea4fbd9e18288f11e6448db/src/main/java/org/gbif/ipt/config/AppConfig.java#L146), [IPT#Longitude](https://github.com/gbif/ipt/blob/89172698ee7bd3934ea4fbd9e18288f11e6448db/src/main/java/org/gbif/ipt/config/AppConfig.java#L158)|`{ "type": "Point", "coordinates": [ 4.334187, 50.842133 ] }`
dcat:themeTaxonomy|resource|skos:ConceptScheme|1|static|`<http://eurovoc.europa.eu/218403> a skos:ConceptScheme ; dct:title "biodiversity"@en .`
dct:language|resource|dct:LinguisticSystem|1|static|`dct:language <http://id.loc.gov/vocabulary/iso639-1/en> .`

## dcat:Dataset

## URI

The URI for an IPT dataset will be `http://homepage-of-ipt/resource?r=dataset-name#dataset` (e.g. http://data.inbo.be/ipt/resource?r=bird-tracking-gull-occurrences#Dataset). The URI will become dereferenceable using RDFa. In RDFa, a `rdfs:seeAlso` link will be given to a document which contains the entire DCAT feed (including this URI).

## Concepts

Mandatory concepts are indicated in bold.

predicate | resource or literal | type | # | IPT concept | example
---:|:---:|:---:|:---:|:---|:---
**dct:description**|literal|xsd:string|1|[EML#Description](https://github.com/gbif/gbif-metadata-profile/blob/master/src/main/java/org/gbif/metadata/eml/Eml.java#L753) concatenated|`Bird tracking - GPS tracking of Lesser Black-backed Gull and Herring Gull breeding at the Belgian coast is a species occurrence dataset published by the Research Institute for Nature and Forest (INBO). The dataset curently ...`
**dct:title**|literal|xsd:string|1|[EML#Title](https://github.com/gbif/gbif-metadata-profile/blob/3c312d84f62fb3efbeca08e4fc9178ac4dfe5397/src/main/java/org/gbif/metadata/eml/Eml.java#L718)|`Bird tracking - GPS tracking of Lesser Black-backed Gull and Herring Gull breeding at the Belgian coast`
dcat:contactPoint|resource|vcard:Kind|M|[EML#Contacts](https://github.com/gbif/gbif-metadata-profile/blob/3c312d84f62fb3efbeca08e4fc9178ac4dfe5397/src/main/java/org/gbif/metadata/eml/Eml.java#L661) (not creators)|`[a vcard:Individual; vcard:fn "Eric Stienen"; vcard:hasEmail <mailto:eric.stienen@inbo.be>]`
dct:identifier|literal||1|`http://www.gbif.org/dataset/` + [Resource#Key](https://github.com/gbif/ipt/blob/23c2648cb738fbd5ee69d5244ce41e20983f9ae8/src/main/java/org/gbif/ipt/model/Resource.java#L339)|`http://www.gbif.org/dataset/83e20573-f7dd-4852-9159-21566e1e691e`
dct:issued|literal|xsd:DateTime|1|[Resource#Created](https://github.com/gbif/ipt/blob/23c2648cb738fbd5ee69d5244ce41e20983f9ae8/src/main/java/org/gbif/ipt/model/Resource.java#L339)|`2014-05-15`
foaf:homepage|resource||1|[EML#HomepageURL](https://github.com/gbif/gbif-metadata-profile/blob/3c312d84f62fb3efbeca08e4fc9178ac4dfe5397/src/main/java/org/gbif/metadata/eml/Eml.java#L763)|`http://www.lifewatch.be/birds`
dcat:keyword|literal|xsd:string|M|[EML#Keywords](https://github.com/gbif/gbif-metadata-profile/blob/3c312d84f62fb3efbeca08e4fc9178ac4dfe5397/src/main/java/org/gbif/metadata/eml/Eml.java#L511)|`animal movement`
dcat:landingPage|resource||1|Resource URL|`http://data.inbo.be/ipt/resource?r=bird-tracking-gull-occurrences`
dct:modified|literal|xsd:DateTime|1|[Resource#LastPublished](https://github.com/gbif/ipt/blob/23c2648cb738fbd5ee69d5244ce41e20983f9ae8/src/main/java/org/gbif/ipt/model/Resource.java#L449)|`2015-05-07`
dct:publisher|resource|foaf:Agent|1|`http://www.gbif.org/publisher/` + [Resource#Organization:Key](https://github.com/gbif/ipt/blob/acb9ed2a57bda3bbebacd48c0eb777dfdba8437a/src/main/java/org/gbif/ipt/model/AgentBase.java#L57) with foaf:name [Resource#Organization:Name](https://github.com/gbif/ipt/blob/acb9ed2a57bda3bbebacd48c0eb777dfdba8437a/src/main/java/org/gbif/ipt/model/AgentBase.java#L65)|`http://www.gbif.org/publisher/1cd669d0-80ea-11de-a9d0-f1765f95f18b#Organization` with foaf:name `Research Institute for Nature and Forest (INBO)`
dct:spatial|resource|dct:Location|1|[EML#BoundingCoordinates](https://github.com/gbif/gbif-metadata-profile/blob/c1f766447fbf706f628b98c5e1c88f1ebdd5fb35/src/main/java/org/gbif/metadata/eml/GeospatialCoverage.java#L59)|`{ "type": "Polygon", "coordinates": [ [ [-25, 10], [-25, 60], [10, 60], [10, 10], [-25, 10] ] ] }`
dcat:theme|resource|skos:Concept|1|static|`http://eurovoc.europa.eu/5463`
adms:versionInfo|literal||1|[Resource#Version](https://github.com/gbif/ipt/blob/23c2648cb738fbd5ee69d5244ce41e20983f9ae8/src/main/java/org/gbif/ipt/model/Resource.java#L422)|`5.2`
adms:versionNotes|literal||1|[Resource#ChangeSummary](https://github.com/gbif/ipt/blob/23c2648cb738fbd5ee69d5244ce41e20983f9ae8/src/main/java/org/gbif/ipt/model/Resource.java#L432)|`Update creators, datasetID and occurrenceIDs.`
dcat:distribution|resource|dcat:Distribution|1|DistributionURL - Link to the dwc-a|`http://data.inbo.be/ipt/archive.do?r=bird-tracking-gull-occurrences`
dct:language|resource|dct:LinguisticSystem|1|[Eml#MetaLanguage](https://github.com/gbif/gbif-metadata-profile/blob/3c312d84f62fb3efbeca08e4fc9178ac4dfe5397/src/main/java/org/gbif/metadata/eml/Eml.java#L550)|`dct:language <http://id.loc.gov/vocabulary/iso639-1/eng> .`

## dcat:Distribution

### URI

For each dataset, we'll link to 1 distribution: the Darwin Core Zip file. The URI for such a distribution will be the link to the zip file itself. We ignore EML and RTF distributions, as they do not contain data, only metadata.

### Concepts

Mandatory concepts are indicated in bold.

predicate |  resource or literal | type | # | IPT concept | example
---:|:---:|:---:|:---:|:---|:---
dct:title|literal|xsd:string|1|"Darwin Core Archive of " + [EML#Title](https://github.com/gbif/gbif-metadata-profile/blob/3c312d84f62fb3efbeca08e4fc9178ac4dfe5397/src/main/java/org/gbif/metadata/eml/Eml.java#L718)|`Darwin Core Archive of Bird tracking - GPS tracking of Lesser Black-backed Gull and Herring Gull breeding at the Belgian coast`
dct:description|literal|xsd:string|1|static|`Darwin Core Archive`
dcat:downloadURL|resource||1|URI of distribution|`http://data.inbo.be/ipt/archive.do?r=bird-tracking-gull-occurrences`
dcat:accessURL|resource||1|URL of downloadlocation|`http://data.inbo.be/ipt/resource?r=bird-tracking-gull-occurrences`
dct:format|resource|dct:MediaTypeOrExtent|1|static|`dwc-a`|
dct:license|resource|dct:LicenseDocument|1|[Resource#LicenseURL](https://github.com/gbif/gbif-metadata-profile/blob/3c312d84f62fb3efbeca08e4fc9178ac4dfe5397/src/main/java/org/gbif/metadata/eml/Eml.java#L1273)|`http://creativecommons.org/publicdomain/zero/1.0/legalcode`
dcat:mediaType|resource|dct:MediaTypeOrExtent|1|static|`application/zip`|
