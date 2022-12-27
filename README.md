# West Hartford Crash Map

Interactive heatmap of car crashes in West Hartford CT from 2015 to present, displaying pre-processed data from UConn Crash Data Repository

## Links
- Live map https://bikewesthartford.github.io/wh-crash-map
- UConn Crash Data Repository https://www.ctcrash.uconn.edu

## Credits
Adapted by [Jack Dougherty](https://jackdougherty.org) from the [original Hartford Crash Data heatmap](https://github.com/Picturedigits/hartford-crashes) created by Ilya Ilyankou at [Picturedigits](https://www.picturedigits.com) for Transport Hartford.

![Heatmap gif](./img/demo.gif)

## Create Your Own
This open-source GitHub repository includes a Jupyter Notebook data processor and Leaflet map code that can be adapted for other towns in Connecticut, or other states that have similar data. These instructions assume you have some familiarity with creating your own fork and hosting a GitHub repository of simple Leaflet map code. If not, read [Chapter 10: Edit and Host Code in GitHub](https://handsondataviz.org/github.html) in our Hands-On Data Visualization book.

### Pre-process UConn Crash Repository data
1. Create your own fork of this GitHub repository. Recommended: Use GitHub Desktop to migrate files between your online repository and your local computer.
2. Navigate to https://www.ctcrash.uconn.edu/ and create an account if you don't have one yet.
3. Log in, and go to `Data Query Tool`.
4. Select a `MMUCC(2015-)` dataset, specify dates and town (or multiple towns).
5. Run the query, and then click `Export To CSV` button above the interactive table. A link will be sent to your email account to download the archive. Note that the tool may prevent you from exporting datasets that are "too large". In that case, break down your query (for example, instead of downloading 2015-2020 data, do 2015-2018 as one export, and 2019-2020 as another).
6. Unzip the archive(s), then move to `export_#####` folder to place it inside the `data/` folder of your forked GitHub repository.
7. Delete the existing files named `crashes.csv` and `crashes.json` in the data folder, and also the existing `export_old###` folder.
8. Use Jupyter Notebook <https://jupyter.org> to pre-process the data. One method is to install the free (but large) Anaconda platform on your local computer <https://www.anaconda.com>, then run Jupyter Notebook. NOTE: Previously it was possible to do this by running Jupyter Notebook in your browser (aka JupyterLite) <https://jupyter.org/try-jupyter/lab/>, but that is not working for me today.
9. In Jupyter Notebook, navigate to your local computer to open the Jupyter notebook file inside the data folder, which in this example is `wh-crash-map/data/ProcessCrashes.ipynb`.
10. In step 2 of the Juypter notebook file, insert your export ID (numbers) from your UConn Crash Repo download to the `exports` list. Save your notebook.
11. Important: Go back to step 1 and run the notebook. After all steps are complete, it should generate a new CSV (`crashes.csv`) and a JSON file (`crashes.json`) in the `data/` folder.
12. Migrate any relevant files from your local computer to your forked GitHub repository online, and use the GitHub Pages setting to host your repo online.

### Modify the Leaflet map settings
1. Modify the `index.html` of the Leaflet map in your forked GitHub repository to set custom map title, and `script.js` to change initial coordinates, date ranges, and anything else related to the map. Example:
```
// change dates, where Jan = 0 and Dec = 11
var initFrom = dateToTS(new Date(2017, 0, 1));
var initTo = dateToTS(new Date(2022, 11, 27));  
```
2. This map is fully front-end, and loads data once from the CSV file using PapaParse JS library. Optional: You can change the code to fetch the JSON file using `$.getJSON()` function of jQuery, although it is slightly heavier than the CSV.

### I still have questions
Get in touch with ilya@picturedigits.com if you have any other questions or suggestions!

### License
MIT
