---
title: "H264 Çoklu bit hızı 4 x 3 SD ses 5.1 | Microsoft Docs"
description: "Konuyu genel bir fikir veren ** H264 Çoklu bit hızı 4 x 3 SD ses 5.1* * görev hazır."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: e55dd302-2f42-46b5-ae17-bd3c72329c03
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: c2e1b5a5d246a512a847c0ca2601d685a9aaeb27
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="h264-single-bitrate-4x3-sd-audio-51"></a><span data-ttu-id="39189-103">H264 Çoklu bit hızı 4 x 3 SD ses 5.1</span><span class="sxs-lookup"><span data-stu-id="39189-103">H264 Single Bitrate 4x3 SD Audio 5.1</span></span>
<span data-ttu-id="39189-104">`Media Encoder Standard`kodlama işler oluştururken kullanabileceğiniz hazır kodlama kümesi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="39189-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="39189-105">Kullanabilir bir `preset name` hangi biçimine medya dosyanızın kodlamak istediğiniz belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="39189-105">You can either use a `preset name` to specify into which format you would like to encode your media file.</span></span> <span data-ttu-id="39189-106">Veya, kendi JSON veya XML tabanlı hazır (UTF-8 veya UTF-16 kodlamasını kullanıyor. oluşturabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="39189-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="39189-107">Ardından kodlayıcıya önceden özel geçirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="39189-107">You would then pass the custom preset to the encoder.</span></span> <span data-ttu-id="39189-108">Bu tarafından desteklenen tüm hazır adlarının listesi için `Media Encoder Standard` encoder bkz [Medya Kodlayıcısı standart için görev hazır](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="39189-108">For the list of all the preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="39189-109">Bu konuda gösterilmektedir `H264 Single Bitrate 4x3 SD Audio 5.1` XML ve JSON biçiminde hazır.</span><span class="sxs-lookup"><span data-stu-id="39189-109">This topic shows the `H264 Single Bitrate 4x3 SD Audio 5.1` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="39189-110">Bu önceden ayarlanmış bir bit hızı 1800 kbps ve AAC 5.1 ses ile tek bir MP4 dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="39189-110">This preset produces a single MP4 file with a bitrate of 1800 kbps, and AAC 5.1 audio.</span></span> <span data-ttu-id="39189-111">Profili hakkında ayrıntılı bilgi için örnekleme hızını bu vb. bit hızı, önceden, XML veya JSON aşağıda tanımlanan inceleyin.</span><span class="sxs-lookup"><span data-stu-id="39189-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine the XML or JSON defined below.</span></span> <span data-ttu-id="39189-112">Hangi her öğe anlamına gelir ve geçerli değerlerin her öğe için açıklamalar için bkz [Medya Kodlayıcısı standart şema](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="39189-112">For explanations of what each element means, and the valid values for each element, see the [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>  
  
 <span data-ttu-id="39189-113">XML</span><span class="sxs-lookup"><span data-stu-id="39189-113">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>1800</Bitrate>  
          <Width>640</Width>  
          <Height>480</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>1800</MaxBitrate>  
        </H264Layer>  
      </H264Layers>  
      <Chapters />  
    </H264Video>  
    <AACAudio>  
      <Profile>AACLC</Profile>  
      <Channels>6</Channels>  
      <SamplingRate>48000</SamplingRate>  
      <Bitrate>384</Bitrate>  
    </AACAudio>  
  </Encoding>  
  <Outputs>  
    <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">  
      <MP4Format />  
    </Output>  
  </Outputs>  
</Preset>  
```  
  
 <span data-ttu-id="39189-114">JSON</span><span class="sxs-lookup"><span data-stu-id="39189-114">JSON</span></span>  
  
```  
{  
  "Version": 1.0,  
  "Codecs": [  
    {  
      "KeyFrameInterval": "00:00:02",  
      "SceneChangeDetection": true,  
      "H264Layers": [  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 1800,  
          "MaxBitrate": 1800,  
          "BufferWindow": "00:00:05",  
          "Width": 640,  
          "Height": 480,  
          "BFrames": 3,  
          "ReferenceFrames": 3,  
          "AdaptiveBFrame": true,  
          "Type": "H264Layer",  
          "FrameRate": "0/1"  
        }  
      ],  
      "Type": "H264Video"  
    },  
    {  
      "Profile": "AACLC",  
      "Channels": 6,  
      "SamplingRate": 48000,  
      "Bitrate": 384,  
      "Type": "AACAudio"  
    }  
  ],  
  "Outputs": [  
    {  
      "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",  
      "Format": {  
        "Type": "MP4Format"  
      }  
    }  
  ]  
}  
```
