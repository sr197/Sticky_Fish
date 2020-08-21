# Sticky_Fish
All the code needed to replicate the Nature Comms Bio 2020 Paper titled "Substrate-dependent fish have shifted less in distribution under climate change."

This file does the following: 
1. Load packages and functions needed to run the code 
2. Prepare the NEFSC bottom trawl dataset from the original format. The original data can be downloaded from oceanadapt.rutgers.edu
3. Select species that are present in a certain number of trawls 
4. Run gams to determine how species CPUE are influenced by different environmental covariates. 
5. Calculate shifts in geographic distributions such as biomass weighted mean centroids and range sizes. 
6. load species classifications from literature 
7. Combine the data 
8. Create figures and perform two sided wilcoxon nonparametric tests


You will need the following datasets for this to run: 

FROM OCEAN ADAPT: 
"neus_Survdat.RData" - 
		Northeast US bottom trawl survey data, in binary format (readable by R). Each line is a  		 record for a species caught within a haul/tow on a cruise. These data have already had conversion factors applied and filtered for "good" tows (shg < 136).

		CRUISE6: six-digit cruise id (first four digits are the year)
		STATION: station number (within a cruise)
		STRATUM: statistical stratum 
		SVSPP: species id. matches to SVSPP in neusSVSPP.RData file
		CATCHSEX: sex of the catch
			0: unsexed
			1: male
			2: female
			3-6?
		SVVESSEL: vessel id
		YEAR: year
		SEASON: season (FALL or SPRING)
		LAT: latitude in decimal degrees
		LON: longitude in decimal degrees
		DEPTH: depth in meters
		SURFTEMP: surface temperature in degrees Celsius
		SURFSALIN: surface salinity 
		BOTTEMP: bottom temperature, deg C
		BOTSALIN: bottom salinity


"neus_SVSPP.RData" - Northeast US bottom trawl species data
	
		SCINAME: scientific name
		SVSPP: species id
		COMNAME: common name
		AUTHOR: author for the species
		
"neusStrata.csv"
		Area for each statistical stratum in the Aleutian Island, Eastern Bering Sea, Gulf of Alaska, and Northeast US surveys. Not all files have all fields.
	
		NPFMCArea: region name
		SubareaDescription: subarea name
		StratumCode: code for the stratum (matches STRATUM in ai, ebs, and goa files)
		OldStratumCode: stratum code from older classification system (only neus)
		DepthIntervalm: range of depths for the stratum, in meters
		Areakm2: area of the stratum in km2
		Areanmi2: area in square nautical miles

FROM AUTHORS WORK 
"ocean_adapt_hab_vars.csv" - NEFSC lat long and time data combined with NAO and AMO data from Hurrel and TNC North Atlantic Marine Ecosystem Regional Assessment dataset in ArcGis. See methodology for details. 

"spp_depth_profiles.csv" - depth profiles collected from literature for each species as well as the information on species orders and types (i.e fish or invertebrate)
