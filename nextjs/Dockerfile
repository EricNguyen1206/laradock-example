# **********
# base stage
# **********
FROM node:20.9.0-alpine AS base

# Set the working directory
WORKDIR /app

# **********
# deps stage
# **********
FROM base AS deps

# Install dependencies
COPY package*.json ./
# Copy available lock file
COPY package.json package-lock.json* ./
RUN npm install

# Disable the telementary
ENV NEXT_TELEMETRY_DISABLED 1

# ***********
# inter stage
# ***********
FROM deps AS inter

# Copy all other files excluding the ones in .dockerignore
COPY . .

# exposing the port
EXPOSE 3000

# **********
# prod stage
# **********
FROM inter AS prod

RUN npm run build

CMD ["npm", "start"]

# **********
# dev stage
# **********
FROM inter AS dev

CMD ["npm", "run", "dev"]