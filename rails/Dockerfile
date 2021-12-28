FROM ruby:2.6.5

ENV LANG C.UTF-8
ENV APP_HOME /numbatApp

RUN apt-get update -qq && apt-get install -y build-essential nodejs npm && npm install --global yarn

# This is a error handling when to be occurred yarn error.
# RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
# RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && apt-get update && apt-get install -y yarn

RUN rm -rf /var/lib/apt/lists/*

RUN mkdir $APP_HOME
WORKDIR $APP_HOME
COPY ./Gemfile $APP_HOME/Gemfile
COPY ./Gemfile.lock $APP_HOME/Gemfile.lock
RUN bundle install
RUN rails webpacker:install
COPY . $APP_HOME

EXPOSE  3000
