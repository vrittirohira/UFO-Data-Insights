# Content Detection Assignment - 3 - 

Features [our analysis](http://ufo.usc.edu) on UFO data obtained from first and second assignments. 

## Team Members

1.  Akashdeep Singh
2.  Koustav Mukherjee
3.  Sayali Ghaisas
4.  Shiva Deviah
5.  Vritti Rohira

## Getting Started

## Part 1 - Visualizations with D3

Scripts for Generating Data for D3 Visualizations can be found in folder: `d3-data-generation-scripts`

Each script name is the name of the visualization followed by the features it uses for analysis. 
To run each file: 

	python dashboard_elevation_statewise_sightings.py

The corresponding data file is generated in `ufo.usc.edu\Data` folder

The D3 HTML files that use this data are found in `ufo.usc.edu\d3-visualizations` with the same naming convention. 

## Part 2 - Ingesting with Apache Solr

The commands too create a Solr index are all  listed in `solr\commands.txt`

1. Delete any containers with the name "ufo" 
	
	solr.cmd delete -c ufo

2. Create a new container for the data you wish to ingest

	solr.cmd create -c ufo -s 2 -rf 2

3. Create a schema for your index

	curl -X POST -H 'Content-type:application/json' --data-binary "{\"add-field\": {\"name\":\"sighted_at\", \"type\":\"pdate\", 		\"multiValued\":false, \"stored\":true,\"indexed\":true}}" http://localhost:8983/solr/ufo/schema
	
	curl -X POST -H 'Content-type:application/json' --data-binary "{\"add-field\": {\"name\":\"state\", \"type\":\"string\", 		\"multiValued\":false, \"stored\":true,\"indexed\":true}}" http://localhost:8983/solr/ufo/schema

	curl -X POST -H 'Content-type:application/json' --data-binary "{\"add-field\": {\"name\":\"shape\", \"type\":\"string\", 		\"multiValued\":false, \"stored\":true,\"indexed\":true}}" http://localhost:8983/solr/ufo/schema

	curl -X POST -H 'Content-type:application/json' --data-binary "{\"add-copy-field\" : {\"source\":\"*\",\"dest\":\"_text_\"}}" 		http://localhost:8983/solr/ufo/schema

4. Ingest your index

	java -jar -Dc=ufo -Dauto ../example/exampledocs/post.jar "./sightings_state.csv"
	

## Part 3 - Similarity with Memex ImagCat and Image Space

### Part A - FLANN Plugin 

### Part B - SMQTK Plugin  
