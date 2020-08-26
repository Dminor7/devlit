## Introduction To Danfo.js -  Manipulating And Processing Structured Data

<img border="0" data-original-height="1080" data-original-width="1080" src="https://1.bp.blogspot.com/-kuDrk0ZKUg4/X0Q3ro57n0I/AAAAAAAADfs/0YQmHV9pY08iGImUl7Bn-cy4FIz6OhGygCLcBGAsYHQ/s1600/Danfo%2BJS.gif" style="width:100%" data-action="zoom">

# Danfo.js
An open-source, JavaScript library providing high-performance, intuitive, and easy-to-use data structures for manipulating and processing structured data. It is heavily inspired by the Python's [Pandas](https://pandas.pydata.org/) library and provides a similar interface and API. Moreover, Danfo.js is fast and It is built on [Tensorflow.js](https://www.tensorflow.org/js) and supports tensors out of the box. 

Data science thrives in Python because of the ecosystem of open-source libraries - NumPy, Pandas, sklearn, and more. It's great to see similar tools being developed by the JavaScript community. This could be the start of something big. So let us see Danfo.js in action.

# Installation

There are two ways to get danfo.js. To install it via npm, you can do the following:

```
npm install danfojs-node
```

We can also install and use it in the browsers by using the CDN below:

```
<script src="https://cdn.jsdelivr.net/npm/danfojs@0.1.1/dist/index.min.js"></script>
```
---
### Creating a Series object by passing a list of values, letting danfo.js create a default integer index:

```
const dfd = require("danfojs-node")
s = new dfd.Series([1, 3, 5, undefined, 6, 8])
s.print()
```
<div style="overflow: auto; max-height: 300px;">
    <table class="df-table">
      <thead>
        <tr>
          <th></th>
          <th class="int32">0</th>
        </tr>
      </thead>
      <tbody>
        
          <tr>
            <th>0</th>
            <td class="int32">1</td>
          </tr>
        
          <tr>
            <th>1</th>
            <td class="int32">3</td>
          </tr>
        
          <tr>
            <th>2</th>
            <td class="int32">5</td>
          </tr>
        
          <tr>
            <th>3</th>
            <td class="int32">NaN</td>
          </tr>
        
          <tr>
            <th>4</th>
            <td class="int32">6</td>
          </tr>
        
          <tr>
            <th>5</th>
            <td class="int32">8</td>
          </tr>
        
      </tbody>
    </table>
    </div>

<h2>Reading JSON data and vector operations</h2>

```
const json_data = [{ A: 0.4612, B: 4.28283, C: -1.509, D: -1.1352 },
            { A: 0.5112, B: -0.22863, C: -3.39059, D: 1.1632 },
            { A: 0.6911, B: -0.82863, C: -1.5059, D: 2.1352 },
            { A: 0.4692, B: -1.28863, C: 4.5059, D: 4.1632 }]
df = new dfd.DataFrame(json_data) 
 // Adding to series object, can use sub, mul, div, and pow
df['A'].add(df['B']).print()
df['A'].pow(2).print()
// Maximum value of C
console.log(df['C'].max()) // 4.505899
```


<div style="overflow: auto; max-height: 300px;">
<h3>Add A and B</h3>
    <table class="df-table">
      <thead>
        <tr>
          <th></th>
          <th class="float32">A</th>
        </tr>
      </thead>
      <tbody>
        
          <tr>
            <th>0</th>
            <td class="float32">4.744029998779297</td>
          </tr>
        
          <tr>
            <th>1</th>
            <td class="float32">0.2825700044631958</td>
          </tr>
        
          <tr>
            <th>2</th>
            <td class="float32">-0.13752996921539307</td>
          </tr>
        
          <tr>
            <th>3</th>
            <td class="float32">-0.8194299936294556</td>
          </tr>
        
      </tbody>
    </table>
    </div>
<br>
    <div style="overflow: auto; max-height: 300px;">
<h3>A Square</h3>
    <table class="df-table">
      <thead>
        <tr>
          <th></th>
          <th class="float32">A</th>
        </tr>
      </thead>
      <tbody>
        
          <tr>
            <th>0</th>
            <td class="float32">0.21270543336868286</td>
          </tr>
        
          <tr>
            <th>1</th>
            <td class="float32">0.2613254487514496</td>
          </tr>
        
          <tr>
            <th>2</th>
            <td class="float32">0.4776192009449005</td>
          </tr>
        
          <tr>
            <th>3</th>
            <td class="float32">0.22014862298965454</td>
          </tr>
        
      </tbody>
    </table>
    </div>
 
---
### Reading CSV file from URL

```
dfd.read_csv("https://raw.githubusercontent.com/curran/data/gh-pages/jsLibraries/jsLibs.csv")
  .then(df => {

    //prints the first five columns
    df.head().print()

  }).catch(err => {
    console.log(err);
  })

```



<div style="overflow: auto; max-height: 300px;">
      <table class="df-table">
        <thead>
          <tr>
            <th></th>
            <th class="string">Library</th><th class="int32">Minified File Size (kb)</th><th class="int32">Github Stars</th>
          </tr>
        </thead>
        <tbody>
         <tr>
              <th>0</th>
              <td class="string">Knockout.js</td><td class="int32">17</td><td class="int32">5036</td>
            </tr>
          
            <tr>
              <th>1</th>
              <td class="string">Angular.js</td><td class="int32">106</td><td class="int32">24580</td>
            </tr>
          
           <tr>
              <th>2</th>
              <td class="string">Ember.js</td><td class="int32">71</td><td class="int32">10368</td>
            </tr>
          
            <tr>
              <th>3</th>
              <td class="string">Can.js</td><td class="int32">82</td><td class="int32">928</td>
            </tr>
          
            <tr>
              <th>4</th>
              <td class="string">React.js</td><td class="int32">123</td><td class="int32">7015</td>
            </tr>
          
        </tbody>
      </table>
      </div>

---
### Calculate descriptive statistics for all numerical columns
```
df.describe().print()
```

<div style="overflow: auto; max-height: 300px;">
    <table class="df-table">
      <thead>
        <tr>
          <th></th>
          <th class="float32">Minified File Size (kb)</th><th class="float32">Github Stars</th>
        </tr>
      </thead>
      <tbody>
        
          <tr>
            <th>count</th>
            <td class="float32">7</td><td class="float32">7</td>
          </tr>
        
          <tr>
            <th>mean</th>
            <td class="float32">58.071426</td><td class="float32">9464.286133</td>
          </tr>
        
          <tr>
            <th>std</th>
            <td class="float32">49.75978</td><td class="float32">9038.434833</td>
          </tr>
        
          <tr>
            <th>min</th>
            <td class="float32">1</td><td class="float32">156</td>
          </tr>
        
          <tr>
            <th>median</th>
            <td class="float32">71</td><td class="float32">7015</td>
          </tr>
        
          <tr>
            <th>max</th>
            <td class="float32">123</td><td class="float32">24580</td>
          </tr>
        
          <tr>
            <th>variance</th>
            <td class="float32">2476.035714</td><td class="float32">81693304.23</td>
          </tr>
      </tbody>
    </table>
    </div>

---
### The shape of the data, column names, and dtypes
```    
console.log(df.shape);
    
console.log(df.column_names);

df.ctypes.print()   
```

```
[ 7, 3 ]
[ 'Library', 'Minified File Size (kb)', 'Github Stars' ]
```

<div style="overflow: auto; max-height: 300px;">
    <table class="df-table">
      <thead>
        <tr>
          <th></th>
          <th class="string">0</th>
        </tr>
      </thead>
      <tbody>
        
          <tr>
            <th>Library</th>
            <td class="string">string</td>
          </tr>
        
          <tr>
            <th>Minified File Size (kb)</th>
            <td class="string">float32</td>
          </tr>
        
          <tr>
            <th>Github Stars</th>
            <td class="string">int32</td>
          </tr>
        
      </tbody>
    </table>
    </div>


```
dfd.read_csv("https://raw.githubusercontent.com/curran/data/gh-pages/jsLibraries/jsLibs.csv")
    .then(df => {
        df['Library'].print()
    }).catch(err => {
        console.log(err);
    })
```

<div style="overflow: auto; max-height: 300px;">
    <table class="df-table">
      <thead>
        <tr>
          <th></th>
          <th class="string">Library</th>
        </tr>
      </thead>
      <tbody>
        
          <tr>
            <th>0</th>
            <td class="string">Knockout.js</td>
          </tr>
        
          <tr>
            <th>1</th>
            <td class="string">Angular.js</td>
          </tr>
        
          <tr>
            <th>2</th>
            <td class="string">Ember.js</td>
          </tr>
        
          <tr>
            <th>3</th>
            <td class="string">Can.js</td>
          </tr>
        
          <tr>
            <th>4</th>
            <td class="string">React.js</td>
          </tr>
        
          <tr>
            <th>5</th>
            <td class="string">Backbone.js</td>
          </tr>
        
          <tr>
            <th>6</th>
            <td class="string">Model.js</td>
          </tr>
        
      </tbody>
    </table>
    </div>

---
### Selecting on a multi-axis by label, by slicing, and by query
```
dfd.read_csv("https://raw.githubusercontent.com/curran/data/gh-pages/jsLibraries/jsLibs.csv")
    .then(df => {
        // Selection by label
        const sub_df = df.loc({ rows: [0, 1], columns: ["Library", "Github Stars"] })
        sub_df.print()
       
       // Selection by slicing
        const slice_df = df.loc({ rows: ["0:4"], columns: ["Library", "Github Stars"] })
        slice_df.print()
       
       // Selection by query
        const query_df = df.query({ "column": "Github Stars", "is": ">", "to": 10000 })
        query_df.print()   
    }).catch(err => {
        console.log(err);
    })
```
 <div style="overflow: auto; max-height: 300px;">
        <h3>Selection By Multi-Axis Label</h3>
    <table class="df-table">
      <thead>
        <tr>
          <th></th>
          <th class="string">Library</th><th class="int32">Github Stars</th>
        </tr>
      </thead>
      <tbody>
        
          <tr>
            <th>0</th>
            <td class="string">Knockout.js</td><td class="int32">5036</td>
          </tr>
        
          <tr>
            <th>1</th>
            <td class="string">Angular.js</td><td class="int32">24580</td>
          </tr>
        
      </tbody>
    </table>
    </div>
    <div style="overflow: auto; max-height: 300px;">
        <h3>Selection By Slicing</h3>
    <table class="df-table">
      <thead>
        <tr>
          <th></th>
          <th class="string">Library</th><th class="int32">Github Stars</th>
        </tr>
      </thead>
      <tbody>
        
          <tr>
            <th>0</th>
            <td class="string">Knockout.js</td><td class="int32">5036</td>
          </tr>
        
          <tr>
            <th>1</th>
            <td class="string">Angular.js</td><td class="int32">24580</td>
          </tr>
        
          <tr>
            <th>2</th>
            <td class="string">Ember.js</td><td class="int32">10368</td>
          </tr>
        
          <tr>
            <th>3</th>
            <td class="string">Can.js</td><td class="int32">928</td>
          </tr>
        
      </tbody>
    </table>
    </div>
    <div style="overflow: auto; max-height: 300px;">
        <h3>Selection By Query</h3>
    <table class="df-table">
      <thead>
        <tr>
          <th></th>
          <th class="string">Library</th><th class="float32">Minified File Size (kb)</th><th class="int32">Github Stars</th>
        </tr>
      </thead>
      <tbody>
        
          <tr>
            <th>1</th>
            <td class="string">Angular.js</td><td class="float32">106</td><td class="int32">24580</td>
          </tr>
        
          <tr>
            <th>2</th>
            <td class="string">Ember.js</td><td class="float32">71</td><td class="int32">10368</td>
          </tr>
        
          <tr>
            <th>5</th>
            <td class="string">Backbone.js</td><td class="float32">6.5</td><td class="int32">18167</td>
          </tr>
        
      </tbody>
    </table>
    </div>


#### There are many mathematical [operations](https://danfo.jsdata.org/api-reference) we can perform over the dataframe object.
---
### Danfo supports plotting

Danfo uses [Plotly.js](https://plotly.com/javascript/) as backend for plotting. This gives us the ability to make interactive plots from DataFrame and Series. Plotting only works in the browser version of danfo.js, and requires an HTML div to show plots. 

```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
     <!--danfojs CDN -->
    <script src="https://cdn.jsdelivr.net/npm/danfojs@0.1.1/dist/index.min.js"></script>
    <title>Document</title>
</head>

<body>

    <div id="plot_div"></div>
    <script>

         dfd.read_csv("https://raw.githubusercontent.com/curran/data/gh-pages/jsLibraries/jsLibs.csv")
            .then(df => {

                var layout = {
                    title: 'JavaScript Libraries and Github Stars',
                    xaxis: {
                        title: 'Libraries',
                    },
                    yaxis: {
                        title: 'Stars',
                    }
                }

                new_df = df.set_index({key:"Library"})
                new_df.plot("plot_div").bar({columns:["Github Stars"],layout: layout })

            }).catch(err => {
                console.log(err);
            })
         
    </script>
</body>

</html>

```


![newplot.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1598425279483/tvu6G1ZCO.png)


