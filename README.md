# jquery-vasttrafik
A jQuery plugin for retrieving realtime data from Västtrafik, the company running public transit in Västra Götaland, Sweden

### Demo
A demo of jquery-vasttrafik is available [here](https://joel.f-eri.cf/ITG-Infoskarm).

### Download
Either git clone this repository or download from [releases](https://github.com/itggot-joel-eriksson/jquery-vasttrafik/releases).

### Including it in your project
Include jQuery either before closing `</head>` or `</body>`
```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.4/jquery.min.js"></script>
```
Right after the above `<script>` include jquery-vasttrafik either the non-minified version
```html
<script src="jquery-vasttrafik.js"></script>
```
or the minified version
```html
<script src="jquery-vasttrafik.min.js"></script>
```

### Usage

##### HTML
```html
<table>
    <thead>
        <th>
            Line
        </th>
        <th>
            Destination
        </th>
        <th>
            Stop
        </th>
        <th>
            Next
        </th>
        <th>
            Thereafter
        </th>
    </thead>
    <tbody id="#realtime"></tbody>
</table>
```
##### JavaScript
```javascript
$("#realtime").vasttrafik();
```

`.vasttrafik()` takes two arguments the first one being settings as a JavaScript object and the second being a callback function.

###### Settings
| Setting       | DataType  | Description                                                   | Default                                           |
|---------------|-----------|---------------------------------------------------------------|---------------------------------------------------|
| url           | String    | Which url to use for the AJAX call                            | "https://api.fam-ericsson.se/vasttrafik/?id="     |
| stopId        | String    | What stop to retreive realtime from                           | "9021014001960000"                                |
| method        | String    | What HTTP method to use with AJAX                             | "GET"                                             |
| crossDomain   | Boolean   | Wheather the AJAX call is cross-domain or not                 | true                                              |
| cache         | Boolean   | Wheather the AJAX result should be cahced or not              | false                                             |
| async         | Boolean   | Wheather the AJAX call should be asynchronous or not          | true                                              |
| departureNow  | String    | What text should be displayed when a departure is now         | "now"                                             |
| departureNone | String    | What text should be displayed when there are no departures    | "No departures"                                   |
| lineColors    | Object    | Defines custom colors for specified lines                     | {55: {bgColor: "#EAF5CC", fgColor: "#3AB73D"}}    |

###### Callback
The callback returns wheather the AJAX call succeeded or not and a reason together with an HTTP status code.

###### Example
```javascript
$("#chalmersplatsenTable").vasttrafik({
    url: "https://api.fam-ericsson.se/vasttrafik/?id=",
    stopId: "9021014001960000",
    method: "GET",
    crossDomain: true,
    cache: false,
    async: true,
    departureNow: "now",
    departureNone: "No departures",
    lineColors: {
        55: {
            bgColor: "#EAF5CC",
            fgColor: "#3AB73D"
        }
    }
});
```

### PRO-TIPS
- jquery-vasttrafik does not run on any interval. If you would want the data to reload you could use `setInterval`. Just keep in mind that it is not necessary to update more than once per minute altought the JSON response is cached for 30 seconds.
- The API is hosted at [api.fam-ericsson.se](https://api.fam-ericsson.se/vasttrafik), if you would like to host it yourself create a new [issue](https://github.com/itggot-joel-eriksson/jquery-vasttrafik/issues). The only prerequisite is that you have a server with PHP version >= 5.6 installed.
