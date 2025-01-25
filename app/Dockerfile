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

RUN apk add tree py3-scikit-learn

RUN tree

RUN pip install poetry

RUN tree

RUN poetry install

CMD [ "poetry", "run", "python", "dash_app/src/app.py" ]