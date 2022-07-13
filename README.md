# Platform Click ID URL Parameter Collection

A living collection of url parameters from various traffic platforms (organic and paid). 

## Purpose of Click ID's

Social media (and advertising) platforms commonly incorporate click ID's on outbound links, which in effect are suffixed url parameters onto outbound URL's added within the platform. The parameters are used in conjunction with the platforms' marketing tag (pixel) which is recommended to be placed on the brands' website. The tag commonly references the click ID and drops a first-party cookie in the users' browser with the click ID parameter stored in its value, which is later used for (ad) attribution purposes.

## Problem

Website Analytics tools, such as Google Analytics 4, Adobe Analytics, Amplitude or similar by default stores the URL alongside each event, which in most above scenarios would include the click id parameters. In a typical site content report inside GA4, the brand usually wants to be able to compare the number of e.g. `page_view` events and `conversions` (performance) between unique pages of their site, such as below, between the homepage `/` and the Product Showcase Page `/product-showcase`:

Page Path + Query String                | Page Views    | Conversions 
--------------------------------------- | ------------- | -----------
`/`                                     | 10,478        | 345
`/product-showcase`                     | 6,578         | 834
 
Becuase the brand has driven traffic to the website using popular ad platforms such as Facebook and Google, each unique platform click (and ultimately landing page view) report onto an individual row due to click id's generated by the platform e.g.:

Page Path + Query String                | Page Views    | Conversions 
--------------------------------------- | ------------- | -----------
`/`                                     | 1             | 0
`/?fbclid=12345`                        | 1             | 0
`/?fbclid=23456`                        | 1             | 1
`/?fbclid=34567`                        | 1             | 0
`/?fbclid=45678`                        | 1             | 0
`/?fbclid=56789`                        | 1             | 0
`.......etc`
`/product-showcase?gclid=123abc`        | 1             | 0
`/product-showcase?gclid=234bcd`        | 1             | 0
`/product-showcase?gclid=345cde`        | 1             | 1
`/product-showcase?gclid=456def`        | 1             | 0
`/product-showcase?gclid=567efg`        | 1             | 0
`.......etc`

This makes it difficult to analyze the data set unless employing additional manipulation, such as pivot tables, aggregation/consolidation and using advanced filters and regular expressions.

Example: a brand creates a post on Facebook with a headline, description and a landing page URL, meant to encourage and lead a user to the brand's website. The brand relies on GA4 on their site to collect user behaviour and struggle with the native `page location` or `page path + query string` dimension which is scattered in hundreds of unique rows, as every pageview generated from that post arrives on the site with a unique click ID in the URL. 

## Solution

Using a list similar to this, the brand can anticipate incoming traffic from any of these platforms (they might not always know from where traffic comes) and build a tool or configure URL manipulation on their backend (e.g. using GTM, Google Analytics, GA3, GA4) that helps with this, either by sending "clean" URL's to the analytics tools in the first page and/or using the list to manipulate or truncate incoming traffic if the tool supports it, which can then be used for reporting.

# Active Lists

### Ad/Analytics Platform URL Query Parameters (Click ID's)

_updated 12 July 2022_

Query Parameter       | Description                                       
--------------------- | ------------------------------------------------- 
`s_cid`               | Adobe                
`gclid`               | Google (non-iOS devices)                          
`gbraid`              | Google (iOS 14.5+ opted out devices) (web-to-app) 
`wbraid`              | Google (iOS 14.5+ opted out devices) (app-to-web) 
`dclid`               | Google Display (Enhanced Attribution)
`gclsrc`              | Google Search Ads 360
`srsltid`             | Google Shopping Free Listings Result ID
`igshid`              | Instagram            
`li_fat_id`           | Linkedin             
`fbclid`              | Meta (Facebook/Instagram/Messenger/Whatsapp)
`cvid`                | Microsoft MSN/Bing   
`oicd`                | Microsoft MSN/Bing   
`msclkid`             | Microsoft            
`mc_cid`              | Mailchimp            
`mc_eid`              | Mailchimp            
`ml_subscriber`       | MailerLite           
`ml_subscriber_hash`  | MailerLite           
`mkt_tok`             | Marketo              
`oly_anon_id`         | Olytics              
`oly_enc_id`          | Olytics              
`otc`                 | Olytics              
`_openstat`           | OpenStat             
`dicbo`               | Outbrain             
`rdt_cid`             | Reddit               
`s_cid`               | Adobe                
`tblci`               | Taboola              
`auctid`              | Teads                
`ttclid`              | TikTok               
`twclid`              | Twitter              
`vero_conv`           | Vero                 
`vero_id`             | Vero                 
`wickedid`            | Wicked Reports       
`vmcid`               | Yahoo DSP            
`afid`                | Yahoo Native Params  
`soc_src`             | Yahoo                
`soc_trk`             | Yahoo                
`yclid`               | Yandex/Yahoo         
`_z1_agid`            | Zemanta              
`_z1_caid`            | Zemanta              
`_z1_msid`            | Zemanta              
`_z1_pub`             | Zemanta              

### Miscellaneous URL Query Parameters

_updated 12 July 2022_

Query Parameter     | Description          
------------------- | ------------------------------------------------- 
`__s`               | Drip                 
`hsCtaTracking`     | HubSpot              
`__hssc`            | Hubspot              
`__hstc`            | Hubspot              
`__hsfp`            | Hubspot               
`_hsmi`             | Hubspot              
`_hsenc`            | Hubspot              
`ICID`              | Other                
`campaign`          | Microsoft            
`subafid`           | Other                
`rb_clickid`        | Other                

## Sourcing and Inspiration

[Brave Browser Known Tracker Parameters](https://www.cookiestatus.com/brave/#other)

[Chrome UTM Stripper Extension](https://github.com/jparise/chrome-utm-stripper)

## Feedback and Assistance

If you have knowledge of other parameters, from other platforms or tools, feel free to send a pull request.

## Plans
- Build `JSON` or `CSV` to be used programmatically; being able to pull updated lists via a mirrored CDN resource `cdn.jsdelivr.net/gh/cremedigital/platform-url-click-id-parameters@main/filename.json`) into your tool (such as a GTM custom template).
- Build of a GTM Custom Variable Template (Web and/or Server-side)for specific purposes. Ideas are welcome.
