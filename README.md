# aloha-bigym_switch

## aloha-bigym

### install
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



### 
