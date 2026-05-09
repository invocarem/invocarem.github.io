# build pytorch and etc

I have the following env setup (buildenv.sh)
```
export TORCH_CUDA_ARCH_LIST="12.1"
export PATH=/usr/local/cuda/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
export MAX_JOBS=4
export CMAKE_BUILD_PARALLEL_LEVEL=4
```

```
python setup install
```
it finally succeed

```
uv pip list
Using Python 3.12.3 environment at: /home/chenchen/runtime-sglang/.sglang
Package           Version
----------------- -------------------
filelock          3.29.0
fsspec            2026.4.0
jinja2            3.1.6
markupsafe        3.0.3
mpmath            1.3.0
networkx          3.6.1
packaging         26.2
pip               26.1
pyyaml            6.0.3
setuptools        81.0.0
sympy             1.14.0
torch             2.13.0a0+git27b9a62
typing-extensions 4.15.0
(.sglang) chenchen@spark1:~/runtime-sglang/pytorch$ 
```
install sglang core

```

pip install --no-deps -e "python"

# Install runtime dependencies (excluding torch)
pip install --no-deps \
  transformers accelerate sentencepiece protobuf \
  fastapi uvicorn aiohttp requests tiktoken openai \
  jsonschema nvidia-ml-py prometheus-client psutil

```


install 
```
uv pip install numpy pillow
```

## restore
```
cd ~/runtime-sglang/pytorch
uv pip install --force-reinstall --no-deps .
cd ~/runtime-sglang/vision
uv pip install --force-reinstall --no-deps .
cd ~/runtime-sglang/audio
uv pip install --force-reinstall --no-deps .


```