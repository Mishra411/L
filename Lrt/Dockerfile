# === Step 1: Build frontend ===
FROM node:20 AS frontend-build
WORKDIR /frontend
COPY frontend/package*.json ./
RUN npm install
COPY frontend/ ./
RUN npm run build

# === Step 2: Setup backend ===
FROM python:3.12-slim
WORKDIR /app
COPY backend/requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt
COPY backend/ ./

# === Step 3: Copy frontend build into backend (if you want backend to serve it) ===
COPY --from=frontend-build /frontend/dist ./frontend-dist

# === Step 4: Start backend ===
ENV PORT 8000
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
