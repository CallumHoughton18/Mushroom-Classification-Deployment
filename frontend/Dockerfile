FROM callumhoughton22/mushroom-classification-front-end:latest

RUN yarn add serve
RUN yarn build

CMD ["serve", "-p", "80", "-s", "./build"]