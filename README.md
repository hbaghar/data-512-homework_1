
# DATA 512: Human Centered Data Science

## Homework 1: Professionalism &amp; Reproducibility

### Goal

Construct, analyze, and publish a dataset of monthly article traffic for a select set of pages from English Wikipedia from July 1, 2015 through September 30, 2022.

Specifically, the set of pages can be found [here](https://docs.google.com/spreadsheets/d/1zfBNKsuWOFVFTOGK8qnTr2DmHkYK4mAACBKk1sHLt_k/edit?usp=sharing). It contains a list of dinosaur names and their corresponding Wikipedia article link.

### Source data licenses

The source data is distributed under the Creative [Commons Attribution-ShareAlike 3.0 Unported License](https://creativecommons.org/licenses/by-sa/3.0/) which states:

1. You are free to:
   - **Share** — copy and redistribute the material in any medium or format
   - **Adapt** — remix, transform, and build upon the material for any purpose, even commercially
2. Under the following terms:
   - **Attribution** — You must give appropriate credit, provide a link to the license, and indicate if changes were made. You may do so in any reasonable manner, but not in any way that suggests the licensor endorses you or your use
   - **ShareAlike** - If you remix, transform, or build upon the material, you must distribute your contributions under the same license as the original
3. Additionally, you may not apply legal terms or technological measures that legally restrict others from doing anything the license permits.

[Wikimedia Foundation REST API Terms of Use](https://www.mediawiki.org/wiki/REST_API#Terms_and_conditions)

### References to API

- [Pageviews API Documentation](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Pageviews)
- [API Endpoint](https://wikimedia.org/api/rest_v1/#/Pageviews_data/get_metrics_pageviews_aggregate_project_access_agent_granularity_start_end)

### Outputs

The code in `HW1.ipynb` creates the following 3 JSON files:

1. `dino_monthly_desktop_start201507-end202209.json`: This file stores the number of desktop views for each dinosaur at a year month level starting from July 2015 to September 2022
2. `dino_monthly_mobile_start201507-end202209.json`: This file stores the number of mobile views (sum of both mobile app and mobile web views) for each dinosaur at a year month level starting from July 2015 to September 2022
3. `dino_monthly_cumulative_start201507-end202209.json`: This file stores the number of cumulative views (a running total for each dinosaur that combines desktop and mobile views listed above) for each dinosaur at a year month level starting from July 2015 to September 2022.

Each JSON file is organised as an array of arrays. The larger array represents a single dinosaur and the nested array within each larger array holds JSON objects that represent the pageviews for a particular month for that dinosaur. The following is a description of each of the fields present in the JSON objects:

|Key name|Data Type|Description|
|---|---|---|
|`project`|`string`|If you want to filter by project, use the domain of any Wikimedia project, for example 'en.wikipedia.org', 'www.mediawiki.org' or 'commons.wikimedia.org'|
|`article`|`string`|The title of any article in the specified project. Any spaces should be replaced with underscores. It also should be URI-encoded, so that non-URI-safe characters like %, / or ? are accepted. Example: Are_You_the_One%3F|
|`granularity`|`string`|The time unit for the response data. As of today, the only supported granularity for this endpoint is `daily` and `monthly`|
|`timestamp`|`string`|The timestamp of the returned datapoint in YYYYMMDDHH format|
|`agent`|`string`|The type of agent that is considered when returning the number of views. If you want to filter by agent type, use one of `user`, `automated` or `spider`. If you are interested in pageviews regardless of agent type, use `all-agents`|
|`views`|`int`|The number of page views for the article at a timestamp that falls within the range for the given agent type|

### Known Issues and Special Considerations

1. Check all article name inputs in the list of dinosaur names given under **Goal** for special characters and clean/encode them in URI format before hitting the API.
