# Etapa 1: Build
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
# Usar npm install en lugar de npm ci para desarrollo
RUN npm install --only=production

# Etapa 2: Producción
FROM node:20-alpine
WORKDIR /app

# Instalar dumb-init para manejar señales correctamente
RUN apk add --no-cache dumb-init

# Copiar node_modules desde builder
COPY --from=builder /app/node_modules ./node_modules

# Copiar código fuente
COPY . .

# Crear usuario no-root para seguridad
RUN addgroup -g 1001 -S nodejs && \
    adduser -S nodejs -u 1001 && \
    chown -R nodejs:nodejs /app
USER nodejs

# Variables de entorno por defecto
ENV NODE_ENV=production
ENV PORT=3000

# Exponer puerto
EXPOSE 3000

# Usar dumb-init para manejar señales
ENTRYPOINT ["dumb-init", "--"]
CMD ["node", "index.js"]
