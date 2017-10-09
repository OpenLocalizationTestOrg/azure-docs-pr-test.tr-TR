---
title: "Yeni bir Azure Application Insights kaynağı aaaCreate | Microsoft Docs"
description: "El ile yeni dinamik bir uygulama için Application Insights izleme işlevini ayarlama."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 878b007e-161c-4e36-8ab2-3d7047d8a92d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: bwren
ms.openlocfilehash: 3aba7045e1f8fe43d473f0be01dd52106ab992a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-insights-resource"></a>Application Insights kaynağı oluşturma
Azure Application Insights, Microsoft Azure'da uygulamanızı hakkındaki verileri görüntüler *kaynak*. Yeni kaynak oluşturma parçasıdır bu nedenle [Application Insights toomonitor yeni bir uygulama ayarı][start]. Çoğu durumda, kaynak oluştururken otomatik olarak IDE hello tarafından yapılabilir. Ancak bazı durumlarda, bir kaynak el ile oluşturmanız - Örneğin, geliştirme ve üretim için ayrı kaynaklar toohave uygulamanızın veya oluşturur.

Merhaba kaynak oluşturduktan sonra kendi izleme anahtarı edinme ve Merhaba uygulaması bu tooconfigure hello SDK kullanın. Merhaba kaynak anahtar bağlantıları telemetri toohello kaynak hello.

## <a name="sign-up-toomicrosoft-azure"></a>Azure tooMicrosoft oturum
Henüz geldiyseniz bir [Microsoft hesabı, hemen edinin](http://live.com). (Outlook.com, OneDrive, Windows Phone veya XBox LIVE gibi hizmetleri kullanıyorsanız, zaten bir Microsoft hesabınız vardır.)

Bir abonelik çok etmeniz[Microsoft Azure](http://azure.com). Ekibinizin ve kuruluşunuzun bir Azure aboneliğiniz varsa, hello sahibi, tooit, Windows Live ID'nizi kullanarak ekleyebilirsiniz Yalnızca, kullanım için ücret ödersiniz. Merhaba varsayılan temel plan, belirli bir miktar ücretsiz Deneysel kullanım için sağlar.

TooApplication bilgiler erişim tooa abonelik var olduğunda oturum [http://portal.azure.com](https://portal.azure.com)ve Live ID toologin kullanın.

## <a name="create-an-application-insights-resource"></a>Application Insights kaynağı oluşturma
Merhaba, [portal.azure.com](https://portal.azure.com), Application Insights kaynağı ekleyin:

![Yeni, Application Insights öğesine tıklayın](./media/app-insights-create-new-resource/01-new.png)

* **Uygulama türü** hello genel bakış dikey penceresinde ve hello özellikler kullanılabilir Görünenleri etkiler [ölçüm Gezgini][metrics]. Uygulama, türünü görmüyorsanız, genel seçin.
* **Abonelik** ödeme hesabınız azure'da.
* **Kaynak grubu** özelliklerini yönetmek için kullanışlı olan erişim denetimi ister. Diğer Azure kaynaklarına zaten oluşturduysanız, tooput bu yeni kaynak hello seçebilirsiniz aynı grubu.
* **Konum** burada biz verilerinizi tutmak olduğu.
* **PIN toodashboard** kaynağınız için hızlı erişim kutucuğu, Azure giriş sayfasında koyar. Önerilir.

Uygulamanızı oluştururken yeni bir dikey pencere açılır. Bu dikey pencere, performans ve kullanım verileri uygulamanız hakkında gördüğünüz ' dir. 

tooget geri tooit tooAzure içinde oturum hello uygulamanızın hızlı başlangıç kutucuğu arayın başlatıldığında Panosu (giriş ekranı). Veya Gözat toofind'ı tıklatın.

## <a name="copy-hello-instrumentation-key"></a>Merhaba izleme anahtarını kopyalama
Merhaba izleme anahtarı oluşturduğunuz hello kaynak tanımlar. Bu toogive toohello SDK gerekir.

![Essentials'ı tıklatın, hello izleme anahtarı, CTRL + C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-hello-sdk-in-your-app"></a>Uygulamanızda Hello SDK yükleme
Merhaba Application Insights SDK'sı, uygulamanızın yükleyin. Bu adım, son derece uygulamanızın hello türüne bağlıdır. 

Merhaba araçları anahtar tooconfigure kullanmak [uygulamanızda yüklediğiniz SDK hello][start].

Merhaba SDK telemetri toowrite kalmadan herhangi bir kod Gönder Standart modüller içerir. tootrack kullanıcı eylemleri veya daha fazla ayrıntı sorunları tanılamak [hello API kullanan] [ api] toosend kendi telemetrinizi.

## <a name="monitor"></a>Telemetri verileri bakın
Kapat hello hızlı hello Azure portal dikey penceresinde tooreturn tooyour uygulama Dikey başlatın.

Merhaba arama döşeme toosee tıklatın [tanılama arama][diagnostic], burada hello ilk olaylar görünür. 

Daha fazla veri bekliyorsunuz tıklatmak **yenileme** birkaç saniye sonra.

## <a name="creating-a-resource-automatically"></a>Bir kaynak otomatik olarak oluşturma
Yazma bir [PowerShell Betiği](app-insights-powershell.md) toocreate kaynak otomatik olarak.

## <a name="next-steps"></a>Sonraki adımlar
* [Pano oluşturma](app-insights-dashboards.md)
* [Tanılama Araması](app-insights-diagnostic-search.md)
* [Ölçümleri keşfetme](app-insights-metrics-explorer.md)
* [Analytics sorguları yazma](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

