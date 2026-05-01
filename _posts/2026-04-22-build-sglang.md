## build sglang for dgx spark

1 create vertual environment
```
uv venv .sglang --python 3.12
source .sglang/bin/activate
```

2 install pyTorch (13.0)
```
uv pip install torch==2.9.1 torchvision==0.24.1 torchaudio==2.9.1  --force-reinstall   --index-url https://download.pytorch.org/whl/cu130

```

3 clone sglang
```
git clone https://github.com/sgl-project/sglang.git
cd sglang
uv pip install -e "python"
cd sgl-kernel
```

I have got issue with python.
```
 sudo apt-get update
 sudo apt-get install -y python3.12-dev
```
and another one:
```
 curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
 # select 1 (option)
 source ~/.cargo/env
 cargo --version
 rustc --version
```

fix another error:
```
 sudo apt-get install -y protobuf-compiler
```
use the following command to check sglang
``` 
  uv pip list | grep sglang
``` 
4 install system dependences
```
sudo apt-get install -y libnuma-dev libibverbs-dev
uv pip install build wheel "cmake<4.0" ninja scikit-build-core
```

5 set cud env variable
```
export PATH=/usr/local/cuda/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
```
I make update into ~/.bashrc.


6 build wheel (spark)
```
TORCH_CUDA_ARCH_LIST="12.1a" MAX_JOBS=4 CMAKE_BUILD_PARALLEL_LEVEL=1  python -m build --wheel --no-isolation
```

 sudo apt-get install -y protobuf-compiler

 7 install wheel
 ```
 uv pip install --no-deps dist/sgl_kernel*.whl
 ```

``` 
  uv pip install triton==3.6.0

 python -c "
import torch
print('PyTorch version:', torch.__version__)
print('CUDA archs:', torch.cuda.get_arch_list())
print('CUDA version:', torch.version.cuda)
"
PyTorch version: 2.13.0a0+gitdff4497
CUDA archs: ['sm_121']
CUDA version: 13.0
```
### cmake need to include pytorch

```
export CMAKE_PREFIX_PATH=$(python -c "import torch; print(torch.utils.cmake_prefix_path)")

```