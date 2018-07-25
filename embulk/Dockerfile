FROM openjdk:8-jre

# system update
RUN apt-get -y update && apt-get -y upgrade

# locale
RUN apt-get -y install locales && \
  localedef -f UTF-8 -i ja_JP ja_JP.UTF-8
ENV LANG ja_JP.UTF-8
ENV LANGUAGE ja_JP:ja
ENV LC_ALL ja_JP.UTF-8

# timezone (Asia/Tokyo)
ENV TZ JST-9

RUN apt-get -y install nkf

RUN useradd -ms /bin/bash bulkload
COPY --chown=bulkload:bulkload ./bin /usr/local/embulk
RUN ln -sf /usr/local/embulk/bin/embulk-0.8.0 /usr/local/bin/embulk \
  && chmod +x /usr/local/bin/embulk

USER bulkload

WORKDIR /usr/local/embulk/bundle
# embulk0.8.0未満だと動かない（0.7.4, 5, 11で確認）
RUN embulk bundle
