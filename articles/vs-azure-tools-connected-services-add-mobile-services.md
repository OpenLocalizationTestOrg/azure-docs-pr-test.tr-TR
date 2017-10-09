---
title: "Visual Studio'da bağlı hizmetler kullanılarak Mobile Services aaaAdding | Microsoft Docs"
description: "Mobile Services hello Visual Studio bağlı Hizmetleri Ekle iletişim kutusunu kullanarak ekleme"
services: visual-studio-online
documentationcenter: na
author: mlhoop
manager: douge
editor: 
ms.assetid: 75c3cb93-88e1-476d-a416-f34caa3608e3
ms.service: visual-studio-online
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: mobile
ms.date: 12/16/2015
ms.author: mlearned
ms.openlocfilehash: c47b6fb63dc99fbc012e1c627c6c7e95249de7a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-mobile-services-by-using-visual-studio-connected-services"></a>Visual Studio bağlı Hizmetleri kullanılarak Mobile Services ekleme
Visual Studio 2015 ile tooAzure mobil hello kullanarak hizmetlere bağlanabilir **bağlı hizmet Ekle** iletişim. Tüm C# istemci uygulamaları, tüm JavaScript uygulaması veya platformlar arası Cordova uygulaması bağlanabilir. Bağlandıktan sonra oluşturmak ve verilere erişmek, özel API'leri ve zamanlanmış işler oluşturmak veya anında iletme bildirimleri için destek eklemek.  Merhaba bağlı hizmetler işlemi tüm uygun başvuruları ve bağlantı kodu ekler. Ayrıca Azure AD gibi popüler kimlik düzenleri, çeşitli kimlik doğrulaması için yerleşik destek yararlanabilirsiniz Facebook, Twitter ve Microsoft Accounts.

## <a name="supported-project-types"></a>Desteklenen proje türleri
> [!NOTE]
> Visual Studio 2015'te hello bağlı Hizmetleri Ekle iletişim kutusunu kullanarak Azure Mobile Services tooa Windows Evrensel (Windows 10) projelerine ekleme desteklenmiyor. Projeniz için hello NuGet Paket Yöneticisi'ni kullanarak hello uygun paketleri yükleyerek Azure Mobile Services ekleyebilirsiniz.
> 
> 

Merhaba bağlantılı Hizmetler iletişim tooconnect tooAzure Mobile Services proje türleri aşağıdaki hello kullanabilirsiniz.

* .NET Windows 8.1 mağazası, telefon ve evrensel uygulama projeleri
* JavaScript Windows 8.1 mağazası, telefon ve evrensel uygulama projeleri
* Apache Cordova için Visual Studio Araçları kullanılarak oluşturulan projeleri

## <a name="connect-tooazure-mobile-services-using-hello-add-connected-services-dialog"></a>TooAzure Mobile Services hello bağlı Hizmetleri Ekle iletişim kutusunu kullanarak bağlan
1. Bir Azure hesabı olduğundan emin olun. Bir Azure hesabınız yoksa, oturum açabileceğiniz bir [ücretsiz deneme sürümü](http://go.microsoft.com/fwlink/?LinkId=518146).
2. Açık hello **bağlı Hizmetleri Ekle** iletişim kutusu.
   
   * .NET uygulamaları için projenizi Visual Studio'da hello açık hello bağlam menüsünü açın **başvuruları** Çözüm Gezgini'nde, düğümünü ve ardından **bağlı hizmet Ekle**
     
        ![TooAzure mobil hizmeti bağlanma](./media/vs-azure-tools-connected-services-add-mobile-services/IC797635.png)
   * Apache Cordova uygulaması projeleri için projenizi Visual Studio'da Çözüm Gezgini'nde, proje düğümüne hello açık hello bağlam menüsünü açın ve ardından **bağlı hizmet Ekle**.
3. Merhaba, **bağlı hizmet Ekle** iletişim kutusunda, seçin **Azure Mobile Services**ve ardından hello **Yapılandır** düğmesi. Önceden yapmadıysanız Azure içine istendiğinde toolog olabilir.
   
    ![Bir Azure mobil hizmeti ekleme](./media/vs-azure-tools-connected-services-add-mobile-services/IC797636.png)
4. Merhaba, **Azure Mobile Services** iletişim kutusunda, yoksa mevcut bir mobil hizmeti seçin. Yeni bir Azure mobil hizmeti toocreate gerekiyorsa, aşağıdaki toodo hello yordamı izleyin. Aksi halde toohello sonraki adıma geçin.
   
    toocreate yeni bir mobil hizmet hesabı:
   
   1. Merhaba seçin ** hizmet oluşturma ** hello hello iletişim kutusunun alt kısmındaki bağlantıda.
       ![Yeni mobil bağlı hizmet ekleme](./media/vs-azure-tools-connected-services-add-mobile-services/IC797637.png)
   2. Merhaba üzerinde **mobil hizmet Oluştur** iletişim kutusu, seçebileceğiniz bir JavaScript arka uç mobil hizmet ya da bir .NET arka uç mobil hizmet hello **çalışma zamanı** aşağı açılan liste. 
      
       ![Bir mobil hizmet oluşturma](./media/vs-azure-tools-connected-services-add-mobile-services/IC797638.png)
      
       Basit ve güçlü bir JavaScript arka uç hizmeti. Bir JavaScript arka uç mobil hizmet oluşturmak, hello sunucu tarafı JavaScript kodu hello bulutta depolanır, ancak Sunucu Gezgini veya hello Azure yönetim portalını kullanarak sunucu komut dosyalarını düzenleyebilirsiniz. 
      
       Bir .NET arka uç mobil hizmet hello tam güç ve Entity Framework ile Web API ve esneklik sağlar. Bir .NET arka uç mobil hizmet oluşturursanız, proje sizin için oluşturulur ve tooyour çözüm eklenir. 
   3. Merhaba seçin **bölge** , hello mobil hizmet istediğiniz ve ardından hello sunucusu için bir kullanıcı adı ve parola girin.
   4. Tüm gerekli hello bilgileri girdikten sonra hello seçin **oluşturma** düğmesini toocreate hello mobil hizmet.
   5. Merhaba yeni mobil hizmet hello hello Hizmet listesinde görüntülenmedir **Azure Mobile Services** iletişim kutusu. Merhaba yeni mobil hizmet hello listede seçin ve ardından hello **Ekle** düğmesini tooadd hello hizmeti tooyour projesi.
5. Gözden geçirme hello görünür ve projenizin nasıl değiştirildiği Bul sayfası Başlarken. Bağlı hizmet eklediğinizde Başlarken sayfa tarayıcınızda görüntülenir. Gözden geçirebilirsiniz önerilen sonraki adımlar ve kod örnekleri hello veya hangi başvuruları tooyour proje eklendi ve kod ve yapılandırma dosyalarınızı nasıl değiştirildi toohello ne sayfa toosee geçin.
6. Merhaba kod örnekleri bir kılavuz olarak kullanarak, mobil hizmetinize kod tooaccess yazma başlayın!

## <a name="how-your-project-is-modified"></a>Projenizi nasıl değiştirilir
Visual Studio, projenizin nasıl değiştirdiğini hello proje türüne göre değişir. C# istemci uygulamaları için bkz: [ne – C# projeleri](http://go.microsoft.com/fwlink/p/?LinkId=513119). JavaScript istemci uygulamaları için bkz: [ne – JavaScript projeleri](http://go.microsoft.com/fwlink/p/?LinkId=513120). Cordova uygulamaları için bkz: [ne – Cordova projeleri](http://go.microsoft.com/fwlink/p/?LinkId=513116).

## <a name="next-steps"></a>Sonraki adımlar
Soru sorun ve Yardım alın: 

* [MSDN forumu: Azure mobil hizmetler](https://social.msdn.microsoft.com/forums/azure/home?forum=azuremobile)
* [Azure Mobile Services konumundaki hello Microsoft Azure ekibi blogu](https://azure.microsoft.com/blog/topics/mobile/)
* [Azure.microsoft.com adresindeki Azure mobil hizmetler](https://azure.microsoft.com/services/mobile-services/)
* [Azure.microsoft.com adresindeki Azure Mobile Services belgeleri](https://azure.microsoft.com/documentation/services/mobile-services/)

