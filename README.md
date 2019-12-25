# bubble_maps (Create any country's map using custom maps)
Inspired by @markmarkoh from his repository Datamaps at https://github.com/markmarkoh/datamaps.

I have created the example for bublble map for three countries. India, USA and Canada as you can find in the repository
[india.html](https://github.com/Anujarya300/bubble_maps/blob/master/india.html), [usa.html](https://github.com/Anujarya300/bubble_maps/blob/master/usa.html) and [canada.html](https://github.com/Anujarya300/bubble_maps/blob/master/canada.html) respectively.

### 1. Bubble map on India Geographical region

![india bubble map](https://github.com/Anujarya300/bubble_maps/blob/master/images/india.jpg)

```
 var bubble_map = new Datamap({
            element: document.getElementById('india'),
            scope: 'india',
            geographyConfig: {
                popupOnHover: true,
                highlightOnHover: true,
                borderColor: '#444',
                borderWidth: 0.5,
                dataUrl: 'https://rawgit.com/Anujarya300/bubble_maps/master/data/geography-data/india.topo.json'
                //dataJson: topoJsonData
            },
            fills: {
                'MAJOR': '#306596',
                'MEDIUM': '#0fa0fa',
                'MINOR': '#bada55',
                defaultFill: '#dddddd'
            },
            data: {
                'JH': { fillKey: 'MINOR' },
                'MH': { fillKey: 'MINOR' }
            },
            setProjection: function (element) {
                var projection = d3.geo.mercator()
                    .center([78.9629, 23.5937]) // always in [East Latitude, North Longitude]
                    .scale(1000);
                var path = d3.geo.path().projection(projection);
                return { path: path, projection: projection };
            }
});

// bubbles based on state or ISO code (i.e. bubbles on center of state)
// use centered property
let bubbles = [
            {
                centered: "MH",
                fillKey: "MAJOR",
                radius: 20,
                state: "Maharastra"
            },
            {
                centered: "UP",
                fillKey: "MAJOR",
                radius: 22,
                state: "Uttar Pradesh"
            }
        ]

// bubbles based on the co-ordinates of the state/city or any
// use latitute and longitude properties
// let bubbles = [
        //     {
        //         latitude: 19.7515,
        //         longitude: 75.7139,
        //         fillKey: "MAJOR",
        //         radius: 20,
        //         state: "Maharastra"
        //     },
        //     {
        //         latitude: 25.7677,
        //         longitude: 80.6627,
        //         fillKey: "MAJOR",
        //         radius: 22,
        //         state: "Uttar Pradesh"
        //     }
        // ]

        // // ISO ID code for city or <state></state>
setTimeout(() => { // only start drawing bubbles on the map when map has rendered completely.
    bubble_map.bubbles(bubbles, {
        popupTemplate: function (geo, data) {
            return `<div class="hoverinfo">city: ${data.state}, Slums: ${data.radius}%</div>`;
        }
    });
}, 1000);
```

###### Set the correct projection for India map on world map with the help of Longitude and Latitute of India (you can google it India Longitude and Latitute)
Please use **india.toto.json** for India geopraphy json data from https://github.com/Anujarya300/bubble_maps/blob/master/data/geography-data/india.topo.json, otherwise your map wont work. (I have truncated IND. from all state ISO code(2-digit ISO code), e.g IND.JH for Jharkhand state truncated to JH)  

Please note in setProjection method, I have set [78.9629, 23.5937] to locate center point for India in the world map. That means
Latitude = 78.9629 E and Longitude = 23.5937 N. Remember Latitute and Longitude are always East and North. For western countries, Latitude are in West so make it convert as Negative of East. e.g 102.3421 W ==> -102.3421 E.

### 2. Bubble map on Canada Geographical region

![canada bubble map](https://github.com/Anujarya300/bubble_maps/blob/master/images/canada.jpg)

```
var bubble_map = new Datamap({
            element: document.getElementById('canada'),
            scope: 'canada',
            geographyConfig: {
                popupOnHover: true,
                highlightOnHover: true,
                borderColor: '#444',
                borderWidth: 0.5,
                dataUrl: 'https://rawgit.com/Anujarya300/bubble_maps/master/data/geography-data/canada.topo.json'
                //dataJson: topoJsonData
            },
            fills: {
                'MAJOR': '#306596',
                'MEDIUM': '#0fa0fa',
                'MINOR': '#bada55',
                defaultFill: '#dddddd'
            },
            data: {
                'JH': { fillKey: 'MINOR' },
                'MH': { fillKey: 'MINOR' }
            },
            setProjection: function (element) {
                  var projection = d3.geo.mercator()
                .center([-106.3468, 68.1304]) // always in [East Latitude, North Longitude]
                .scale(250)
                .translate([element.offsetWidth / 2, element.offsetHeight / 2]);

                var path = d3.geo.path().projection(projection);
                return { path: path, projection: projection };
            }
        });
```

###### Set the correct projection for Canada map on world map with the help of Longitude and Latitute of Canada (you can google it Canada Longitude and Latitute)

Please use **canada.toto.json** for India geopraphy json data from https://github.com/Anujarya300/bubble_maps/blob/master/data/geography-data/canada.topo.json, otherwise your map wont work. (I have truncated CA. from all state ISO code(2-digit ISO code), e.g CA.TN to TN)
        
Please note in setProjection method, I have set [-106.3468, 68.1304] to locate center point for Canada in the world map. That means
Latitude = 106.3468 W and Longitude = 68.1304 N. Remember Latitute and Longitude are always East and North. For western countries, Latitude are in West so make it convert as Negative of East. e.g 102.3421 W ==> -102.3421 E.

You can adjust this latitude and longitude co-ordinates by minor changing. 
e.g, if your map is not showing full view of North then you can change 68.1304 N to 70.3200 N or 71.3200 etc.
     if your map is not showing full view of East then you can change 32.1304 E to 70.3200 E or 30.3200 etc.

### 3. Bubble map on USA Geographical region

![usa bubble map](https://github.com/Anujarya300/bubble_maps/blob/master/images/usa.jpg)

```
var bubble_map = new Datamap({
            element: document.getElementById('usa'),
            scope: 'usa',
            geographyConfig: {
                popupOnHover: true,
                highlightOnHover: true,
                borderColor: '#444',
                borderWidth: 0.5,
                dataUrl: 'https://rawgit.com/Anujarya300/bubble_maps/master/data/geography-data/usa.topo.json'
                //dataJson: topoJsonData
            },
            fills: {
                'MAJOR': '#306596',
                'MEDIUM': '#0fa0fa',
                'MINOR': '#bada55',
                defaultFill: '#dddddd'
            },
            data: {
                'NY': { fillKey: 'MINOR' },
                'CA': { fillKey: 'MINOR' }
            }
        });
```
      
Here in the case of USA, you do not need to change the anything on usa.topo.json, since its cities are already in 2-digit ISO code.
usa.totp.json: https://github.com/Anujarya300/bubble_maps/blob/master/data/geography-data/usa.topo.json
  
You do not have to worry about USA map region since d3 already hadled it.

## If you need to add some other countries map say country {xyz} other than India, Canada, USA. You need to do the folowing:
1. Find the {xyz}.topo.json file for you country xyz. You can find from https://github.com/markmarkoh/datamaps/tree/master/dist.
2. Extract Datamap.prototype.{xyz}Topo json and save it file named {xyz}.topo.json
3. If the state codes contains dot(.) in the topo json, then you need to remove the dot from the code e.g, if your state code is CA.AL, remove CA. part to get 2-digit ISO code AL. If the states code are already in 2-digit ISO or do't have dot(.) then don't do any modification follow next steps.
4. Objects country name in {xyz}.topo.json should be same as you declared in the Datamap scope. e.g, for Canada, in canada.topo.json we have {"type":"Topology","objects":{"can":{"type":"GeometryCollection"}}} and we have provided scope as 'canada' in the canada.html page. So this case 'can' in canada.topo.json must be as 'canada' i.e {"type":"Topology","objects":{"canada":{"type":"GeometryCollection"}}}.
5. You need to override setProjection method, which is explained above three countires. You can refer any one.
6. Done
