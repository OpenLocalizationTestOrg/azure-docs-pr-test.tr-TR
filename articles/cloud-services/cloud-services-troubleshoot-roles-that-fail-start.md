---
title: "toostart başarısız aaaTroubleshoot rolleri | Microsoft Docs"
description: "Bir bulut hizmeti rolü toostart neden başarısız olabileceği bazı yaygın nedenler şunlardır. Çözümler toothese sorunlar de sağlanmıştır."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 674b2faf-26d7-4f54-99ea-a9e02ef0eb2f
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: e2fbecb08a10984add79dfc74e73de6869bb314f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-toostart"></a>Toostart başarısız bulut hizmeti rolleriyle ilgili sorunları giderme
Bazı yaygın sorunlar ve toostart başarısız çözümleri ilgili tooAzure bulut Hizmetleri rolleri aşağıda verilmiştir.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a>Eksik DLL'leri veya bağımlılıkları
Yanıt vermeyen rolleri ve arasında geçiş yapma rolleri **başlatılıyor**, **meşgul**, ve **durdurma** durumları DLL'leri veya derlemeleri eksik kaynaklanabilir.

DLL'leri veya derlemeleri eksik Belirtiler şunlar olabilir:

* Rol örneği dolaşma **başlatılıyor**, **meşgul**, ve **durdurma** durumları.
* Rol örneği çok taşındı**hazır** ancak tooyour web uygulaması giderseniz, hello sayfası görünmez.

Bu sorunları incelemeye için önerilen çeşitli yöntemler vardır.

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a>Web rolü eksik DLL sorunları tanılama
Bir web rolünde dağıtılan tooa Web sitesine gidin ve bir sunucu hatası benzer toohello aşağıdaki hello tarayıcı görüntüler, DLL eksik olduğunu gösteriyor olabilir.

!['/' Uygulamasında sunucu hatası.](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a>Özel hatalar devre dışı bırakarak sorunlarını tanılamak
Daha ayrıntılı hata bilgileri hello web.config hello web rolü tooset hello özel hata modu tooOff için yapılandırma ve hello hizmet dağıtarak görüntülenebilir.

tooview daha tamamlamak hataları Uzak Masaüstü'nü kullanmadan:

1. Merhaba çözümü Microsoft Visual Studio'da açın.
2. Merhaba, **Çözüm Gezgini**, hello web.config dosyasını bulun ve açın.
3. Merhaba web.config dosyasında hello system.web bölümünü bulun ve hello aşağıdaki satırı ekleyin:

    ```xml
    <customErrors mode="Off" />
    ```
4. Merhaba dosyasını kaydedin.
5. Yeniden paketleyin ve hello hizmeti yeniden dağıtın.

Merhaba hizmet imzalanmasını sonra eksik derleme veya DLL hello hello adı ile bir hata iletisi görürsünüz.

## <a name="diagnose-issues-by-viewing-hello-error-remotely"></a>Merhaba hata uzaktan görüntüleyerek sorunlarını tanılamak
Uzak Masaüstü tooaccess hello rolünü kullanın ve Uzaktan daha eksiksiz hata bilgilerini görüntüleyin. Uzak Masaüstü'nü kullanarak aşağıdaki adımları tooview hello hatalar hello kullan:

1. Azure SDK 1.3 veya üstü yüklü olduğundan emin olun.
2. Visual Studio kullanarak hello çözüm Hello dağıtımı sırasında çok seçin "yapılandırma Uzak Masaüstü bağlantıları...". Merhaba Uzak Masaüstü bağlantısı yapılandırma hakkında daha fazla bilgi için bkz: [Azure rolleri ile Uzak Masaüstü kullanarak](../vs-azure-tools-remote-desktop-roles.md).
3. Merhaba örneği durumunu gösterir sonra hello Microsoft Azure Klasik Portalı'nda, **hazır**, hello rol örnekleri birine tıklayın.
4. Merhaba tıklatın **Bağlan** hello simgesinde **uzaktan erişim** hello Şerit alanı.
5. Toohello sanal makinede hello uzak masaüstü yapılandırması sırasında belirtilen hello kimlik bilgilerini kullanarak oturum açın.
6. Bir komut penceresi açın.
7. `IPconfig` yazın.
8. Başlangıç IPv4 adresi değerini not edin.
9. Internet Explorer'ı açın.
10. Başlangıç adresi ve hello hello web uygulamasının adını yazın. Örneğin, `http://<IPV4 Address>/default.aspx`.

Web sitesi, toohello gezinme şimdi daha açık hata iletileri döndürür:

* '/' Uygulamasında sunucu hatası.
* Açıklama: Hello geçerli web isteği hello yürütülmesi sırasında işlenmemiş bir özel durum oluştu. Lütfen hello hata hakkında daha fazla bilgi için hello yığın izleme ve hello kodda geldiği gözden geçirin.
* Özel durum ayrıntıları: System.IO.FIleNotFoundException: dosya veya derleme yüklenemedi ' Microsoft.WindowsAzure.StorageClient, sürüm 1.1.0.0, Culture = neutral, PublicKeyToken = 31bf856ad364e35 =' ya da bağımlılıklarından biri. Merhaba Sistem belirtilen hello dosyası bulunamıyor.

Örneğin:

!['/' Uygulamasında açık sunucu hatası](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-hello-compute-emulator"></a>Merhaba işlem öykünücüsü kullanarak sorunları tanılamak
Merhaba Microsoft Azure işlem öykünücüsü toodiagnose ve bağımlılıklar ve web.config hataları eksik sorunlarını giderme kullanabilirsiniz.

Tanılama bu yöntemi kullanmanın en iyi sonuçlar için bir bilgisayarı veya Windows temiz bir yüklemesini sanal makine kullanmanız gerekir. toobest hello Azure ortamı benzetimini yapmak için Windows Server 2008 R2 x64 kullanın.

1. Merhaba Hello tek başına sürümünü yüklemek [Azure SDK'sı](https://azure.microsoft.com/downloads/).
2. Merhaba geliştirme makinenizde hello bulut hizmeti projesi oluşturun.
3. Windows Gezgini'nde hello bulut hizmeti projesi, toohello klasörüne gidin.
4. Merhaba .csx klasörünü ve toodebug hello sorunları kullandığınız .cscfg dosya toohello bilgisayara kopyalayın.
5. Temiz makine Hello üzerinde bir Azure SDK komut istemi penceresi açıp `csrun.exe /devstore:start`.
6. Merhaba komut istemine yazın `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.
7. Merhaba rol başladığında, Internet Explorer'da ayrıntılı hata bilgileri görürsünüz. Standart Windows sorun giderme araçları da kullanabilirsiniz toofurther hello sorunu tanılamak.

## <a name="diagnose-issues-by-using-intellitrace"></a>IntelliTrace kullanarak sorunları tanılamak
Çalışan ve .NET Framework 4 kullanan web rolleri için kullanabileceğiniz [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), Microsoft Visual Studio Enterprise'da kullanılabilir olduğu.

Bu adımları toodeploy hello hizmeti etkin IntelliTrace ile izleyin:

1. Azure SDK 1.3 veya üstü yüklü olduğunu onaylayın.
2. Visual Studio kullanarak Hello çözümü dağıtın. Dağıtım sırasında hello denetleyin **.NET 4 rolleri için IntelliTrace'i etkinleştirin** onay kutusu.
3. Merhaba örneği başlatır, hello açın **Sunucu Gezgini**.
4. Merhaba genişletin **Azure\\bulut Hizmetleri** düğümü ve hello dağıtımını bulun.
5. Merhaba dağıtım hello rol örnekleri görene kadar genişletin. Merhaba örnekleri birine sağ tıklayın.
6. Seçin **görünüm IntelliTrace günlüklerini**. Merhaba **IntelliTrace Özet** açılır.
7. Merhaba özel durumlar hello Özet bölümünü bulun. Özel durumlar varsa, hello bölüm etiketli **özel durum verileri**.
8. Merhaba genişletin **özel durum verileri** ve Ara **System.IO.FileNotFoundException** benzer toohello aşağıdaki hatalar:

![Özel durum verileri, eksik dosya veya derleme](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a>Adres eksik DLL'ler ve derlemeler
DLL ve derleme hatalarını eksik tooaddress şu adımları izleyin:

1. Merhaba çözümü Visual Studio'da açın.
2. İçinde **Çözüm Gezgini**açın hello **başvuruları** klasör.
3. Merhaba hata tanımlanan hello derleme'yi tıklayın.
4. Merhaba, **özellikleri** bölmesinde bulun **kopya yerel özellik** ve hello değeri çok**doğru**.
5. Merhaba bulut hizmeti yeniden dağıtın.

Tüm hataları düzelttikten olduğunu doğruladıktan sonra hello denetlemeden hello hizmeti dağıtabilirsiniz **.NET 4 rolleri için IntelliTrace'i etkinleştirin** onay kutusu.

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi görüntülemek [sorun giderme makalelerini](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) bulut Hizmetleri için.

tootroubleshoot bulut hizmet rolü nasıl sorunları Azure PaaS bilgisayar tanılama verilerini kullanarak toolearn bkz [Kevin Williamson'ın blog dizisini](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
