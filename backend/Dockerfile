FROM node:22-slim
RUN apt-get update && apt-get install -y --no-install-recommends python3 python3-venv \
    && rm -rf /var/lib/apt/lists/*
WORKDIR /app

COPY package*.json ./
RUN npm ci --omit=dev

COPY ai/requirements.txt ai/requirements.txt
RUN python3 -m venv /opt/venv && /opt/venv/bin/pip install --no-cache-dir -r ai/requirements.txt
ENV PATH="/opt/venv/bin:$PATH" PYTHON=/opt/venv/bin/python NODE_ENV=production

COPY . .
CMD ["node", "start.js"]
