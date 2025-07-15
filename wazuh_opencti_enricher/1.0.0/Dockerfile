# Base our app image off of the Shuffle App SDK image
FROM frikky/shuffle:app_sdk as base

# Builder stage to install Python dependencies
FROM base as builder
RUN apk --no-cache add --update alpine-sdk libffi libffi-dev musl-dev openssl-dev

# Install Python packages
RUN mkdir /install
WORKDIR /install
COPY requirements.txt .
RUN pip install --prefix="/install" -r requirements.txt

# Final stage
FROM base
COPY --from=builder /install /usr/local
COPY app.py /app/app.py
COPY requirements.txt /app/requirements.txt

WORKDIR /app
CMD python app.py --log-level DEBUG
