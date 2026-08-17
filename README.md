To build your own TOM (Target Observation Manager), check out the [getting started guide](https://tomtoolkit.github.io/docs/getting_started). The Supernova Exchange (2.0) is an interface for viewing and sharing observational data of supernovae, and for requesting and managing observations with the [LCO](https://lco.global/) network. SNEx 2.0 is currently live at [supernova.exchange](https://supernova.exchange/). Most pages are private (proprietary data), but the "TNS Targets" page is public.

This is Megan Newsome's copycat version of SNEx 2.0 to investigate how an already-existing TOM works on a local connection.
Steps to get running:

Clone the repo:
`git clone https://github.com/drmegannewsome/snex2.git`

Change into the repo directory:
`cd snex2/`

Use a Python3+ environment:
```
conda create name_of_py3_env --python=3.11
conda activate name_of_py3_env
```

Make sure you can use `uv` for a Python project manager:
```
uv pip install -e .
uv python pin 3.11
```

Sync:
`uv sync`

From this point on, we need to make sure that we're startign with clean ports for postgres servers. If you have old postgres servers you will need to create a local_settings.py file with available ports, or clear old servers.

Make sure your Docker daemon is running and then run:
`docker run -d --name snex2-db   -e POSTGRES_DB=snex2   -e POSTGRES_USER=postgres   -e POSTGRES_PASSWORD=postgres   -p 5432:5432   postgis/postgis:15-3.3-alpine`

If you had to delete old postgres servers, recreate a cache table:

`uv run python manage.py createcachetable`

Now complete the creation of the SNEx2 server:
`uv run python manage.py migrate`
`uv run python manage.py createsuperuser`

Input your desired login credentials for your local version of SNEx2.0. Then run
`uv run python manage.py runserver`
and visit http://127.0.0.1:8000 in your browser to view.

