---
title: "aaaLicensing Microsoft® kesintisiz akış istemci bağlantı noktası oluşturma Seti"
description: "Nasıl toolicensing hello hakkında Microsoft® kesintisiz akış istemci bağlantı noktası oluşturma Seti öğrenin."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: e3b488e7-8428-4c10-a072-eb3af46c82ad
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: xpouyat
ms.openlocfilehash: 56c3dccda73dd02207bb4dbe8109ba6fda917a6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a>Kit taşıma lisanslama Microsoft® kesintisiz akış istemcisi
## <a name="overview"></a>Genel Bakış
Microsoft kesintisiz akış istemci bağlantı noktası oluşturma Seti (**SSPK** kısaca) en iyi duruma getirilmiş toohelp katıştırılmış cihaz üreticisinin, kablo ve mobil işleçleri, içerik hizmet sağlayıcıları, ahize kesintisiz akış bir istemci uygulaması Üreticiler, bağımsız yazılım satıcılarının (ISV'ler) ve çözüm sağlayıcıları toocreate ürünleri ve kesintisiz akış biçiminde Uyarlamalı akış içeriği akışla Hizmetleri. SSPK bir cihaz ve platform bağımsız hello edinmediyseniz tooany cihaz ve platform tarafından bağlantı noktalı kesintisiz akış istemci uygulamasıdır. 

Aşağıda yüksek düzey bir mimari ve IIS kesintisiz akış bağlantı noktası oluşturma Seti kutusunu Microsoft tarafından sağlanan hello Smooth Streaming Client uygulamasıdır ve kesintisiz akış içeriği kayıttan yürütmeyi için tüm hello çekirdek mantığını içerir. Bundan sonra belirli bir aygıt veya platformu için iş ortakları tarafından uygun arabirimleri uygulayarak verilen. 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a>Açıklama
SSPK mükemmel iş değerini sunan koşullarınızda lisanslıdır. SSPK lisans ile Merhaba endüstri sağlar:

* C++'ta kesintisiz akış bağlantı noktası oluşturma Seti kaynak 
  * Smooth Streaming Client işlevselliğini hayata Geçiren
  * ayrıştırma, arabelleğe alma mantığı, vb. buluşsal yöntemler, biçimi ekler.
* Oynatıcı uygulaması API'leri 
  * medya oynatıcı uygulaması ile etkileşim için programlama arabirimleri
* Platform Soyutlama Katmanı (PAL) arabirimi 
  * Merhaba işletim sistemi (iş parçacıkları, yuva) ile etkileşim için programlama arabirimleri
* Donanım özet düzeyi (HAL) arabirimi 
  * programlama arabirimleri donanım A ile etkileşim için / (kod çözme, işleme) V kod çözücüleri
* Dijital Hak Yönetimi (DRM) arabirimi 
  * DRM hello DRM özet düzeyi (DAL) işlemek için programlama arabirimleri
  * Microsoft PlayReady bağlantı noktası oluşturma Seti ayrı olarak gelir ancak bu arabirimi aracılığıyla tümleştirir. Microsoft PlayReady Device lisanslama hakkında daha fazla ayrıntı için tıklatın [burada](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).
* Uygulama örnekleri 
  * Linux için örnek PAL uygulama
  * Örnek HAL uygulama GStreamer için

## <a name="licensing-options"></a>Lisanslama Seçenekleri
Microsoft kesintisiz akış istemci bağlantı noktası oluşturma Seti altında iki ayrı lisans sözleşmelerini kullanılabilir toolicensees yapılır: bir kesintisiz akış istemci geçici ürünleri ve kesintisiz akış istemci son ürünler tooend kullanıcılara dağıtmak için başka bir geliştirmek için.

* Yonga kümesi üreticileri, sistem tümleştiricileri veya bağımsız yazılım satıcıları (ISV) bir kaynak kod bağlantı noktası oluşturma gereksinim duyan toodevelop geçici ürünler, bir Microsoft kesintisiz akış istemci bağlantı noktası oluşturma Seti Seti **geçici Ürün lisans** yürütülmelidir.
* Cihaz üreticileri veya kesintisiz akış istemci son ürünler tooend kullanıcılar için dağıtım hakları gerektiren ISV'ler hello için Microsoft kesintisiz akış istemci bağlantı noktası oluşturma Seti **son ürün lisans** yürütülmelidir.

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a>Microsoft Smooth Streaming Client Seti geçici Ürün lisans bağlantı noktası oluşturma
Bu lisansı altında Microsoft bir kesintisiz akış istemci bağlantı noktası oluşturma Seti sunar ve gerekli fikri mülkiyet hakları toodevelop hello ve kesintisiz akış istemci geçici ürünleri tooother kesintisiz akış istemci bağlantı noktası oluşturma Seti aygıt lisans sahipleri dağıtmak, Kesintisiz akış istemci son ürünler dağıtın.

#### <a name="fee-structure"></a>Ücret yapısı
ABD 50.000 tek seferlik lisans ücret erişim toohello kesintisiz akış istemci bağlantı noktası oluşturma Seti sağlar. 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a>Microsoft Smooth Streaming Client Seti son ürün lisans bağlantı noktası oluşturma
Bu lisansı altında diğer kesintisiz akış istemci bağlantı noktası oluşturma Seti lisans sahipleri ve şirket markalı-kesintisiz akış istemci son toodistribute tüm gerekli fikri mülkiyet hakları tooreceive kesintisiz akış istemci geçici ürünleri Microsoft yapılandırmayı sunar. Ürünleri tooend kullanıcılar.

#### <a name="fee-structure"></a>Ücret yapısı
Merhaba kesintisiz akış istemci son ürün altında lisanslı model olarak altında sunulur:

* cihaz uygulaması başına 0,10 sevk
* Merhaba lisanslı 50.000 her yıl tutulabilir
* İlk 10.000 cihaz uygulamaları her yıl için hiçbir lisanslı 

## <a name="licensing-procedure-and-sspk-access"></a>Lisans yordamı ve SSPK erişim
Lütfen e-posta [ sspkinfo@microsoft.com ](mailto:sspkinfo@microsoft.com) tüm lisans sorgular.

Merhaba [SSPK dağıtım portal](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) geçici lisans sahipleri için erişilebilir tooregistered değil.

Lisans sahipleri için geçici ve son SSPK gönderebilir teknik sorular çok[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a>Microsoft istemci geçici ürün sözleşmesi lisans sahipleri akış kesintisiz
* Adroit işletme çözümleri, Inc
* Gelişmiş dijital yayın SA'sı
* AirTies Kablosuz Iletism Sanayive Dış Ticaret A.S.
* Albis teknolojileri Ltd.
* Alticast Corporation
* Amazon dijital Hizmetleri, Inc.
* Arion Technology, Inc.
* AVC multimedya yazılım Co., Ltd.
* Cavium, Inc.
* EchoStar Corporation'ın satın alma
* Enseo, Inc.
* Fluendo Güney Amerika
* HANDAN BroadInfoCom Co., Ltd.
* Infomir GMBH
* Irdeto ABD Inc.
* iWEDIA Güney Amerika 
* Serbest genel Hizmetleri BV
* MediaTek Inc.
* MStar Co, Ltd
* Nintendo Co., Ltd.
* OpenTV, Inc.
* Saffron dijital sınırlı
* Sichuan Changhong elektrik Co., Ltd
* SoftAtHome
* Sony Corporation
* Tatung Technology Inc.
* TCL Technoly elektronik bileşenleri (Huizhou) Co., Ltd.
* Üst sırrı Yatırımlar, Ltd
* Vestel Elektronik Sanayi ullanıcı Ticaret A.S.
* VisualOn, Inc.
* ZTE Corporation

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a>Microsoft istemci son ürün sözleşmesi lisans sahipleri akış kesintisiz
* Gelişmiş dijital yayın SA'sı
* AirTies Kablosuz Iletism Sanayive Dış Ticaret A.S.
* Albis teknolojileri Ltd.
* Amazon dijital Hizmetleri, Inc.
* AmTRAN teknoloji Co., Ltd.
* Arcadyan teknoloji Corporation
* Arion Technology, Inc.
* ATMACA ELEKTRONİK SAN. HEDEFTEKİ TİC. A.Ş
* İngiliz Sky yayın sınırlı
* CastPal Technology Inc. Shenzhen
* Compal Electronics, Inc.
* Dongguan dijital AV teknolojisi Corp., Ltd
* EchoStar Corporation'ın satın alma
* Enseo, Inc.
* Filmflex filmler sınırlı
* Fluendo Güney Amerika
* Gibson yenilikleri sınırlı
* Haier bilgi Applicantion S.R.L
* HANDAN BroadInfoCom Co., Ltd.
* Hisense uluslararası Co., Ltd. 
* Homecast Co., Ltd
* Hon Hai duyarlık endüstri Co., Ltd.
* Infomir GMBH
* Kaonmedia Co., Ltd.
* KDDI Corporation
* Nintendo Co., Ltd.
* Turuncu SA'sı
* Saffron dijital sınırlı
* Sagemcom geniş bant SAS
* Shenzhen Coship Electronics CO., LTD
* Shenzhen Jiuzhou elektrik Co., Ltd
* Shenzhen Skyworth dijital teknoloji Co., Ltd
* Sichuan Changhong elektrik Co., Ltd.
* Skardin endüstriyel Corp.
* Deutschland Fernsehen GmbH & Co. KG sky
* SmarDTV Güney Amerika
* SoftAtHome
* Sony Corporation
* TCL deniz aşırı pazarlama (Offshore Makao ticari) sınırlı
* Technicolor teslim teknolojileri, SAS
* Tongfang genel Ltd.
* Üst sırrı Yatırımlar, Ltd
* Toshiba Lifestyle ürünler ve hizmetler Corporation
* Evrensel medya Corporation /Slovakia/ s.r.o.
* VIZIO, Inc.
* Wistron Corporation
* ZTE Corporation


## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

