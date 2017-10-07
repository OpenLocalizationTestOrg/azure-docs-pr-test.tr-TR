---
title: "aaaService Fabric uygulama yükseltme Öğreticisi | Microsoft Docs"
description: "Bu makalede bir Service Fabric uygulaması dağıtma, hello kodunu değiştirme ve Visual Studio kullanarak bir yükseltmesinde hello deneyimi anlatılmaktadır."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a3181a7a-9ab1-4216-b07a-05b79bd826a4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: d069ff0b291018dbac846e65cddff1e9d73d156c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-tutorial-using-visual-studio"></a>Visual Studio kullanarak Service Fabric uygulaması yükseltme Öğreticisi
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-application-upgrade-tutorial-powershell.md)
> * [Visual Studio](service-fabric-application-upgrade-tutorial.md)
> 
> 

<br/>

Azure Service Fabric yalnızca değiştirilen Hizmetleri yükseltilir ve uygulama sağlığını hello yükseltme işlemi boyunca izlenir sağlayarak bulut uygulamaları yükseltme hello işlemini basitleştirir. Bu da otomatik olarak geri sorunları karşılaşıldığında hello uygulama toohello önceki sürümü yapar. Service Fabric uygulaması yükseltmelerin *sıfır kapalı kalma süresi*, kapalı kalma süresi ile Merhaba uygulaması yükseltilebilir beri. Bu öğretici kapsayan nasıl toocomplete yükseltme Visual Studio'dan.

## <a name="step-1-build-and-publish-hello-visual-objects-sample"></a>1. adım: Oluşturma ve yayımlama hello görsel nesneler örnek
İlk olarak, hello karşıdan [görsel nesneler](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Actors/VisualObjects) github'dan uygulama. Ardından, yapı ve hello uygulama yayımlama hello uygulama projesine sağ tıklayarak **VisualObjects**, hello seçerek **Yayımla** hello Service Fabric menü öğesi komutunu.

![Service Fabric uygulaması bağlam menüsü][image1]

Seçme **Yayımla** açılan bir pencere ortaya getirir ve hello ayarlayabilirsiniz **hedef profil** çok**PublishProfiles\Local.xml**. Merhaba penceresinde hello tıklamadan önce aşağıdaki gibi görünmelidir **Yayımla**.

![Service Fabric uygulaması yayımlama][image2]

Tıklayabilirsiniz artık **Yayımla** hello iletişim kutusunda. Kullanabileceğiniz [Service Fabric Explorer, tooview Merhaba küme ve hello uygulaması](service-fabric-visualizing-your-cluster.md). Merhaba görsel nesneler uygulama sahip tooby yazarak gidebilirsiniz bir web hizmeti [http://localhost:8081/visualobjects/](http://localhost:8081/visualobjects/) hello tarayıcınızın adres çubuğuna.  Merhaba ekranında hareket etmek, 10, kayan görsel nesneler görmeniz gerekir.

**Not:** çok dağıtmayı`Cloud.xml` profil (Azure Service Fabric) Merhaba uygulaması kullanılabilir olmalıdır **http://{ServiceFabricName}. { Region}.cloudapp.Azure.com:8081/visualobjects/**. Sahip olduğunuzdan emin olun `8081/TCP` hello yük dengeleyici yapılandırılmış (Merhaba yük dengeleyici hello Bul hello Service Fabric örneği ile aynı kaynak grubunda).

## <a name="step-2-update-hello-visual-objects-sample"></a>2. adım: Güncelleştirme hello görsel nesneler örnek
1. adımda dağıtılan hello sürümüyle hello visual nesneleri değil döndürme fark edebilirsiniz. Şimdi burada hello görsel nesneler de döndürme bu uygulama tooone yükseltin.

Merhaba VisualObjects.ActorService projesi hello VisualObjects çözüm içinde seçin ve açın hello **VisualObjectActor.cs** dosya. Bu dosyanın içindeki toohello yöntemi Git `MoveObject`, çıkışı açıklama `visualObject.Move(false)`ve açıklama durumundan çıkarmanız `visualObject.Move(true)`. Merhaba hizmet yükseltildikten sonra bu kodu değişikliği hello nesnesini döndürür.  **(Yeniden oluşturmaz) yapı artık hello çözüm**, hangi hello yapıların projeleri değiştirdi. Seçerseniz *tüm yeniden*, tüm projeleri hello için tooupdate hello sürümlere sahip.

Biz de tooversion uygulamamız gerekir. değişiklikler hello üzerinde sağ sonra toomake hello sürümü **VisualObjects** projesi hello Visual Studio kullanabilirsiniz **bildirim sürümleri Düzenle** seçeneği. Bu seçeneğin belirlenmesi hello iletişim kutusunda edition sürümleri için şu şekilde getirir:

![Sürüm oluşturma iletişim kutusu][image3]

Güncelleştirme hello sürümleri hello için projeleri ve hello uygulama tooversion 2.0.0 yanı sıra bunların kod paketleri değiştirdi. Merhaba değişiklikler yapıldıktan sonra hello bildirimi hello aşağıdaki gibi görünmelidir (kalın bölümleri göster hello değişiklikleri):

![Güncelleştirme sürümleri][image4]

Merhaba Visual Studio Araçları seçtikten sonra sürümlerinin otomatik toplamaları yapabilir **otomatik olarak uygulama ve hizmet sürümleri güncelleştirme**. Kullanırsanız [SemVer](http://www.semver.org), tooupdate hello kodu gerekli ve/veya yapılandırma paketi sürümü bu, tek başına seçeneği işaretlidir.

Merhaba değişiklikleri kaydetmek ve şimdi hello denetle **yükseltme hello uygulama** kutusu.

## <a name="step-3--upgrade-your-application"></a>3. adım: uygulamanızı yükseltin
Merhaba ile öğrenmeniz [uygulama yükseltme parametreleri](service-fabric-application-upgrade-parameters.md) ve hello [yükseltme işlemi](service-fabric-application-upgrade.md) tooget çeşitli yükseltme parametreleri, zaman aşımları ve için sistem durumu ölçüt hello iyi anlamış uygulanması. Bu kılavuzda hello hizmet sistem durumu değerlendirme ölçüt toohello varsayılan (izlenmeyen modu) ayarlanır. Seçerek bu ayarları yapılandırabilirsiniz **yükseltme ayarlarını yapılandır** ve istediğiniz gibi hello parametrelerini değiştirme.

Biz tüm kümesi toostart hello uygulama artık seçerek yükseltme **Yayımla**. Bu seçenek, uygulama tooversion içinde hello nesneleri döndürme 2.0.0 yükseltir. Service Fabric (bazı nesneler ilk olarak, başkaları tarafından ve ardından güncelleştirilir) bir defada tek bir güncelleştirme etki alanı yükseltme ve hello hizmeti hello yükseltme sırasında erişilebilir olarak kalır. Erişim toohello hizmeti istemci (tarayıcı) denetlenebilir.  

Şimdi, uygulama yükseltme devam eder hello gibi bu Service Fabric Explorer ile hello kullanarak izleyebilirsiniz **yükseltme devam eden** hello uygulama sekmesinde.

Birkaç dakika içinde (tamamlandı) tüm güncelleme etki alanına yükseltilmesi ve hello Visual Studio çıkış penceresi de o hello yükseltme tamamlandıktan durumlarında. Ve, bulmalıdır *tüm* hello visual nesneleri Tarayıcı pencerenizde şimdi döndürme!

Merhaba sürümleri değiştirme ve bir alıştırma olarak sürüm 2.0.0 tooversion 3.0.0 taşıma tootry istediğiniz ya da tooversion 1.0.0 bile 2.0.0 sürümünden geri. Zaman aşımları ve sistem durumu ilkeleri toomake kendiniz bunları aşina yürütün. Azure küme olarak tooan dağıtma tooa yerel küme değil, kullanılan hello parametreler toodiffer olabilir. Merhaba zaman aşımlarını ölçülü ayarlamanızı öneririz.

## <a name="next-steps"></a>Sonraki adımlar
[PowerShell kullanarak uygulamanızı yükseltme](service-fabric-application-upgrade-tutorial-powershell.md) PowerShell kullanarak bir uygulama yükseltme yol gösterir.

Kullanarak uygulamanızı nasıl yükseltilir kontrol [yükseltme parametreleri](service-fabric-application-upgrade-parameters.md).

Uygulama yükseltme öğrenme tarafından uyumlu hale getirmek nasıl toouse [veri seri hale getirme](service-fabric-application-upgrade-data-serialization.md).

Uygulamanız çok başvurarak yükseltirken toouse işlevselliği nasıl Gelişmiş öğrenin[konuları Gelişmiş](service-fabric-application-upgrade-advanced.md).

Toohello adımlarda başvurarak uygulama yükseltmeleri sık karşılaşılan sorunları düzeltmek [uygulama yükseltme sorunlarını giderme](service-fabric-application-upgrade-troubleshooting.md).

[image1]: media/service-fabric-application-upgrade-tutorial/upgrade7.png
[image2]: media/service-fabric-application-upgrade-tutorial/upgrade1.png
[image3]: media/service-fabric-application-upgrade-tutorial/upgrade5.png
[image4]: media/service-fabric-application-upgrade-tutorial/upgrade6.png
