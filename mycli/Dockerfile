FROM python:3

RUN pip install mycli

RUN apt update
RUN apt install -y less

# See docs at mycli.net/pager
ENV PAGER less
ENV LESS='-XFS'
