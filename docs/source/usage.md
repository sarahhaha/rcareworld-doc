## RFUniverse Dependency
We use [RFUniverse](https://wenqiangx.github.io/robotflowproject/project/rfuniverse/) to construct Unity side and to communicate with Python side. 
Since RFUnivese has not been made public, please reach out to Cathy (ry273@cornell.edu) to get code for RFUniverse.

## Experiments
### Train
run `python train.py --algo tqc --env KinovaDressing-v1`
### Test
run `python enjoy.py --algo tqc --env KinovaDressing-v1 -f logs/ -n 1000`
### Record Video
run `python -m utils.record_video --algo tqc --env KinovaDressing-v1 -f logs/ -n 1000`
![image](https://user-images.githubusercontent.com/16759982/173900389-2fb0dafb-ebe6-4aa2-a8a5-56fae09c95b2.png)
