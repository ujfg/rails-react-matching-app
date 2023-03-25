# ベースとなるDockerイメージ
# ruby:XXXはdebian系
FROM ruby:3.0

# OSのコマンドを実行
# apt-get update: インストール可能なパッケージの「一覧」を更新する。実際のパッケージのインストール、アップグレードなどはおこなわない。
# apt-get install: 指定したパッケージをインストールする
# build-essential: 開発に必須のビルドツールを提供しているパッケージ(gcc, g++, make)
# libpq-dev: PostgreSQLのlib
RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs

# 環境変数の設定
ENV APP_PATH /myapp

RUN mkdir $APP_PATH
# 以降の作業ディレクトリの指定
WORKDIR $APP_PATH

# ローカルのディレクトリ及びファイルをDockerコンテナにマウント
COPY Gemfile $APP_PATH/Gemfile
COPY Gemfile.lock $APP_PATH/Gemfile.lock
RUN bundle install

COPY . $APP_PATH

COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
# 最初に実行するコマンドの指定
ENTRYPOINT ["entrypoint.sh"]
# Dockerコンテナを公開するポート番号の指定
EXPOSE 3000
# デフォルトで実行するコマンドの指定
CMD ["rails", "server", "-b", "0.0.0.0"]