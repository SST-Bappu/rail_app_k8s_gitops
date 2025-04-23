# Use official Ruby image
FROM ruby:3.1

# Set environment variables
ENV RAILS_ENV=production \
    NODE_ENV=production \
    BUNDLER_VERSION=2.3.26 \
    TZ=UTC \
    SECRET_KEY_BASE=3a1de0c0393ceab695fa5687810aedc07b6e34abd11f7e81f1da0ff40285521177c822072454a6639c6d9b6fb15e7945e702b2ce62db6947bbea603c880f6b9f

# Install dependencies
RUN apt-get update -qq && \
    apt-get install -y build-essential libpq-dev nodejs npm yarn

    # Set working directory
WORKDIR /app

# Copy Gemfiles and install gems
COPY Gemfile* ./
RUN bundle install

# Copy all files
COPY . .

# Install node modules for stylelint
RUN npm install && \
    npm install --save-dev stylelint@13.x stylelint-scss@3.x stylelint-config-standard@21.x stylelint-csstree-validator@1.x

# Precompile assets (optional, for production)
RUN bundle exec rake assets:precompile

# Expose port
EXPOSE 3000

# Start server
CMD ["rails", "server", "-b", "0.0.0.0"]



