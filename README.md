

# Deaths due to covid-19 identified virus and unidentified (suspected) virus, community

Because I have not found current covid data, I have compiled data on deaths in Spain in 2020 by community. The first button activates deaths caused by covid officially, and the other activates deaths that may be caused by covid but not officially.
These data are collected at https://www.ine.es/index.htm



![alt-text](https://github.com/antonioluzon/d3-js-pin-scale/blob/main/Animation.gif)

# Steps

```bash
npm install
```

* Let's install the needed packages to work with:

```bash
npm install topojson-client --save
```

```bash
npm install @types/topojson-client --save-dev
```

* Let's install topojson:

```bash
npm install topojson --save
```

```bash
npm install @types/topojson --save-dev
```

* Let's install the _composite projections_ project to display the Canary Island just below spain.

```bash
npm install d3-composite-projections --save
```

##


* Calculation of radius' circles  

```typescript

const calculateRadiusBasedOnAffectedCases = (comunidad: string,data: data_covid_2020[]) => {
  const entry = data.find(item => item.name === comunidad);
  const affectedRadiusScale = d3
  .scaleLinear()
  .domain([0, 10000])
  .range([5, 40]); 
  return entry ? affectedRadiusScale(entry.value) : 0;
};
```



* Update circles 

```typescript
const updateCircles = (data: data_covid_2020[]) => {
    const circles = svg.selectAll("circle");
    circles
      .data(latLongCommunities)
      .merge(circles as any)
      .transition()
      .duration(500)
      .attr("r", d => calculateRadiusBasedOnAffectedCases(d.name, data));
  };
```

* Application of update circle

```typescript
document
  .getElementById("Covid")
  .addEventListener("click", function handleResultsNow() {
    updateCircles(defuncionesCovid);
  });

document
  .getElementById("PosibleCovid")
  .addEventListener("click", function handleResultsInitial() {
    updateCircles(defuncionesPosibleCovid);
  });

  ```

I have also modified _./src/stats.ts_ with the corresponding data from the INE.


Finally, to add the image and due to a problem, I had to add ```type="module"``` in _./src/index.html_

```html
<body>
    <img src="./tabla.png" />
    <script src="./index.ts", type="module"></script>
</body>
```
