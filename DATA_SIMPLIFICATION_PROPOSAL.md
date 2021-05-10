# Data and Service Linking Simplification - Consolidated Proposal

## Introduction

Author: EC JRC based on input from INSPIRE MIWP sub-group 2.3.1.

Short description:
This is a consolidated proposal, based on the collection and comparison of proposals received from the contributing Member State representatives (NL, FR, ES, LT) of this subgroup.

This proposal implements the requirements and recommendations as initially described in the discussion paper and further improved by the subsequent proposals made by members of the sub-group.
This proposal is aligned with the discussion paper and the reference for the metadata specification is INSPIRE TG version 2.0.1. 


## Proposal

1. For the protocol codelist, the INSPIRE Registry already offers a series of external codelist values here: https://inspire.ec.europa.eu/metadata-codelist/ProtocolValue

2. Regarding the codelist labels, in the OGC vocabularies they specify a simple label. For instance, the preferred label for `http://www.opengis.net/def/serviceType/ogc/wfs` is `wfs`. For those OGC protocol cases, we think that we can keep the format `OGC:***`.

#### View Services

```xml
<gmd:applicationProfile>
    <gmx:Anchor xlink:href="http://inspire.ec.europa.eu/metadata-codelist/SpatialDataServiceType/view">view</gmx:Anchor>
</gmd:applicationProfile>
```

OGC Vocabulary
http://defs.opengis.net/vocprez/object?uri=http%3A//www.opengis.net/def/serviceType

Then, the protocol must be specified. In INSPIRE, WMS 1.3.0 (preferred) or WMS 1.1.1 (optional)

```xml
<gmd:protocol>
    <gmx:Anchor xlink:href="http://www.opengis.net/def/serviceType/ogc/wms">OGC:WMS</gmx:Anchor>
</gmd:protocol>
```

alternatively, the WMTS protocol from another OGC vocabulary can be specified (http://defs.opengis.net/vocprez/object?uri=http%3A//www.opengis.net/def/standards-baseline)

```xml
<gmd:protocol>
    <gmx:Anchor xlink:href="http://www.opengis.net/def/serviceType/ogc/wmts">OGC:WMTS</gmx:Anchor>
</gmd:protocol>
```

#### Download services

```xml
<gmd:applicationProfile>
    <gmx:Anchor xlink:href="http://inspire.ec.europa.eu/metadata-codelist/SpatialDataServiceType/download">download</gmx:Anchor>
</gmd:applicationProfile>
```

##### ATOM

```xml
<gmd:protocol>
    <gmx:Anchor xlink:href="https://tools.ietf.org/html/rfc4287">ATOM Syndication Format</gmx:Anchor>
</gmd:protocol>
```

##### OGC (WFS, SOS)

```xml
<gmd:protocol>
    <gmx:Anchor xlink:href="http://www.opengis.net/def/serviceType/ogc/wfs">OGC:WFS</gmx:Anchor>
</gmd:protocol>
```

```xml
<gmd:protocol>
    <gmx:Anchor xlink:href="http://www.opengis.net/def/serviceType/ogc/sos">OGC:SOS</gmx:Anchor>
</gmd:protocol>
```

```xml
<gmd:protocol>
    <gmx:Anchor xlink:href="http://www.opengis.net/def/serviceType/ogc/wcs">OGC:WCS</gmx:Anchor>
</gmd:protocol>
```

NOTE: tbd how to express OGC APIs (OGC SensorThings API, OGC API - Features) 

#### Use of the FUNCTION element instead of DESCRIPTION to distinguish GetCapabilities from "download" operations (GetMap/GetFeature)

GetCapabilities
```xml
<gmd:function>
    <gmd:CI_OnLineFunctionCode codeList="http://standards.iso.org/iso/19139/resources/gmxCodelists.xml#CI_OnLineFunctionCode" codeListValue="information" />
</gmd:function>
```

"Download" operations
```xml
<gmd:function>
    <gmd:CI_OnLineFunctionCode codeList="http://standards.iso.org/iso/19139/resources/gmxCodelists.xml#CI_OnLineFunctionCode" codeListValue="download" />
</gmd:function>
```

### Examples (XML encoded)

1.	Link to GetCapabilities of an INSPIRE WMS view service containing the dataset.
- **protocol** element contains an anchor with the value *OGC:WMS* and the definition of the protocol (http://www.opengis.net/def/serviceType/ogc/wms),
- **applicationProfile** element contains an anchor with the value *view* and the servicetype (http://inspire.ec.europa.eu/metadata-codelist/SpatialDataServiceType/view),
- **name** element contains the name of the service,
- **function** element contains a CI_OnLineFunctionCode element with codeListValue *information* from codelist http://standards.iso.org/iso/19139/resources/gmxCodelists.xml#CI_OnLineFunctionCode to denote *GetCapabilities*.

```xml
<gmd:transferOptions>
  <gmd:MD_DigitalTransferOptions>
      [...]
    <gmd:onLine>
      <gmd:CI_OnlineResource>
        <gmd:linkage>
          <gmd:URL>http://inspirelab.geonovum.nl/test/kad/wms?request=GetCapabilities&amp;service=WMS</gmd:URL>
        </gmd:linkage>
        <gmd:protocol>
          <gmx:Anchor xlink:href="http://www.opengis.net/def/serviceType/ogc/wms">OGC:WMS</gmx:Anchor>
        </gmd:protocol>
        <gmd:applicationProfile>
          <gmx:Anchor xlink:href="http://inspire.ec.europa.eu/metadata-codelist/SpatialDataServiceType/view">view</gmx:Anchor>
        </gmd:applicationProfile>
        <gmd:name>
          <gco:CharacterString>Bestuurlijke grenzen WMS</gco:CharacterString>
        </gmd:name>
        <gmd:function>
          <gmd:CI_OnLineFunctionCode codeList="http://standards.iso.org/iso/19139/resources/gmxCodelists.xml#CI_OnLineFunctionCode" codeListValue="information" />
        </gmd:function>
      </gmd:CI_OnlineResource>
    </gmd:onLine>
      [...]
  </gmd:MD_DigitalTransferOptions>
</gmd:transferOptions>
```


```xml
<examplexml>
                  <gmd:onLine>
                  <gmd:CI_OnlineResource>
                     <gmd:linkage>
                        <gmd:URL>http://inspirelab.geonovum.nl/test/kad/wms?request=GetCapabilities&amp;service=WMS</gmd:URL>
                     </gmd:linkage>
                     <gmd:protocol>
                        <gmx:Anchor xlink:href="http://www.opengis.net/def/serviceType/ogc/wms">OGC:WMS</gmx:Anchor>
                     </gmd:protocol>
                     <gmd:applicationProfile>
                        <gmx:Anchor xlink:href="http://inspire.ec.europa.eu/metadata-codelist/SpatialDataServiceType/view">view</gmx:Anchor>
                     </gmd:applicationProfile>
                     <gmd:name>
                        <gco:CharacterString>Bestuurlijke grenzen WMS</gco:CharacterString>
                     </gmd:name>
                     <gmd:description>
                        <gmx:Anchor xlink:href="http://inspire.ec.europa.eu/metadata-codelist/OnLineDescriptionCode/accessPoint">accessPoint</gmx:Anchor>
                     </gmd:description>
                  </gmd:CI_OnlineResource>
               </gmd:onLine>
</examplexml>
```

```xml
<examplexml>
               <gmd:onLine>
                  <gmd:CI_OnlineResource>
                     <gmd:linkage>
                        <gmd:URL>http://inspirelab.geonovum.nl/test/kad/wfs?request=GetCapabilities&amp;service=WFS</gmd:URL>
                     </gmd:linkage>
                     <gmd:protocol>
                        <gmx:Anchor xlink:href="http://www.opengis.net/def/serviceType/ogc/wfs">OGC:WFS</gmx:Anchor>
                     </gmd:protocol>
                     <gmd:applicationProfile>
                        <gmx:Anchor xlink:href="http://inspire.ec.europa.eu/metadata-codelist/SpatialDataServiceType/download">download</gmx:Anchor>
                     </gmd:applicationProfile>
                     <gmd:name>
                        <gco:CharacterString>Bestuurlijke grenzen WFS</gco:CharacterString>
                     </gmd:name>
                     <gmd:description>
                        <gmx:Anchor xlink:href="http://inspire.ec.europa.eu/metadata-codelist/OnLineDescriptionCode/accessPoint">accessPoint</gmx:Anchor>
                     </gmd:description>
                  </gmd:CI_OnlineResource>
               </gmd:onLine>
</examplexml>
```

### Advantages/disadvantages of the proposed approach
_text here. Expose criticalities, limits or already know open issues about this proposal_

### Conclusions 
_text here_
