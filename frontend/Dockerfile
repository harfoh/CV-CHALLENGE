# Stage 1: Build
FROM node:20-alpine AS build

# Set the working directory
WORKDIR /app

# Copy only the necessary files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application files
COPY . .

# Build the application for production
RUN npm run build

# Stage 2: Serve
FROM node:20-alpine AS production

# Set the working directory
WORKDIR /app

# Install a lightweight HTTP server for static files
RUN npm install -g serve

# Copy only the built application and static assets
COPY --from=build /app/dist ./dist

# Expose the port the application will run on
EXPOSE 5173

# Serve the application
CMD ["serve", "-s", "dist", "-l", "5173"]
