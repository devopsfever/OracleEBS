FROM node:16
LABEL project="angular project"
LABEL author="devopsfever104f@gmail.com"
RUN git clone https://github.com/gothinkster/angular-realworld-example-app.git
RUN cd angular-realworld-example-app
WORKDIR /angular-realworld-example-app
RUN sed 's/jasmine-core": "~3.6.0/jasmine-core": "~3.8.0/g' package.json > mypkg.json
RUN sed 's/jasmine": "~3.6.0"/jasmine": "~3.8.0"/g' mypkg.json > opkg.json
RUN cp opkg.json package.json
RUN npm install -g @angular/cli && npm install
EXPOSE 4200
WORKDIR /angular-realworld-example-app
CMD ["ng", "serve", "--host", "0.0.0.0" , "--disable-host-check"]
