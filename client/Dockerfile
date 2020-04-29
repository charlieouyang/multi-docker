# first build phase
from node:alpine
WORKDIR '/app'
COPY ./package.json ./
RUN npm install
COPY . .
# /app/build will have all of the result build files
RUN npm run build

# REMEMBER.. This nginx is not the nginx that's doing the routing between '/' and
# '/api'.. This it he nginx that's serving up the PRODUCTION react app

# second phase
FROM nginx
# Need to expose port 3000 on AWS app
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=0 /app/build /usr/share/nginx/html

# no need to RUN or CMD.. nginx starts by itself
