FROM python:3

# pymysql 0.9.3 removes a function "convert_mysql_datetime" that mycli 1.10.0 relies on
RUN pip install pymysql==0.9.2
# mycli > 1.10.0 runs slow on Docker
RUN pip install mycli==1.10.0

RUN apt update
RUN apt install -y less

# See docs at mycli.net/pager
ENV PAGER less
ENV LESS='-XFS'
