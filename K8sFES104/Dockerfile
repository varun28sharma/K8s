# Step 1: Build stage (Node.js for React/Vite)
FROM node:20 AS build-stage
WORKDIR /app

# Install git to allow repo cloning
RUN apt-get update && apt-get install -y git

# Clone your repo (will create a subdirectory with the repo contents)
RUN git clone https://github.com/varun28sharma/K8s.git .

# The frontend lives in the K8S_Ecommerce_Frontend subfolder — build from there
RUN cd K8sFES104/K8S_Ecommerce_Frontend \
   && npm install --no-audit --no-fund \
   && npm run build


# Step 2: Runtime stage (Tomcat for serving)
FROM tomcat:9-jdk21
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy React build output from the frontend subfolder into Tomcat webapps
COPY --from=build-stage /app/K8sFES104/K8S_Ecommerce_Frontend/dist /usr/local/tomcat/webapps/ecommerce

EXPOSE 8080
CMD ["catalina.sh", "run"]