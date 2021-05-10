FROM callumhoughton22/mushroom-classification-front-end:latest
ENV API_BASE_URL=https://mushroomlapi.callums-stuff.net/api    
                                                                                                   
RUN yarn add serve
RUN yarn build

CMD ["serve", "-p", "80", "-s", "./build"]