---
title: "aaaAzure App Service planlarına ayrıntılı genel bakış | Microsoft Docs"
description: "Azure uygulama hizmeti iş için nasıl uygulama hizmeti planları ve bunların, yönetim deneyimi nasıl yararlı öğrenin."
keywords: "app service, azure app service, ölçek, ölçeklenebilir, app service planı, app service maliyeti"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: dea3f41e-cf35-481b-a6bc-33d7fc9d01b1
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: b384790d9e69b234ca69ac591164c48a4b6ed210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a>Azure App Service planlarına ayrıntılı genel bakış

Uygulama hizmeti planları, uygulamalarınızı kullanılan fiziksel kaynakları toohost hello koleksiyonunu temsil eder.

App Service planları şunları tanımlar:

- Bölge (Batı ABD, Doğu ABD, vb.)
- Ölçek sayısı (bir, iki, üç örnekleri, vb.)
- (Küçük, Orta, büyük) örnek boyutu
- SKU (Ücretsiz, Paylaşılan, Temel, Standart, Premium)

İçinde Apps, Mobile Apps, API uygulamaları, işlev uygulamalarının (veya işlevler), web [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) bir uygulama hizmeti planındaki tüm çalışma.  Uygulamaları hello bir uygulama hizmeti planı aynı abonelikte ve bölgede paylaşabilirsiniz. 

Atanan tüm uygulamalar için tooan **uygulama hizmeti planı** tanımladığı hello kaynakları paylaşır. Bu paylaşımı para birden fazla uygulama tek bir uygulama hizmeti planında barındırdığında kaydeder.

**Uygulama hizmeti planı** gelen ölçeklendirebilirsiniz **serbest** ve **paylaşılan** SKU'ları çok**temel**, **standart**, ve **Premium** , vermiş SKU'ları erişim toomore kaynakları ve özellikleri hello boyunca yolu.

Uygulama hizmeti planınızı çok ayarlarsanız**temel** SKU veya daha yüksek hello denetleyebilirsiniz sonra **boyutu** ve ölçeklendirme hello VM'ler sayısı.

Örneğin, planınız yapılandırılmış toouse iki "küçük" Merhaba standart hizmet katmanındaki ise, bu planla ilişkili tüm uygulamalar hem örneklerinde çalıştırın. Uygulamaların erişim toohello standart hizmet katmanı özellikleri de vardır. Plan örneği uygulamaları çalıştırdığınız tam olarak yönetilen ve yüksek oranda kullanılabilir.

> [!IMPORTANT]
> Merhaba **SKU** ve **ölçek** Merhaba uygulama hizmeti planı hello maliyet ve değil hello sayısını içinde barındırılan uygulamalar belirler.

Bu makalede katmanı ve bir uygulama hizmeti planının ölçek ve nasıl uygulamalarınızı yönetmeye çalışırken oyuna geldikleri gibi hello anahtar özelliklerini inceler.

## <a name="apps-and-app-service-plans"></a>Uygulamalar ve uygulama hizmeti planları

Uygulama hizmeti bir uygulamada verilen herhangi bir zamanda yalnızca bir uygulama hizmeti plan ile ilişkili olabilir.

Uygulamaları ve planları içerdiği bir **kaynak grubu**. Bir kaynak grubu içinde olan her kaynak için hello yaşam döngüsü sınırı olarak görev yapar. Kaynak grupları toomanage uygulama tüm hello parçaları birlikte kullanabilirsiniz.

Tek bir kaynak grubu birden çok uygulama hizmeti planları olduğundan farklı uygulamalar toodifferent fiziksel kaynakları tahsis edebilirsiniz.

Örneğin, geliştirme, test ve üretim ortamları arasında kaynakları ayırabilirsiniz. Üretim ve geliştirme ve test için ayrı ortamlara sahip kaynakları ayırmanıza olanak tanır. Bu şekilde, uygulamalarınızı yeni bir sürümü karşı test yük Merhaba aynı rekabet edemez kaynaklar gerçek müşteriler hizmet veren, üretim uygulamalarınızı olarak.

Tek bir kaynak grubu içinde birden çok planına sahip olduğunuzda, coğrafi bölgeler kapsayan bir uygulama da tanımlayabilirsiniz.

Örneğin, iki bölgelerde çalışan yüksek oranda kullanılabilir bir uygulama, en az iki planları, her bölge için bir tane ve her plan ile ilişkili bir uygulama içerir. Böyle bir durumda hello uygulama tüm hello kopyalarını ardından tek bir kaynak grubu içinde yer alır. Birden çok planları ve birden çok uygulama ile bir kaynak grubu büyük kolay toomanage, Denetim ve görünüm hello hello uygulama durumunu sağlar.

## <a name="create-an-app-service-plan-or-use-existing-one"></a>Bir uygulama hizmeti planı oluşturun veya varolan bir kullanın

Bir uygulama oluşturduğunuzda, bir kaynak grubu oluşturmayı düşünebilirsiniz. Üzerinde bu uygulama daha büyük bir uygulama için bir bileşen ise diğer yandan Merhaba, büyük bu uygulama için ayrılan hello kaynak grubunda oluşturun.

Merhaba uygulama tamamen yeni bir uygulama veya daha büyük bir parçası olup olmadığını belirtir, var olan bir planı toohost toouse seçebilirsiniz, ya da yeni bir tane oluşturun. Daha fazla kapasite ve beklenen yükü soru karardır.

Yeni bir uygulama hizmeti uygulamanızı yalıtma öneririz ne zaman planlama:

- Yoğun bir kaynak uygulamasıdır.
- Uygulama hello öğesinden farklı ölçeklendirme etkenleri var olan bir planı barındırılan diğer uygulamalar vardır.
- Uygulamanın farklı bir coğrafi bölgede kaynak gerekir.

Böylece uygulamanız için yeni bir kaynak kümesini ayırmak ve uygulamalarınızın daha fazla denetim kazanmak.

## <a name="create-an-app-service-plan"></a>App Service planı oluşturma

> [!TIP]
> Bir uygulama hizmeti ortamı varsa, hello belgeleri belirli tooApp hizmeti ortamları burada gözden geçirebilirsiniz: [bir uygulama hizmeti ortamı'nda bir uygulama hizmeti planı oluştur](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)

Uygulama hizmeti planı gözatma deneyimi hello veya uygulaması oluşturma işleminin bir parçası olarak boş bir uygulama hizmeti planı oluşturabilirsiniz.

Merhaba, [Azure portal](https://portal.azure.com), tıklatın **yeni** > **Web + mobil**ve ardından **Web uygulaması** veya diğer uygulama hizmeti uygulaması türü.

![Hello Azure portalında bir uygulama oluşturun.][createWebApp]

Ardından, seçin veya hello hello yeni uygulaması için uygulama hizmeti planı oluşturun.

 ![Bir uygulama hizmeti planı oluşturun.][createASP]

toocreate bir uygulama hizmeti planı tıklatın **[+] oluştur yeni**, türü hello **uygulama hizmeti planı** adlandırın ve ardından uygun bir seçin **konumu**. Tıklatın **fiyatlandırma katmanı**ve ardından hello hizmeti için uygun bir fiyatlandırma katmanı seçin. Seçin **tüm görüntüle** daha seçenekleri gibi fiyatlandırma tooview **serbest** ve **paylaşılan**. Fiyatlandırma katmanı hello seçtikten sonra hello tıklatın **seçin** düğmesi.

## <a name="move-an-app-tooa-different-app-service-plan"></a>Bir uygulama tooa farklı uygulama hizmeti planı taşıma

Bir uygulama tooa farklı uygulama hizmeti planı hello taşıyabilirsiniz [Azure portal](https://portal.azure.com). Merhaba planları hello olduğu sürece, uygulamaları planları arasında taşıyabilirsiniz aynı kaynak grubunu ve coğrafi bölge.

bir uygulama tooanother planı toomove:

- Toomove istediğiniz toohello uygulamasına gidin.
- Merhaba, **menü**, Merhaba Ara **App Service planı** bölümü.
- Seçin **değişiklik uygulama hizmeti planı** toostart hello işlemi.

**Uygulama hizmeti planını Değiştir** açılır hello **uygulama hizmeti planı** Seçici. Bu noktada, bu uygulamaya var olan bir planı toomove seçebilirsiniz.

> [!IMPORTANT]
> Merhaba select uygulama hizmeti planı kullanıcı Arabirimi tarafından hello ölçütleri aşağıdaki filtre:
> - Merhaba içinde aynı mevcut kaynak grubu
> - Hello aynı var. coğrafi bölge
> - Merhaba içinde aynı mevcut Web alanı
>
> Bir Web alanı, sunucu kaynaklarını gruplandırması tanımlayan bir App Service içinde mantıksal bir yapıdır. Coğrafi bölge (örneğin, Batı ABD) uygulama hizmetini kullanarak sipariş tooallocate müşteriler birçok Web alanları içeriyor. Şu anda, uygulama hizmeti kaynaklarına arasında izlemiyor taşınmış mümkün toobe değil.
>

![Uygulama hizmeti planı Seçici.][change]

Her plan kendi fiyatlandırma katmanı vardır. Örneğin, bir site ücretsiz katmanı tooa standart katmanından bir taşıma, tooit toouse hello özellikleri ve kaynakları hello standart katmanı atanmış tüm uygulamaları etkinleştirir.

## <a name="clone-an-app-tooa-different-app-service-plan"></a>Bir uygulama tooa farklı uygulama hizmeti planı Kopyala

Toomove hello uygulama tooa farklı bir bölgeye istiyorsanız, bir uygulama alternatiftir kopyalama. Kopyalama, yeni veya var olan uygulama hizmeti planındaki tüm bölgelerdeki uygulamanızı bir kopyasını oluşturur.

Bulabileceğiniz **kopya uygulama** hello içinde **geliştirme araçları** hello menüsünün bölümünde.

> [!IMPORTANT]
> Kopyalama sırasında hakkında bilgi edinebilirsiniz bazı sınırlamalara sahiptir [Azure portalını kullanarak Azure uygulama hizmeti kopyalama](../app-service-web/app-service-web-app-cloning-portal.md).

## <a name="scale-an-app-service-plan"></a>Ölçek bir uygulama hizmeti planı

Bir plan üç yolu tooscale vardır:

- **Değişiklik hello planı katmanı fiyatlandırma**. Bir planı hello temel katmanındaki dönüştürülmüş tooStandard olabilir ve tüm uygulamalar tooit toouse hello standart katmanı hello özelliklerini atanmış.
- **Merhaba planın örnek boyutunu değiştirin**. Örnek olarak, bir planı küçük örnekleri kullanan hello temel katmanındaki değiştirilen toouse büyük örnekleri olabilir. Şimdi bu planla ilişkili tüm uygulamalar hello ek bellek ve büyük örnek boyutu teklifleri hello CPU kaynaklarını kullanabilirsiniz.
- **Merhaba planın örnek sayısı değiştirme**. Örneğin, toothree örnekleri ölçeklendirilmiş bir standart planı ölçeklendirilmiş too10 örnekleri olabilir. Premium planı too20 örnekleri (konu tooavailability) genişletilebilir. Şimdi bu planla ilişkili tüm uygulamalar hello ek bellek ve büyük örnek sayısı teklifleri hello CPU kaynaklarını kullanabilirsiniz.

Fiyatlandırma katmanı ve örnek boyutunda hello tıklayarak hello değiştirebileceğiniz **ölçeği Artır** hello uygulama ya da hello uygulama hizmeti planı ayarları altında öğesi. Değişiklikler toohello uygulama hizmeti planı uygulamak ve onu barındıran tüm uygulamaları etkiler.

 ![Bir uygulama yukarı değerleri tooscale ayarlayın.][pricingtier]

## <a name="app-service-plan-cleanup"></a>Uygulama hizmeti planı temizleme

> [!IMPORTANT]
> **Uygulama hizmeti planları** tooreserve hello işlem kapasitesini devam hala ücretlendirme hiçbir ilişkili uygulamalar toothem sahip.

tooavoid bir uygulama hizmeti planında barındırılan hello son uygulama silindiğinde, beklenmeyen ücretleri hello elde edilen boş uygulama hizmeti planı da silinir.

## <a name="summary"></a>Özet

Uygulama hizmeti planları, bir özellik kümesini ve Web siteleriniz arasında paylaşabileceğiniz kapasite temsil eder. Uygulama hizmeti esneklik tooallocate belirli uygulamaları tooa kaynak kümesi hello ve daha fazla Azure kaynak kullanımınızı iyileştirmek verin planlar. Bu şekilde, test ortamınızda, toosave para istiyorsanız bir planı birden çok uygulama arasında paylaşabilirsiniz. Ayrıca verimlilik, üretim ortamınız için birden çok bölgeler ve planları arasında ölçeklendirme tarafından en üst düzeye çıkarabilirsiniz.

## <a name="whats-changed"></a>Yapılan değişiklikler

- Web siteleri tooApp hizmet gelen bir kılavuzu toohello değişiklik için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
