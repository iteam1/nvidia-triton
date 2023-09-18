# nvidia-triton
nvidia-triton example

# Serve a Model in 3 Easy Steps

    # Step 1: Create the example model repository
    git clone -b r23.08 https://github.com/triton-inference-server/server.git
    cd server/docs/examples
    ./fetch_models.sh

    # Step 2: Launch triton from the NGC Triton container
    sudo docker run --gpus=1 --rm --net=host -v ${PWD}/model_repository:/models nvcr.io/nvidia/tritonserver:23.08-py3 tritonserver --model-repository=/models

    # Step 3: Sending an Inference Request
    # In a separate console, launch the image_client example from the NGC Triton SDK container
    sudo docker run -it --rm --net=host nvcr.io/nvidia/tritonserver:23.08-py3-sdk

    # Step 4 (Inside the container) Run inference:
    /workspace/install/bin/image_client -m densenet_onnx -c 3 -s INCEPTION /workspace/images/mug.jpg

    # Inference should return the following
    Image '/workspace/images/mug.jpg':
        15.346230 (504) = COFFEE MUG
        13.224326 (968) = CUP
        10.422965 (505) = COFFEEPOT

*Note:* required images:

    nvcr.io/nvidia/tritonserver   23.08-py3-sdk                        587bf52f933e   4 weeks ago    10.1GB
    nvcr.io/nvidia/tritonserver   23.08-py3                            3e96065a3dcc   4 weeks ago    12.4GB

model_repository

        model_repository
        ├── densenet_onnx
        │   ├── 1
        │   │   └── model.onnx
        │   ├── config.pbtxt
        │   └── densenet_labels.txt
        ├── inception_graphdef
        │   ├── 1
        │   │   └── model.graphdef
        │   ├── config.pbtxt
        │   └── inception_labels.txt
        ├── simple
        │   ├── 1
        │   │   └── model.graphdef
        │   └── config.pbtxt
        ├── simple_dyna_sequence
        │   ├── 1
        │   │   └── model.graphdef
        │   └── config.pbtxt
        ├── simple_identity
        │   ├── 1
        │   │   └── model.savedmodel
        │   │       └── saved_model.pb
        │   └── config.pbtxt
        ├── simple_int8
        │   ├── 1
        │   │   └── model.graphdef
        │   └── config.pbtxt
        ├── simple_sequence
        │   ├── 1
        │   │   └── model.graphdef
        │   └── config.pbtxt
        └── simple_string
            ├── 1
            │   └── model.graphdef
            └── config.pbtxt

# references

[triton-inference-server/user-guide](https://docs.nvidia.com/deeplearning/triton-inference-server/user-guide/docs/getting_started/quickstart.html)

[triton-inference-server](https://github.com/triton-inference-server/server)

[triton-tutorial](https://github.com/triton-inference-server/tutorials)

[Getting Started with NVIDIA Triton Inference Server](https://www.youtube.com/watch?v=NQDtfSi5QF4)
