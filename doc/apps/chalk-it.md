# Chalk'it

To deploy a [Chalk'it](https://github.com/ifpen/chalk-it) application in Ploomber Cloud you need:

- A `Dockerfile`
- A Chalk'it projet definition JSON file renamed to `dashboard.xprjson`

## `Dockerfile`

You just need to use this [template](https://github.com/ploomber/doc/blob/main/examples/docker/chalk-it/Dockerfile) `Dockerfile`:

```Dockerfile
FROM python:3.11

# assume your dashboard is named dashboard.xprjson
COPY dashboard.xprjson dashboard.xprjson

# install py-chalk-it and gunicorn
RUN pip install py-chalk-it gunicorn

# this configuration is needed for your app to work, do not change it
ENTRYPOINT ["gunicorn", "chlkt.render:app", "run", "--bind", "0.0.0.0:80"]
```

## Testing locally

To test your app, you can use `docker` locally:

```sh
# build the docker image
docker build . -t dashboard

# run it
docker run -p 5000:80 dashboard
```

Now, open [http://0.0.0.0:5000/](http://0.0.0.0:5000/) to see your app.


## Deploy

Once you have all your files, create a zip file.

To deploy a Chalk'it app from the deployment menu, follow these instructions:

![](../static/docker.png)