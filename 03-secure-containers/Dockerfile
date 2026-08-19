# Use the absolute latest Nginx Alpine image
FROM nginx:alpine

# The DevSecOps Magic: Force the OS to update all packages during build
RUN apk update && apk upgrade --no-cache

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
