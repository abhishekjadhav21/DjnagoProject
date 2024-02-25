FROM python:3.12

ENV PYTHONBUFFERED=1

WORKDIR /django

COPY requirements.txt requirements.txt

# Install dependencies, including libpq-dev for PostgreSQL support
RUN apt-get update \
    && apt-get install -y libpq-dev \
    && pip install -r requirements.txt

COPY . .

# Add wait-for-it script
ADD https://raw.githubusercontent.com/vishnubob/wait-for-it/master/wait-for-it.sh /usr/local/bin/wait-for-it
RUN chmod +x /usr/local/bin/wait-for-it



# Wait for PostgreSQL service to be ready
CMD ["wait-for-it", "postgres:5432", "--", "python", "manage.py", "runserver", "0.0.0.0:8000"]
