# --- Stage 1: Build Environment ---
# Use Node.js 14 as the base image for building the application
FROM node:14 AS web-build

# Set the working directory inside the container
WORKDIR /usr/src/app

# Copy package files first to leverage Docker layer caching
# This prevents re-installing dependencies if package.json hasn't changed
COPY package*.json ./

# Install project dependencies
RUN npm install

# Copy the rest of the application source code
COPY . .

# Execute the Angular production build
# Optimization: --max-old-space-size=1024 limits Node.js memory usage to 1GB
# This is crucial for successful builds on low-RAM instances like AWS t3.micro
RUN node --max-old-space-size=1024 ./node_modules/@angular/cli/bin/ng build --prod

# --- Stage 2: Production Environment ---
# Use Nginx to serve the static files generated in the build stage
FROM nginx:latest

# Copy only the compiled production assets from the 'web-build' stage
# This keeps the final image size small by excluding node_modules and source code
COPY --from=web-build /usr/src/app/dist/client/ /usr/share/nginx/html

# Replace the default Nginx configuration with our custom project config
# Essential for handling Angular's client-side routing
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80 to allow external HTTP traffic
EXPOSE 80