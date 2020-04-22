# Swiss API - States, locations and ZIP codes
[Swagger documentation here](https://swiss-state-npa-location.herokuapp.com/)

## Francais:
Cette API REST fournit la liste de tous les cantons suisses, de toutes les localités du pays, ainsi que leurs numéros postaux coorrespondants. Les données proviennent du "Répertoire des localités suisses" publié par l'Office fédéral de la statistique (Ici). En outre, elle offre des points d'entrée qui peuvent être utilisés pour l'autocomplétion des codes postaux et des localités dans vos formulaires html !

## Deutsch:
Diese RESTful API stellt alle Schweizer Staaten, alle Standorte und die entsprechenden Postleitzahlen. Die Daten stammen vom Schweizerischen Bundesamt für Statistik in dem Bericht "Ortschaftenverzeichnis der Schweiz" (Hier). Darüber hinaus bietet sie Einstiegspunkte, die für die automatische Vervollständigung von Postleitzahl und Ort in Ihren HTML Formularen verwendet werden können !

## Italiano:
Questa RESTful API mette a disposizione tutti gli stati svizzeri, tutte le località e i relativi codici di avviamento postale. I dati provengono dall'Ufficio federale di , nel rapporto "Elenco delle località svizzere" (Qui). Inoltre, offre punti d'ingresso che possono essere utilizzati per l'autocompletamento del codice di avviamento postale e della località nei vostri moduli !

## English:
This RESTful API provides all swiss states, all locations and their corresponding ZIP codes. The data comes from the Swiss federal statistical office (Here). Furthermore, it offers entry points that can be used for ZIP-code and location autocompletion in your html forms !

# Example of use
Location autocompletion. Give it a try here: https://github.com/JobinJohan/swiss_locations_api

```html
<!DOCTYPE html>
<html lang="fr">
  <head>
    <meta charset="utf-8">
    <title>Autocompletion example</title>
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
    <style>
    /*This code makes the arrow visible for all browsers.
    By default Firefox, IE, Edge don't display any arrow for datalist
    Note: In order for the datalist to work on Firefox, add aucomplete="off" as attribute in the input element*/
    input::-webkit-calendar-picker-indicator {
      display: none;/* remove default arrow */
    }
    .myarrow:after {
      content: url(https://i.stack.imgur.com/i9WFO.png);
      margin-left: -20px;
      padding: .1em;
      pointer-events:none;
    }
    </style>
  </head>
  <body>
    <h1>Enter location name</h1>
    <form>
      <span class="myarrow"><input type="text" list="dataList" id="autocompletionForm" autocomplete="off" onkeyup="fetchData()"></span>
      <datalist id="dataList">
      </datalist>
    </form>

    <script type="text/javascript">
    const fetchData = () => {

      // Reset the list
      document.getElementById("dataList").innerHTML="";

      // Get the input value
      var element = document.getElementById("autocompletionForm");
      var user_input = element.value;

      // Avoid API call when input is smaller than 2 characters
      if (user_input.length<2){
        return 0;
      }

      // Look for all locations matching with the input
      url = "https://swiss-state-npa-location.herokuapp.com/localite-autocompletion/"+user_input;
      axios.get(url)
      .then(response => {
        allLocations = response.data;

        // Add an option for each location received from the API
        for (var i=0; i<allLocations.length; i++){
          console.log("test");
          document.getElementById("dataList").appendChild(document.createElement("option")).setAttribute("value", allLocations[i].location + ", " + allLocations[i].canton);
        }
      })
      .catch(error => console.error(error));
    }
    </script>
  </body>
</html>

```


```javascript

```
