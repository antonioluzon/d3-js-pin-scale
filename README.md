

# Deaths due to covid-19 identified virus and unidentified (suspected) virus, community

Because I have not found current covid data, I have compiled data on deaths in Spain in 2020 by community. The first button activates deaths caused by covid officially, and the other activates deaths that may be caused by covid but not officially.
These data are collected at https://www.ine.es/index.htm



![alt-text](https://github.com/antonioluzon/d3-js-pin-scale/blob/main/Animation.gif)

# Steps

```bash
npm install
```

- When you deal with maps you can use two map formats GeoJSON or TopoJSON, topo JSON is lightweight and offers some extra
  features, let's install the needed packages to work with:

```bash
npm install topojson-client --save
```

```bash
npm install @types/topojson-client --save-dev
```

- Let's install topojson:

```bash
npm install topojson --save
```

```bash
npm install @types/topojson --save-dev
```

- Let's install the _composite projections_ project to display the Canary Island just below spain.

```bash
npm install d3-composite-projections --save
```

```typescript
const calculateRadiusBasedOnAffectedCases = (comunidad: string,data: Numbers[]) => {
  const entry = data.find(item => item.name === comunidad);
  const affectedRadiusScale = d3
  .scaleLinear()
  .domain([0, 10000])
  .range([5, 40]); 
  return entry ? affectedRadiusScale(entry.value) : 0;
};
```
