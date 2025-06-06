# Implementation of CamLoPA
**We have released the next-generation version of this work, which eliminates the need for parameter assumptions in the current localization model and addresses its sensitivity to irregular user movement and varying speeds. Refer to:https://github.com/CamLoPA/DiffLoc**
  **CamLoPA** is a framework for detecting and locating hidden wireless cameras, designed using a Raspberry Pi 4B and based on the analysis of wireless signal propagation paths. This repository contains the implementation code and steps for CamLoPA. Before proceeding, please ensure you have completed the following tasks:

- Install the nexmon-csi tool on your Raspberry Pi 4B. 
- Configure an external network card for wireless communication, to connect with your phone via an SSH tool (since nexmon-csi disables the wireless function, you will need to manually re-enable and configure it). 
- Set up another external network card with monitoring capabilities, ensuring it is set to monitor mode and named wlan2mon before use (the name can be modified in the code).

### Detection and Localization
Run **camscan.py** to automatically perform snooping camera detection and localization. During detection and localization, the user needs to follow the prompts and mimic the demonstration in the demo by walking for a total of 45 seconds.

**location.py** is the localization algorithm. As mentioned in Section VI C, CamLoPA scales the fluctuation durations of CSI for certain paths. For specific scaling parameters, please refer to this document.

Due to the difference in the RSSI values returned by the Raspberry Pi’s network card compared to standard methods, this code includes APs with readings of -39dBm or higher (as reported by the built-in Raspberry Pi network card) in the scanning range.

**Demo of CamLoPA**

Here is a demo video about CamLoPA: see CamLoPAdemo.mp4
[![Introduction Video](CamLoPAdemo.mp4)

Thanks for [nexmon_csi](https://github.com/seemoo-lab/nexmon_csi) and [CSIKit](https://github.com/Gi-z/CSIKit)

**Note**

The 360 camera can, in fact, be detected. In our paper, it was undetectable due to limitations of the external USB sniffer used. We recommend using the TX-N600, which is capable of capturing packets from the 360 camera. Different types of USB WiFi NICs may fail to capture packets from certain camera models; however, switching to a different USB NIC can often resolve this issue. We are currently exploring the use of the Raspberry Pi’s built-in WiFi module as a potential solution. When detecting suspicious devices, it’s best to stay indoors and perform large movements to stimulate camera traffic. For camera detection, begin with active large movements inside the room, then leave the room during the second half of the detection process.

Our experiments were conducted using 2.4GHz WiFi. If using 5GHz WiFi, please adjust the relevant parameters accordingly—for example, change `'--bandwidth', '20'` to `'--bandwidth', '40'` in the location settings.

### Citation
@inproceedings{zhang2025camlopa,
author={Zhang, Xiang and Zhang, Jie and Ma, Zehua and Huang, Jinyang and Li, Meng and Yan, Huan and Zhao, Peng and Zhang, Zijian and Liu, Bin and Guo, Qing and Zhang, Tianwei and Yu, NengHai },
booktitle = { 2025 IEEE Symposium on Security and Privacy (SP) },
title = {CamLoPA: A Hidden Wireless Camera Localization Framework via Signal Propagation Path Analysis },
year = {2025},
volume = {},
ISSN = {2375-1207},
pages = {3653-3671},
address = {Los Alamitos, CA, USA},
month =May}
