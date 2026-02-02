FROM python:3.14.2-alpine

WORKDIR /app

COPY . .
RUN pip install --no-cache-dir flask

EXPOSE 5000

CMD ["python", "app.py"]
