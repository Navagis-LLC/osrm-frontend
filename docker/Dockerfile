FROM alpine:3.5

ARG GITHUB_TOKEN

# Enables customized options using environment variables
ENV OSRM_BACKEND='http://localhost:5000'
ENV OSRM_CENTER='38.8995,-77.0269'
ENV OSRM_ZOOM='13'
ENV OSRM_LANGUAGE='en'
ENV OSRM_LABEL='Car (fastest)'

# Copy package.json
RUN mkdir -p /src
COPY package.json /src
COPY .npmrc /src

# Install app dependencies
RUN apk add --no-cache sed nodejs && \
    cd /src && \
    echo "//npm.pkg.github.com/:_authToken=$GITHUB_TOKEN" >> .npmrc && \
    npm install && \
    rm .npmrc

# Create app directory
COPY . /src
WORKDIR /src

# Run App
EXPOSE 9966
CMD ["npm", "start"]
