# Changelog

All notable changes to this project will be documented in this file.

For more information about changelogs, check
[Keep a Changelog](http://keepachangelog.com) and
[Vandamme](http://tech-angels.github.io/vandamme).

## 0.3.0  - Unreleased

**How to upgrade**

If your code calls `Funky::Video#find` for existing video but without counters,
it used to return a video object with `nil` values. Now it will return its
own `Funky::CountersNotFound` error instead, so it should be handled properly.

## 0.2.32 - 2018/06/07

* [FEATURE] Raise `Funky::CountersNotFound` error when a video does not have
its view count.

## 0.2.31 - 2017/10/25

* [BUGFIX] Revert the change of version 0.2.29 and do not use request to get app
access token.
* [ENHANCEMENT] Allow funky to scrape view count for more videos, by changing
the way how to scrape.

## 0.2.30 - 2017/10/16

* [BUGFIX] Test should pass when call Page#videos. Partly revert the change
of version 0.2.28

## 0.2.29 - 2017/10/16

* [ENHANCEMENT] Use request to get app access token. Do not use
`app_id|app_secret` string.

## 0.2.28 - 2017/10/05

* [FEATURE] Add `since` option when it calls Page#videos and Page#posts to reduce
amount of requests when it gets only recent items.

## 0.2.27 - 2017/08/28

* [BUGFIX] Fetch the correct view count even for non-English pages

## 0.2.26 - 2017/06/06

* [ENHANCEMENT] Raise ContentNotFound if Page#find is called with an invalid URI

## 0.2.25 - 2017/05/16

* [FEATURE] Retry up to 5 times if Facebook responds with error

## 0.2.24 - 2017/05/10

* [BUGFIX] Raise Funky::ContentNotFound error when a page does not return
its name. This change will filter out cases a full url of website entered
as page_id argument of `Funky::Page#find`, instead of username.

## 0.2.23 - 2017/05/09

* [FEATURE] Print out logs for each pagination
* [BUGFIX] Use cursor-based pagination for `Funky::Page#posts` to resolve
infinite loop issue when the page has life events with old backdated time.

## 0.2.22 - 2017/05/05

* [FEATURE] Add `Funky::Page#posts`.
* [FEATURE] Add `Funky::Page#has_featured_video?`.

## 0.2.21 - 2017/05/03

* [FEATURE] Add `Funky::Page#fan_count`.

## 0.2.20 - 2017/04/20

* [BUGFIX] Fix `Funky::Page#videos` by adding condition for an edge case.

## 0.2.19 - 2017/04/20

* [IMPROVEMENT] Retry 3 times after a server error or a socket error, to fetch
  data even with any temporary issue from Facebook.

## 0.2.18 - 2017/04/19

* [ENHANCEMENT] `Funky::Page#videos` now fetches more videos by time-based pagination.

## 0.2.17 - 2017/04/17

* [FEATURE] Add `Funky::Page.find` class method to find a page by its page ID.
* [FEATURE] Add `Funky::Page#videos` instance method to list all videos under a page fetched by API call.

## 0.2.16 - 2017/04/02

* [ENHANCEMENT] Video.where(id: [..ids..]) now works even with more than 50 ids.

## 0.2.15 - 2017/03/21

* [BUGFIX] Return a string for the description field of a Funky::Video
  object even when the Facebook video has no description

## 0.2.14 - 2017/02/06

* [ENHANCEMENT] Add the Funky::Page API to fetch name, username,
  location, city, state, zip, street, country, longitude,
  and latitude fields from the Facebook Graph API given a page ID.

## 0.2.13 - 2017/01/25

* [BUGFIX] Correctly fetch data for videos that belong to a Facebook page with a username that contains URL-unsafe characters. For instance "https://www.facebook.com/KinoToPrzygoda /" (with a space) is a valid Facebook page URL.
* [ENHANCEMENT] Use 2.8 of Facebook Graph API (upgrade from 2.6).
- There were deprecations in v2.8 of the Facebook Graph API as well as additions documented in [the changelog](https://developers.facebook.com/docs/apps/changelog).
- The current API of Funky is not affected.

## 0.2.12 - 2017/01/19

* [ENHANCEMENT] Parse new format of share & comment count in Facebook HTML
* [BUGFIX] Fix regular expression for likecount

## 0.2.11 - 2017/01/19

* [ENHANCEMENT] Follow redirects when Facebook responds with 302
* [ENHANCEMENT] Parse new format of view count in Facebook HTML

## 0.2.10 - 2016/12/20

* [ENHANCEMENT] Add a facebook page ID as a part of the Funky::Video API
* [ENHANCEMENT] Add a facebook page URL as a part of the Funky::Video API

## 0.2.9 - 2016/12/13

* [BUGFIX] Allow a video ID to be parsed out of facebook video URLs with
trailing slashes.

## 0.2.8 - 2016/12/12

* [BUGFIX] Change the way that "like counts" are parsed now that Facebook has changed the structure of the HTML and can include multiple "likecounts" elements in the same page.

## 0.2.7 - 2016/08/18

* [ENHANCEMENT] When Funky makes a request to an HTML page, Funky would now raise `Funky::ConnectionError` should the following errors occur:
OpenSSL::SSL::SSLError,
Errno::ETIMEDOUT,
Errno::EHOSTUNREACH,
Errno::ENETUNREACH,
Errno::ECONNRESET,
Net::OpenTimeout,
SocketError

## 0.2.6 - 2016/08/05

* [BUGFIX] Force scraping to use English-US version of Facebook by appending `locale=en_US` to the query string. This prevents cases where Funky's requests originate from non English speaking countries and receiving different HTML templates.

## 0.2.5 - 2016/07/25

* [ENHANCEMENT] Allow Funky to also scrape view count that uses dot delimiters. Previously, it only scraped view count with comma delimiters.

## 0.2.4 - 2016/06/28

* [ENHANCEMENT] Change the way views are scraped from a Facebook page, by not depending the regex on the word "Views". This has the added benefit of being able to scrape the Facebook pages that are not just in English, but also in Hebrew. Potentially, it could scrape from other languages too, but that is  speculation for now.

## 0.2.3 - 2016/06/22

* [FEATURE] Add `page_name` of a video found by API call (which is `Funky::Video.where`)

## 0.2.2 - 2016/06/17

* [BUGFIX] Single video id passed to the `Funky::Video.where` clause will not
error even if the response is not 200. It would return an empty array.

## 0.2.1  - 2016/06/16

* [FEATURE] Add method to find video by url, `Funky::Video.find_by_url!(url)`.
The following URL formats are currently supported:
- `https://www.facebook.com/{page_name}/videos/vb.{alt_page_id}/{video_id}/`
- `https://www.facebook.com/{page_name}/videos/{video_id}/`
- `https://www.facebook.com/{page_id}/videos/{video_id}/`
- `https://www.facebook.com/video.php?v={video_id}`

## 0.2.0  - 2016/06/07

**How to upgrade**

If your code never calls `Funky::Video#view_count`, then you are good to go.

If it does, then be aware that Facebook has started displaying two types of
view counts in the video page: 'views from this post' and 'cumulative views'.
For coherence with the videos without this new type of page, `view_count` will
always return the "views from this post" (whereas it was returning cumulative
views in 0.1.1)

* [ENHANCEMENT] Always return 'views from this post' in `Funky::Video#view_count`.

## 0.1.1  - 2016/06/07

* [BUGFIX] Added support for scraping view count from the new cumulative views that Facebook recently started rolling out.

## 0.1.0  - 2016/05/26

* [FEATURE] Added support for Facebook video data. Currently we can get the video id, length, description, created_time, picture, view_count, share_count, comment_count, and like_count.
