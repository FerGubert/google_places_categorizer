# Google Places Categorizer

This tool makes it easy to get data from the google places API, as well as enrich it with other categories of interest. It also provides a match of the existing categories in the data with the fourth-level categories from the Yelp database.

## 💻 Prereqs:

To get started make sure you meet the following requirements:

* Python environment - Version 3.7.4+

## ⚙️ Install:

To install `Google Places Categorizer` you need clone the follow repository:

```
git clone git@github.com:FerGubert/google_places_categorizer.git
```

Create the `.env` file with your google places API key, as indicated in the `.env.example`.

After then do you need install environment:

```
pip install .
```

## 🚀 Run:

This tool provides two different flows, the flow you want to run must be passed as an argument when executing the main. Below are the details of each flow.

### Calculate Coordinates

This flow generates a csv file with the geographic coordinates of a rectangular area and according to a predetermined step in meters.

First, it is necessary to set the variables described below in the file `config.py`:

* NORTHEAST_LAT, NORTHEAST_LON: indicates the extreme northeast of the area.
* SOUTHWEST_LAT, SOUTHWEST_LON: indicates the extreme southwest of the area.
* RADIUS: indicates the radius of reach for each coordinate that is created within the area.

Then you must pass the argument that indicates this flow when executing the file `main.py`:

```
python src/main.py --flow coordinates
```

The calculated coordinates will be available in `data/output/lat_lon_calculated.csv`.

### Request Google Places API

This flow performs requests to the Google places API, according to the geographic coordinates defined in the input file and a predetermined radius. It enriches the data according to the categories also defined in the input file and handles the return of the API, making the data available in a csv file.

First, it is necessary to set the variable described below in the file `config.py`:

* RADIUS: indicates the range for each coordinate that will be used in the request.

It is also necessary to provide in `data/input` a csv file with the geographic coordinates that will be used in the request, as indicated in the `lat_lon.csv` file. 

If you want to enrich the data obtained from the Google places API with more specific categories, a csv file with the desired categories must be made available in the same path or use the categories of the fourth hierarchical level of the Yelp base already available in `/data/input/categories_request.csv`.

Then you must pass the argument that indicates this flow when executing the file `main.py`:

```
python src/main.py --flow request
```

The processed data will be available in `data/output/establishments.csv`.

### Matching Category Phrases

This flow creates the Yelp phrases using the category hierarchical levels and creates the establishment phrases using the Google categories and the enrichment categories. The records of establishments with their phrases are exported in a csv file. Then, for each sentence of the establishment, it retrieves the Yelp sentence with the highest semantic textual similarity, making these matchings available with their respective scores in a csv file.

To execute this flow, the `hierarchical_yelp_categories.csv` file is used, containing the 4 hierarchical levels of the Yelp categories, available in `data/input`. It is also necessary to have available in `data/output` the csv file with the establishments retrieved from the Google places API, without changing the column schema and the name `establishments.csv`. 

Then you must pass the argument that indicates this flow when executing the file `main.py`:

```
python src/main.py --flow match
```

The data of the establishments with their phrases will be available in `data/output/establishments_phrases.csv` and the match of the phrases of the establishments with the phrases Yelp, as well as the score, will be available in `data/output/matching_category_phrases.csv`.

## 🤝 Members:

Who are committers:

<b>Fernanda R Gubert</b>
