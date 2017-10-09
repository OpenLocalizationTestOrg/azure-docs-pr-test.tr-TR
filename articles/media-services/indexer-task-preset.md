---
title: "Azure Media Indexer için önceden aaaTask"
description: "Bu konu Azure Media Indexer için önceden görev genel bir bakış sağlar."
services: media-services
documentationcenter: 
author: Asolanki
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: adsolank;juliako;
ms.openlocfilehash: ca0b3e7aa9f6dd9fdecddfc5b3137281ed5cef35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="task-preset-for-azure-media-indexer"></a>Görev için Azure Media Indexer hazır

Azure Media Indexer olan görevleri aşağıdaki tooperform hello kullandığınız medya işlemcisi: ortam dosyaları ve içerik aranabilir yapmanıza, kapalı açıklamalı alt yazı izler ve anahtar sözcükler oluşturmak, Varlığınızı parçası olan varlık dosyaları dizini.

Bu konu, hello açıklar görev Önayar iş dizin toopass tooyour gerekir. Tam örnek için bkz: [Azure Media Indexer ortam dosyalarıyla dizin](media-services-index-content.md).

## <a name="azure-media-indexer-configuration-xml"></a>Azure Media Indexer yapılandırma XML

Merhaba aşağıdaki tabloda öğeleri ve hello yapılandırma XML öznitelikleri açıklanmaktadır.

|Ad|Gerektirme|Açıklama|
|---|---|---|
|Girdi|TRUE|Varlık dosyaları tooindex istiyor.<br/>Azure Media Indexer ortam dosya biçimleri aşağıdaki hello destekler: MP4, MOV, WMV, MP3, M4A, WMA, AAC, WAV. <br/><br/>Merhaba dosya adı (s) hello belirtebilirsiniz **adı** veya **listesi** hello özniteliği **giriş** (aşağıda gösterildiği gibi) öğesi. Hangi varlık dosyası tooindex belirtmezseniz hello birincil dosya çekilir. Herhangi bir birincil varlık dosyası ayarlarsanız hello ilk hello giriş varlık dosyasında dizine alınır.<br/><br/>tooexplicitly hello varlık dosya adı belirtin, yapın:<br/>```<input name="TestFile.wmv" />```<br/><br/>Ayrıca, birden çok varlık dosyaları aynı anda (too10 dosyaları) dizin oluşturabilirsiniz. toodo bu:<br/>-Bir metin dosyası (bildirim dosyası) oluşturun ve bir .lst uzantısı verin.<br/>-Tüm hello varlık dosya adlarının bir listesini giriş varlık toothis bildirim dosyanıza ekleyin.<br/>-(Karşıya yükleme) thanifest dosya toohello varlık ekleyin.<br/>-Hello giriş'ın liste özniteliğinde hello bildirim dosyası hello adını belirtin.<br/>```<input list="input.lst">```<br/><br/>**Not:** 10'dan fazla dosyaları toohello bildirim dosyası eklerseniz, hello dizin oluşturma işi hello 2006 hata kodu ile başarısız olur.|
|Meta veriler|False|Varlık dosyaları hello için meta verileri belirtilmiş.<br/>```<metadata key="..." value="..." />```<br/><br/>Önceden tanımlanmış anahtarlar için değer sağlayabilir. <br/><br/>Şu anda anahtarları aşağıdaki hello desteklenir:<br/><br/>**Başlık** ve **açıklama** -tooupdate hello dil modeli tooimprove konuşma tanıma doğruluğunu kullanılır.<br/>```<metadata key="title" value="[Title of hello media file]" /><metadata key="description" value="[Description of hello media file]" />```<br/><br/>**Kullanıcı adı** ve **parola** - http veya https üzerinden internet dosyaları yüklerken kimlik doğrulaması için kullanılır.<br/>```<metadata key="username" value="[UserName]" /><metadata key="password" value="[Password]" />```<br/>hello kullanıcı adı ve parola değerlerini tooall medya URL'leri hello giriş bildiriminde uygulayın.|
|SaaS Uygulamaları Geliştirme<br/><br/>Sürüm 1.2 eklendi. Şu anda, konuşma tanıma ("ASR") yalnızca desteklenen hello özelliğidir.|False|Merhaba konuşma tanıma özelliği hello ayarları anahtarları aşağıdaki sahiptir:<br/><br/>Dil:<br/>-hello multimedya dosyasında tanınan doğal dil toobe hello.<br/>-İngilizce, İspanyolca<br/><br/>CaptionFormats:<br/>-hello noktalı virgülle ayrılmış bir listesini istenen çıkış resim yazısı biçimleri (varsa)<br/>-ttml; sami; webvtt<br/><br/><br/>GenerateAIB:<br/>-Bir AIB dosyası (kullanmak için SQL Server ve hello müşteri dizin oluşturucu IFilter ile) gerekli olup olmadığını belirten boolean bir bayrak. Daha fazla bilgi için Azure Media Indexer ve SQL Server ile AIB dosyaları kullanma konusuna bakın.<br/>-True; False<br/><br/>GenerateKeywords:<br/>-Bir anahtar sözcük XML dosyasını gerekli olup olmadığını belirten boolean bir bayrak.<br/>-True; FALSE.|

## <a name="azure-media-indexer-configuration-xml-example"></a>Azure Media Indexer yapılandırma XML örneği

``` 
<?xml version="1.0" encoding="utf-8"?>  
<configuration version="2.0">  
  <input>  
    <metadata key="title" value="[Title of hello media file]" />  
    <metadata key="description" value="[Description of hello media file]" />  
  </input>  
  <settings>  
  </settings>  
  
  <features>  
    <feature name="ASR">    
      <settings>  
        <add key="Language" value="English"/>  
        <add key="CaptionFormats" value="ttml;sami;webvtt"/>  
        <add key="GenerateAIB" value ="true" />  
        <add key="GenerateKeywords" value ="true" />  
      </settings>  
    </feature>  
  </features>  
  
</configuration>  
```
  
## <a name="next-steps"></a>Sonraki adımlar

Bkz: [Azure Media Indexer ortam dosyalarıyla dizin](media-services-index-content.md).

