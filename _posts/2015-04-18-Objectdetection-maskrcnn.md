---
layout: post
title:  "Object Detection의 첫걸음 Mask RCNN"
date:   2015-04-18T14:25:52-05:00
author: Dominic
categories: ObjectDetection
tags: objectdetection
---
***개인적인 연구를 정리한 것이며 정확하지 않는 내용을 포함할 수 잇습니다.***


# MASK RNN에 대한 연구

<br>
<br>

![alt text]({{ site.baseurl }}/assets/RCNN.png "Profile Picture")
<br>
굳이 분류를 해보자면 Object Detection 분야는 2가지로 뽑을 수 있다.<br>
<div markdown="1"> 
- **Two Statge Detection** : RCNN(Fast, Faster 포함), SSP-NET 등
- **One Stage Detection** : Yolo, SSD 등
</div>
<br>
Vision 분야는 Inference Time이 핵심이다. 모델의 정확도 외에 Inference Time을 줄이기 위해서 많은 연구가 있었고 
현재 Two Stage 모델들이 사용되지 않는 이유도 이 때문이라고 생각을 한다. 따라서 현재 Detection 분야에서 가장 많이 사용되는
모델은 Yolo라고 할 수 있다.
<br>
<br>
<details>
<summary>개인적인 생각</summary>
<div markdown="1">       
<u>
석사연구원으로 연구를 하면서 모델을 개발하고 모델의 성능을 높이기 위한 연구를 주로 해왔다. 연구원으로 지내며 가장 궁금했던 점은
누군가는 이 모델을 사용해야 할 텐데 Inference Time을 줄이기 위한 연구와 또한 API를 패키징(당시에는 이 말조차도 몰랐다.)을 위한
연구를 나중에 해보고 싶다는 생각을 했었다.
</u>
</div>
</details>
<br>
<br>
Yolo 포스팅은 추후에 할 것이며 Object Detecting을 연구하기 위한 첫 걸음인 **RCNN**에 대해 보고자 한다.
RCNN은 Two stage 모델이며 one stage 와의 차이점은 Resion Proposal 이다.  Resion Proposal을 한 후 이미지를 Crop한 후(first)
이 이미지가 Network의 Input이 되어 Box Regression, Classification이 된다.(Second)
<br>
<br>

## Resion Proposal
<br>
<br>
![alt text]({{ site.baseurl }}/assets/selectsearch.png "Profile Picture")
<br>
<br>

