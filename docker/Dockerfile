# Set the base image
FROM ubuntu:20.04

# Set environment variables to avoid interactive prompts during package installation
ENV DEBIAN_FRONTEND=noninteractive

# Install required packages
RUN apt-get update && apt-get install -y \
    git \
    build-essential \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Clone the repository
RUN git clone --depth 1 https://github.com/sarazeyn/raspberrypi.git

# List the contents to verify the structure (for debugging purposes)
RUN ls -l raspberrypi

# Create target directories
RUN mkdir -p Viper-produce/raspberrypi

# Check if the 'transactionalmachinelearning' directory exists and copy it
RUN if [ -d "transactionalmachinelearning" ]; then \
      cp -R transactionalmachinelearning Viper-produce/transactionalmachinelearning; \
    else \
      echo "Directory transactionalmachinelearning not found"; \
    fi

# Check if 'raspberrypi/transactionalmachinelearning' exists and copy it if necessary
RUN if [ -d "raspberrypi/transactionalmachinelearning" ]; then \
      cp -R raspberrypi/transactionalmachinelearning Viper-produce/transactionalmachinelearning; \
    else \
      echo "Directory raspberrypi/transactionalmachinelearning not found"; \
    fi

# Set the working directory
WORKDIR Viper-produce

# Change permissions for the 'transactionalmachinelearning' directory
RUN chmod -R 755 transactionalmachinelearning

# Final command (you can replace this with your desired command, e.g., starting a service)
CMD ["echo", "Dockerfile built successfully!"]
