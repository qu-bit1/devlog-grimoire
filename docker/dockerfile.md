- A script with instructions to build an [[images]].
- Defines what gets installed, copied, run, etc.

basic dockerfile

```dockerfile
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
CMD ["npm", "start"]
```

```bash
docker run -d -p 3000:3000 -v $(pwd):/app myimage
```
