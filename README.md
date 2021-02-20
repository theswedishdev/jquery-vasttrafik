# jquery-vasttrafik
A jQuery plugin for retrieving realtime data from Västtrafik, the company running public transit in Västra Götaland, Sweden

## Maintenance
:warning: This project is no longer being maintained.

## Download
Either git clone this repository or download from [releases](https://github.com/joel-eriksson/jquery-vasttrafik/releases).

## Including it in your project
Include jQuery either before closing `</head>` or `</body>`
```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>
```
Right after the above `<script>` include jquery-vasttrafik either the non-minified version
```html
<script src="jquery-vasttrafik.js"></script>
```
or the minified version
```html
<script src="jquery-vasttrafik.min.js"></script>
```

## Usage

#### HTML
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
    <tbody id="realtime"></tbody>
</table>
```
#### JavaScript
```javascript
$("#realtime").vasttrafik();
```

`.vasttrafik()` takes two arguments the first one being settings as a JavaScript object and the second being a callback function.

##### Settings
| Setting         | Type    | Description                                                | Default           |
|-----------------|---------|------------------------------------------------------------|-------------------|
| `url`           | String  | Which url to use for the AJAX call                         | `""`              |
| `stopId`        | String  | What stop to retreive realtime from                        | `""`              |
| `method`        | String  | What HTTP method to use with AJAX                          | `"GET"`           |
| `crossDomain`   | Boolean | Wheather the AJAX call is cross-domain or not              | `true`            |
| `cache`         | Boolean | Wheather the AJAX result should be cahced or not           | `false`           |
| `async`         | Boolean | Wheather the AJAX call should be asynchronous or not       | `true`            |
| `departureNow`  | String  | What text should be displayed when a departure is now      | `"now"`           |
| `departureNone` | String  | What text should be displayed when there are no departures | `"No departures"` |
| `lineColors`    | Object  | Defines custom colors for specified lines                  | `{}`              |

##### Callback
The callback returns wheather the AJAX call succeeded or not and a reason together with an HTTP status code.

##### Example
```javascript
$("#realtime").vasttrafik({
    url: "https:/example.com/api/departures/?id=",
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
}, function(response) { /*Callback*/ });
```

## Projects using jquery-vasttrafik
* [ITG-Infoskarm](https://github.com/joel-eriksson/ITG-Infoskarm)


## PRO-TIPS
- jquery-vasttrafik does not run on any interval. If you would want the data to reload you could use `setInterval`. Just keep in mind that it is not necessary to update more than once per minute altought the JSON response is cached for 30 seconds.
- The API for this plugin is not hosted anywhere, but the OpenAPI Specification for the required response model is available [here](https://github.com/joel-eriksson/jquery-vasttrafik/blob/master/openapi.yml).
    - There is version of this API created that is no longer hosted. Create a new [issue](https://github.com/joel-eriksson/jquery-vasttrafik/issues/new) if you would like access to the source code to host it yourself. The only prerequisite is that you have a server with PHP version >= 5.6 installed.

## License
See [LICENSE](https://github.com/joel-eriksson/jquery-vasttrafik/blob/master/LICENSE)