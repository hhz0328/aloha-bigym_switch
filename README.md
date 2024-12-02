# aloha-bigym_switch

## 1.aloha-bigym
### 1.0 运行
```
cd /home/hhz/UCAS/2025/aloha-bigym

conda activate aloha-bigym
source .venv/bin/activate
```

### 1.1 install
```
git clone https://github.com/AlmondGod/aloha-bigym.git
cd aloha-bigym

conda create --name aloha-bigym python=3.12
conda activate aloha-bigym
python3.12 -m venv .venv
source .venv/bin/activate
pip install .
git submodule update --init --recursive   
```
#### error1
- If you encounter this error: `ImportError: cannot import name 'MujocoElement' from 'mojo.elements'`, add this line: 
`from mojo.elements.element import MujocoElement` 
to `.venv/lib/python3.12/site-packages/gymnasium/envs/mujoco/mujoco_rendering.py`
#### error2
If this error is encountered: 

```
from mojo.elements import Body, Site, MujocoElement
ImportError: cannot import name 'MujocoElement' from 'mojo.elements'
```

Add this line to `site-packages/mojo/elements/__init__.py` in your python directory:

`from mojo.elements.element import MujocoElement`



### 1.2 复现过程
#### 1.2.1 switch手柄：https://github.com/tocoteron/joycon-python
```
pip install joycon-python hidapi pyglm
pip install hid
```

#### 1.2.2 本地文件没找到，导致无法import
把`from reduced_configuration import ReducedConfiguration`

改成`from .reduced_configuration import ReducedConfiguration
`
```
reduced_configuration.py 文件和 teleop_aloha.py 文件在同一目录下，可以直接使用相对导入
├── control/
    ├── teleop_aloha.py
    ├── reduced_configuration.py
    └── loop_rate_limiters.py
```
改成`from ..reduced_configuration import ReducedConfiguration`
```
在 prevs 目录下的脚本（例如 joycon_aloha.py）中，可以使用相对导入来导入 reduced_configuration.py 文件
├── control/
    ├── prevs/
    │   ├── __init__.py
    │   ├── joycon_aloha.py
    │   └── other_files.py
    ├── reduced_configuration.py
    └── teleop_aloha.py
```
#### 1.2.3 少python包
```
pip install loop_rate_limiters
pip install mink
pip install pynput
pip install h5py
```
#### error1
`ImportError: Unable to load any of the following libraries:libhidapi-hidraw.so libhidapi-hidraw.so.0 libhidapi-libusb.so libhidapi-libusb.so.0 libhidapi-iohidmanager.so libhidapi-iohidmanager.so.0 libhidapi.dylib hidapi.dll libhidapi-0.dll`

在 Ubuntu 系统中，您可以通过安装系统的 hidapi 库来解决这个问题。运行以下命令来安装相关依赖：
```
sudo apt-get install libhidapi-dev
```
#### error2
`hid.HIDException: unable to open device`

参考链接：https://bbs.archlinux.org/viewtopic.php?id=278341
```
sudo mkdir -p /etc/udev/rules.d/

echo 'KERNEL=="hidraw*", SUBSYSTEM=="hidraw", MODE="0666", TAG+="uaccess", TAG+="udev-acl"' | sudo tee /etc/udev/rules.d/92-viia.rules

sudo udevadm control --reload-rules

sudo udevadm trigger
```

## 2.bigym

### 2.1 install
```
git clone https://github.com/chernyadev/bigym.git
cd bigym

conda create --name bigym python=3.11
conda activate bigym
pip install .
```
