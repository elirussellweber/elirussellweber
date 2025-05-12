---
layout: post
title:  "Capstone Project: Cloud Robotics"
date:   2025-05-01
categories: jekyll update
---
For our Capstone Computing Project, my team developed software for the [PuppyPi](https://www.hiwonder.com/products/puppypi?srsltid=AfmBOoob_T0YRTQcpE1lJoqemL3ZmjQ1DwDOW8U412TIGdCUq_nBo4oG),
a simple quadruped robot. We set out to support K12 STEM programs, and we achieved this be making the robot voice interactive,
such that one could speak to the robot in natural language and it would respond in real time. 

To do this, we created a cloud architecture, depicted below.  
![Cloud Architecture](/assets/cloud_arch.png)  
After the wake word- Scuffy- is detected by the Picovoice program, audio is recorded until quiet is detected, and then saved into a file and uploaded to AWS lambda. It is then sent through OpenAI Whisper to extract text from the audio file. Once a transcription is created, it is then sent to OpenAI ChatGPT in a custom prompt, in which ChatGPT is asked to select any number of actions based on what the transcription. JSON is then returned from ChatGPT and sent to the PuppyPi. The PuppyPi then translates this JSON into ROS websocket commands using a payload dictionary, which are then sent to the Docker container running the ROS and executed.  

One of the best aspects of using an LLM for interpretation is that is allows users to be inderect, vague, or even misspeak, while still achieving the desired behavior from the PuppyPi. For example, if you wanted the PuppyPi to walk forward, you could say walk forward, move straight, stroll along, or take some steps. Scuffy would walk forward in response to any of these. Likewise, Scuffy responds to any language recognized by Whisper and ChatGPT, making the robot responsive to every widely-spoken language.  

Demo video: 
<iframe width="560" height="315" src="https://www.youtube.com/embed/qUq1ZZ1_EhI?si=5hAZLLw7iD4rQ3--&amp;start=2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

[Github Repository Link](https://github.com/CS-495-Cloud-Robotics-Team/PuppyPi)


