ARG BUILD_FROM
FROM $BUILD_FROM

ENV LANG C.UTF-8

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

# Install basics
RUN set -eux; \
	apk add --update --no-cache git \
	npm \
	musl-dev \
	g++ \
	python3-dev \
	libxml2 \
	libxml2-dev && \
	apk add libxslt-dev
	
RUN set -eux; \
	pip install aiohttp \
	alembic \
	aniso8601 \
	async-timeout \
	attrs \
	babel \
	beautifulsoup4 \
	blinker \
	certifi \
	chardet \
	click \
	feedparser \
	flake8 \
	flask \
	flask-babel \
	flask-login \
	flask-migrate \
	flask-paginate \
	flask-principal \
	flask-restful \
	flask-sqlalchemy \
	flask-talisman \
	flask-wtf \
	idna \
	itsdangerous \
	jinja2 \
	lxml \
	mako \
	markupsafe \
	mccabe \
	multidict \
	opml \
	psycopg2-binary \
	pycodestyle \
	pydot \
	pyflakes \
	pyparsing \
	python-dateutil \
	python-editor \
	pytz \
	requests \
	requests-futures \
	six \
	soupsieve \
	sqlalchemy \
	sqlalchemy-schemadisplay \
	urllib3 \
	werkzeug \
	wtforms \
	yarl

# Install poetry
# RUN set -eux; \
# 	curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python -

# Install newspipe
RUN set -eux; \
	git clone https://git.sr.ht/~cedric/newspipe; \
	cd newspipe/; \
	npm install; \
# 	source $HOME/.poetry/env; \
# 	poetry config virtualenvs.create false; \
# 	poetry install; \
# 	poetry shell; \
	pybabel compile -d newspipe/translations; \
	export NEWSPIPE_CONFIG=sqlite.py; \
	export FLASK_APP=runserver.py; \
	export FLASK_ENV=development; \
	flask db_create

# Copy root filesystem
#COPY rootfs /

# Labels
LABEL \
    io.hass.name="newspipe" \
    io.hass.description="newspipe" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Berichta" \
    org.label-schema.description="newspipe" \
    org.label-schema.build-date=${BUILD_DATE} \
    org.label-schema.name="newspipe" \
    org.label-schema.schema-version="1.0" \
    org.label-schema.url="https://github.com/berichta/hassio-addons" \
    org.label-schema.usage="https://github.com/berichta/hassio-addons/blob/master/newspipe/README.md" \
    org.label-schema.vcs-ref=${BUILD_REF} \
    org.label-schema.vcs-url="https://github.com/berichta/hassio-addons" \
    org.label-schema.vendor="Berichta"
