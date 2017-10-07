---
title: "aaaSetting adlı kimlik doğrulama kimlik bilgilerini ayarlama | Microsoft Docs"
description: "Visual Studio tooauthenticate istekleri tooAzure toopublish Visual Studio veya toomonitor var olan bir uygulama tooAzure kullanabileceğiniz tootooprovide kimlik bilgileri bulut hizmeti nasıl bilgi edinin... "
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 61570907-42a1-40e8-bcd6-952b21a55786
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/22/2017
ms.author: kraigb
ms.openlocfilehash: 3cc147a2f7a3e766293ca282f56078cf24281346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-named-authentication-credentials"></a>Adlandırılmış kimlik doğrulama kimlik bilgilerini ayarlama
bir uygulama tooAzure Visual Studio veya toomonitor var olan bir bulut hizmetini toopublish, kimlik bilgilerini sağlamanız gerekir istekleri tooAzure Visual Studio tooauthenticate kullanabilirsiniz. Visual Studio'da, bu kimlik bilgileri tooprovide içinde nerede imzalayabilirsiniz çeşitli yerlerde vardır. Örneğin, Sunucu Gezgini hello hello hello kısayol menüsünü açabilirsiniz **Azure** düğümü seçin **tooMicrosoft Azure aboneliğine Bağlan...** . Oturum açtığınızda Visual Studio'da Azure hesabınızla ilişkili hello abonelik bilgilerini kullanılabilir ve daha fazla toodo sahip bir şey yok.

Azure araçlarını da destekler kimlik bilgileri, sağlama daha eski bir şekilde hello abonelik dosyasını (.publishsettings) kullanarak. Bu konu Azure SDK 2.2 hala desteklenmektedir bu yöntem açıklar.

kimlik doğrulama tooAzure için öğeleri izleyen hello gereklidir:

* Abonelik kimliği
* Geçerli bir X.509 v3 sertifikası

> [!NOTE]
> Hello hello X.509 v3 sertifikanın anahtar uzunluğu en az 2048 bit olmalıdır. Azure, bu gereksinimi karşılamıyor veya geçerli olmayan herhangi bir sertifikayı reddeder.
>
>

Visual Studio abonelik Kimliğinizi hello sertifika verileri ile birlikte kimlik bilgileri olarak kullanır. Merhaba uygun kimlik bilgilerini hello sertifika için bir ortak anahtar içeren hello abonelik dosyasında (.publishsettings dosyasını) başvurulur. Merhaba abonelik dosyası birden fazla aboneliğiniz için kimlik bilgileri içerebilir.

Merhaba hello abonelik bilgilerini Düzenle **yeni/Düzenle abonelik** iletişim kutusunda, bu konunun ilerleyen bölümlerinde açıklandığı gibi.

Toocreate bir sertifika kendiniz istiyorsanız toohello yönergelerinde başvurabilir [oluşturun ve Azure için yönetim sertifikası karşıya](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) ve hello sertifika toohello el ile karşıya [Klasik Azure portalı ](http://go.microsoft.com/fwlink/?LinkID=213885).

> [!NOTE]
> Visual Studio bulut hizmetlerinizi olmayan toomanage gerektirir bu kimlik bilgileri gerekli tooauthenticate aynı kimlik bilgileri isteği hello Azure storage hizmetlerine karşı hello.
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a>İçeri aktarma, ayarlama veya Visual Studio'da kimlik doğrulama bilgilerini Düzenle
İçeri aktarma, ayarlama veya hello kimlik doğrulama kimlik bilgilerinizi değiştirmek **yeni abonelik** eylem aşağıdaki hello gerçekleştirirseniz görünür iletişim kutusu:

* İçinde **Sunucu Gezgini**açın hello hello kısayol menüsünü **Azure** düğümü seçin **yönetin ve filtre abonelikleri...** , hello seçin **sertifikaları** sekmesini tıklatın ve hello aşağıdakilerden birini yapın:

    * Seçin **alma** tooopen hello Microsoft Azure abonelikleri alma iletişim burada indirebilirsiniz hello için hello abonelikleri dosyası şu anda yüklenen abonelik, Gözat tooits konumu karşıdan yükleyip kullanmak için alma kimlik doğrulaması.
    * Seçin **yeni** tooopen hello Yeni Abonelik iletişim burada ayarlayabilirsiniz kimlik doğrulaması kullanmak için yeni bir abonelik.
    * Seçin **Düzenle** (sonra etkin aboneliğinizi seçme) burada düzenleyebilirsiniz kimlik doğrulaması kullanmak için mevcut bir aboneliğe tooopen hello abonelik Düzenle iletişim. 

Merhaba aşağıdaki yordamı varsayar bu hello **yeni abonelik** iletişim kutusunu açın.

### <a name="tooset-up-authentication-credentials-in-visual-studio"></a>Visual Studio'da kimlik doğrulama kimlik bilgileri tooset
1. Merhaba, **varolan bir sertifikayı seçin** kimlik doğrulama listesi için bir sertifika seçin.
2. Merhaba seçin **hello tam yol Kopyala** bağlantı. Merhaba hello sertifika (.cer dosyası) kopyalanan toohello Pano yoludur.

   > [!IMPORTANT]
   > toopublish Azure uygulamanızı Visual Studio'dan Bu sertifika toohello yüklemelisiniz [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
   >
   >
3. tooupload hello sertifika toohello Azure portalı:

   1. Açık hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
   2. İstenirse, toohello Portalı'nda oturum açın ve ardından çok gidin**ayarları**, **yönetim sertifikaları**.
   3. Merhaba yönetim sertifikaları bölmesinde seçin **karşıya**.
   4. Azure aboneliğinizi seçin, oluşturulan yeni hello .cer dosyasının tam yolunu hello yapıştırın ve **karşıya**.
