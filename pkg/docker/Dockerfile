FROM python:3.13-alpine3.21

ENV TZ=Asia/Shanghai \
    CYCLE=86400 \
    RESTART_AUTO_UPDATE=false

# 安装依赖
RUN set -ex && \
    apk add --no-cache bash tini tzdata build-base gcc g++ && \
    python3 -m pip install --no-cache-dir --upgrade pip

# 复制仓库代码到镜像中
COPY ./ /app

# 安装 Python 依赖
RUN pip install --no-cache-dir -r /app/requirements.txt && \
    apk del --purge build-base gcc g++ && \
    rm -rf /root/.cache /tmp/*

# 复制 entrypoint
COPY --chmod=755 ./pkg/docker/entrypoint.sh /entrypoint.sh

ENTRYPOINT ["tini", "-g", "--", "/entrypoint.sh"]
CMD ["--media", "/media"]
