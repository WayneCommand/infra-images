FROM ubuntu:25.04

# 设置环境变量
ENV DEBIAN_FRONTEND=noninteractive
ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US:en
ENV LC_ALL=en_US.UTF-8

# 更新系统包列表并安装所需包（包含 locales）
RUN apt-get update && apt-get install -y --no-install-recommends \
    # 基础工具
    curl \
    wget \
    vim \
    ca-certificates \
    software-properties-common \
    # Python3
    python3 \
    python3-pip \
    python3-dev \
    # ffmpeg 依赖
    libavcodec-extra \
    ffmpeg \
    # 本地化支持
    locales \
    # 其他必要库
    libc6 \
    libgcc-s1 \
    libstdc++6 \
    && rm -rf /var/lib/apt/lists/*

# Add the intel-graphics PPA
RUN add-apt-repository -y ppa:kobuk-team/intel-graphics
RUN apt-get update && apt-get install -y --no-install-recommends \
    intel-media-va-driver-non-free \
    libmfx-gen1 \
    vainfo \
    && rm -rf /var/lib/apt/lists/*

# 生成并配置 en_US.UTF-8 locale
RUN sed -i 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    locale-gen en_US.UTF-8 && \
    update-locale LANG=en_US.UTF-8 LANGUAGE=en_US:en LC_ALL=en_US.UTF-8

# 验证 ffmpeg 支持
RUN ffmpeg -codecs 2>&1 | grep -i hevc || echo "ffmpeg check completed"

# 设置工作目录
WORKDIR /app

# 设置 entrypoint
ENTRYPOINT ["tail", "-f", "/dev/null"]
