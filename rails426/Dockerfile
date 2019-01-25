FROM ruby:2.3.1
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - && apt-get update && apt-get install -y build-essential apt-utils libpq-dev nodejs
RUN mkdir -p /app
WORKDIR /app
ENV HOME=/app PATH=/app/bin:$PATH
RUN gem install bundler -v 1.17
ADD Gemfile* /app/
RUN set -ex && bundle install --jobs 20 --retry 5
# creates user with same name & uid in host OPTIONAL
# RUN useradd --no-create-home --uid 1000 --user-group alfredo
