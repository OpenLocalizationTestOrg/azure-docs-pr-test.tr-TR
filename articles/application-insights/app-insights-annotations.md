---
title: "Application Insights için aaaRelease ek açıklamalar | Microsoft Docs"
description: "Dağıtım ekleme veya tooyour ölçümleri explorer Application Insights grafiklerde işaretçileri oluşturabilirsiniz."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 23173e33-d4f2-4528-a730-913a8fd5f02e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: e802d22701cb69e96fd1a6b469ea67454195f77a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a>Application ınsights'ta ölçüm grafiklerde ek açıklamaları
Ek açıklamalar [ölçüm Gezgini](app-insights-metrics-explorer.md) grafikleri Göster yeni bir yapı veya diğer önemli olay dağıtıldığı. Uygulamanızın performansı üzerinde hiçbir etkisi değişikliklerinizi verip vermediğini bunlar kolay toosee kolaylaştırır. Merhaba tarafından otomatik olarak oluşturulabilir [Visual Studio Team Services yapı sistem](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs). Ek açıklamalar tooflag tarafından gibi herhangi bir olay oluşturabilirsiniz [Powershell'den oluşturma](#create-annotations-from-powershell).

![Sunucu yanıt süresi ile görünür bağıntı ile ek açıklama örneği](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a>VSTS derleme ile yayın ek açıklama

Yayın ek açıklamaları hello bulut tabanlı derleme özelliğidir ve Visual Studio Team Services hizmeti bırakın. 

### <a name="install-hello-annotations-extension-one-time"></a>Merhaba ek açıklamaları uzantısını (bir kez) yükleyin
toobe mümkün toocreate yayın ek açıklamalar, tooinstall biri gerekir Merhaba Visual Studio Market'te bulunan çok sayıda takım hizmeti uzantıları hello.

1. İçinde tooyour oturum [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) projesi.
2. Visual Studio pazarında [hello yayın ek açıklamaları uzantı alınmaya](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)ve tooyour Team Services hesabı ekleyin.

![AT Team Services web sayfasının açık Market sağ üst. Visual Team Services seçin ve ardından derleme ve sürüm altında daha bkz belirtin.](./media/app-insights-annotations/10.png)

Yalnızca toodo bu kez Visual Studio Team Services hesabınız için gerekir. Yayın ek açıklamaları artık hesabınıza herhangi bir projede için yapılandırılabilir. 

### <a name="configure-release-annotations"></a>Yayın ek açıklamaları yapılandırın

Her VSTS yayın şablonu için tooget ayrı bir API anahtarı gerekir.

1. İçinde toohello oturum [Microsoft Azure portalı](https://portal.azure.com) ve uygulamanızı izler hello Application Insights kaynağı açın. (Veya [şimdi oluşturmak](app-insights-overview.md), henüz yapmadıysanız.)
2. Açık **API erişimini**, **uygulama Öngörüler kimliği**.
   
    ![Portal.Azure.com adresinde Application Insights kaynağınıza açın ve Ayarlar'ı seçin. API erişimini açın. Merhaba uygulama Kimliğini kopyalayın](./media/app-insights-annotations/20.png)

4. Ayrı bir tarayıcı penceresi açın (veya oluşturun) Visual Studio Team Services dağıtımlarınızı yönetir hello yayın şablonu. 
   
    Bir görev ekleyin ve Başlangıç menüsünden hello uygulama Öngörüler yayın ek açıklama görevi seçin.
   
    Yapıştır hello **uygulama kimliği** API erişimini dikey penceresinde hello kopyalanan.
   
    ![Visual Studio Team Services sürüm açın, bir yayın tanımı seçin ve Düzenle'yi seçin. Görev Ekle'yi tıklatın ve uygulama Öngörüler yayın ek açıklama seçin. Merhaba uygulama Öngörüler kimliği yapıştırın](./media/app-insights-annotations/30.png)
4. Set hello **apikey ile yapılan** alanı tooa değişkeninin `$(ApiKey)`.

5. Hello Azure penceresi, geri döndüğünüzde yeni bir API anahtar oluşturun ve bir kopyasını alın.
   
    ![Hello API erişimini dikey penceresinde hello Azure penceresi, API anahtarı oluştur'a tıklayın. Bir açıklama sağlayın, yazma ek açıklamaları denetleyin ve anahtar oluştur'a tıklayın. Merhaba yeni anahtarı kopyalayın.](./media/app-insights-annotations/40.png)

6. Merhaba yapılandırma sekmesi hello yayın şablonu açın.
   
    İçin bir değişken tanımı oluşturun `ApiKey`.
   
    API anahtar toohello apikey ile yapılan değişken tanımını yapıştırın.
   
    ![Merhaba Team Services penceresinde hello yapılandırma sekmesini seçin ve değişken Ekle'yi tıklatın. Merhaba adı tooApiKey ayarlamak ve değer hello, az önce oluşturulan hello anahtarını yapıştırın ve hello kilit simgesini tıklatın.](./media/app-insights-annotations/50.png)
7. Son olarak, **kaydetmek** hello yayın tanımı.


## <a name="view-annotations"></a>Görünüm ek açıklamaları
Şimdi, hello yayın şablonu toodeploy yeni bir sürüm kullandığında açıklamanın tooApplication Öngörüler gönderilir. Merhaba ek açıklamaları ölçüm Gezgini grafiklerinde görüntülenir.

Hello sürüm, istek sahibi, kaynak denetimi dalı, sürüm tanımı, ortam ve daha fazlasını dahil olmak üzere hiçbir ek açıklama işaret tooopen ayrıntılarını tıklayın.

![Tüm yayın ek açıklama işaretçisi'ı tıklatın.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a>Özel ek açıklama Powershell'den oluşturma
(VS Team System kullanmadan) gibi herhangi bir işlem ek açıklamaları da oluşturabilirsiniz. 


1. Merhaba yerel bir kopyasını [Powershell betiği github'dan](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).

2. Merhaba uygulama kimliği alın ve API erişimini dikey penceresinde hello bir API anahtarı oluşturun.

3. Bu gibi Hello betik arayın:

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

Bu, kolay toomodify hello komut dosyası, örneğin toocreate ek açıklamalarını hello geçmiş olur.

## <a name="next-steps"></a>Sonraki adımlar

* [İş öğeleri oluşturma](app-insights-diagnostic-search.md#create-work-item)
* [PowerShell ile Automation](app-insights-powershell.md)
