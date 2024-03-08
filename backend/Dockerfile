# python3.9のイメージをダウンロード
FROM python:3.9-buster
ENV PYTHONUNBUFFERED=1

WORKDIR /src

# pipを使ってpoetryをインストール
RUN pip install poetry

# poetryの定義ファイルをコピー (存在する場合)
COPY pyproject.toml* poetry.lock* ./

# poetryでライブラリをインストール (pyproject.tomlが既にある場合)
RUN poetry config virtualenvs.in-project true
RUN if [ -f pyproject.toml ]; then poetry install --no-root; fi

# プロジェクトファイルとテストファイルをコピー
COPY . .

# uvicornのサーバーを立ち上げる
ENTRYPOINT ["poetry", "run", "uvicorn", "api.main:app", "--host", "0.0.0.0", "--reload"]


# poetryで依存関係をインストールする前に、pyproject.toml と poetry.lock をコピー
COPY pyproject.toml poetry.lock* ./

# 開発依存関係を含めて依存関係をインストール
RUN poetry config virtualenvs.in-project true && \
    poetry install --no-root
