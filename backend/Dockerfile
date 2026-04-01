# Ce Dockerfile utilise un multi-stage build pour des raisons de sécurité et de taille d'image.
# Le premier stage installe toutes les dépendances (y compris celles de développement) et exécute les tests,
# permettant de vérifier la qualité du code avant la production. Le second stage utilise une image Alpine légère
# et ne copie que les dépendances de production, réduisant ainsi la taille finale de l'image et minimisant
# la surface d'attaque en excluant les outils de développement et les tests de l'image de production.

# ========================
# Build stage
# ========================

FROM node:20-alpine AS build

ARG ENV_NAME

WORKDIR /app

ENV NODE_ENV=$ENV_NAME

COPY src/package*.json ./
#Install dependancies
RUN npm ci 
#--omit=dev (Not for dev)

COPY src/ ./

# ========================
# Runtime stage
# ========================

FROM node:20-alpine AS runtime

ARG ENV_NAME

WORKDIR /app

ENV NODE_ENV=$ENV_NAME

#Non root user
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

#Copy from build stage
COPY --from=build --chown=appuser:appgroup /app /app

USER appuser

EXPOSE 4000

CMD npm run $NODE_ENV
