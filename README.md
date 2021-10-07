# Assignment A1: Data Curation

This repository contains a report (ipython) and output files for Assignment A1: Data Curation of the course DATA 512 of the 2021 fall quarter in MSDS at UW.

## Goal

The goal of this assignment was to construct, analyze, and publish a dataset of monthly traffic on English Wikipedia from January 1 2008 through August 31 2021.

## License

This content accessed via the Wikimedia REST API is licensed under the CC-BY-SA 3.0 and GFDL licenses. Please read Wikimedia’s [Terms of User](https://wikimediafoundation.org/wiki/Terms_of_Use) and [Privacy Policy](https://wikimediafoundation.org/wiki/Privacy_policy).

## Wikimedia API

In order to cover the full time span from January 2008 to August 2021, two APIs must be used. The first is the legacy PageCounts API - covering the period December 2007 through July 2016 - and the second is the PageViews API - covering traffic from July 2015 and beyond.

The schema for the endpoints of both APIs, as described in https://wikimedia.org/api/rest_v1/#/, is the following:

*/metrics/legacy/pagecounts/aggregate/{project}/{access-site}/{granularity}/{start}/{end}*

*/metrics/pageviews/aggregate/{project}/{access}/{agent}/{granularity}/{start}/{end}*

**project**:

    The name of any Wikimedia project formatted like {language code}.{project name}, for example en.wikipedia.

**access**:

    all-access, desktop, mobile-app, mobile-web

**access-site**:

    all-sites, desktop-site, mobile-site

**agent**:

    This parameter can be used as a filter, accepting one of the following values: all-agents, user, spider, automated. Notice this capability is not present in the legacy API.

**granularity**:

    This parameter can be set as hourly, daily, and monthly. For the purpose of this project, we are interested in monthly data.
    
**start/end**:
    
    The timestamp of the first hour/day/month to include, in YYYYMMDDHH format.

## Files

This repository contains 5 json files with the output of different queries from different APIs. They are named as:

```
{source api}_{device}_{start month in YYYYMM}_{end month in YYYYMM}
```

Each file represents a table with the following columns:

PageCounts: "project", "access-site", "granularity", "timestamp", "count"
PageViews: "project", "access", "agent", "granularity", "timestamp", "views"

The meaning of most of these columns have been covered in the previous section explaining the endpoint parameters. The remaining "count" and "views" contain the total number of views for the date specified in that row. The "timestamp" follows the format YYYYMMDDHH.

This repository also contains 1 csv file, named en-wikipedia_traffic_200712-202108.csv, with the Wikipedia traffic metrics from January 1 2008 through August 31 2021, after data processing, in the following schema:

- year 
- month
- pagecount_all_views: the total number of views across all device types according to the PageCount API for the specified month
- pagecount_desktop_views: the total number of views from desktop devices according to the PageCount API for the specified month
- pagecount_mobile_views: the total number of views mobile devices according to the PageCount API for the specified month
- pageview_all_views: the total number of views across all device types according to the PageView API for the specified month
- pageview_desktop_views: the total number of views from desktop devices according to the PageView API for the specified month
- pageview_mobile_views: the total number of views mobile devices according to the PageView API for the specified month
