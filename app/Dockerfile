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

COPY run.sh /app_data/
COPY SmartHomeBioSignal /app_data/

RUN apk add tree
RUN tree

RUN pip install -r dash-app/requirements.txt

RUN chmod a+x ./run.sh
CMD [ "./run.sh" ]