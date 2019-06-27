FROM ruby:2.5

# Install nodejs
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
# Install yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
# Install packages
RUN apt-get update -qq && apt-get install -y nodejs postgresql-client build-essential libpq-dev yarn

RUN mkdir /test_app
WORKDIR /test_app
COPY Gemfile /test_app/Gemfile
COPY Gemfile.lock /test_app/Gemfile.lock
RUN bundle install
RUN yarn install && yarn cache clean
COPY . /test_app

# Add a script to be executed every time the container starts.
COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
EXPOSE 3000

# Start the main process.
CMD ["rails", "server", "-b", "0.0.0.0"]
