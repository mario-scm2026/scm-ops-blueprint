FROM node:20-alpine
WORKDIR /app

# Instalar dumb-init para manejar señales correctamente
RUN apk add --no-cache dumb-init

# Copiar archivos de dependencias
COPY package*.json ./

# Instalar TODAS las dependencias (incluyendo devDependencies)
# Usar npm install sin --omit=dev para desarrollo
RUN npm install

# Copiar el resto del código
COPY . .

# Crear usuario no-root para seguridad (opcional en desarrollo)
# RUN addgroup -g 1001 -S nodejs && \
#     adduser -S nodejs -u 1001 && \
#     chown -R nodejs:nodejs /app
# USER nodejs

# Variables de entorno
ENV NODE_ENV=development
ENV PORT=3000

EXPOSE 3000

# Usar dumb-init y nodemon para desarrollo
ENTRYPOINT ["dumb-init", "--"]
CMD ["npm", "run", "dev"]
