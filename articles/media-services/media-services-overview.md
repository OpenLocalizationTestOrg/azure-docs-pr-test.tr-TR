---
title: "aaaAzure Media Services genel bakış | Microsoft Docs"
description: "Bu konu Azure Media Services’e genel bir bakış sağlar."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7a5e9723-c379-446b-b4d6-d0e41bd7d31f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/04/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 81f9f4d9ff75effea30c10fd09449e9d2025f377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-overview"></a>Azure Media Services’a genel bakış 

Microsoft Azure Media Services, geliştiricilerin, toobuild ölçeklenebilir medya yönetimi ve teslimi uygulamaları sağlayan genişletilebilir bulut tabanlı bir platformdur. Media Services toosecurely karşıya yükleme sağlayan REST API'leri dayanır, depolamak, kodlamak ve video ve ses içeriklerini hem isteğe bağlı ve canlı akış teslimi toovarious istemcileri için (örneğin, TV, PC ve mobil aygıtlar) paketi.

Yalnızca Media Services’i kullanarak uçtan uca iş akışları oluşturabilirsiniz. Ayrıca, iş akışınızın bazı bölümleri için üçüncü taraf bileşenleri toouse da tercih edebilirsiniz. Örneğin, bir üçüncü taraf kodlayıcısı kullanarak kodlayın. Daha sonra Media Services’i kullanarak yükleyin, koruyun, paketleyin ve teslim edin.

İçeriğinizi Canlı toostream seçin veya isteğe bağlı içerik teslim. Merhaba konu aynı zamanda tooother ilgili konulara bağlantılar içerir.

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
AMS öğrenme yollarını burada görebilirsiniz:

* [AMS Canlı Akış İş Akışı](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [AMS İsteğe Bağlı Akış İş Akışı](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a>Ön koşullar

Azure Media Services'i kullanarak toostart hello şunlara sahip olmanız:

* Bir Azure hesabı. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılar için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com).
* Bir Azure Media Services hesabı. Daha fazla bilgi için bkz. [Hesap Oluşturma](media-services-portal-create-account.md).
* (İsteğe bağlı) Geliştirme ortamı ayarlayın. Geliştirme ortamınız için .NET veya REST API’yi seçin. Daha fazla bilgi için bkz. [Ortam Ayarlama](media-services-dotnet-how-to-use.md).

    Ayrıca, nasıl çok bilgi[tooAMS API program aracılığıyla bağlanma](media-services-use-aad-auth-to-access-ams-api.md).
* Standart veya premium akış uç noktası başlatılmış durumda.  Daha fazla bilgi için bkz. [Akış uç noktalarını yönetme](media-services-portal-manage-streaming-endpoints.md)

## <a name="sdks-and-tools"></a>SDK’lar ve araçlar

toobuild Media Services çözümleri kullanabilirsiniz:

* [Media Services REST API'si](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* Merhaba kullanılabilir istemci SDK'ları biri:
    * [.NET için Azure Media Services SDK](https://github.com/Azure/azure-sdk-for-media-services),
    * [Java için Azure SDK](https://github.com/Azure/azure-sdk-for-java),
    * [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),
    * [Node.js için Azure Media Services](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (Bu, Microsoft dışı bir Node.js SDK sürümüdür. Bu topluluk tarafından korunur ve şu anda hello AMS API'lerinin % 100 kapsamını yok).
* Mevcut araçlar:
    * [Azure portal](https://portal.azure.com/)
    * [Azure-Media-Services-Gezgini](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Gezgini (AMSE), Windows için bir Winforms/C# uygulamasıdır)

## <a name="concepts-and-overview"></a>Kavramlar ve genel bakış
Azure Media Services kavramları hakkında bilgi edinmek için bkz. [Kavramlar](media-services-concepts.md).

Bir nasıl-tooall hello ana bileşenlerinin Azure Media Services tanıtan tooseries için bkz: [Azure Media Services adım adım öğreticiler](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series). Bu seri kavramları harika bir genel bakış vardır ve hello AMSE aracını toodemonstrate AMS görevler kullanır. AMSE aracı bir Windows aracıdır. Bu araç, programlama aracılığıyla elde edebileceğiniz ile Merhaba görevlerin çoğunu destekler [.NET için AMS SDK](https://github.com/Azure/azure-sdk-for-media-services), [Java için Azure SDK](https://github.com/Azure/azure-sdk-for-java), veya [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a>Desteklenen senaryolar ve veri merkezleri arasında Media Services kullanılabilirliği

Ayrıntılı bilgi için bkz. [AMS senaryoları ve veri merkezleri arasında özelliklerin ve hizmetlerin kullanılabilirliği](scenarios-and-availability.md).

## <a name="service-level-agreement-sla"></a>Hizmet Düzeyi Sözleşmesi (SLA)

* Media Services Kodlama için, REST API işlemlerinin %99,9 kullanılabilirliğini garanti ediyoruz.
* Akış için, standart veya premium akış uç noktası satın alındığında mevcut medya içeriğinin %99,9 kullanılabilirliği garantisi ile isteklere başarıyla hizmet vereceğiz.
* Canlı kanallar için çalışan harici bağlantı hello süre en az % 99,9 sahip olma olasılığı garanti ediyoruz.
* İçerik koruma için biz biz başarıyla önemli istekleri en az başlangıç saati % 99,9 oranda karşılayacağımızı garanti ediyoruz.
* Dizin Oluşturucu için başarıyla bir kodlamaya ayrılan ile işlenen dizin oluşturucu görevi isteklerine hizmet vereceğiz birim başlangıç saati % 99,9 oranda.

Daha fazla bilgi için bkz. [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/).

Merhaba veri merkezlerinde kullanılabilirliği hakkında daha fazla bilgi için bkz [Avaiability](scenarios-and-availability.md#availability) bölümü.

## <a name="support"></a>Destek

[Azure Desteği](https://azure.microsoft.com/support/options/), Media Services de dahil olmak üzere Azure için destek seçenekleri sağlar.

## <a name="provide-feedback"></a>Geri bildirimde bulunma

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
