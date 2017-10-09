---
title: "Uygulama hizmeti ortamları için aaaCustom ayarları"
description: "Uygulama hizmeti ortamları için özel yapılandırma ayarları"
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 1d1d85f3-6cc6-4d57-ae1a-5b37c642d812
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: stefsch
ms.openlocfilehash: 3d140688c88b389e71bfdd465c418339cccab3a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a>Uygulama hizmeti ortamları için özel yapılandırma ayarları
## <a name="overview"></a>Genel Bakış
Uygulama hizmeti ortamları yalıtılmış tooa tek müşteri olduğundan var. özel olarak tooApp hizmeti ortamları olabilir yapılandırma ayarları uygulanan belirli Bu makale belgeleri App Service ortamları için kullanılabilen çeşitli belirli özelleştirmelere hello.

Bir uygulama hizmeti ortamı yoksa bkz [nasıl tooCreate bir uygulama hizmeti ortamı](app-service-web-how-to-create-an-app-service-environment.md).

Bir dizi hello yeni kullanarak uygulama hizmeti ortamı özelleştirmeleri depolayabilir **clusterSettings** özniteliği. Bu öznitelik hello "Özellikler" sözlüğü hello içinde bulunan *hostingEnvironments* Azure Resource Manager varlığı.

Merhaba aşağıdaki kısaltılmış Resource Manager şablonu parçacığını gösterir hello **clusterSettings** özniteliği:

    "resources": [
    {
       "apiVersion": "2015-08-01",
       "type": "Microsoft.Web/hostingEnvironments",
       "name": ...,
       "location": ...,
       "properties": {
          "clusterSettings": [
             {
                 "name": "nameOfCustomSetting",
                 "value": "valueOfCustomSetting"
             }
          ],
          "workerPools": [ ...],
          etc...
       }
    }

Merhaba **clusterSettings** özniteliği bir Resource Manager şablonu tooupdate hello uygulama hizmeti ortamı dahil edilebilir.

## <a name="use-azure-resource-explorer-tooupdate-an-app-service-environment"></a>Azure kaynak Gezgini tooupdate bir uygulama hizmeti ortamı kullanın
Alternatif olarak, hello uygulama hizmeti ortamı kullanarak güncelleştirebileceğinizi [Azure kaynak Gezgini](https://resources.azure.com).  

1. Kaynak Gezgini'nde hello uygulama hizmeti ortamı için toohello düğümüne gidin (**abonelikleri** > **resourceGroups** > **sağlayıcıları**  >  **Microsoft.Web** > **hostingEnvironments**). Merhaba tooupdate istediğiniz belirli uygulama hizmeti ortamı'ye tıklayın.
2. Merhaba sağ bölmede **okuma/yazma** hello üst araç tooallow kaynak Gezgini'nde düzenleme etkileşimli olarak.  
3. Merhaba mavi tıklatın **Düzenle** düğmesini toomake hello Resource Manager şablonu düzenlenebilir.
4. Toohello bölmesinin hello sağa kaydırın. Merhaba **clusterSettings** buradan girin veya değerini güncelleştirme hello çok altındaki bir özniteliktir.
5. Hello istediğiniz yapılandırma değerlerini yazın (veya Kopyala ve Yapıştır) hello dizisi **clusterSettings** özniteliği.  
6. Hello yeşil tıklatın **PUT** , düğme hello sağ bölmede toocommit hello değişiklik toohello uygulama hizmeti ortamı hello üstünde bulunan.

Merhaba değişiklik Gönder ancak hello değişikliğin tootake Merhaba uygulama hizmeti ortamı'nda ön uçlar hello sayısı ile çarpılır yaklaşık 30 dakika sürer.
Örneğin, bir uygulama hizmeti ortamı dört ön uçlar varsa, kabaca hello yapılandırmasını güncelleştirme toofinish için iki saat sürer. Merhaba yapılandırma değişikliği alınıyor sırada başka bir ölçeklendirme işlemleri veya yapılandırma değişiklik işlemleri hello uygulama hizmeti ortamı yerinde alabilir.

## <a name="disable-tls-10"></a>TLS 1.0 devre dışı bırak
Yinelenen bir soru müşterilerden özellikle PCI uyumluluğunu ile ilgilenen müşteriler denetimleri, nasıl tooexplicitly devre dışı TLS 1.0 için uygulamalarını.

TLS 1.0 devre dışı bırakılabilir hello aşağıdaki aracılığıyla **clusterSettings** girişi:

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a>Değişiklik TLS şifre paketi sırası
Başka bir soru müşterilerden kendi sunucu tarafından anlaşılan şifrelemeleri hello listesi değiştirebilirsiniz ve bu hello değiştirerek elde olan **clusterSettings** aşağıda gösterildiği gibi. Şifre paketleri kullanılabilir Hello listesi alınabileceği [bu MSDN makalesine](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> SChannel anlayamıyor hello şifre paketi için yanlış değerleri ayarlarsanız, tüm TLS iletişim tooyour server çalışmasını durdurabilir. Böyle bir durumda tooremove hello gerekir *FrontEndSSLCipherSuiteOrder* girdisinden **clusterSettings** ve hello güncelleştirilmiş Resource Manager şablonu toorevert geri toohello varsayılan şifre gönderin Suite ayarları.  Lütfen bu işlevi dikkatli kullanın.
> 
> 

## <a name="get-started"></a>başlarken
Hello Azure hızlı başlangıç Resource Manager şablonu sitesi içeren hello temel tanımı için bir şablonla [bir uygulama hizmeti ortamı oluşturma](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).

<!-- LINKS -->

<!-- IMAGES -->
