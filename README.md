<img src="EMODnet_compact_colour (1).png" align="right" width="50%"></img>
# EMODnet OGC services Workshop
### Tier 2: How to use OGC webservices offered by EMODnet in your data analysis
## 0. Introduction to OGC web services
In case you are familiar with OGC web services, you can continue in the next sections of the workshop:
- [Search through metadata using the OGC Catalogue Service (CSW)](./1_search_metadata_with_CSW.ipynb) 
- [Visualize data using OGC Web Mapping Service (WMS)](./2_visualize_data_with_WMS.ipynb) 
- [Subset and download data using OGC Web Feature and Coverage Services (WFS/WCS)](./3_subset_and_download_data_with_WFS&WCS.ipynb)
- [Use OGC services from common GIS software](./4_OGC_services_from_common_GIS_software.ipynb)
### What are OGC web services?

Web services offer a variety of standard protocols that use the internet to view, access and retrieve data and metadata. The Open Geospatial Consortium (OGC) has defined various different protocols for geospatial data and metadata.


<br>
<img src="./data/ogc_standards.jpg" align="centre" width="70%"></img>
<br>

### CSW requests
A Catalogue Service for the Web (CSW) is a widely used OGC standard to search collections of metadata for data, services and related information objects and export the metadata in a range of formats.
The CSW core supports three main HTTP requests (operations), which are submitted in the form of a URL:
> The ***GetCapabilities*** allows CSW clients to retrieve service metadata from a server, in this example we access the EMODnet Catalogue Service (CSW).
>> Example:<br>
[https://emodnet.ec.europa.eu/geonetwork/emodnet/eng/csw?<br>
service=CSW&<br>
request=GetCapabilities&<br>
version=2.0.2](	https://emodnet.ec.europa.eu/geonetwork/emodnet/eng/csw?service=CSW&request=GetCapabilities&VERSION=2.0.2)

> The ***GetRecords*** request allows to search for records, returning record IDs
>> Example: Return a summary of the metadata for all records on the EMODnet catalogue. This can be filtered down further using the `constraints` parameter, and then limited to only 10 records for the purpose of this example using the `maxrecords` parameter<br>
[https://emodnet.ec.europa.eu/geonetwork/emodnet/eng/csw?<br>
    request=GetRecords&<br>
    service=CSW&<br>
    version=2.0.2&<br>
    elementSetName=summary&<br>
    outputschema=http://www.opengis.net/cat/csw/2.0.2&<br>
    constraintlanguage=filter&<br> 
    constraint_language_version=1.1.0&<br>
    resulttype=results&<br>
    typenames=csw:record&<br>
    maxrecords=10](https://emodnet.ec.europa.eu/geonetwork/emodnet/eng/csw?REQUEST=GetRecords&SERVICE=CSW&VERSION=2.0.2&ELEMENTSETNAME=summary&OUTPUTSCHEMA=http://www.opengis.net/cat/csw/2.0.2&CONSTRAINTLANGUAGE=FILTER&CONSTRAINT_LANGUAGE_VERSION=1.1.0&RESULTTYPE=results&TYPENAMES=csw:Record&&maxRecords=10)

> The ***GetRecordById*** request retrieves the default representation of catalogue records using their identifier
>> Example: return a record of the Marine communities of the coast of La Gomera in the Canary Islands<br>
[https://emodnet.ec.europa.eu/geonetwork/emodnet/eng/csw?<br>
service=CSW&<br>
version=2.0.2&<br>
request=GetRecordById&<br>
elementSetName=full&<br>
id=5c0f13ee-098a-442c-abfc-d4c08a527476](https://emodnet.ec.europa.eu/geonetwork/emodnet/eng/csw?request=GetRecordById&service=CSW&version=2.0.2&elementSetName=full&id=5c0f13ee-098a-442c-abfc-d4c08a527476)

## Data Visualisation services
### WMS requests
The Web Map Service standard (WMS) provides a simple HTTP interface for requesting geo-registered map images from one or more distributed geospatial databases. A WMS request defines the geographic layer(s) and area of interest to be processed. The response to the request is one or more geo-registered map images (returned as JPEG, PNG, etc) that can be displayed in a Geographic Information System (GIS) or in your own web application (OpenLayers, Leaflet,...).

The Web Map Service standard (WMS) provides a simple HTTP interface for requesting geo-registered map images from one or more distributed geospatial databases. A WMS request defines the geographic layer(s) and area of interest to be processed. The response to the request is one or more geo-registered map images (returned as JPEG, PNG, etc) that can be displayed in a Geographic Information System (GIS) or in your own web application (OpenLayers, Leaflet,...).

The WMS supports the ***GetCapabilities***, ***GetMap*** and ***GetFeatureInfo*** operations as defined in the Open Geospatial Consortium (OGC) WMS standard.
#### WMS GetCapabilities
As such, the mandatory ***GetCapabilities*** operation allows WMS clients to retrieve service metadata from a server. The response to a GetCapabilities request shall be an XML document containing metadata of the service (proposed layers, associated projections, author ...).

The standard to construct a WMS ***GetCapabilities*** request is as follows:

>{wms endpoint url}?SERVICE=WMS&VERSION=1.3.0&REQUEST=GetCapabilities

The EMODnet WMS services are accessible from 7 thematics at the Pan-European scale or global scale for some specific data products. Enter one of the following WMS endpoint URLs into your WMS client (QGIS, ArcMap, MapInfo etc.):
|Thematic|	Description|	WMS GetCapabilities|
|--------|-------------|-----------------------|
|Bathymetry|	Data Products|	https://ows.emodnet-bathymetry.eu/wms?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0|
Bathymetry|	CDI data discovery \n and access service|	https://geo-service.maris.nl/emodnet_bathymetry/wms?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0|
Biology|	Data Products|	https://geo.vliz.be/geoserver/Emodnetbio/wms?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0|
Biology|	New Data Products|	https://ows.emodnet.eu/geoserver/biology/ows?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0|
Biology|	Occurrence data|	https://geo.vliz.be/geoserver/Dataportal/wms?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0|
Chemistry|	Eutrophication|	https://ec.oceanbrowser.net/emodnet/Python/web/wms?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0|
Chemistry|	Litter|	https://sextant.ifremer.fr/services/wms/emodnet_chemistry2?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0|
Chemistry|	Contaminants|	https://geoserver.hcmr.gr/geoserver/EMODNET_SHARED/wms?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0|
Chemistry|	CDI data discovery and access service|	https://geo-service.maris.nl/emodnet_chemistry/wms?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0|
Chemistry|	Distribution of CDI observations per data category (P36) and MSFD sea regions|	https://geo-service.maris.nl/emodnet_chemistry_p36/wms?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0|
Geology|	Sea-floor (bedrock)|	https://drive.emodnet-geology.eu/geoserver/bgr/wms?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0|
Geology|	Marine Minerals|	https://drive.emodnet-geology.eu/geoserver/gsi/wms?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0|
Geology|	Seabed substrate maps|	https://drive.emodnet-geology.eu/geoserver/gtk/wms?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0|
Geology|	Events and Probabilities|	https://drive.emodnet-geology.eu/geoserver/ispra/wms?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0|
Geology|	Coastal Behaviour|	https://drive.emodnet-geology.eu/geoserver/tno/wms?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0|
Geology|	Submerged Landscapes|	https://drive.emodnet-geology.eu/geoserver/bgs/wms?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0|
Geology|	Index of borehole and geophysics data|	https://drive.emodnet-geology.eu/geoserver/geus/wms?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0|
Human Activities|	Data and Data Products|	https://ows.emodnet-humanactivities.eu/wms?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0|
Physics	Data and| Data Products|	https://prod-geoserver.emodnet-physics.eu/geoserver/ows?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0|
Physics	Gridded| Products|	https://prod-erddap.emodnet-physics.eu/ncWMS/wms?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0|
Seabed Habitats|	General datasets and products|	https://ows.emodnet-seabedhabitats.eu/geoserver/emodnet_view/wms?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0|
Seabed Habitats|	Individual habitat map and model datasets|	https://ows.emodnet-seabedhabitats.eu/geoserver/emodnet_view_maplibrary/wms?SERVICE=WMS&REQUEST=GetCapabilities&VERSION=1.3.0|
#### WMS GetMap 
Using the information given in the ***GetCapabilities*** request, the ***GetMap*** request returns a raster map containing the requested data layer selected from all the available layers as defined in the XML document. The elements such as the data layer, region, projection, size of the returned image, image format, etc. are defined in the form of arguments.

>Example of a GetMap request that returns an image of the EMODnet Bathymetry Mean depth (DTM) based on source resolution of 1/8 arc minute (~250 meter) in multi colour style:<br>

[https://ows.emodnet-bathymetry.eu/wms?<br>
            service=WMS&<br>
            request=GetMap&<br>
            version=1.1.1&<br>
            layers=emodnet:mean_multicolour&<br>
            styles=&<br>
            format=image/png&<br>
            transparent=true&<br>
            info_format=text/html&<br>
            tiled=false&<br>
            width=400&<br>
            height=628&<br>
            srs=EPSG:3857&<br>
            bbox=-2669794,2250306,4800533,14538934](https://ows.emodnet-bathymetry.eu/wms?service=WMS&request=GetMap&version=1.1.1&layers=emodnet:mean_multicolour&styles=&format=image/png&transparent=true&info_format=text/html&tiled=false&width=400&height=628&srs=EPSG:3857&bbox=-2669794,2250306,4800533,14538934) 

Which returns: 

![Sample Image](https://ows.emodnet-bathymetry.eu/wms?service=WMS&request=GetMap&version=1.1.1&layers=emodnet:mean_multicolour&styles=&format=image/png&transparent=true&info_format=text/html&tiled=false&width=400&height=628&srs=EPSG:3857&bbox=-2669794,2250306,4800533,14538934)
### Web Map Tile Service
In contrast to a WMS service, which offers real time rendered georeferenced images for a custom geographic extent, a Web Map Tile Service (WMTS) serves pre-rendered georeferenced map tiles with a fixed geographic extent for different zoom levels. As images are pre-rendered and can be cached (locally or remotely), WMTS offers a superior performance for web map viewer applications.

The EMODnet WMTS service are accessible from following endpoints:
|Thematic|	Description|	WMTS GetCapabilities|
|--------|-------------|-----------------------|
Bathymetry|	Data Products|	https://tiles.emodnet-bathymetry.eu/wmts/1.0.0/WMTSCapabilities.xml|
Biology|	Data Products|	https://geo.vliz.be/geoserver/Dataportal/gwc/service/wmts?REQUEST=GetCapabilities&SERVICE=WMTS&VERSION=1.0.0|
Biology|	New Data Products|	https://ows.emodnet.eu/geoserver/biology/gwc/service/wmts?REQUEST=GetCapabilities&SERVICE=WMTS&VERSION=1.0.0|
Biology|	Occurrence data|	https://geo.vliz.be/geoserver/Emodnetbio/gwc/service/wmts?REQUEST=GetCapabilities&SERVICE=WMTS&VERSION=1.0.0|
Chemistry|	Contaminants|	https://geoserver.hcmr.gr/geoserver/EMODNET_SHARED/gwc/service/wmts?REQUEST=GetCapabilities&SERVICE=WMTS&VERSION=1.0.0|
Geology|	Sea-floor (bedrock)|	https://drive.emodnet-geology.eu/geoserver/bgr/gwc/service/wmts?REQUEST=GetCapabilities&SERVICE=WMTS&VERSION=1.0.0|
Geology|	Marine Minerals|	https://drive.emodnet-geology.eu/geoserver/gsi/gwc/service/wmts?REQUEST=GetCapabilities&SERVICE=WMTS&VERSION=1.0.0|
Geology|	Seabed substrate maps|	https://drive.emodnet-geology.eu/geoserver/gtk/gwc/service/wmts?REQUEST=GetCapabilities&SERVICE=WMTS&VERSION=1.0.0|
Geology|	Events and Probabilities|	https://drive.emodnet-geology.eu/geoserver/ispra/gwc/service/wmts?REQUEST=GetCapabilities&SERVICE=WMTS&VERSION=1.0.0|
Geology|	Coastal Behaviour|	https://drive.emodnet-geology.eu/geoserver/tno/gwc/service/wmts?REQUEST=GetCapabilities&SERVICE=WMTS&VERSION=1.0.0|
Geology|	Submerged Landscapes|	https://drive.emodnet-geology.eu/geoserver/bgs/gwc/service/wmts?REQUEST=GetCapabilities&SERVICE=WMTS&VERSION=1.0.0|
Geology|	Index of borehole and geophysics data|	https://drive.emodnet-geology.eu/geoserver/geus/gwc/service/wmts?REQUEST=GetCapabilities&SERVICE=WMTS&VERSION=1.0.0|
Human Activities|	Data and Data Products|	https://ows.emodnet-humanactivities.eu/geoserver/gwc/service/wmts?REQUEST=GetCapabilities&SERVICE=WMTS&VERSION=1.0.0|
Physics|	Data and Data Products|	https://prod-geoserver.emodnet-physics.eu/geoserver/gwc/service/wmts?REQUEST=GetCapabilities&SERVICE=WMTS&VERSION=1.0.0|
Seabed Habitats|	General datasets and products|	https://ows.emodnet-seabedhabitats.eu/geoserver/emodnet_view/gwc/service/wmts?REQUEST=GetCapabilities&SERVICE=WMTS&VERSION=1.0.0|
Seabed Habitats|	Individual habitat map and model datasets|	https://ows.emodnet-seabedhabitats.eu/geoserver/emodnet_view_maplibrary/gwc/service/wmts?REQUEST=GetCapabilities&SERVICE=WMTS&VERSION=1.0.0|
## Data download services
The EMODnet data layers are available as a Web Feature Service (WFS) or Web Coverage Service (WCS) in accordance with the Open Geospatial Consortium (OGC) specifications (www.opengeospatial.org).

Note that some thematics provide other, non-OGC, web services too. For example a central EMODnet ERDDAP server, a REST service to the EMODnet Bathymetry DTM, EMODnet Biology allows specific parameters in the WFS requests, EMODnet Chemistry has an OPeNDAP service. See section Non-OGC web services
### WFS requests
WFS defines a standard for exchanging vector data by querying both the data structure and the source data. The basic operations are GetCapabilities, DescribeFeatureType, and GetFeature. WFS supports a variety of WFS output formats (Ex: GML, shapefile, json, geojson, CSV,...). The full list of output formats supported can be found by performing a WFS GetCapabilities request.

The EMODnet WFS services are accessible from following endpoints:

|Thematic|    Description|    WFS GetCapabilities|
|--------|-------------|-----------------------|
Bathymetry|	Data Products|	https://ows.emodnet-bathymetry.eu/wfs?SERVICE=WFS&REQUEST=GetCapabilities&VERSION=2.0.0|
Biology|	Data Products|	https://geo.vliz.be/geoserver/Emodnetbio/wfs?SERVICE=WFS&REQUEST=GetCapabilities&VERSION=2.0.0|
Biology|	Occurrence data|	https://geo.vliz.be/geoserver/Dataportal/wfs?SERVICE=WFS&REQUEST=GetCapabilities&VERSION=2.0.0|
Chemistry|	Litter|	https://sextant.ifremer.fr/services/wfs/emodnet_chemistry2?SERVICE=WFS&REQUEST=GetCapabilities&VERSION=2.0.0|
Chemistry|	Contaminants|	https://geoserver.hcmr.gr/geoserver/EMODNET_SHARED/wfs?SERVICE=WFS&REQUEST=GetCapabilities&VERSION=2.0.0|
Chemistry|	CDI data discovery and access service|	https://geo-service.maris.nl/emodnet_chemistry/wfs?SERVICE=WFS&REQUEST=GetCapabilities&VERSION=2.0.0|
Chemistry|	Distribution of CDI observations per data category (P36) and MSFD sea regions|	https://geo-service.maris.nl/emodnet_chemistry_p36/wfs?SERVICE=WFS&REQUEST=GetCapabilities&VERSION=2.0.0|
Geology|	Sea-floor (bedrock)|	https://drive.emodnet-geology.eu/geoserver/bgr/wfs?SERVICE=WFS&REQUEST=GetCapabilities&VERSION=2.0.0|
Geology|	Marine Minerals|	https://drive.emodnet-geology.eu/geoserver/gsi/wfs?SERVICE=WFS&REQUEST=GetCapabilities&VERSION=2.0.0|
Geology|	Seabed substrate maps|	https://drive.emodnet-geology.eu/geoserver/gtk/wfs?SERVICE=WFS&REQUEST=GetCapabilities&VERSION=2.0.0|
Geology|	Events and Probabilities|	https://drive.emodnet-geology.eu/geoserver/ispra/wfs?SERVICE=WFS&REQUEST=GetCapabilities&VERSION=2.0.0|
Geology|	Coastal Behaviour|	https://drive.emodnet-geology.eu/geoserver/tno/wfs?SERVICE=WFS&REQUEST=GetCapabilities&VERSION=2.0.0|
Geology|	Submerged Landscapes|	https://drive.emodnet-geology.eu/geoserver/bgs/wfs?SERVICE=WFS&REQUEST=GetCapabilities&VERSION=2.0.0|
Geology|	Index of borehole and geophysics data|	https://drive.emodnet-geology.eu/geoserver/geus/wfs?SERVICE=WFS&REQUEST=GetCapabilities&VERSION=2.0.0|
Human Activities|	Data and Data Products|	https://ows.emodnet-humanactivities.eu/wfs?SERVICE=WFS&REQUEST=GetCapabilities&VERSION=2.0.0|
Physics|	Data and Data Products|	https://prod-geoserver.emodnet-physics.eu/geoserver/ows?SERVICE=WFS&REQUEST=GetCapabilities&VERSION=2.0.0|
Seabed Habitats|	General datasets and products|	https://ows.emodnet-seabedhabitats.eu/geoserver/emodnet_open/wfs?SERVICE=WFS&REQUEST=GetCapabilities&VERSION=2.0.0|
Seabed Habitats|	Individual habitat map and model datasets|	https://ows.emodnet-seabedhabitats.eu/geoserver/emodnet_open_maplibrary/wfs?SERVICE=WFS&REQUEST=GetCapabilities&VERSION=2.0.0|

#### WFS Get Cababilities
> the ***GetCapabilities*** request generates a metadata document (xml) describing a WFS service provided by server as well as valid WFS operations and parameters.

#### WFS DescribeFeature
A ***DescribeFeature*** request returns a description of feature types supported by a WFS service.

> Example of a EMODnet Biology ***DescribeFeature*** request:<br>
[https://geo.vliz.be/geoserver/Dataportal/wfs?<br>
            service=wfs&<br>
            version=2.0.0&<br>
            request=DescribeFeatureType&<br>
            typeName=Dataportal:eurobis&<br>
            outputFormat=application/json](https://geo.vliz.be/geoserver/Dataportal/wfs?service=wfs&version=2.0.0&request=DescribeFeatureType&typeName=Dataportal:eurobis&outputFormat=application/json)

>Example of a EMODnet Human Activities ***DescribeFeature*** request:<br>
[https://ows.emodnet-humanactivities.eu/wfs?<br>
            SERVICE=WFS&VERSION=1.1.0&<br>
            request=describeFeatureType&<br>
            typeName=shellfish&<br>
            bbox=-1.3,0.3,49.2,49.9](https://ows.emodnet-humanactivities.eu/wfs?SERVICE=WFS&VERSION=1.1.0&request=describeFeatureType&typeName=shellfish&bbox=-1.3,0.3,49.2,49.9)

#### WFS GetFeature
> the ***GetFeature*** request returns a selection of features from a data source including geometry and attribute values.

>Example of a EMODnet Human Activities ***GetFeature*** request:<br>
[https://ows.emodnet-humanactivities.eu/wfs?<br>
            SERVICE=WFS&VERSION=1.1.0&<br>
            request=getFeature&<br>
            typeName=shellfish&<br>
            bbox=-1.3,0.3,49.2,49.9&<br>
            outputFormat=application/json](https://ows.emodnet-humanactivities.eu/wfs?SERVICE=WFS&VERSION=1.1.0&request=getFeature&typeName=shellfish&bbox=-1.3,0.3,49.2,49.9&outputFormat=application/json)
### WCS requests
A Web Coverage Service (WCS) is a data-access protocol that defines and enables the web-based retrieval of multi-dimensional raster type geospatial datasets.  
The WCS core supports three main HTTP requests (operations), which are submitted in the form of a URL:

The EMODnet thematics provide Web Coverage Services (WCS) to support requests for coverage data (rasters) or gridded data products, accessible from one of the following adresses:

|Thematic|    Description|    WCS GetCapabilities|
|--------|-------------|-----------------------|
Bathymetry|	Data Products|	https://ows.emodnet-bathymetry.eu/wcs?SERVICE=WCS&REQUEST=GetCapabilities&VERSION=2.0.1|
Biology|	Data Products|	https://geo.vliz.be/geoserver/Emodnetbio/wcs?SERVICE=WCS&REQUEST=GetCapabilities&VERSION=2.0.1|
Biology|	New Data Products|	https://ows.emodnet.eu/geoserver/biology/ows?SERVICE=WCS&REQUEST=GetCapabilities&VERSION=2.0.1|
Human Activities|	Data and Data Products|	https://ows.emodnet-humanactivities.eu/wcs?SERVICE=WCS&REQUEST=GetCapabilities&VERSION=2.0.1|
Seabed Habitats|	Individual habitat map and model datasets|	https://ows.emodnet-seabedhabitats.eu/geoserver/emodnet_open_maplibrary/wcs?SERVICE=WCS&REQUEST=GetCapabilities&VERSION=2.0.1|
#### WCS GetCapabilities
A WCS GetCapabilities request returns an XML document with information to the service and data provider and an overview of all the coverages (raster dataset) available on the web server.

#### WCS DescribeCoverage
A WCS ***DescribeCoverage*** request returns an XML document with metadata information fully describing one specific coverage
>Example of an EMODnet Bathymetry ***DescribeCoverage*** request:<br>
[https://ows.emodnet-bathymetry.eu/wcs?<br>
            service=wcs&<br>
            version=1.0.0&<br>
            request=DescribeCoverage&<br>
            coverage=emodnet:mean](https://ows.emodnet-bathymetry.eu/wcs?service=wcs&version=1.0.0&request=DescribeCoverage&coverage=emodnet:mean)

#### WCS GetCoverage
A WCS ***GetCoverage*** request returns a full coverage encoded in a specified format, e.g GeoTiff, XML or netCDF. similarly to a WMS ***GetMap*** request, but with several extensions to support the retrieval of coverages.

>Example of an EMODnet Bathymetry ***GetCoverage*** request:<br>
[https://ows.emodnet-bathymetry.eu/wcs?<br>
            service=wcs&version=1.0.0&<br>
            request=getcoverage&<br>
            coverage=emodnet:mean&<br>
            crs=EPSG:4326&<br>
            BBOX=-2.52,45.6,-1.08,46.40&<br>
            format=image/tiff&<br>
            interpolation=nearest&<br>
            resx=0.00208333&<br>
            resy=0.00208333](https://ows.emodnet-bathymetry.eu/wcs?service=wcs&version=1.0.0&request=getcoverage&coverage=emodnet:mean&crs=EPSG:4326&BBOX=-2.52,45.6,-1.08,46.40&format=image/tiff&interpolation=nearest&resx=0.00208333&resy=0.00208333)
## Non-OGC web services
|Thematic|	web service|	URL|
|--------|-------------|-----------------------|
EMDOnet|	ERDDAP|	https://erddap.emodnet.eu/erddap/index.html|
Bathymetry|	REST API|	https://rest.emodnet-bathymetry.eu/|
Chemistry|	THREDDS|	http://opendap.oceanbrowser.net/thredds/catalog/data/emodnet-domains/catalog.html XML version: http://opendap.oceanbrowser.net/thredds/catalog/data/emodnet-domains/catalog.xml|
Physics|	ERDDAP|	https://prod-erddap.emodnet-physics.eu/erddap/index.html

#### Other useful links with documentation on EMODnet web services
- Biology Github: https://github.com/EMODnet/EMODnet-Biology-Guidance
- Chemistry GitHub: https://github.com/gher-ulg/EMODnet-Chemistry
- Physics GitHub: https://github.com/EMODnet-Physics
- Seabed habitats GitHub: https://github.com/emodnetseabedhabitats
- Other repos in the main EMODnet GitHub: https://github.com/EMODnet

#### OGC service status
Having trouble? Verify the status of the EMODnet OGC services at https://monitor.emodnet.eu.

### [>> Next: Search through metadata using the OGC Catalogue Service (CSW)](Tutorial_Part_1_CSW.ipynb)
<hr>
This workshop was adapted from the [Pydata 2017 workshop of Julia Wagemann](https://github.com/jwagemann/2017_pydata_tutorial) <a rel="license" href="https://creativecommons.org/licenses/by/4.0/"><img style="float: right" alt="Creative Commons Lizenzvertrag" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a>

