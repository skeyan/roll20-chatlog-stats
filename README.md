# roll20-chatlog-stats
Python notebook and dashboard for getting stats from Roll20 D&D 5E rolls. 

![Dashboard Screenshot](https://www.robopenguins.com/assets/wp-content/uploads/2021/roll20/dashboard_thumb.webp)

See <https://www.robopenguins.com/roll20-stats/> for a description of the development process.

The scripts in this repo assume they're running within a virtual environment located in a `.env` directory.

`virtualenv --python=python3 .env`

You can install the required libraries into it with:

```shell
source .env/bin/activate
pip install -r requirements.txt 
```

# 1) Scraping With parsing_notebook.ipynb
Scraping is done with the library, [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/). This ipynb utilizes Roll20's CSS tagging to parse rolls, get their type, and assign a character to them.

See <https://jupyter-notebook-beginner-guide.readthedocs.io/en/latest/> for a guide to getting started with notebooks.

The notebook takes an HTML file saved from a Roll20 message archive (See <https://www.robopenguins.com/roll20-stats/>) and creates a zipped .csv with the columns:

`time,character,session,type,value`

This is specifically tailored to a D&D 5e game, and only looks at 1d20 (with or without modifiers) rolls.

This could easily be changed around by modifying the parsing if you were interested in rolls other then d20's or the exact type or content of the rolls.

Documentation on this TBA.

# 2) Dashboard
The dashboard is a Plotly dash application. This is a framework that creates a Flask app that gives an interactive view into the data.

The one thing I hard coded that would need to be update is the `players` variable which is just to distinguish the player characters from the NPCs for grouping in the dashboard.

This can be run in debug mode with `python dashboard.py`

I also included a `run.sh` and `roll20stats.service` file so that the page can be started as a systemd service <https://medium.com/@benmorel/creating-a-linux-service-with-systemd-611b5c8b91d6> .

You could run this in the cloud in a VPS, or as a Heroku app <https://dash.plotly.com/deployment>
