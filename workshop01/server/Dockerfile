#base image
FROM node:latest  

# define env var
ENV APP_PORT=3000
ENV APP_ROOT=/app
ENV DB_HOST=nwdb
ENV DB_PORT=3306
ENV DB_USER=root
ENV DB_PASSWORD=changeit

# create a root directory, then cd into it
RUN mkdir ${APP_ROOT}
WORKDIR ${APP_ROOT}

# copy source files into WORKDIR
# . mean current directory, adding main.js into current directory (WORKDIR)
# ADD https://excample.com (download from remote)
ADD main.js .
ADD package.json .
ADD package-lock.json .
ADD config config
ADD public public
ADD views views

# install  dependencies
RUN npm install

# configure health check
# -s mean silent  /dev/null <-- whatever output send to rusbish
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
    CMD curl -s -f http://localhost:${APP_PORT}/health > /dev/null || exit 1

# tell docker what port this nodejs using
EXPOSE ${APP_PORT}

# run start command why dont use RUN because it will get run during the build phase 
ENTRYPOINT [ "node", "main.js" ]