# Multistage builds

Can have multiple `FROM` that start new step of build, cleaner than having multiple Dockerfiles

```dockerfile
# Stage 1: Build Client
FROM node:10.11.0-alpine as build
WORKDIR /app

# Install any needed packages specified
COPY ./client/package.json .
COPY ./client/yarn.lock .
RUN yarn install

# Copy the client contents into the container at /app
COPY ./client .

# build app
RUN yarn build


# Stage 2: Run backend that serves client statically
FROM node:10.11.0-alpine
WORKDIR /app

# Copy build from previous container
COPY --from=build /app/build /app/build

# Install backend packages
COPY ./backend/package.json .
COPY ./backend/yarn.lock .
RUN yarn install

# Copy the backend contents into the container at /app
COPY ./backend .

EXPOSE 3001

# Run yarn prod when container launches
CMD ["yarn", "prod"]
```

