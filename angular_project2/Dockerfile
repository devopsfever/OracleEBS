FROM node:16
LABEL project="angular project"
LABEL author="by Devops Fever"
RUN git clone https://github.com/Ismaestro/angular-example-app.git
RUN cd angular-example-app
WORKDIR /angular-example-app
RUN sed -i 's/ng serve --configuration=development-en --open/ng serve --host 0.0.0.0/g' package.json
RUN sed -i 's/ng serve --configuration=development-es --open/ng serve --host 0.0.0.0/g' package.json
RUN npm install --force
EXPOSE 4200
WORKDIR /angular-example-app
CMD ["npm", "start"]
