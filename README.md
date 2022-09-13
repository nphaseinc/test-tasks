# 1) papermill-task

Create ASGI microservice which has API:
- [GET] API for executing jupyter notebook and return HTML response
- [POST] API for adding notebook data into DB
- [PUT] API for adding notebook data
- [DELETE] API for deleting notebook data
- [GET] Health check of microservice

Notebook structure in DB table:
- id - integer (ID of notebook)
- name - string (Name of notebook without `.ipynb`. For example `Rcc Demo Study Token`)
- file_path - string (Path of notebook file in FS. For example `/opt/notebooks/Simple_Print_Params.ipynb`)
- created_date - timestamp (Date of notebook creation)
- updated_date - timestamp (Last update date)

Requirements:
1) https://github.com/orgs/jupyter/repositories - it's all jupyter project and need to investigate how to covert result notebook data into HTML.
2) Provide `Access-Control-Allow-Origin: *` for this microservice.
3) Provide Dockerfile and ability to pass `PG_URI` for PostgreSQL connection in docker container.
4) Provide also `docker-compose.yml` which contains service and PG DB.

# 2) Custom jupyterlab auth

Fork `jupyter_server` repo and add the next code changes:
1) Use JWT token auth instead of default password auth.
2) Use the JWT token in browser via query param, for example: `http://localhost:8080/?token=qwe4dg4svx46nfgf8456`
3) Think about what information the token should store.
4) If there's no such user we must create it.
5) Provide docker image with the custom `jupyter_server` & `jupyterlab`.
6) All these logic have to work in docker container.
