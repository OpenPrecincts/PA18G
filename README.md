# Pennsylvania 2018 precinct matching

Joins precinct geometries with election results for the 2018 Pennsylvania General Election.

Author: [Baxter Demers](https://github.com/baxterdemers)

## Sources

Source files and additional supporting documentation can also be found in [this repository.](https://github.com/OpenPrecincts/PA18G)

### Main Sources

#### [Open Elections - 2018 PA General Election - Precinct Level Results](https://github.com/openelections/openelections-data-pa/blob/master/2018/20181106__pa__general__precinct.csv)

* Relative Path: `data/election-results/open-elections/20181106__pa__general__precinct.csv`
* Link: <https://github.com/openelections/openelections-data-pa/blob/master/2018/20181106__pa__general__precinct.csv>
* Date Accessed: August 25, 2020

#### [US Census Partnership Files](https://www.census.gov/geo/partnerships/pvs/partnership19v1/st42_pa.html)

* Relative Path: `data/shapefiles/pa-precincts/census-partnership`
* Link: <https://www.census.gov/geo/partnerships/pvs/partnership19v1/st42_pa.html>
* Date Accessed: June 25, 2020

### Additional Sources

#### [MEDSL County Level Election Results - PA 2018 General](https://github.com/MEDSL/2018-elections-unoffical/blob/master/raw-returns/Pennsylvania.CSV)

* Relative Path: `data/election-results/MEDSL/pa-county-level-results.csv`
* Link: <https://github.com/MEDSL/2018-elections-unoffical/blob/master/raw-returns/Pennsylvania.CSV>
* Date Accessed: July 9, 2020

#### [PA Department of State - Official Results](https://www.electionreturns.pa.gov/General/SummaryResults?ElectionID=63&ElectionType=G&IsActive=0)

* Relative Path: `data/election-results/official-state-results-pa-2018/pa-department-of-state-official-results.csv`
* Downloaded with: `data/election-results/official-state-results-pa-2018/get_official_county_level_results.ipynb`
* Link: <https://www.electionreturns.pa.gov/General/SummaryResults?ElectionID=63&ElectionType=G&IsActive=0>
* Date Accessed: July 9, 2020

#### [PA 2018 Congresional Districts](https://catalog.data.gov/dataset/tiger-line-shapefile-2018-nation-u-s-116th-congressional-district-national)

* Relative Path: `data/shapefiles/tl_2018_us_cd116`
* Link: <https://catalog.data.gov/dataset/tiger-line-shapefile-2018-nation-u-s-116th-congressional-district-national>
* Date Accessed: July 28, 2020

## Metadata

* `loc_prec`: Unique precinct identifier. (read as "locality, precinct" - locality is analogous to county_id here)
* `GEOID`: Unique county identifier. The State FIPS code concatenated with the County Fips code. [Learn More...](https://github.com/OpenPrecincts/verification#geoid-spec)
* `county_id`: The name of the county the precinct is in
* `precinct`: The name of the precinct
* `G18DemSen`: Votes for Democrats for U.S. Senate
* `G18RepSen`: Votes for Republicans for U.S. Senate
* `G18LibSen`: Votes for Libertarians for U.S. Senate
* `G18GreSen`: Votes for Greens for U.S. Senate
* `G18IndSen`: Votes for Independents for U.S. Senate
* `G18DemGov`: Votes for Democrats for Governor
* `G18RepGov`: Votes for Republicans for Governor
* `G18LibGov`: Votes for Libertarians for Governor
* `G18GreGov`: Votes for Greens for Governor
* `G18IndGov`: Votes for Independents for Governor
* `G18DemHOR`: Votes for Democrats for U.S. House
* `G18RepHOR`: Votes for Republicans for U.S. House
* `G18LibHOR`: Votes for Libertarians for U.S. House
* `G18GreHOR`: Votes for Greens for U.S. House
* `G18IndHOR`: Votes for Independents for U.S. House
* `geometry` : A Polygon outlining the precinct

## Process

### Download the census partnernship files

Used `data/shapefiles/pa-precincts/census-partnership/scrape_census_partnership_files.py` with slight modifications from the [original](https://github.com/PrincetonUniversity/gerryspam/blob/master/General/scrape_partnership.py)

Missing VTDs for these counties:

* Armstrong County (42005)
* Westmoreland County (42129)
* Delaware County (42045)

From the counties that had them were combined into one shapefile:  `data/shapefiles/pa-precincts/census-partnership/compiled`

### Aquire Precinct Maps from missing counties

#### Armstrong County

* 7/7/2020 - Emailed  jbbellas@co.armstrong.pa.us based on this [link](https://co.armstrong.pa.us/index.php/departments-m/elections-voters-registration-m) No reply by (9/11/2020).
* **Action Taken:** Patched in Armstrong shapefiles from the [2016 precinct shapefile](https://github.com/nvkelso/election-geodata/tree/master/data/42-pennsylvania/statewide/2017) (accessed 9/11/2020 stored locally at `data/shapefiles/pa-precincts/VTDs_Oct17`) made by [Michal Migurski](https://github.com/migurski).

#### Delaware County

* 7/7/2020 - Spoke with a man on the phone 610-891-4673. He said I would have to come in person to see the precinct map. He also suggested I contact local campaigns to see if they already had it.
* **Action Taken:** Patched in Delaware shapefiles from the [2016 precinct shapefile](https://github.com/nvkelso/election-geodata/tree/master/data/42-pennsylvania/statewide/2017) (accessed 9/11/2020 stored locally at `data/shapefiles/pa-precincts/VTDs_Oct17`) made by [Michal Migurski](https://github.com/migurski).

#### Westmoreland County

* 7/7/2020 - Spoke with Eric Glod on the phone (724) 830-3996. Emailed him a written proposal so he could circulate it to his coworkers to see if he could share the map.
* Was unable to get Eric Glod to follow up.
* **Action Taken:** Patched in Westmoreland shapefiles from the [2016 precinct shapefile](https://github.com/nvkelso/election-geodata/tree/master/data/42-pennsylvania/statewide/2017) (accessed 9/11/2020 stored locally at `data/shapefiles/pa-precincts/VTDs_Oct17`) made by [Michal Migurski](https://github.com/migurski).
* Only tricky part of matching were the 8 Hempfield Township precincts, which were numbered in the results and named in the shapefiles. Fortunately, their [polling locations](https://apps.co.westmoreland.pa.us/elections/ElectionBallots/Ballots/Precincts.aspx?pk_campaign=Ballots) (accessed 9/11/2020 - screen shot stored locally at `Unmatched precincts/Westmoreland/Polling Locations -Screen Shot 2020-09-11 at 12.40.21 PM.png`) had both the number and the name for each precinct, so I used that to match them up.

### Compare Open Elections and MEDSL Election Results

Wrote `Open Elections + VTDs precinct matching.ipynb` and `data/election-results/MEDSL/MEDSL + VTDs precinct matching.ipynb` to attempt to match the precinct results with the VTD shapefile from the census. Prepared `data/election-data-report.pdf` to highlight the differences between the data sources. Ultimately, the Open Elections results seemed to be most compatible with the VTDs so I proceed to match the VTDs with the Open Elections Results.

### Fixing Mismatches

To match the precinct geometries and election results a first pass of string manipluation was applied to attempt to remove noise. This fuzzy matching resulted in `96.699%` of precinct being matched up. However, that `~3%` of precincts that weren't matched meant hundreds of unmatched precincts. Moreover, in some cases the fuzzy match removes too much information resulting in one to many or many to many matches. For example, in some counties it was helpful to remove `Township` and `Borough` from precinct names, but in others there could be `Almaden Township` **and** `Almaden Borough` - in this case removing `Township` and `Borough` would mean two precincts named `Almaden`.

The 2018 redraw of Pennsylvannia's Congressional Districts also resulted in a handful of mismatches as the precinct geometries were out of date. After identifing these geometries, I corrected them using the 2018 congressional district shapefile published by the U.S. Census.

Another problem arrises for precinct geometries in the same county with duplicate `NAMELSAD` values. In most cases, these ambiguities were the result of a [township](https://en.wikipedia.org/wiki/Township_(Pennsylvania)#:~:text=A%20Pennsylvania%20township%20or%20township,majority%20of%20land%20areas%20in) and [borough](https://en.wikipedia.org/wiki/Borough_(Pennsylvania)#:~:text=In%20the%20U.S.%20commonwealth%20of,density%20in%20its%20residential%20areas.) with the same name. In the VTD shapefile their names were the same, but the borough/township distinciton was made in the Open Elections results. Therefore, I could simply search (with google maps) for boundries of the the borough and assign the borough election results to that geometry.

The steps I took to rectify both types of mismatches are described below:

#### Allegheny County

* In VTD shapefile `['whitehall 1 a (cong 14)', 'whitehall 1 b (cong 18)']`
* In OE shapefile `['whitehall 1']`
* Based on the 2018 re-draw (`PA 2018 Congresional Districts`), the VTD shapefile is out of date. Whitehall is fully contained in PA's 18th Congressionl District.
* Action taken: Combined `'whitehall 1 a (cong 14)', 'whitehall 1 b (cong 18)'` into one geometry and renamed it to `'whitehall 1`

#### Beaver County

* In VTD Shapefile `['ellwood city', 'new sewickley feazel', 'new sewickley freedom', 'new sewickley unionville']`
* In OE shapefile `['new sewickley 1', 'new sewickley 2', 'new sewickley 3', 'north sewickley 4']`
* Found `Unmatched precincts/Beaver County/beaver-polling-places.pdf` from Beaver County's [website](http://www.beavercountypa.gov/Depts/Elections/Documents/polling%20places.pdf)
* Used Google Maps to geocode the location of polling places to match the polling places with precinct geometeries. Then used the names of the polling places to determine which election results should be attributed to each shape (possible because the polling places have the same naming convention as the election results).

#### Bedford County

* In the election results, the precinct were listed as numbers (e.g. 0701) whereas the VTDs had names (e.g. BEDFORD DISTRICT 01). I used this [PDF](https://www.bedfordcountypa.org/document_center/Elections/Precincts%20-%20Temporary%202020%20precincts.pdf) (stored locally at `county-files/Bedford County/Precincts - Temporary 2020 precincts.pdf`) of precinct locations from Bedford County's Board of Elections to create a lookup table (`county-files/Bedford County/split_polling_locations.csv`) that allowed me to convert from numbers to names. Applying this lookup table to the election results yielded a complete match with the VTDs.

#### Berks County

* VTDs: `['1', 'adamstown', 'cumru 1 a (cong 6)', 'cumru 1 b (cong 16)', 'exeter 5', 'laureldale 1 a (cong 6)', 'laureldale 1 b (cong 16)']`
* OEs:  `['(4 cong)', '(9 cong)', 'cumru 1', 'exeter 5 1 (6 cong)', 'exeter 5 2 (9 cong)', 'laureldale 1']`
* Precinct `1` in the VTDs was divided into the 4th congressional and 9th congressional because of the 2018 redraw.
* Similarly, Exeter 5 needs to be split into 6th and 9th.
* Based on the 2018 re-draw (`PA 2018 Congresional Districts`), `laureldate 1` is fully contained in PA CD-9, so it was dissolved into one shape.
* Based on the 2018 re-draw (`PA 2018 Congresional Districts`), `cumru 1` is fully contained in PA CD-9, so it was dissolved into one shape.
* Adamstown votes in Lancaster county so that was marked accordingly in the County ID Column.

#### Blair County

* VTDs: `['tunnelhill']`
* OEs:  `[]`
* tunnelhill is a part of the tunnelhill precinct Cambria County (combined with the precinct in Cambria)

#### Bucks County

* 2 geometries called "NEWTOWN DISTRICT 01"
* 2 geometries called "NEWTOWN DISTRICT 02"
* Used `VTD duplicate precincts/Bucks/2018generalelection-certifiedreturnsmunicipality.pdf` (downloaded from Bucks County's [website](http://www.buckscounty.org/government/CommunityServices/BoardofElections/ElectionInformation)) to determine which geometries where Newtown Boro and which were Newtown Twp.

#### Cambria County

* VTDs: ` ['johns 11', 'johns 8 2', 'johns center town 1', 'johns center town 2', 'barr south a (cong 9)', 'barr south b (cong 12)', 'east taylor 3', 'east taylor 4', 'northern cambria 3 a (cong 9)', 'northern cambria 3 b (cong 12)', 'reade north', 'reade south'] `
* OEs: ` ['johns center town', 'johns 21', 'barr', 'northern cambria 3', 'reade'] `
* Combine reade north and south shapes into one shape 'reade' to match with the results for reade (elections results are aggregated under reade (consistent in MEDSL and Open Elections))
* Combine 'johns center town 1' and 'johns center town 2' shapes into one shape 'johns center town' (elections results are aggregated under 'johns center town' (consistent in MEDSL and Open Elections))
* Combine 'barr south a (cong 9)', 'barr south b (cong 12)' into 'barr' (now both in PA-CD-15 with 2018 redraw)
* Combine 'northern cambria 3 a (cong 9)', 'northern cambria 3 b (cong 12)' into 'northern cambria 3' (now both in PA-CD-15 with 2018 redraw)
* VTD Orphans: ` ['johns 11', 'johns 8 2',  'east taylor 3', 'east taylor 4'] `
Johnstown-8th Ward 2 - in 2016 but not 2018
Johnstown - Eleventh Ward in 2016 not 2018
East Taylor Twp 3 in 2016 but not 2018
East Taylor Twp 4 in 2016 not 2018
* October 2, Called [Cambria County PA Board of Elections](https://www.cambriacountypa.gov/election-and-voter-registration.aspx) and spoke with the Director.
* Was informed of the following mergers:
* Johnstown-8th Ward 2 was combined with Johnstown-8th Ward 3
* JOHNSTOWN WARD 11 was combined with JOHNSTOWN DISTRICT OLD CONEMAUGH
* The 2018 redraw of congressional districts sliced East Taylor Twp 3 and East Taylor Twp 4 as they were in 2016. Accordinly, parts of those districts that were in Congresional District 15 were combined with EAST TAYLOR DISTRICT 01 under the name "EAST TAYLOR DISTRICT 01". Likewise, parts of East Taylor Twp 3 and East Taylor Twp 4 that were in Congressional District 13 were combined with EAST TAYLOR DISTRICT 02 under the name "EAST TAYLOR DISTRICT 02".
* I coded mergers according to the information from the County Board of Elections as laid out in this section.

#### Carbon County

* VTDs: ` [] `
* OEs: ` ['penn forest 2 northeast', 'fast penn south', 'franklin twp�harrity', 'i towamensing south 1'] `
* All OCR (object character recognition) mistakes - I manually corrected them in the script and it yielded full matching for Carbon County:
* 'fast penn south', originally '7 Fast Penn Twp-South', is a misread of '7 East Penn Twp-South'. So renamed 'fast penn south' to 'east penn south'.
* 'penn forest 2 northeast', originally '51-4 Penn Forest Two-Northeast' is a misread of '51-4 Penn Forest Twp-Northeast'. so renamed to 'penn forest north east'
* 'franklin twp�harrity' -> 'franklin harrity'
* '57-I Towamensing Twp-South-1' is a misread of '57-1 Towamensing Twp-South-1'. So rename 'i towamensing south 1' to 'towamensing south 1'

#### Centre County

* In the election results, the precinct were listed as numbers (e.g. 12) whereas the VTDs had names (e.g. halfmoon precinct east central). I used Centre County's [polling place website](https://centrecountyvotes.com/voting/voting-locations/) to create a lookup table (stored locally at `county-files/Centre County/num_to_name.csv`) that allowed me to convert from numbers to names.
* Applying this lookup table + a few corrections/additions from [Centre County](https://centrecountypa.gov/DocumentCenter/View/7758/2018-General-Precinct-Results) (stored locally at `county-files/Centre County/2018_general_precinct_results.pdf`)  to the election results yielded a complete match with the VTDs.

#### Chester County

* VTDs: `['kennett 2 a (cong 7)', 'kennett 2 b (cong 16)', 'phoenixville middle 1 (hd 157)', 'phoenixville middle 1 (hd 155)']`
* OEs: ` ['kennett 2', 'phoenixville middle 1'] `
* VTDs were split in the map preceeding the 2018 redraw of PA's congressional districts so the VTDs are out of date.
* 'kennett 2 a (cong 7)' and 'kennett 2 b (cong 16)' renamed to 'kennet 2'
* 'phoenixville middle 1 (hd 157)' and 'phoenixville middle 1 (hd 155)' renamed to 'phoenixville middle 1'
  
#### Clarion County

* VTDs: ` ['farmington west', 'farmington north', 'farmington south', 'piney a (cong 3)', 'piney b (cong 5)', 'emlenton'] `
* OEs: ` ['farmington', 'piney'] `
* Combined 'piney a (cong 3)', 'piney b (cong 5)' under the name 'piney' (now both in PA-CD-15 with 2018 redraw)
* emlenton is part of the emlenton precinct in Venango County (combined with the precinct in Venango)
* Combined 'farmington west', 'farmington north' and 'farmington south' into one shape 'farmington' to match with the results for farmington (elections results are aggregated under farmington (consistent in MEDSL and Open Elections))

#### Columbia County

* VTDs: ` ['ashland'] `
* OEs: ` [] `
* ashland is part of the ashland precinct in Schuylkill County (combined with the precinct in Schuylkill)

#### Cumberland County

* VTDs: ` [] `
* OEs: ` ['lower allen 1 annex'] `
* See also `Unmatched precincts/Cumberland/LowerAllen_precincts.pdf`
* Spoke to Board of Elections - Annex and 1 are two different school districts - seperate polling places, seperate results. I could just combine them (ballot is the same) or keep seperate. I emailed `gis@ccpa.net`
* They sent me their precinct shapefile via this link: <https://open-data-ccpa.hub.arcgis.com/datasets/voting-precincts> (also availible locally at `county-files/Cumberland County/Voting_Precincts-shp`) I substituted the Census VTDs for Cumberland with the shapefile from the county and that fixed all my remaining issues (after I parsed out the Open Elections precinct name pattern from their columns)
* 'north middleton 3' and 'north middleton 1' have seperate shapefiles for CD 10 and CD 13, but the [official county election results](https://records.ccpa.net/weblink_public/9/edoc/1142717/Official%20Precinct%20Report.pdf) only split those precincts for the congressional races. The rest of the offices e.g. Senator have results that don't differentiate between voters in CD 10 and CD 13. Therefore, I merged the geometries for CD 10 and CD 13.

#### Dauphin County

* VTDs: ` ['highspire 1', 'highspire 2', 'millersburg 2', 'steelton 2 2', 'steelton 3 1', 'steelton 3 2', 'millersburg 1', 'steelton 2 1', 'susquehanna 1 a (cong 11)', 'susquehanna 3 a (cong 4)', 'susquehanna 3 b (cong 11)', 'susquehanna 1 b (cong 4)'] `
* OEs: ` ['highspire', 'millersburg', 'steelton 2', 'steelton 3', 'susquehanna 1', 'susquehanna 3', 'swatara 10'] `
* Contacted Dauphin County and aquired their most up to date precinct shapefile. Availible at this link: <https://data-dauphinco.opendata.arcgis.com/datasets/voting-districts> and locally at `county-files/Dauphin County/Voting_Districts-shp`. I substituted the Census VTDs for Dauphin with the shapefile from the county and that fixed all my remaining issues (after I parsed out the Open Elections precinct name pattern from their columns)

#### Elk County

* VTDs: ` ['horton'] `
* OEs: ` ['north horton', 'south horton'] `
* Needed to aquire the shapefile which splits north and south horton. They should be split like in the [results](https://www.co.elk.pa.us/images/Elections/PriorElectionResults/precinct2018general.pdf) (stored in this directory at `county-files/Elk County/precinct2018general.pdf`)
* August 27, recieved a shapefile of Elk County Precincts from James M. Abbey, Director, Elk County IT/GIS Department. Stored locally at `county-files/Elk County/ElkCoPAdistricts`. Replaced the VTDs from the census with these precincts for Elk County.

#### Erie County

* VTDs: ` ['corry 4', 'waterford east', 'waterford west', 'wesleyville east', 'wesleyville west', 'voting districts not defined'] `
* OEs: ` ['wesleyville 1', 'wesleyville 2', 'waterford 1', 'waterford 2']
* `corry 4` is indeed in the Erie County [Precinct Map](https://eriecountypa.gov/wp-content/uploads/2017/06/voting_districts_color_archd_2017.pdf) (stored in this directory at `county-files/Erie County/voting_districts_color_archd_2017.pdf`) but missing from the [results](https://eriecountypa.gov/wp-content/uploads/2019/08/election-master-compiled-2018-general.xls) (stored in this directory at `county-files/Erie County/election-master-compiled-2018-general.xls`) so that precinct's results should be accounted for.
* Emailed Douglas R. Smith, Erie County Clerk, about 'corry 4' and he told me that corry 4 was combined with corry 3 for the 2018 election. So I disolve corry 4 into corry 3.
* `voting districts not defined` is just all the water on Lake Erie + Presque Ilse Bay. (Therefore it was removed (no voters))
* wesleyville and waterford matches were made using the MEDSL results votes in each district and mathcing that to the votes in the OE results.

#### Fayette County

* VTDs: ` ['brownsville', 'franklin', 'masontown 1', 'masontown 2', 'springs'] `
* OEs: ` ['bvilletwp', 'bvillew1', 'bvillew2', 'bvillew3', 'franklind1', 'franklind2', 'masontwn'] `
* Franklin, brownsville (bvilleX in the OE results) need shapes
* Masontown is seperate in the results and in the polling place pdf `county-files/Fayette County/Polling Places 07.08.2020_202007081357174572.pdf` (downloaded from Fayette County's [website](https://www.fayettecountypa.org/DocumentCenter/View/247/Polling-Precincts-PDF))
* Spoke to Fayette County Board of Elections on 8/27 - they don't have any shapefiles
* They said the breakdown on precincts in the election results is correct. Since they don't have the shapefiles for the subdivisions of brownsville shape and franklin shape.
* **Action Taken:** springs merged into the springs precinct in Somerset County
* In the VTD shapefile there are two geometries called "BROWNSVILLE Voting District". They differ by their VTDST attribute; one is 000020, and the other is 000035.
* In the Open Elections Results file there are precincts named: "BvilleTwp", "BvilleW1", "BvilleW2", "BvilleW3".
* Using the addresses of the precinct locations identified in `VTD duplicate precincts/Fayette/Polling Places 07.08.2020_202007081357174572.pdf` (downloaded from Fayette County's [website](https://www.fayettecountypa.org/DocumentCenter/View/247/Polling-Precincts-PDF)) I determined that the "BvilleTwp" polling place is contained in the precinct geometry with VTD 000020 and the others are within the precinct geometry with VTD 000035. Accordingly, the votes for "BvilleTwp" were assigned to the precinct geometry with VTD 000020 and the votes for "BvilleW1", "BvilleW2" and "BvilleW3" were assigned to the precinct geometry with VTD 00035.
* The `franklin, mason, and springs` duplicates were also disambiguated with their VTDST field.

#### Fulton County

* VTDs: ` ['brush creek and valley hi'] `
* OEs: ` ['brush creek', 'valley hi'] `
* Used the 2016 election shapefile (`data/shapefiles/pa-precincts/PA_VTDs`) to get the split of these files.

#### Huntingdon County

* VTDs: ` ['penn b (9 cong)', 'penn a (5 cong)'] `
* OEs: ` ['penn'] `
* both shapes from the VTD are in the PA-CD-13 for 2018. Accordingly, they were both given the `penn` name.

#### Lancaster County

* VTDs: ` ['lancaster 3 1', 'lancaster 7 8'] `
* OEs: ` ['lancaster 7 8 (cv)', 'lancaster 7 8 (ls)'] `
* Resolved 3 1 by renaming (just a township vs. city) distrinction.
* Need to call lancaster about cv vs. ls I think (or use a different year)
* <http://vr.co.lancaster.pa.us/ElectionReturns/June_2>,_2020_-_General_Primary/261ByPrecinct.html
* Called Lancaster County Board of elections: (717) 299-8297 August 27, 2020
* Spoke with Diane who told me that 'lancaster 7 8' has two different school districts, but their ballots are the same other than school district related items. Therefore I combined their results under the single shapefiles.

#### Lebanon County

* VTDs: ` ['north lebanon east b (cong 15)', 'north lebanon east a (cong 6)'] `
* OEs: ` ['north lebanon east'] `
* both shapes from the VTD are in the PA-CD-9 for 2018. Accordingly, they were both given the 'north lebanon east' name.

#### Luzerne County

* VTDs: ` ['conyngham 1', 'dallas north', 'dallas south'] `
* OEs: ` [] `
* dallas north and south were identified by matching their shapes with MEDSL, and finding the corresponding results in OE results. conyngham 1 was determined to be conyngham twp, not boro using google maps. The open elections precincts for all three were conflated with other precincts in the batch string manipulation, but I correctly renamed them using VTDST.

#### Mifflin County

* VTDs: ` ['armagh new', 'armagh old', 'brown', 'lewistown 1 1', 'lewistown 5 1', 'lewistown 2', 'lewistown 6'] `
* OEs: ` ['armagh east', 'armagh west', 'brown reedsville big va', 'brown church hill', 'lewistown west', 'lewistown central', 'lewistown north', 'lewistown south'] `
* Was able to use the map to determine which precinct numbers correspond with the cardinal direction suffix by using QGIS (excluding "brown..." precincts)
* Brown VTD ('000040') needs to be split into 2: 'brown reedsville big va', 'brown church hill' (not in either 2016 shapefile)
* 'lewistown west', 'lewistown central', 'lewistown north', 'lewistown south'
* brown needs to be split into its subdivisions: <https://www.lewistownsentinel.com/news/local-news/2018/09/brown-township-voting-precinct-split-approved/>
* Emailed [Laura](http://www.co.mifflin.pa.us/dept/GIS/Pages/default.aspx) on August 25 to ask about it. She responded the same day with questions about how the data would be used. I answered her questions within one hour of recieving her email.
* Sep 8, 2020 - I sent a follow up email.
* Friday, October 2. Still haven't been able to get a response from Laura, so I combined 'brown reedsville big va', 'brown church hill' results into the 'browns' shape.

#### Monroe County

* VTDs: ` [] `
* OEs: ` ['smithfield 4'] `
* Smithfield One inside the VTD for : ['smithfield 1']
* Smithfield Two inside the VTD for : ['smithfield 2']
* Smithfield Three inside the VTD for : ['smithfield 3']
* Smithfield Four inside the VTD for : ['smithfield 1']
* Emailed [Sara](http://www.monroecountypa.gov/Dept/Voter/Pages/default.aspx) on August 25 to ask about it.
* Recieved a shapefile on August 28, 2020, but their shapefiles don't have a smithfield 4 shape.
* The polling location for smithfield 1 and smithfield 4 is the same address, so I decided to just add the smithfield 4 results to smithfield 1. Link to polling locations (accessed on 9/9/2020): <http://www.monroecountypa.gov/Dept/Voter/Pages/Precincts.aspx>

#### Montgomery County

* VTDs: ` ['franconia 2', 'hatfield 5 2 a (cong 13)', 'hatfield 5 2 b (cong 8)', 'horsham 2 2 b (cong 13)', 'horsham 2 2 a (cong 7)', 'horsham 2 1', 'horsham 4 2', 'lower merion 2 2 a (cong 2)', 'lower merion 2 2 b (cong 13)', 'lower merion 12 2', 'lower merion 12 3', 'perkiomen 1 a (cong 6)', 'perkiomen 1 b (cong 7)'] `
* OEs: ` ['franconia 2 4', 'franconia 2 1', 'hatfield 5 2', 'horsham 2 1 1', 'horsham 2 1 4', 'horsham 2 2', 'horsham 2 2 7', 'horsham 4 2 1', 'horsham 4 2 4', 'lower merion 2 2', 'lower merion 12 2 4', 'lower merion 12 2 5', 'lower merion 12 3 4', 'lower merion 12 3 5', 'perkiomen 1', 'perkiomen 1 7'] `
* 'Franconia 2' needs to be split into the 1st and 4th congressional district
* 'horsham 2 1' needs to be split into the 1st and 4th congressional district
* 'horsham 4 2' needs to be split into the 1st and 4th congressional district
* 'lower merion 12 2' needs to be split into the 4th and 5th congressional district
* 'lower merion 12 3' needs to be split into the 4th and 5th congressional district
* 'hatfield 5 2 a (cong 13)', 'hatfield 5 2 b (cong 8)', are both in CD in 2018. Therefore rename both to 'hatfield 5 2'.
* 'horsham 2 2 b (cong 13)', 'horsham 2 2 a (cong 7)' are both in CD 4 in 2018. Therefore rename both to 'horsham 2 2'.
* 'lower merion 2 2 a (cong 2)', 'lower merion 2 2 b (cong 13)' are both in CD 4 in 2018. Therefore rename both to 'lower merion 2 2'.
* 'perkiomen 1 a (cong 6)', 'perkiomen 1 b (cong 7)' are both in CD 4 in 2018. But the are seperate in the results too because there was a special election for who would hold the 7th seat from nov. to jan that only 'perkiomen 1 b (cong 7)' participated in.

#### Northampton County

* VTDs: ` ['bethlehem 17 b (cong 17)', 'bethlehem 17 a (cong 15)'] `
* OEs: ` ['bethlehem 17', 'palmer upper west naz ind'] `
* `['bethlehem 17 b (cong 17)', 'bethlehem 17 a (cong 15)']` are both in CD 7 in 2018. Therefore renamed both to ''bethlehem 17'.
* PALMER TWP UPPER WESTERN - NAZ IND missing from precinct.
* Called 610-829-6260 and learned that "NAZ IND" is only seperate for school district related elections. For Federal Elections, it is the same precinct as PALMER TOWNSHIP UPPER WEST DISTRICT EASTON. Addressed this in the script.

#### Northumberland County

* VTDs: ` ['riverside b (cong 11)', 'riverside a (cong 10)', 'sunbury 3'] `
* OEs: ` ['riverside'] `
* 'riverside b (cong 11)', 'riverside a (cong 10)' are both in CD 12 in 2018. Therefore rename both to 'riverside b'.
* sunbury is missing from the OE results for some reason. Found official results for that precinct from <https://www.norrycopa.net/documents/elections/2018_11_06_official/votecenter-65.htm>
* corrected sunbury 3 using omission using MEDSL data set and made a Git issue for Open Elections to correct the ommission.
* Open Elections addressed the issue and I redownloaded their fixed file.

#### Perry County

* VTDs: ` ['south west madison', 'north east madison'] `
* OEs: ` ['madison', 'sandy hill'] `
* Merged 'north east madison' into is 'sandy hill' and 'south west madison' is 'madison' based on <http://www.usboundary.com/Areas/661963>

#### Philadelphia County

* VTDs: ` ['40 42 a (sd 1)', '40 42 b (sd 8)', '40 49 a (sd 1)', '40 49 b (sd 8)'] `
* OEs: ` ['5 30', '5 31', '5 32', '5 33', '5 34', '18 18', '40 42', '40 49'] `
* Aquired state senate shapefile from <http://www.redistricting.state.pa.us/Maps/Senate.cfm> (stored locally at `county-files/Philadelphia County/FinalSenatePlan2012`)
* Aquired election results from <https://www.philadelphiavotes.com/en/resurces-a-data/ballot-box-app> (stored locally at 1`county-files/Philadelphia County/2018_general.csv`)
* '5 30', '5 31', '5 32', '5 33', '5 34', '18 18', are missing from the shapefiles - so need to aquire a shapefile for those results
* August 20, 2020 - called Philadelphia board of election. Said that although [this source](http://data-phl.opendata.arcgis.com/datasets/160a3665943d4864806d7b1399029a04_0.zip) (stored locally at `county-files/Philadelphia County/Political_Divisions-shp`) is dated 2014, if it has 1703 precincts it is the correct, most up to date datafile.
* This source has more precincts than the open elections shapefile.
* Talked to Garrett at board of elections August 21, 2020. He says he will ask GIS department for maps.
* 9/4 Garrett emailed me the historically accurate shapefiles for the 2018 election. They are stored locally at `county-files/Philadelphia County/Divisions_2018General`. I replaced the Census VTDs for the county with the shapefile that Garret sent me. Once I used these shapes (and parsed conformed their names to Open Elections' results) it fixed all the outlying issues with the county.

#### Schuylkill County

* VTDs: ` ['cass 1', 'cass 2', 'pine grove 1', 'pine grove 2'] `
* OEs: ` ['cass north', 'cass south', 'pine grove north', 'pine grove south'] `
* used QGIS to visually determine that cass 1 and pine grove 1 are the northern precincts and assigned the names accordingly

#### Somerset County

* In Open Elections and the VTD shapefile there are two "Adison" precincts with the same name. In the VTD the only distinguishing feature is the VTDST attribute. Accordingly, I corrected the results using [results](http://www.co.somerset.pa.us/files/voter_files/F2018Status.pdf) from Somerset County for reference.

#### Tioga County

* VTDs: ` ['shippen a (cong 5)', 'shippen b (cong 10)'] `
* OEs: ` ['shippen'] `
* Shippen is fully contained in PA-CD-12 for the 2018 congresional map. Assigned both to VTDs to the same name (shippen)

#### Washington County

* VTDs: ` ['canton 3', 'fallowfield 2 a (cong 9)', 'fallowfield 2 b (cong 18)'] `
* OEs: ` ['fallowfield 2', 'petersxd 3'] `
* 'fallowfield 2' is fully contained in PA-CD-14 for the 2018 congresional map. Assigned both to VTDs to the same name ('fallowfield 2')
* The canton 3 vtd looks like it was combined with the canton 1. Based on the county GIS website <http://www.arcgis.com/home/webmap/viewer.html?webmap=e7a17c9d3da74dae8f0962a793df9407&extent=-80.6865,39.9905,-79.6724,40.4393>
* 'petersxd 3' looks like a mis-scan of 'peter d-3' renamed it accordingly.

# Election Shapefile Verification Report

[Open Precincts Verification Script](https://github.com/OpenPrecincts/verification)

[Verification Report Breakdown](https://github.com/OpenPrecincts/verification#verification-report-breakdown)

## Validation Metadata

* `Year Validated:` 2018
* `Race Validated:` U.S. Senate
* `State Validated:` PA
* `File Provider:` Princeton Gerrymandering Project

## Statewide Reports

### Quality Scores:
|                                                                                                            |                |
|:-----------------------------------------------------------------------------------------------------------|---------------:|
| [vote_score](https://github.com/OpenPrecincts/verification#vote-score)                                     |    1.00007     |
| [county_vote_score_dispersion](https://github.com/OpenPrecincts/verification#county-vote-score-dispersion) | 6322.24        |
| [worst_county_vote_score](https://github.com/OpenPrecincts/verification#vote-score)                        |    1.04645     |
| [median_county_area_difference_score](https://github.com/OpenPrecincts/verification#area-difference-score) |    0.000713403 |
| [worst_county_area_difference_score](https://github.com/OpenPrecincts/verification#area-difference-score)  |    0.00765105  |

### Library Compatibility:
|                    |    |
|:-------------------|---:|
| can_use_maup       |  ✅ |
| can_use_gerrychain |  ✅ |

### Raw Data:
|                               |         |
|:------------------------------|:--------|
| all_precincts_have_a_geometry | ✅      |
| n_votes_democrat_expected     | 2792437 |
| n_votes_republican_expected   | 2134848 |
| n_two_party_votes_expected    | 4927285 |
| n_votes_democrat_observed     | 2792656 |
| n_votes_republican_observed   | 2134991 |
| n_two_party_votes_observed    | 4927647 |

## County Level Reports
|   geoid | name                  |   vote_score |   area_difference_score |   n_votes_democrat_expected |   n_votes_republican_expected |   n_two_party_votes_expected |   n_votes_democrat_observed |   n_votes_republican_observed |   n_two_party_votes_observed |
|--------:|:----------------------|-------------:|------------------------:|----------------------------:|------------------------------:|-----------------------------:|----------------------------:|------------------------------:|-----------------------------:|
|   42001 | Adams County          |     1        |             0.000762873 |                       14880 |                         23419 |                        38299 |                       14880 |                         23419 |                        38299 |
|   42003 | Allegheny County      |     1        |             0.000491828 |                      355907 |                        176351 |                       532258 |                      355907 |                        176351 |                       532258 |
|   42005 | Armstrong County      |     1        |             0.000826309 |                        8570 |                         15449 |                        24019 |                        8570 |                         15449 |                        24019 |
|   42007 | Beaver County         |     1        |             0.000504956 |                       34442 |                         31916 |                        66358 |                       34442 |                         31916 |                        66358 |
|   42009 | Bedford County        |     1        |             0.000440888 |                        4567 |                         14044 |                        18611 |                        4567 |                         14044 |                        18611 |
|   42011 | Berks County          |     0.999993 |             0.000442192 |                       73714 |                         68159 |                       141873 |                       73713 |                         68159 |                       141872 |
|   42013 | Blair County          |     1.00012  |             0.00116668  |                       14599 |                         27826 |                        42425 |                       14602 |                         27828 |                        42430 |
|   42015 | Bradford County       |     0.995641 |             0.000448954 |                        6926 |                         13032 |                        19958 |                        6900 |                         12971 |                        19871 |
|   42017 | Bucks County          |     1        |             0.00157264  |                      165408 |                        124133 |                       289541 |                      165408 |                        124133 |                       289541 |
|   42019 | Butler County         |     1        |             0.00147183  |                       31010 |                         46875 |                        77885 |                       31010 |                         46875 |                        77885 |
|   42021 | Cambria County        |     1        |             0.00112042  |                       21590 |                         27367 |                        48957 |                       21590 |                         27367 |                        48957 |
|   42023 | Cameron County        |     1        |             0.00153223  |                         653 |                          1080 |                         1733 |                         653 |                          1080 |                         1733 |
|   42025 | Carbon County         |     1        |             0.000624512 |                        8739 |                         13519 |                        22258 |                        8739 |                         13519 |                        22258 |
|   42027 | Centre County         |     1        |             0.00060579  |                       34778 |                         24332 |                        59110 |                       34778 |                         24332 |                        59110 |
|   42029 | Chester County        |     1        |             0.00128803  |                      140138 |                         92380 |                       232518 |                      140138 |                         92380 |                       232518 |
|   42031 | Clarion County        |     1        |             0.000877755 |                        4924 |                          8838 |                        13762 |                        4924 |                          8838 |                        13762 |
|   42033 | Clearfield County     |     1        |             0.000652196 |                        9540 |                         16852 |                        26392 |                        9540 |                         16852 |                        26392 |
|   42035 | Clinton County        |     1        |             0.000692122 |                        5289 |                          6869 |                        12158 |                        5289 |                          6869 |                        12158 |
|   42037 | Columbia County       |     1        |             0.000652698 |                        8837 |                         13437 |                        22274 |                        8837 |                         13437 |                        22274 |
|   42039 | Crawford County       |     1        |             0.000342731 |                       11720 |                         17813 |                        29533 |                       11720 |                         17813 |                        29533 |
|   42041 | Cumberland County     |     1        |             0.00160245  |                       47738 |                         54525 |                       102263 |                       47738 |                         54525 |                       102263 |
|   42043 | Dauphin County        |     1        |             0.00414084  |                       59533 |                         47152 |                       106685 |                       59533 |                         47152 |                       106685 |
|   42045 | Delaware County       |     1        |             0.00260445  |                      163216 |                         84423 |                       247639 |                      163216 |                         84423 |                       247639 |
|   42047 | Elk County            |     1        |             0.00174254  |                        4498 |                          6610 |                        11108 |                        4498 |                          6610 |                        11108 |
|   42049 | Erie County           |     1        |             0.00765105  |                       58906 |                         40348 |                        99254 |                       58906 |                         40348 |                        99254 |
|   42051 | Fayette County        |     1        |             0.0009279   |                       19563 |                         20514 |                        40077 |                       19563 |                         20514 |                        40077 |
|   42053 | Forest County         |     0.999472 |             0.00124501  |                         693 |                          1201 |                         1894 |                         692 |                          1201 |                         1893 |
|   42055 | Franklin County       |     1        |             0.000702464 |                       17385 |                         36735 |                        54120 |                       17385 |                         36735 |                        54120 |
|   42057 | Fulton County         |     1        |             0.0006684   |                        1061 |                          4173 |                         5234 |                        1061 |                          4173 |                         5234 |
|   42059 | Greene County         |     1        |             0.00106898  |                        5819 |                          6422 |                        12241 |                        5819 |                          6422 |                        12241 |
|   42061 | Huntingdon County     |     1        |             0.000431619 |                        5126 |                         10491 |                        15617 |                        5126 |                         10491 |                        15617 |
|   42063 | Indiana County        |     1        |             0.000590801 |                       12702 |                         16314 |                        29016 |                       12702 |                         16314 |                        29016 |
|   42065 | Jefferson County      |     1        |             0.000491797 |                        4437 |                         10872 |                        15309 |                        4437 |                         10872 |                        15309 |
|   42067 | Juniata County        |     0.998548 |             0.000918149 |                        2412 |                          5853 |                         8265 |                        2409 |                          5844 |                         8253 |
|   42069 | Lackawanna County     |     1        |             0.000825345 |                       51444 |                         31922 |                        83366 |                       51444 |                         31922 |                        83366 |
|   42071 | Lancaster County      |     1        |             0.000672803 |                       90521 |                        107454 |                       197975 |                       90521 |                        107454 |                       197975 |
|   42073 | Lawrence County       |     1        |             0.00327414  |                       14324 |                         17375 |                        31699 |                       14324 |                         17375 |                        31699 |
|   42075 | Lebanon County        |     1        |             0.000360864 |                       18368 |                         29836 |                        48204 |                       18368 |                         29836 |                        48204 |
|   42077 | Lehigh County         |     1        |             0.000716573 |                       73632 |                         52576 |                       126208 |                       73632 |                         52576 |                       126208 |
|   42079 | Luzerne County        |     1        |             0.00038713  |                       49200 |                         58040 |                       107240 |                       49200 |                         58040 |                       107240 |
|   42081 | Lycoming County       |     1        |             0.000505788 |                       13893 |                         26488 |                        40381 |                       13893 |                         26488 |                        40381 |
|   42083 | McKean County         |     1        |             0.00045121  |                        3972 |                          8285 |                        12257 |                        3972 |                          8285 |                        12257 |
|   42085 | Mercer County         |     1        |             0.000436643 |                       18136 |                         22290 |                        40426 |                       18136 |                         22290 |                        40426 |
|   42087 | Mifflin County        |     1.04645  |             0.000474396 |                        3934 |                          9564 |                        13498 |                        4188 |                          9937 |                        14125 |
|   42089 | Monroe County         |     1        |             0.000967372 |                       30626 |                         23968 |                        54594 |                       30626 |                         23968 |                        54594 |
|   42091 | Montgomery County     |     0.9996   |             0.000599364 |                      248454 |                        126666 |                       375120 |                      248454 |                        126516 |                       374970 |
|   42093 | Montour County        |     0.999276 |             0.00163489  |                        2966 |                          3943 |                         6909 |                        2963 |                          3941 |                         6904 |
|   42095 | Northampton County    |     1        |             0.00153782  |                       62275 |                         50385 |                       112660 |                       62275 |                         50385 |                       112660 |
|   42097 | Northumberland County |     0.999508 |             0.00116656  |                       10524 |                         17926 |                        28450 |                       10521 |                         17915 |                        28436 |
|   42099 | Perry County          |     1        |             0.000840822 |                        5186 |                         11607 |                        16793 |                        5186 |                         11607 |                        16793 |
|   42101 | Philadelphia County   |     1        |             0.00666779  |                      481467 |                         66653 |                       548120 |                      481467 |                         66653 |                       548120 |
|   42103 | Pike County           |     1        |             0.00108902  |                        8696 |                         11772 |                        20468 |                        8696 |                         11772 |                        20468 |
|   42105 | Potter County         |     1        |             0.00040153  |                        1537 |                          4564 |                         6101 |                        1537 |                          4564 |                         6101 |
|   42107 | Schuylkill County     |     1        |             0.000496391 |                       17691 |                         30452 |                        48143 |                       17691 |                         30452 |                        48143 |
|   42109 | Snyder County         |     1        |             0.00082335  |                        4322 |                          8826 |                        13148 |                        4322 |                          8826 |                        13148 |
|   42111 | Somerset County       |     1        |             0.000713403 |                        9322 |                         18896 |                        28218 |                        9322 |                         18896 |                        28218 |
|   42113 | Sullivan County       |     1        |             0.000723782 |                         962 |                          1720 |                         2682 |                         962 |                          1720 |                         2682 |
|   42115 | Susquehanna County    |     1        |             0.00050088  |                        5521 |                         10112 |                        15633 |                        5520 |                         10113 |                        15633 |
|   42117 | Tioga County          |     1        |             0.000517018 |                        4145 |                         10242 |                        14387 |                        4145 |                         10242 |                        14387 |
|   42119 | Union County          |     1        |             0.000812342 |                        5901 |                          8317 |                        14218 |                        5901 |                          8317 |                        14218 |
|   42121 | Venango County        |     1        |             0.000460417 |                        6945 |                         11210 |                        18155 |                        6945 |                         11210 |                        18155 |
|   42123 | Warren County         |     1        |             0.000697455 |                        5390 |                          8734 |                        14124 |                        5390 |                          8734 |                        14124 |
|   42125 | Washington County     |     1        |             0.000633807 |                       39220 |                         41958 |                        81178 |                       39220 |                         41958 |                        81178 |
|   42127 | Wayne County          |     1        |             0.000872762 |                        7625 |                         12269 |                        19894 |                        7625 |                         12269 |                        19894 |
|   42129 | Westmoreland County   |     1        |             0.000819782 |                       63778 |                         79078 |                       142856 |                       63778 |                         79078 |                       142856 |
|   42131 | Wyoming County        |     1        |             0.000645428 |                        3868 |                          6582 |                        10450 |                        3868 |                          6582 |                        10450 |
|   42133 | York County           |     1        |             0.000666381 |                       69272 |                         95814 |                       165086 |                       69272 |                         95814 |                       165086 |
