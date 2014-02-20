---
permalink: /developer/recalls.html
layout: post
title: Recalls API
tags: recalls api
---

[DigitalGov Search](/index.html) > [APIs for Developers](/developer/index.html) > Recalls API

<a href="https://github.com/GSA-OCSIT"><img style="position: absolute; top: 41px; right: 0; border: 0;" src="https://s3.amazonaws.com/github/ribbons/forkme_right_orange_ff7600.png" alt="Fork me on GitHub"></a>

Helping alert the public to unsafe, hazardous, or defective products.

<ul>
  <li class="overview current"><a href="#overview">Overview</a></li>
  <li class="api"><a href="#using-the-api">Using the API</a></li>
  <li class="parameters"><a href="#parameters">Parameters</a></li>
  <li class="sources"><a href="#data-sources">Data Sources</a></li>
  <li class="returns"><a href="#what-it-returns">What it Returns</a></li>
</ul>

<a name="overview"></a>

## Overview

When you're buying and using products, safety comes first.

Six federal regulatory agencies issue recalls on [Recalls.gov](http://www.recalls.gov).

This Recalls API allows you to tap into a list of (1) drug and food safety recalls from the [Food and Drug Administration](http://www.fda.gov) (FDA), [U.S. Department of Agriculture's Food Safety and Inspection Service](http://www.fsis.usda.gov) (UDSA FSIS), and [FoodSafety.gov](http://www.FoodSafety.gov); (2) car safety recalls from the [National Highway Traffic Safety Administration](http://www.nhtsa.gov) (NHTSA); and (3) product safety recalls from the [Consumer Product Safety Commission](http://www.cpsc.gov) (CPSC).

This API is great for consumer safety websites or applications, news organizations, and websites or magazines targeted to specific audiences, such as parents.

<a name="using-the-api"></a>

## Using the API

This Recalls API accepts a GET request.

Recalls are searchable by keyword, issuing agency, date, UPC code, vehicle-specific attributes, or any combination of these.

The base URL is http://api.usa.gov/recalls/search.json?**parameters**

Sample API requests follow.

All recalls  
<http://api.usa.gov/recalls/search.json?>

All cribs  
<http://api.usa.gov/recalls/search.json?query=cribs>

All cribs that pose a choking hazard  
<http://api.usa.gov/recalls/search.json?query=cribs+choking>


All cribs that pose a choking hazard sorted by date  
<http://api.usa.gov/recalls/search.json?query=cribs+choking&sort=date>

<a name="parameters"></a>

## Parameters

Seven generic parameters are accepted.

1. query
1. organization
1. start_date
1. end_date
1. page
1. per_page
1. sort

There are additional parameters that are specific to food, product, and car safety recalls. None are required.

### query

Attempts to extract as much "signal" as possible from the input text. Handles word variants, so a search on "choke" will find a recall categorized as a "choking" hazard.

### organization

Specifies which agency issued the recall. Possible values are `CPSC`, `FDA`, `NHTSA`, or `USDA`.

Example (one agency): <http://api.usa.gov/recalls/search.json?organization=nhtsa>

Example (multiple agencies): <http://api.usa.gov/recalls/search.json?organization=fda+usda>

### start_date

Specifies the start date of the recall.

Example: <http://api.usa.gov/recalls/search.json?start_date=2012-01-01>

### end_date

Specifies the end date of the recall.

Example: <http://api.usa.gov/recalls/search.json?end_date=2012-12-31>

### page

Specifies the pagination of search results. Possible values are `1` to `20`.

Example: <http://api.usa.gov/recalls/search.json?page=3>

### per_page

Specifies the number of search results for each page. Possible values are `1` to `50`.

Example: <http://api.usa.gov/recalls/search.json?per_page=10>

### sort

Results are sorted by relevance by default. Possible values are `rel` or `date`. Use 'sort=date' to sort results by date with the most recent listed first.

Example: <http://api.usa.gov/recalls/search.json?sort=date>

### food_type 
Only for drug and food safety recalls. Possible values are `food` or `drug`.

Example: <http://api.usa.gov/recalls/search.json?food_type=drug>

### upc

Only for CPSC recalls. Specifies the UPC code when available. Not all products have UPC codes.

Example: <http://api.usa.gov/recalls/search.json?upc=042666601627>

### make, model, year, and code (only for NHTSA recalls)

* `make` specifies the make of the vehicle or equipment. Example: <http://localhost:3000/search?make=winnebago>
* `model` specifies the model of the vehicle or equipment. Example: <http://localhost:3000/search?model=ellipse>
* `year` specifies the year of the vehicle or equipment. Example: <http://localhost:3000/search?year=2010>
* `code` specifies the NHTSA code. Possible values are `E`, `V` [for vehicles], `I`, `T`, `C`, or `X`. Example: <http://localhost:3000/search?code=v>

<a name="data-sources"></a>

## Data Sources

We've tailored this Recalls API for our use in the [USA.gov iPhone app](http://apps.usa.gov/usagov.shtml). 

Data are normalized across (1) drug and food safety recalls from the [FDA](http://www.fda.gov), [UDSA FSIS](http://www.fsis.usda.gov), and [FoodSafety.gov](http://www.FoodSafety.gov); (2) car safety recalls from the [NHTSA](http://www.nhtsa.gov); and (3) product safety recalls from the [CPSC](http://www.cpsc.gov).

So, we encourage you to use the five original data sources directly or via [Recalls.gov](http://www.recalls.gov).

1. [FDA recalls, market withdrawals, and safety alerts](http://www.fda.gov/Safety/Recalls/default.htm)
2. [USDA FSIS recalls and public health alerts](http://www.fsis.usda.gov/wps/portal/fsis/topics/recalls-and-public-health-alerts)
3. [FoodSafety.gov recalls and alerts](http://www.foodsafety.gov/recalls)
4. [NHTSA recalls and defects](http://www.nhtsa.gov/Vehicle+Safety/Recalls+&+Defects)
5. [CPSC recalls](http://www.cpsc.gov/Recalls/)

<a name="what-it-returns"></a>

## What it Returns

Below are three sample JSON responses for food, product, and car safety recalls.

### Food Recalls

	{
		success: {
			total: 82,
			results: [
				{
					organization: "USDA",
					recall_number: "1df0a5440b",
					recall_date: "2011-05-14",
					recall_url: "http://www.fsis.usda.gov/News_&_Events/Recall_037_2011_Release/index.asp",
					description: "Rose & Shore Meat Co., a Vernon, Calif., establishment, is recalling approximately 15,900 pounds of ready-to-eat deli meat products that may be contaminated with Listeria monocytogenes.",
					summary: "California Firm Recalls Deli Meat Products for Possible Listeria Contamination"
				},
				{
					organization: "FDA",
					recall_number: "51d9096a25",
					recall_date: "2010-06-21",
					recall_url: "http://www.fda.gov/Safety/Recalls/ucm216371.htm",
					description: "Portland Shellfish Company, Inc. is expanding this voluntarily recall to include the Meat Without Feet private label food service (2 Lb bags), pack of ready to eat frozen lobster claw and knuckle meat. Lot 13310, as recent tests show the product has the potential to be contaminated with Listeria monocytogenes, an organism which can cause serious and sometimes fatal infections in young children, frail or elderly people, and others with weakened immune systems",
					summary: "Portland Shellfish Company Expands Recall to Include Meat Without Feet Label, Lobster Claw and Knuckle Meat, because of Possible Health Risk"
				}
		    ]
	}}

### Product Recalls

	{"success":{
	    "total":2,
	    "results":[
	        {
	            "organization":"CPSC",
	            "recall_number":"12080",
	            "recall_date":"2012-01-05",
	            "recall_url":"http://www.cpsc.gov/cpscpub/prerel/prhtml12/12080.html",
	            "manufacturers":["Target"],
	            "product_types":["Lights & Accessories"],
	            "descriptions":["Target 6-pc. LED Flashlight Sets"],
	            "upcs":["490021010049"],
	            "hazards":["Fire & Fire-Related Burn"],
	            "countries":["China"]
	        },
	        {
	            "organization":"CPSC",
	            "recall_number":"12710",
	            "recall_date":"2012-01-05",
	            "recall_url":"http://www.cpsc.gov/cpscpub/prerel/prhtml12/12710.html",
	            "manufacturers":["Sterno"],
	            "product_types":["Candles & Candle Holders"],
	            "descriptions":["Sterno Bulk Pack 5 Hour Tea Lights"],
	            "upcs":null,
	            "hazards":["Fire & Fire-Related Burn"],
	            "countries":["Thailand"]
	        }
	    ]
	}}

### Car Recalls

	{"success":{
	    "total":2,
	    "results":[
	        {
	            "organization":"NHTSA",
	            "recall_number":"12V579000",
	            "recall_date":"2012-12-18",
	            "recall_url":"http://www-odi.nhtsa.dot.gov/recalls/recallresults.cfm?start=1&SearchType=QuickSearch&rcl_ID=12V579000&summary=true&PrintVersion=YES",
	            "records":[
	                {
	                    "component_description":"VISIBILITY/WIPER",
	                    "make":"SPARTAN",
	                    "manufacturer":"Spartan Chassis, Inc.",
	                    "manufacturing_begin_date":"2012-10-01",
	                    "manufacturing_end_date":"2012-10-31",
	                    "model":"GLADIATOR",
	                    "recalled_component_id":"000051813001317776000001349",
	                    "year":2012
	                },
	                {
	                    "component_description":"VISIBILITY/WIPER",
	                    "make":"SPARTAN",
	                    "manufacturer":"Spartan Chassis, Inc.",
	                    "manufacturing_begin_date":"2012-10-01",
	                    "manufacturing_end_date":"2012-10-31",
	                    "model":"METROSTAR",
	                    "recalled_component_id":"000051813001317777000001349",
	                    "year":2012
	                }
	            ],
	            "manufacturer_campaign_number":"12016",
	            "component_description":"VISIBILITY/WIPER",
	            "manufacturer":"Spartan Chassis, Inc.",
	            "code":"V",
	            "potential_units_affected":"36",
	            "initiator":"MFR",
	            "report_date":"20121210",
	            "defect_summary":"Spartan Motors Chassis is recalling certain model year 2012-2013 Gladiator, Metro Star, Metro Star-X, and Force emergency rescue chassis cabs built between October 1, 2012, through October 31, 2012.  The wiper motor shaft and the wiper arm shaft have diff",
	            "consequence_summary":"If the windshield wipers become inoperative, the driver could have reduced visibility, which may increase the risk of a crash.  ",
	            "corrective_summary":"The remedy for this recall campaign is still under development.  The manufacturer has not yet provided a notification schedule.  Owners may contact Spartan at 1-800-543-5008.",
	            "notes":"Spartan's recall campaign number is 12016.Owners may also contact the National Highway Traffic Safety Administration Vehicle Safety Hotline at 1-888-327-4236 (TTY 1-800-424-9153), or go to www.safercar.gov.",
	            "recall_subject":"Windshield Wipers may become Inoperative"
	        },
	        {
	            "organization":"NHTSA",
	            "recall_number":"12V571000",
	            "recall_date":"2012-12-18",
	            "recall_url":"http://www-odi.nhtsa.dot.gov/recalls/recallresults.cfm?start=1&SearchType=QuickSearch&rcl_ID=12V571000&summary=true&PrintVersion=YES",
	            "records":[
	                {
	                    "component_description":"FUEL SYSTEM, GASOLINE:DELIVERY:FUEL PUMP",
	                    "make":"JAGUAR",
	                    "manufacturer":"JAGUAR CARS LTD",
	                    "manufacturing_begin_date":"2012-10-03",
	                    "manufacturing_end_date":"2012-10-12",
	                    "model":"XF",
	                    "recalled_component_id":"000051654001723816000000152",
	                    "year":2013
	                },
	                {
	                    "component_description":"ELECTRICAL SYSTEM",
	                    "make":"JAGUAR",
	                    "manufacturer":"JAGUAR CARS LTD",
	                    "manufacturing_begin_date":"2012-10-03",
	                    "manufacturing_end_date":"2012-10-12",
	                    "model":"XF",
	                    "recalled_component_id":"000051654001723816000000200",
	                    "year":2013
	                }
	            ],
	            "manufacturer_campaign_number":"J028",
	            "component_description":"ELECTRICAL SYSTEM",
	            "manufacturer":"Jaguar Land Rover North America, LLC",
	            "code":"V",
	            "potential_units_affected":"13",
	            "initiator":"MFR",
	            "report_date":"20121207",
	            "defect_summary":"Jaguar Land Rover is recalling certain model year 2013 XF vehicles manufactured October 3, 2012, through October 12, 2012 and equipped with a gasoline engine.",
	            "consequence_summary":"An engine stall without warning while driving may lead to a loss of motive power, a loss of power-assisted braking and a loss of power-assisted steering.",
	            "corrective_summary":"Jaguar Land Rover will notify owners, and dealers will install an additional wiring harness to the in-tank fuel pump, free of charge.",
	            "notes":"Jaguar's campaign recall number is J028.Owners may also contact the National Highway Traffic Safety Administration Vehicle Safety Hotline at 1-888-327-4236 (TTY 1-800-424-9153), or go to www.safercar.gov.",
	            "recall_subject":"Fuel Starvation may cause Vehicle Stall"
	        }
	    ]
	}}

## Open Source Code

The server code that runs this API is on Github. If you're a Rails developer, fork our [Recalls Server API](https://github.com/GSA/recalls_api) repo to add features (such as additional datasets) or fix bugs.

Better yet, send us a [pull request](https://github.com/GSA/recalls_api/pulls) to contribute your changes to our project and improve this API for everyone who is using it.

## Feedback

E-mail us at <search@support.digitalgov.gov> with any suggestions about what you'd like to see in the next version of API.

## Terms of Use

By accessing the Recalls API, you agree to [USA.gov's Terms of Service for Developer Resources](http://www.usa.gov/About/developer-resources/terms-of-service.shtml).
