---
title: "aaaManage Azure Media Services Azure CDN önbelleğe alma ilke | Microsoft Docs"
description: "Bilgi nasıl toomanage Azure Media Services Azure CDN önbellek ilkesi."
services: media-services,cdn
documentationcenter: .NET
author: juliako
manager: erikre
editor: 
ms.assetid: be33aecc-6dbe-43d7-a056-10ba911e0e94
ms.service: media-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/04/2017
ms.author: juliako
ms.openlocfilehash: 4c7ee2922fcbb5727e10fbe44fc6e61b79f6917c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-cdn-caching-policy-in-azure-media-services"></a>Azure Media Services ilkesinde önbelleğe alma Azure CDN yönetme
Azure Media Services, Uyarlamalı akış ve aşamalı indirme HTTP tabanlı sağlar. Akışa göre HTTP proxy ve CDN Katmanlar yanı sıra istemci tarafında önbelleğe alma önbelleğe alma avantajları ile yüksek düzeyde ölçeklenebilirdir. Akış uç noktaları genel akış özellikleri ve ayrıca HTTP önbellek üstbilgileri yapılandırmasını sağlar. Akış uç noktaları ayarlar HTTP Cache-Control: Maksimum yaş ve Expires üstbilgileri. Daha fazla bilgi için HTTP önbellek üstbilgileri almak [W3.org](http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html).

## <a name="default-caching-headers"></a>Varsayılan önbelleğe alma üstbilgileri
Varsayılan akış uç noktaları 3 gün önbellek üstbilgileri isteğe bağlı Akış verilerini (gerçek medya parçasının/öbekleri) ve manifest(playlist) için geçerlidir. Canlı akış, akış uç noktalarını 3 gün önbellek üstbilgileri verileri (gerçek medya parçasının/öbekleri) için geçerlidir ve 2 saniye başlığı manifest(playlist) istekleri için önbelleğe al. Canlı program tooon isteğe bağlı (dinamik arşivi) döndüğünde isteğe bağlı Akış önbellek üstbilgileri uygulayın.

## <a name="azure-cdn-integration"></a>Azure CDN tümleştirme
Azure Media Services sağlar [CDN tümleşik](https://azure.microsoft.com/updates/azure-media-services-now-fully-integrated-with-azure-cdn/) akış uç noktaları için. Cache-control üstbilgileri geçerlidir hello aynı şekilde akış uç noktaları tooCDN akış uç noktalarını etkin olarak. Dahili olarak yapılandırılan uç noktası önbellek değerleri toodefine hello yaşam süresini hello akış azure CDN kullanan nesneleri önbelleğe ve ayrıca bu değeri tooset hello teslim önbellek üstbilgileri kullanır. CDN kullanarak akış uç noktalarını etkinleştirildiğinde tooset küçük önbellek değerlerini önerilmez. Küçük değerleri ayarlama hello performansını düşürebilir ve CDN hello yararı azaltın. Akış uç noktalarını tooset önbellek üstbilgileri CDN 600 saniye daha küçük etkin verilmez.

> [!IMPORTANT]
>Azure Media Services, Azure CDN ile tam tümleştirme vardır. Tek bir tıklatmayla akış uç noktası CDN standart ve Premium ürünler dahil olmak üzere tüm hello kullanılabilir Azure CDN sağlayıcıları (Akamai ve Verizon) tooyour tümleştirebilirsiniz. Daha fazla bilgi için bkz [duyuru](https://azure.microsoft.com/blog/standardstreamingendpoint/).
> 
> Uç nokta tooCDN akış gelen veri ücretlerini yalnızca devre dışı hello CDN akış uç noktası API'leri veya Azure Yönetim Portalı'nın akış uç noktası bölümünü kullanarak üzerinden etkinleştirilirse. El ile tümleştirme veya doğrudan CDN API'leri veya portal bölüm kullanarak bir CDN uç noktası oluşturma hello veri ücretlerini devre dışı değil.

## <a name="configuring-cache-headers-with-azure-media-services"></a>Önbellek üstbilgileri Azure Media Services ile yapılandırma
Azure Yönetim Portalı veya Azure Media Services API'leri tooconfigure önbellek üstbilgi değerleri kullanabilirsiniz.

1. Yönetimi'ni kullanarak tooconfigure önbellek üstbilgileri portal başvurun çok[nasıl tooManage akış uç noktaları](../media-services/media-services-portal-manage-streaming-endpoints.md) bölüm yapılandırma hello akış uç noktası.
2. Azure Media Services REST API [StreamingEndpoint](https://msdn.microsoft.com/library/azure/dn783468.aspx#StreamingEndpointCacheControl).
3. Azure Media Services .NET SDK'sı [StreamingEndpointCacheControl özellikleri](http://go.microsoft.com/fwlink/?LinkId=615302).

## <a name="cache-configuration-precedence-order"></a>Önbellek yapılandırma öncelik sırası
1. Azure Media Services yapılandırılmış önbellek değeri varsayılan değerini geçersiz kılar.
2. El ile yapılandırma yoksa, varsayılan değerler geçerlidir.
3. Varsayılan olarak 2 önbellek üstbilgileri geçerlidir toolive manifest(playlist) Azure medya veya Azure depolama yapılandırması bakılmaksızın akış ve bu değeri geçersiz kılma saniye kullanılabilir değil.

