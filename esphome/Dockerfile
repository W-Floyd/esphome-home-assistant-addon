ARG BUILD_FROM
FROM ${BUILD_FROM}

# Replace the device-builder install script to use the patched fork
# instead of the latest PyPI prerelease.
# See: https://github.com/esphome/device-builder/issues/XXX
RUN printf '#!/usr/bin/with-contenv bashio\n\
if ! bashio::config.true '"'"'use_new_device_builder'"'"'; then\n\
  exit 0\n\
fi\n\
bashio::log.info "Installing patched esphome-device-builder from fork..."\n\
if command -v uv > /dev/null; then\n\
  uv pip install --system --no-cache-dir \\\n\
    "git+https://github.com/W-Floyd/device-builder.git" ||\n\
    bashio::exit.nok "Failed installing esphome-device-builder."\n\
else\n\
  pip install --no-cache-dir \\\n\
    "git+https://github.com/W-Floyd/device-builder.git" ||\n\
    bashio::exit.nok "Failed installing esphome-device-builder."\n\
fi\n\
bashio::log.info "Installed patched esphome-device-builder."\n\
' > /etc/cont-init.d/40-device-builder.sh
