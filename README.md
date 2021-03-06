# TalkSearch scraper

This scraper is an API that indexes captions of YouTube videos. It works either with a channel, a playlist or a video URL.

![TalkSearch](UI/static/logo-talksearch-line@2x.png)

> This is part of the [TalkSearch](https://community.algolia.com/talksearch)
> project by [Algolia](https://algolia.com)

[Website](https://community.algolia.com/talksearch) |
[embed](https://github.com/algolia/talksearch-embed) |
[**scraper**](https://github.com/algolia/talksearch-scraper) |
[landing page source](https://github.com/algolia/talksearch)


The index that list all indexed video is `ALL_VIDEOS`.

The generated indices are:
* `<channelName>`: one indexed channel
* `<channelName>-playlist-<playlistId>`: one indexed playlist
* `<channelName>-video-<videoId>`: one indexed video

The `/index` route returns the following JSON:
```
{
  success: Boolean,
  message: String,      // Message in case of error
  indexName: String,
  totalVideos: Number,
  failures: Array,      // Array of videos' IDs that failed (no english subtitles)
  indexedVideos: Number
}
```

## Run the API

`yarn install`

Make sure to set the env variables before running the app.

`yarn dev`

## Routes

POST `/index`
```
{
  youtubeURL: String,  // The YouTube URL of the channel/playlist/video
  name: String,        // Name of the conference
  speaker: {
    extract: Boolean,
    regex: String,     // Optional
    nbSubStr: Number   // Optional
  },
  title: {
    extract: Boolean,
    regex: String,     // Optional if extract is false
    nbSubStr: Number   // Optional if extract is false
  },
  accentColor: String, // Optional, css color
  lang: String         // Optional, default 'en'
}
```

GET `/reindex`
```
{
    indexName: String // Optional, reindex either one index
                         or all of them if indexName is null
}
```

## Env variables

* `APP_ID`
* `API_KEY`
* `YOUTUBE_API_KEY`
* `API_TOKEN`

## Deploy to heroku

The heroku `master` branch is up-to-date with this `master` branch.

`git push heroku master`

## TODO

- [ ] Put the admin page behind an Okta wall/proxy
- [ ] Extract tags using [https://indico.io/](https://indico.io/)
