# build pytorch

```
git clone --recursive https://github.com/pytorch/pytorch
cd pytorch
export TORCH_CUDA_ARCH_LIST="12.1"
python setup.py install # I am having issue with it

uv pip install -e . -v --no-build-isolation
```

# aftermath

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
