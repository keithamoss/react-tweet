<p align="center">
  <img src="https://raw.githubusercontent.com/artnotfound/react-tweet/master/tweet.png" />
</p>

[live demo](https://react-tweet.herokuapp.com/)

React.js component for rendering tweets as they are presented on Twitter.com. Currently themed after the Desktop
experience with the idea of a fixed width timeline. See the [example app](https://github.com/mannynotfound/react-tweet/blob/master/example/app.js) for
an example of a tweet stream.

## Motivation

`react-tweet` should make it easier to boostrap Twitter based React.js apps. This way we can focus
on interesting ways to use and manipulate the API without the pains of rendering. Styles, assets, and HTML have
been lifted from [twitter.com](https://twitter.com) and [twitter dev docs](https://dev.twitter.com/overview/documentation).
`react-tweet` uses only inline styles and while written in ES6, compiles to plain JS meant to be absorbed by any React project.
`react-tweet` can be used a 'dumb' component for simply rendering data or could be a starting point for a more ambitious Tweet component.

## Dependencies

To get full video functionality, include videojs in your app. You can use the `http://vjs.zencdn.net/5-unsafe/video.js` as a CDN path.
If you dont include videojs it should fall back to native HTML5 video.

## Usage

Pass in tweet objects returned from twitter API Requests as a 'data' prop. Designed for use with
[search](https://dev.twitter.com/rest/reference/get/search/tweets) & [home_timeline](https://dev.twitter.com/rest/reference/get/statuses/home_timeline) methods,
although any object can be used as long as it has the following properties:


```js
import React from 'react'
import Tweet from 'react-tweet'

const tweetData = {
  id_str: 'XXX',
  user: {
    name: 'XXX',
    screen_name: 'XXX',
    profile_image_url: 'XXX'
  },
  text: 'XXX',
  created_at: 'XXX',
  favorite_count: 'XXX',
  retweet_count: 'XXX',
  entities: {
    media: [],
    urls: [],
    user_mentions: [],
    hashtags: [],
    symbols: []
  } 
}

class MyTweetComponent extends React.Component {
  render () {
    // use linkProps if you want to pass attributes to all links
    const linkProps = {target: '_blank', rel: 'noreferrer'}

    return (
      <Tweet data={tweetData} linkProps={linkProps} />
    )
  }
}
```

## Prop Types
| Property | Type | Required? | Description |
|:---|:---|:---:|:---|
| data | Object | ✓ | A Tweet object to render. Ref [Introduction to Tweet JSON](https://developer.twitter.com/en/docs/tweets/data-dictionary/overview/intro-to-tweet-json) |
| linkProps | Object |  | Optional props to pass to all `<a>` links in the tweet. e.g. `{target: "_blank", rel: "noreferrer"}` |
| tweetStyles | Object |  | [React-style CSS styles](https://reactjs.org/docs/dom-elements.html#style) to pass to the root tweet `<div>` element. Useful to dynamically controlling tweet style. If you need to change the style of all tweet objects, just write regular CSS targeting `div.tweet`. Becareful  |
| onTweetAction | Function |  | Callback invoked whenever a tweet action button (reply, retweet, or favourite) is clicked: `(tweetAction: string, tweet: object)` tweetAction can be `reply`, `retweet`, or `favourite`. If provided, overrides the default behaviour of opening the tweet on twitter.com.
| onMediaLoad | Function |   | Callback invoked whenever an image or video embedded within the tweet loads successfully.
| onMediaLoadError | Function |   | Callback invoked whenever an image or video embedded within the tweet fails to load.

## Demo
  * live: [live demo](https://react-tweet.herokuapp.com/)
  * local: run `npm start` & visit `localhost:8080`

## Supported
  * Desktop Twitter.com styles
  * Retweets
  * Quote tweets
  * Auto-linking via [twitter-text](https://www.npmjs.com/package/twitter-text)
  * Twitter Emoji support via [twemoji](https://github.com/twitter/twemoji)
  * Modal mode for images
  * Isomorphic Rendering

## TODO:
  * Mobile style support
  * ~~Better video support, seems Twitter uses custom player~~
  * ~~Mimick video controls of Twitter.com~~
  * Add slideshow controls in Modal mode
  * Refactor how images get cropped, kind of a mess rn
  * Support for Tweet threads
  * Tests


