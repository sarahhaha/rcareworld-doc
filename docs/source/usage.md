# RFUniverse Dependency
We use [RFUniverse](https://wenqiangx.github.io/robotflowproject/project/rfuniverse/) to construct Unity side and to communicate with Python side. 
Since RFUnivese has not been made public, please reach out to Cathy (ry273@cornell.edu) to get full Unity code for RFUniverse.

# Quick Start Guide
Download Unity exectuable file [Windows] [Ubuntu]

Install pyrfuniverse module. 
```
cd pyrfuniverse
conda create -n rcare python=3.8
conda activate rcare
pip install -r requirements.txt
pip install -e .
```
Use the editor

For Windows, `./Player.exe -edit`. For Ubuntu, `./Player.x86_64 -edit`
