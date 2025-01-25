# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
ARG BUILD_FROM
FROM $BUILD_FROM

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Execute during the build of the image
ARG TEMPIO_VERSION BUILD_ARCH
RUN \
  curl -sSLf -o /usr/bin/tempio \
  "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}"

WORKDIR /app_data

COPY SmartHomeBioSignal/dash-app/ /app_data/
RUN apt install software-properties-common
RUN add-apt-repository ppa:deadsnakes/ppa -y
# RUN apk add tree py3-scikit-learn
RUN apt-get update && apt-get install -y build-essential python3.13 tree python3-sklearn python3-pip

RUN pip install poetry

RUN poetry install

CMD [ "poetry", "run", "python", "dash_app/src/app.py" ]