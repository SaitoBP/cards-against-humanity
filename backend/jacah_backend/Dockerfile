FROM alpine:latest

# install elixir
RUN apk add --update elixir

# install hex
RUN mix local.hex --force

# install rebar
RUN mix local.rebar --force

# create app directory
RUN mkdir /app

# set working directory
WORKDIR /app

# copy the mix files
COPY mix.exs mix.lock ./

# install dependencies
RUN mix deps.get

# copy the rest of the files
COPY . .

# expose port 4000
EXPOSE 4000
EXPOSE 4001

ARG POSTGRES_USER
ARG POSTGRES_PASSWORD
ARG POSTGRES_DB
ARG POSTGRES_HOST
ARG POSTGRES_PORT
ARG RUN_DATABASE_SETUP

# setup the database
# start the server
CMD ["/bin/sh", "-c", "mix ecto.setup; mix phx.server"]
# CMD ["sh", "-c", "ping pgdatabase"]