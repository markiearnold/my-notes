# Rails: Webpacker inside Docker Container

```ruby
# config/initializers/content_security_policy.rb

Rails.application.config.content_security_policy do |p|
  p.default_src :self, :https, :unsafe_inline
  p.font_src    :self, :https, :data, :unsafe_inline
  p.img_src     :self, :https, :data, :unsafe_inline
  p.object_src  :none
  p.script_src  :self, :https, :unsafe_inline
  p.style_src   :self, :https, :unsafe_inline

  # To allow connections to the webpack-dev-server running in
  # a separate docker container
  if Rails.env.development?
    p.connect_src :self, :https, 'http://localhost:3035', 'ws://localhost:3035', 'http://0.0.0.0:3035', 'ws://0.0.0.0:3035'
  end

  # Specify URI for violation reports
  # p.report_uri "/csp-violation-report-endpoint"
end
```

```yml
# config/webpacker.yml

development:

  # ...
  
  dev_server:
    host: webpacker
    port: 3035
    public: localhost:3035
    # ...
```

```yml
# docker-compose.yml

version: '3'
volumes:
  bundle:
  database:
services:
  web:
    build:
      context: .
      args:
        precompileassets: "disable"
    volumes:
      - .:/home/app/src
      - bundle:/usr/local/bundle
    ports:
      - "8080:3000"
  webpacker:
    build:
      context: .
      args:
        precompileassets: "disable"
    env_file:
      - '.env.docker'
    command: bash -c "rm -rf /app/public/packs; rm -rf /home/app/src/spec/dummy/tmp/pids/server.pid; ./bin/webpack-dev-server"
    volumes:
      - .:/home/app/src
    ports:
      - '3035:3035'
```

```sh
# startup.sh

if [ $# -eq 0 ] ; then
  echo '=========== Precompiling'
  cd spec/dummy; RAILS_ENV=production SECRET_KEY_BASE=does_not_matter_here bin/rails assets:precompile
else
  if [ $1 = "disable" ] ; then
    echo "=========== Precompile disabled"
  else
    echo 'argument supplied but different from not, precompiling'
    cd spec/dummy; RAILS_ENV=production SECRET_KEY_BASE=does_not_matter_here bin/rails assets:precompile
  fi
fi
```

```sh
FROM phusion/passenger-customizable:0.9.27
ARG precompileassets

RUN bash -lc 'rvm remove all --force && rvm install ruby-2.5.0 && rvm --default use ruby-2.5.0 && gem install bundler -v 1.16.1'
RUN /pd_build/ruby_support/install_ruby_utils.sh
RUN /pd_build/ruby_support/finalize.sh

ENV NVM_VERSION v0.33.8
ENV NODE_VERSION v8.9.4
ENV NPM_VERSION 5.4.2
ENV YARN_VERSION 1.13.0
ENV NVM_DIR /home/app/.nvm
ENV PATH $NVM_DIR/versions/node/$NODE_VERSION/bin:$PATH
RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/$NVM_VERSION/install.sh | bash \
    && . $NVM_DIR/nvm.sh \
    && nvm install $NODE_VERSION \
    && nvm alias default $NODE_VERSION \
    && nvm use default \
    && npm install -g npm@$NPM_VERSION yarn@$YARN_VERSION

WORKDIR /home/app/src

ADD lib/playbook/version.rb /home/app/src/lib/playbook/
ADD Gemfile* *.gemspec /home/app/src/
RUN bundle install --frozen

ADD package.json yarn.lock /home/app/src/
RUN yarn install
RUN npm rebuild node-sass

COPY ./startup.sh /
RUN chmod +x /startup.sh

ADD --chown=app:app . /home/app/src
RUN mkdir /etc/service/puma && ln -s /home/app/src/services/puma.sh /etc/service/puma/run

RUN /startup.sh $precompileassets
```
