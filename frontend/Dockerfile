FROM callumhoughton22/mushroom-classification-front-end:latest

COPY ./start.sh ./start.sh
RUN chmod u+x ./start.sh

RUN yarn add serve

CMD ["/app/start.sh"]