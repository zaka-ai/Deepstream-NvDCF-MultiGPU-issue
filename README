# NvDCF issue
**•	Hardware Platform (Jetson / GPU)** T4 GPU
**•	DeepStream Version** Deepstream-5.0
**•	NVIDIA GPU Driver Version (valid for GPU only)** 460.32.03

I have multiple GPUs on my instance. I am trying to run the whole pipeline on the GPU-id 1. Everything is working fine, but when I am using the NvDCF tracker I am getting a redundant process on GPU 0 (default GPU according to SDK) that is consuming 0% utilization of GPU 0. However, it is reducing the processing time of the whole video by a significant amount (for 15 videos - each is 10 min - and 3 models, running the whole pipeline on GPU 0 requires 6 min of processing while running it on GPU 1 with this redundant process consuming 0% utilization on GPU 0 the required processing time is around 10 min).

Using KLT or no tracker, this redundant process is absent. This is affecting our scalability a lot. Can you plz follow up with the issue?

*****************************************************************************
* Copyright (c) 2018 NVIDIA Corporation.  All rights reserved.
*
* NVIDIA Corporation and its licensors retain all intellectual property
* and proprietary rights in and to this software, related documentation
* and any modifications thereto.  Any use, reproduction, disclosure or
* distribution of this software and related documentation without an express
* license agreement from NVIDIA Corporation is strictly prohibited.
*****************************************************************************

Prequisites:

Please follow instructions in the apps/sample_apps/deepstream-app/README on how
to install the prequisites for Deepstream SDK, the DeepStream SDK itself and the
apps.

You must have the following development packages installed
   GStreamer-1.0
   GStreamer-1.0 Base Plugins
   GStreamer-1.0 gstrtspserver
   X11 client-side library

To install these packages, execute the following command:
   sudo apt-get install libgstreamer-plugins-base1.0-dev libgstreamer1.0-dev \
   libgstrtspserver-1.0-dev libx11-dev

Compilation Steps:
  $ cd apps/deepstream-test1/
  $ make
  $ ./deepstream-test1-app <h264_elementary_stream>

This document shall describe about the sample deepstream-test1 application.

It is meant for simple demonstration of how to use the various DeepStream SDK
elements in the pipeline and extract meaningful insights from a video stream.

This sample creates instance of "nvinfer" element. Instance of
the "nvinfer" uses TensorRT API to execute inferencing on a model. Using a
correct configuration for a nvinfer element instance is therefore very
important as considerable behaviors of the instance are parameterized
through these configs.

For reference, here are the config files used for this sample :
1. The 4-class detector (referred to as pgie in this sample) uses
    dstest1_pgie_config.txt

In this sample, we first create one instance of "nvinfer", referred as the pgie.
This is our 4 class detector and it detects for "Vehicle , RoadSign, TwoWheeler,
Person".
nvinfer element attach some MetaData to the buffer. By attaching
the probe function at the end of the pipeline, one can extract meaningful
information from this inference. Please refer the "osd_sink_pad_buffer_probe"
function in the sample code. For details on the Metadata format, refer to the
file "gstnvdsmeta.h"

