# Base image
FROM mcr.microsoft.com/devcontainers/base:jammy

# Install Python and pip
RUN apt-get update && \
    apt-get install -y \
        python3 \
        # Instal virtual environment tool
        python3-venv \
        # Install pip
        python3-pip \
        && \
    apt-get clean && \
    # Clean up to reduce image size
    rm -rf /var/lib/apt/lists/*

# Use bash to run commands
SHELL ["/bin/bash", "-c"]

# Set up environment variable for virtual environment path
ENV VENV_PATH=/opt/venv
# Create a virtual environment at /opt/venv
RUN python3 -m venv $VENV_PATH

# Adjust the environment's search path
ENV PATH="$VENV_PATH/bin:$PATH"

# Install Python packages. Keeps the image smaller by skipping the pip cache.
RUN pip3 install --no-cache-dir \
    ipykernel \
    matplotlib \
    numpy \
    pandas \
    scipy

# Register the virtualenv as a Jupyter kernel
ENV JUPITER_KERNEL_NAME='Python (devcontainer venv)'
RUN python -m ipykernel install --name devcontainer-venv --display-name "$JUPITER_KERNEL_NAME"