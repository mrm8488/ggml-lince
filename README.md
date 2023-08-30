# Run GGML quantized version of  ClibrAIn's Lince-zero

This scipts is heavely based on `ggml` conversion and run repositories for LLMs.

Just modified it to run the quantized version of Lince-zero.

## Usage

```bash
#!/bin/bash

# License: Apache-2.0

# This script sets up and runs the lince model
# Ensure you have wget, git, cmake, and make installed before running this script.

# Set model and directory variables
MODEL_URL="https://huggingface.co/clibrain/lince-zero-f16-ggml-q4_0/resolve/main/lince-zero-f16-ggml-q4_0.bin"
MODEL_DIR="$HOME/lince-model"
MODEL_BIN="${MODEL_DIR}/lince-zero-f16-ggml-q4_0.bin"
GGML_REPO="https://github.com/mrm8488/ggml-lince.git"
BUILD_DIR="build"

# Create model directory
mkdir -p $MODEL_DIR

# Download the model
wget $MODEL_URL -O $MODEL_BIN || { echo "Failed to download model"; exit 1; }

# Clone the repository
git clone $GGML_REPO || { echo "Failed to clone repository"; exit 1; }

# Navigate into the repository directory
cd ggml-lince || { echo "Directory does not exist"; exit 1; }

# Create build directory and navigate into it
mkdir -p $BUILD_DIR && cd $BUILD_DIR || { echo "Failed to create or navigate to build directory"; exit 1; }

# Build project
cmake .. || { echo "cmake failed"; exit 1; }
cd examples/falcon || { echo "Directory does not exist"; exit 1; }
make || { echo "make failed"; exit 1; }

# Navigate back to run the model
cd ../../$BUILD_DIR/bin || { echo "Directory does not exist"; exit 1; }

# Show the help message
./lince -h || { echo "./lince failed"; exit 1; }

# Run the model
./lince -m  $MODEL_BIN \
-p "A continuación hay una instrucción que describe una tarea, junto con una entrada que\
proporciona más contexto. Escriba una respuesta que complete adecuadamente la solicitud.\n\n\
### Instrucctión:\nDame una lista de sitios a visitar en España\n\n### Respuesta:" \
-n 64
 ```