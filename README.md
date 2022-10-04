# multiple-overpass-turbo-tags
I need to find out how to make multiple overpass tags correspond instead of replace eachother. 
Hello everyone

i want to create an overpass turbo query where i can filter out all of the "amenity=drinking_water" from the "landuse=cemetery". i need this for a project that i am working on. 

i have tried the following queries to find these so i can filter out of the database. 

[out:json][timeout:500];
// gather results
(
  node["landuse"="cemetery"]["amenity"="drinking_water"]({{bbox}});
  way["landuse"="cemetery"]["amenity"="drinking_water"]({{bbox}});
  relation["landuse"="cemetery"]["amenity"="drinking_water"]({{bbox}});
);
// print results
out body;
>;
out skel qt;

this query gives me no results because it filters on both tags

and

*/
[out:json][timeout:500];
// fetch area “Carinthia” to search in
{{geocodeArea:Carinthia}}->.searchArea;
// gather results
(
  // query part for: “landuse=cemetery”
  node["landuse"="cemetery"](area.searchArea);
  node["amenity"="drinking_water"](area.searchArea);
  way["landuse"="cemetery"](area.searchArea);
  way["amenity"="drinking_water"](area.searchArea);
  relation["landuse"="cemetery"](area.searchArea);
  relation["amenity"="drinking_water"](area.searchArea);
);
// print results
out body;
>;
out skel qt;

this query gives me all the drinking water points and cemeteries

But the ultimate goal is to see all of the drinking water of an area, while excluding the ones that are inside of cemetery area's.

