# Deploying an Angular Application on App Engine
These Notes cover a simple walkthrough of deploying an `Angular` application on Google Cloud's `App Engine` utilizing `Nginx`, `Docker` and `Cloud Build`.

## Before Starting
1. Select or Create a Google Cloud Project
2. Enable the App Engine, Cloud Build, and Container Registry APIs.


## Angular project and App Engine environment variable Setup
1. Create a new local Angular Project.
2. Verify the app works by serving and checking out on your localhost.
3. In the `src/assets` folder, add `envconfig.js` and `envconfig.template.js` files.
4. Copy the following code into the `envconfig.js` file.

```javascript
    (function(window) {
        window["envconfig"] = window["envconfig"] || {};

        //Environment variables
        window["envconfig"]["apiurl"] = "http://localhost:8080/api";
    })(this);
```

5. Copy the following code into the `envconfig.template.js` file:
```javascript
(function(window) {
      window.envconfig = window.envconfig || {};

      // Environment variables
      window["envconfig"]["apiurl"] = "${API_URL}";           
})(this);
```
6. Add a reference to the envconfig.js file in index.html.

7. Remove / from `<base href="">` in the index.html file. This will be useful when you want to use dispatch.yaml later.

8. Update the `environment.ts` file with this code:

```javascript
export const environment = {
     production: false,
     webapiurl: (window as any)["envconfig"]["apiurl"] || "default"                   
};
```

9. For testing whether API_URL is working or not, add usage of this environment.webapiurl anywhere in the application.

10. For example, you can add it as shown in the sample code in app.component.html and app.component.ts.

11. Update outputPath in the build section of the angular.json file with "outputPath": "dist".

12. Build your Angular project again and verify that you are able to see the webapiurl value as http://localhost:8080/api when you open the app in a browser.

13. If everything is working, then you can go to the next steps using Cloud Build.

## Cloud Build
You can use Cloud Build in many ways. This will use the `dist` build output folder of the sample app

1. Create an `nginx-hosting` folder and copy the `dist` folder into it.
   
2. Add a `Dockerfile` file in the `nginx-hosting` folder, and copy the following code into the file:

```dockerfile
# The standard nginx container just runs nginx. The configuration file added
# below will be used by nginx.
FROM nginx

# Copy the nginx configuration file. This sets up the behavior of nginx. Most
# important, it ensures that nginx listens on port 8080. Google App Engine expects
# the runtime to respond to HTTP requests at port 8080.
COPY nginx.conf /etc/nginx/nginx.conf

# create log dir configured in nginx.conf
RUN mkdir -p /var/log/app_engine

# Create a simple file to handle health checks. Health checking can be disabled
# in app.yaml, but is highly recommended. Google App Engine will send an HTTP
# request to /_ah/health and any 2xx or 404 response is considered healthy.
# Because 404 responses are considered healthy, this could actually be left
# out as nginx will return 404 if the file isn't found. However, it is better
# to be explicit.
RUN mkdir -p /usr/share/nginx/www/_ah && \
    echo "healthy" > /usr/share/nginx/www/_ah/health

# Finally, all static assets.
ADD dist/ /usr/share/nginx/www/sampleapp

CMD ["/bin/sh",  "-c",  "envsubst < /usr/share/nginx/www/sampleapp/assets/envconfig.template.js > /usr/share/nginx/www/sampleapp/assets/envconfig.js && exec nginx -g 'daemon off;'"]
```

3. Add an `nginx.conf` file in the `nginx-hosting` folder, and copy the following code into the file:

```
events {
   worker_connections 768;
}

http {
    sendfile on;
    tcp_nopush on;
    tcp_nodelay on;
    keepalive_timeout 65;
    types_hash_max_size 2048;
    include /etc/nginx/mime.types;
    default_type application/octet-stream;

    # Logs will appear on the Google Developer's Console when logged to this
    # directory.
    access_log /var/log/app_engine/app.log;
    error_log /var/log/app_engine/app.log;

    gzip on;
    gzip_disable "msie6";

    server {
        # Google App Engine expects the runtime to serve HTTP traffic from port 8080.
        listen 8080;  

        # Root directory and index files
        index index.html index.htm;

        location / {
            root /usr/share/nginx/www/sampleapp;
        }

        location /sampleapp/ {
        root /usr/share/nginx/www;
        }
    }
}
```

4. Add a `cloudbuild.yaml` file in the `nginx-hosting` folder, and copy the following code into the file:

```yaml
steps:
- name: 'gcr.io/cloud-builders/docker'
  args: ['build', '-t', 'us.gcr.io/$PROJECT_ID/angular-nginx-container', '.']
- name: 'gcr.io/cloud-builders/docker'
  args: ['push', 'us.gcr.io/$PROJECT_ID/angular-nginx-container']
images: ['us.gcr.io/$PROJECT_ID/angular-nginx-container']
```

5. Add an `app.yaml` file in the `nginx-hosting` folder, and copy the following code into the file:

6. If you want to verify the setup in your local Docker environment, you can do so with the following two commands on the `nginx-hosting` folder. (To make this work you have to comment out `listen 8080`; in the nginx file.)
   
```powershell
docker build -t sampleapp .
docker run --env API_URL="https://webapi-dev.appname.com" -dp 8080:80 sampleapp
```

Verify on `http://localhost:8080` that everything works.

7. You can directly use the above four files to deploy your app in App Engine using the `gcloud` command-line tool. To do so, run the following commands:
   1. Create the Docker image on the specified path in the `cloudbuild.yaml` file.
   ```powershell
   gcloud builds submit
   ```
   After this command, verify that you have a container image created at `https://console.cloud.google.com/gcr/images/yourprojectid?project=yourprojectid`.

   2. Deploy your image to App Engine with the service name that you provided in the `app.yaml ` file:
   
   ```powershell
   gcloud app deploy --image-url us.gcr.io/yourprojectid/angular-nginx-container
   ```

8. Verify that the `webapiurl` matches what you provided in the environment variable as shown in the flow diagram at the beginning of this tutorial.

## App Engine dispatch
You can extend the solution for `dispatch.yaml`. This deployment using nginx supports additional locations so that when you use `dispatch` as shown in the following example, you should be able to access your application using the root URL of your project. To make this work, you have to update the `nginx` location with your service name as a location `angular-ui-dev` and you should be able to access your application using the `https://your-project-id.uc.r.appspot.com/angular-dev-ui/` URL.

```yaml
  dispatch:
  # Default service serves simple hostname request.
  - url: "your-project-id.uc.r.appspot.com/"
    service: default

  # Dispatch UI
  - url: "*/angular-ui-dev/*"
    service: angular-ui-dev
```