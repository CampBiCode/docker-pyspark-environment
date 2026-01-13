FROM python:3.10-slim-bookworm

RUN apt-get update && apt-get install -y \
    openjdk-17-jdk-headless \
    ca-certificates \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Set JAVA_HOME
ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
ENV PATH="$JAVA_HOME/bin:$PATH"

WORKDIR /notebooks

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

RUN python -m ipykernel install --sys-prefix --name python3 --display-name "Python 3 (PySpark)"

EXPOSE 8888

CMD ["jupyter", "lab", \
     "--ip=0.0.0.0", \
     "--port=8888", \
     "--no-browser", \
     "--allow-root", \
     "--ServerApp.token="]