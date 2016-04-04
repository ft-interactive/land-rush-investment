# Tracking

For FT analytics

1. Add the Polyfill Service to the `<head>` before the Shorthand head script...

```
<head>
	...
	<!-- add polyfill service -->
	<script src="https://cdn.polyfill.io/v2/polyfill.min.js"></script>
	
	<!-- example shorthand head script -->
	<script type="text/javascript" src="./static/build/js/head.2792.min.js"></script>
	...
</head>
```

2. Ensure old iJento tracking is removed. It's at the begnning of the `<body>` and looks like this.

```
    <script>
var FT = FT || {}; FT.Properties = FT.Properties || {}; FT.Properties.ENV = 'p';
</script>
<!-- FT tracking module 1.2.4 -->
<script src="http://s2.ft-static.com/scripts/392b9acc/bundles/tracking.js"></script>
<noscript>
<img alt="" border="0" width="1" height="1" src="http://track.ft.com/track/track.js?javascript=disabled"/>
<img alt="" border="0" width="1" height="1" src="http://stats.ft.com/si/track.gif?WT.js=No"/>
</noscript>
```

3. Add the snippet below to the beginning of the `<body>`.

**You must** also include the UUID (from the link file) and microsite name which is always `land-rush-investment` for these pages.

To do this, find and replace the following in the snippet below:

* replace __UUID__ with the UUID of the link file for **this story** 
* replace __MICROSITE__ with `land-rush-investment`

```
<script>(function(){function init(){var oTracking=Origami['o-tracking'];oTracking.init({server:'https://spoor-api.ft.com/px.gif',system:{is_live:true},context:{product:'IG'}});oTracking.link.init();oTracking.page({content:{asset_type:'interactive',uuid:'__UUID__',microsite_name: '__MICROSITE__'}});}var o=document.createElement('script');o.async=o.defer=true;o.src='https://build.origami.ft.com/v2/bundles/js?modules=o-tracking';var s=document.getElementsByTagName('script')[0];if(o.hasOwnProperty('onreadystatechange')){o.onreadystatechange=function(){if(o.readyState==='loaded'){init();}};}else{o.onload=init;}s.parentNode.insertBefore(o,s);}());</script><noscript data-o-component="o-tracking"><img src="https://spoor-api.ft.com/px.gif?data=%7B%22action%22%3A%22view%22%2C%22category%22%3A%22page%22%2C%22context%22%3A%7B%22content%22%3A%7B%22asset_type%22%3A%22interactive%22%2C%22uuid%22%3A%22__UUID__%22%7D%2C%22product%22%3A%22IG%22%2C%22microsite_name%22%3A%22__MICROSITE__%22%7D%2C%22system%22%3A%7B%22is_live%22%3Atrue%2C%22apiKey%22%3A%22qUb9maKfKbtpRsdp0p2J7uWxRPGJEP%22%2C%22source%22%3A%22o-tracking-ns%22%2C%22version%22%3A%221.0.0%22%7D%7D" height="1" width="1" /></noscript>
```

This snippet includes the o-tracking library and configures the page level data. It also has a noscript method of tracking. 
