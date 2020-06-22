[![Build Status](https://qa.nuxeo.org/jenkins/buildStatus/icon?job=master/plugins_nuxeo-web-ui-master-master)](https://qa.nuxeo.org/jenkins/job/master/job/plugins_nuxeo-web-ui-master-master/)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/5d8cd2a3c56745ecaae7e7f92a683ea7)](https://www.codacy.com/app/Nuxeo/nuxeo-web-ui)

## Nuxeo Web UI

### About
Nuxeo Web UI is a standard base web application for Nuxeo Platform. It is highly customizable and scalable, developed with [Polymer](https://polymer-library.polymer-project.org/) and leveraging [nuxeo-elements](https://github.com/nuxeo/nuxeo-elements), our library of custom elements.

### Install dependencies

```sh
npm config set @nuxeo:registry https://packages.nuxeo.com/repository/npm-public
npm install
```

### Development workflow

#### Configure

For convenience you should create an `.env` file to set default environment variables:

```sh
cp .env.sample .env
```

#### Environment variables

Variable | Used by | Description | Default
--- | --- | --- | ---
NUXEO_PACKAGES | Webpack, Docker (Nuxeo) | List of packages to enable for Web UI and Nuxeo
NUXEO_URL | Webpack | URL used to connect to Nuxeo server from Web UI | /nuxeo
NUXEO_HOST | Webpack | Nuxeo host address to proxy calls from the dev server | localhost:8080 
NUXEO_WEB_UI_VERSION | Docker compose | Version of Web UI image to build /start
NUXEO_VERSION | Docker compose | Version of Nuxeo server to launch

#### Serve / watch

```sh
npm run start
```

This makes the Web UI available on http://0.0.0.0:5000/ to locally test. A nuxeo platform is expected to run on http://0.0.0.0:8080/ with the following `cors-config.xml`:

```xml
<component name="org.nuxeo.corsi.demo">
  <extension target="org.nuxeo.ecm.platform.web.common.requestcontroller.service.RequestControllerService" point="corsConfig">
    <corsConfig name="foobar" supportedMethods="GET,POST,HEAD,OPTIONS,DELETE,PUT" 
exposedHeaders="Accept-Ranges,Content-Range,Content-Encoding,Content-Length,Content-Disposition">
      <pattern>/nuxeo/.*</pattern>
    </corsConfig>
  </extension>
</component>
```

#### Run tests
The following commands can be run in order to run tests against Web UI.

##### Unit Tests

```sh
npm run test
```
##### Functional Tests

```sh
npm run ftest
```

#### Build & Vulcanize

```sh
npm run build
```

Build and optimize the current project, ready for deployment. This includes linting as well as vulcanization, image, script, stylesheet and HTML optimization and minification.

#### Run with Docker Compose

After building the project with `npm run build` you can try a Docker compose based deployment with:

```sh
docker-compose up --build
```

This builds the `nuxeo-web-ui` Docker image and starts the Docker compose cluster.

Web UI will then be available at http://localhost:8080/nuxeo/ui

### Production workflow

#### Marketplace package

```sh
mvn clean install
```

This will build the  `plugin/web-ui/marketplace/target/nuxeo-web-ui-marketplace-${project.version}.zip` Web UI marketplace to be deployed in a nuxeo server.

```sh
mvn clean install -Pftest
```

This also builds the marketplace running the functionnal tests.

## License

[Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0.html) 

(C) Copyright Nuxeo Corp. (http://nuxeo.com/)

All images, icons, fonts, and videos contained in this folder are copyrighted by Nuxeo, all rights reserved.

## About Nuxeo

Nuxeo dramatically improves how content-based applications are built, managed and deployed, making customers more agile, innovative and successful. Nuxeo provides a next generation, enterprise ready platform for building traditional and cutting-edge content oriented applications. Combining a powerful application development environment with SaaS-based tools and a modular architecture, the Nuxeo Platform and Products provide clear business value to some of the most recognizable brands including Verizon, Electronic Arts, Sharp, FICO, the U.S. Navy, and Boeing. Nuxeo is headquartered in New York and Paris. More information is available at www.nuxeo.com.
