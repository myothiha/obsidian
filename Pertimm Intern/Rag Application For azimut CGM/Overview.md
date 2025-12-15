
# Data
- Json/XML
	- 1day for one day for each parameters (each param is mobile website or other). for example, 1M visitors for website in December 12th. 
- CSV files
	- all data that used to calculate the figures. 
	- very big. average size for 1 day is 82GB of data in gzip format.
- two format log files. Both are csv. 
	- desktop/mobile websites
	- android app
- Look up table represent mapping between which log file belongs to which parameter. included some metadata such as brand (to do cross analysis between family under same brand.) 
- how to access?
	- use archive - DSF

Terminologies
- A param can be a website, a mobile app or a group of websites.

Naming convention

- five measurement tools
- less than 1000 websites (params)
- Three files
	- PV File - (page view) include stats like
		- date measured
- VH - Weekly data (accumulate)
- For some params are one month (in xml)
- VQ 


Website Log file Description
- Timestamp
- ID ?
- Anonymized IP - lose accuracy for IP
- web domain 
- unique visitor ID
	- always the same for the same visitor inside this param for the whole week
	- if same visitor go to another website, that ID will be different. 
- Visit ID
	- defined by ACPM
	- when visitor go to website, the visit start. 
	- when inactive for example 30 min, it's new visit. If he comes back over 30 min, it's a new visit.
- URL
- Monthly figure does not exist
- Visitor ID will not changed for one whole week. 

- Application Logs
	- App name
	- Visitor ID
	- URL when it use web view
	- country code of IP
	- They have
		- daily
		- weekly
		- monthly
	- same visitor ID for whole month

Notes:
- For big picture statistics, if you find two different params with same domain, ignore one side.

# Existing Alerts

Great to have
- Data files: three sources.
- Technical documents for data and alerts. 

# Laurent's Notes

## Sources
- raw data : CSV inside S3-compatible OVH Storage
- DSF Declaration Systematique de Fréquentation : GZIP manually sent by Bertrand
- mapping between MEDIA ID and MEDIA NAME + manifests for all MEDIA ID : extract from databases manually sent by Bertrand : Dump

## Privacy of DATA
Data already sanitized, must respect CNIL rules

## Measurement tools : 5 actives, less than a thousand websites

## Measure files

```
YYYYMMDD_<measure-tool-ID>_<perimeter-ID>.json
```


- PV : Page Vues
- V : visites
- VQ : visiteurs Quotidien
- VH : visiteurs Hebdo --> One only, or sometimes one per day, erasing previous ones until ends of week
- VM : visiteurs Mensuels

A perimeter could be a website, a mobile application, a group of websites (example : "France television")

## Limitation

Be careful about website already contained insite a group of websites, example "France television".


Documentation about DSF format sent by Bertrand

## Raw log files

### Desktop/website Raw log file (CSV format, "|" separator file)

#### Format
- date, timezone Paris, format "2025:12:01:00:00:00"
- website ID, example "328"
- IP of visitor, sanitized (last replaced by 0), example "179.245.236.0"
- domain, example "www.lequipe.fr"
- Visitor ID
- Visite ID
- Full visited URL
- User-Agent
- Country Code, before anonymising the IP, or "Anithing bu FRANCE" ("XX")
#### Frequency
Daily and weekly figures

### Mobile Application Raw log file (CSV format, "|" separator file)
#### Format
- timestamp, timezone Paris, format "2025:12:01:00:00:00"
- Mobile app ID
- Visitor or Terminal ID
- uri page if existing
- Mobile agent
- IP of visitor, sanitized (last replaced by 0), example "179.245.236.0"
- Country Code, before anonymising the IP, or "Anithing bu FRANCE" ("XX")
#### Frequency
Daily and weekly and monthly figures



"Rolling averrage"


--> Comportement anormal par rapport à la moyenne (rapidité des visites, anomalie dans le traffic, )