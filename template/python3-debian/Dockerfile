FROM python:3

RUN curl -sSL https://github.com/openfaas/faas/releases/download/0.9.4/fwatchdog > /usr/bin/fwatchdog \
    && chmod +x /usr/bin/fwatchdog
WORKDIR /root/

COPY index.py           .
COPY requirements.txt   .
RUN pip install -r requirements.txt

RUN mkdir -p function
RUN touch ./function/__init__.py
WORKDIR /root/function/
COPY function/requirements.txt	.
RUN pip install -r requirements.txt

WORKDIR /root/
COPY function           function

WORKDIR /root/

ENV fprocess="python3 index.py"

HEALTHCHECK --interval=1s CMD [ -e /tmp/.lock ] || exit 1

CMD ["fwatchdog"]
