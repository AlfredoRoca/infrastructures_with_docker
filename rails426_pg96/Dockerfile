FROM ruby:2.3.1
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - && apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs

# 2: We'll set the application path as the working directory
RUN mkdir -p /code
WORKDIR /code

# 3: We'll add the app's binaries path to $PATH:
ENV HOME=/code PATH=/code/bin:$PATH

RUN gem install bundler

ADD code/Gemfile* /code/

RUN set -ex && bundle install --jobs 20 --retry 5

# Copy the main application.
COPY /code /code/

# Expose port 3000 to the Docker host, so we can access it from the outside.
EXPOSE 3000

# Configure an entry point, so we don't need to specify "bundle exec" for each of our commands.
ENTRYPOINT ["bundle", "exec"]

# The main command to run when the container starts
# The main purpose of a CMD is to provide defaults for an executing container.
# CMD ["rails", "server", "-b", "0.0.0.0"]
CMD ["/bin/bash"]
