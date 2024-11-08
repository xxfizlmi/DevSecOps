FROM node:alpine

RUN addgroup -S myuser && adduser -S myuser -G myuser
USER myuser

WORKDIR /app

# Salin file `package.json` dan `package-lock.json` terlebih dahulu
COPY package*.json ./

RUN npm install

# Salin sisa kode setelah dependensi diinstal
COPY . .

CMD ["node", "app.js"]
