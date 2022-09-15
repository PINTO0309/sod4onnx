# sod4onnx
**S**imple model **O**utput OP **D**eletion tools for **ONNX**.

https://github.com/PINTO0309/simple-onnx-processing-tools

[![Downloads](https://static.pepy.tech/personalized-badge/sod4onnx?period=total&units=none&left_color=grey&right_color=brightgreen&left_text=Downloads)](https://pepy.tech/project/sod4onnx) ![GitHub](https://img.shields.io/github/license/PINTO0309/sod4onnx?color=2BAF2B) [![PyPI](https://img.shields.io/pypi/v/sod4onnx?color=2BAF2B)](https://pypi.org/project/sod4onnx/) [![CodeQL](https://github.com/PINTO0309/sod4onnx/workflows/CodeQL/badge.svg)](https://github.com/PINTO0309/sod4onnx/actions?query=workflow%3ACodeQL)

<p align="center">
  <img src="https://user-images.githubusercontent.com/33194443/190423861-1de6e4ac-288f-4868-9048-0f2aa74c37fc.png" />
</p>

### 1-1. HostPC
```bash
### option
$ echo export PATH="~/.local/bin:$PATH" >> ~/.bashrc \
&& source ~/.bashrc

### run
$ pip install -U onnx \
&& python3 -m pip install -U onnx_graphsurgeon --index-url https://pypi.ngc.nvidia.com \
&& pip install -U sod4onnx
```
### 1-2. Docker
https://github.com/PINTO0309/simple-onnx-processing-tools#docker

## 2. CLI Usage
```
$ sod4onnx -h

usage:
    sod4onnx [-h]
    -if INPUT_ONNX_FILE_PATH
    -on OUTPUT_OP_NAMES [OUTPUT_OP_NAMES ...]
    -of OUTPUT_ONNX_FILE_PATH
    [-n]

optional arguments:
  -h, --help
        show this help message and exit.

  -if INPUT_ONNX_FILE_PATH, --input_onnx_file_path INPUT_ONNX_FILE_PATH
        Input onnx file path.

  -on OUTPUT_OP_NAMES [OUTPUT_OP_NAMES ...], --output_op_names OUTPUT_OP_NAMES [OUTPUT_OP_NAMES ...]
        Output name to be deleted to the models output OP.
        e.g.
        --output_op_names "output1" "output3"

  -of OUTPUT_ONNX_FILE_PATH, --output_onnx_file_path OUTPUT_ONNX_FILE_PATH
        Output onnx file path.

  -n, --non_verbose
        Do not show all information logs. Only error logs are displayed.
```

## 3. In-script Usage
```python
>>> from sod4onnx import outputs_delete
>>> help(outputs_delete)

Help on function outputs_delete in module sod4onnx.onnx_model_output_deleter:

outputs_delete(
    input_onnx_file_path: Union[str, NoneType] = '',
    onnx_graph: Union[onnx.onnx_ml_pb2.ModelProto, NoneType] = None,
    output_op_names: Union[List[str], NoneType] = [],
    output_onnx_file_path: Union[str, NoneType] = '',
    non_verbose: Union[bool, NoneType] = False
) -> onnx.onnx_ml_pb2.ModelProto

    Parameters
    ----------
    input_onnx_file_path: Optional[str]
        Input onnx file path.
        Either input_onnx_file_path or onnx_graph must be specified.
        Default: ''

    onnx_graph: Optional[onnx.ModelProto]
        onnx.ModelProto.
        Either input_onnx_file_path or onnx_graph must be specified.
        onnx_graph If specified, ignore input_onnx_file_path and process onnx_graph.

    output_op_names: List[str]
        Output name to be deleted to the models output OP.
        e.g.
        output_op_names = ["output1", "output3"]

    output_onnx_file_path: Optional[str]
        Output onnx file path. If not specified, no ONNX file is output.
        Default: ''

    non_verbose: Optional[bool]
        Do not show all information logs. Only error logs are displayed.
        Default: False

    Returns
    -------
    outputops_deleted_graph: onnx.ModelProto
        onnx.ModelProto with output OP deleted
```

## 4. CLI Execution
```bash
$ sod4onnx \
--input_onnx_file_path movenet_multipose_lightning_192x256_nopost.onnx \
--output_op_names "cast1_output" \
--output_onnx_file_path movenet_multipose_lightning_192x256_nopost_tmp.onnx
```

## 5. In-script Execution
```python
from sod4onnx import outputs_delete

onnx_graph = rename(
    input_onnx_file_path="movenet_multipose_lightning_192x256_nopost.onnx",
    output_op_names=["cast1_output"],
    output_onnx_file_path="movenet_multipose_lightning_192x256_nopost_tmp.onnx",
)
```

## 6. Sample
```bash
$ sod4onnx \
--input_onnx_file_path movenet_multipose_lightning_192x256_nopost.onnx \
--output_op_names "cast1_output" \
--output_onnx_file_path movenet_multipose_lightning_192x256_nopost_tmp.onnx
```
### Before
![image](https://user-images.githubusercontent.com/33194443/190411104-6c63a57a-610c-4b25-aa6a-0eafdac3844a.png)

### After
![image](https://user-images.githubusercontent.com/33194443/190411589-42a69dc0-5fba-4c81-afbb-39fd12db935e.png)

## 7. Reference
1. https://github.com/onnx/onnx/blob/main/docs/Operators.md
2. https://docs.nvidia.com/deeplearning/tensorrt/onnx-graphsurgeon/docs/index.html
3. https://github.com/NVIDIA/TensorRT/tree/main/tools/onnx-graphsurgeon
4. https://github.com/PINTO0309/simple-onnx-processing-tools
5. https://github.com/PINTO0309/PINTO_model_zoo

## 8. Issues
https://github.com/PINTO0309/simple-onnx-processing-tools/issues
