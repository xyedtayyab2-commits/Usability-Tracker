Usability Tracker 
A lightweight JavaScript library that records how users interact with a web
page and exports the data as XML or JSON. It can also draw a click heatmap
on top of the page. No dependencies, no build step.


FEATURES
- Click tracking with a short CSS selector path for each target
- Rage click detection (several rapid clicks in the same spot)
- Dead click detection (clicks on non-interactive elements)
- Touch tap tracking for mobile devices
- Throttled mouse movement sampling (uses requestAnimationFrame)
- Scroll depth milestones: 25%, 50%, 75%, 100%
- Tab visibility tracking (visible / hidden)
- Privacy: text from inputs, textareas, selects and editable elements is
  redacted
- Memory safe: the event log is capped at 5,000 events
- Session persistence using sessionStorage
- Export to XML or JSON, as a string or a downloaded file
- Canvas heatmap overlay
- Optional batched sending to your own server endpoint (uses sendBeacon
  when the page is closed)


FILES
usability-tracker.xml   Demo page (XHTML) that contains the tracker script
README.txt              This file


QUICK START
1. Open usability-tracker.xml in a browser.
2. Click around, move the mouse, scroll, and click the same spot quickly a
   few times.
3. Use the buttons at the top of the page:
   - Show summary     Prints session statistics
   - Toggle heatmap   Shows or hides the click heatmap
   - Download XML     Saves the session data as an XML file

To use the tracker on your own website, copy the JavaScript from inside the
<script> block of usability-tracker.xml into your page (or into a separate
.js file) and include it on the pages you want to track.


API
---
All functions are available on window.UsabilityTracker:

  getLogs()              Returns a copy of all recorded events
  getSummary()           Returns session id, duration, event counts, max
                         scroll percent and page size
  exportXML()            Returns the session as an XML string
  exportJSON()           Returns the session as a JSON string
  downloadXML()          Downloads the session as an .xml file
  downloadJSON()         Downloads the session as a .json file
  toggleHeatmap('click') Shows or hides the heatmap overlay
  clear()                Clears all recorded data

Example (browser console):

  UsabilityTracker.getSummary();
  console.log(UsabilityTracker.exportXML());
  UsabilityTracker.toggleHeatmap('click');


CONFIGURATION
-------------
Settings are in the CONFIG object at the top of the script:

  moveSampleMs      Mouse movement sampling interval (default 100 ms)
  maxEvents         Maximum events kept in memory (default 5000)
  rageClicks        Clicks needed to count as a rage click (default 3)
  rageWindowMs      Time window for rage clicks (default 800 ms)
  rageRadiusPx      Max distance between rage clicks (default 30 px)
  scrollMilestones  Scroll depth percentages to record
  endpoint          URL to send events to (default null = disabled)
  flushIntervalMs   How often events are sent (default 10000 ms)
  persist           Save logs to sessionStorage (default true)

To send data to your server, set endpoint to your URL, for example
'/analytics'. Events are sent as JSON:

  { "sessionId": "...", "events": [ ... ] }


XML OUTPUT FORMAT
  <usabilitySession id="..." page="..." durationMs="...">
    <summary totalEvents="..." maxScrollPercent="...">
      <count type="click">12</count>
    </summary>
    <events>
      <event type="click" x="320" y="540" selector="..." t="1520"/>
    </events>
  </usabilitySession>


EVENT TYPES
click, deadclick, rageclick, tap, mousemove, scrolldepth, visibility


PRIVACY NOTE
This tool records user behaviour. If you use it on a live website, tell your
users about it (for example in a privacy policy) and follow the data
protection laws that apply to you. Do not use it to collect sensitive
information.




AUTHOR
------
Add your name and contact details here.
