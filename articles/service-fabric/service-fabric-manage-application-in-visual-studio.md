---
title: "aaaManage Visual Studio uygulamalarınızda | Microsoft Docs"
description: "Visual Studio toocreate kullanın, geliştirmek, paket, dağıtmak ve Service Fabric uygulamaları ve Hizmetleri hata ayıklama."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: c317cb7e-7eae-466e-ba41-6aa2518be5cf
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: b2d5803d85e4f9645dcbece33a2208bc0955498d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-toosimplify-writing-and-managing-your-service-fabric-applications"></a>Visual Studio toosimplify yazma ve Service Fabric uygulamaları yönetme
Azure Service Fabric uygulamaları ve Hizmetleri Visual Studio aracılığıyla yönetebilirsiniz. Seçtiğiniz sonra [geliştirme ortamınızı ayarlama](service-fabric-get-started.md), Visual Studio toocreate Service Fabric uygulamaları, hizmetleri veya paket, kayıt eklemeniz ve yerel geliştirme kümenizdeki uygulamaları dağıtma.

## <a name="deploy-your-service-fabric-application"></a>Service Fabric uygulamanızı dağıtma
Varsayılan olarak, bir uygulama dağıtımı aşağıdaki adımları basit tek bir işlemle hello birleştirir:

1. Merhaba uygulama paketi oluşturma
2. Merhaba uygulama paketi toohello görüntü deposuna karşıya yükleme
3. Merhaba uygulama türünü kaydetme
4. Herhangi bir kaldırma uygulama örnekleri çalıştırma
5. Uygulama örneğini oluşturma

Visual Studio'da tuşuna basarak **F5** uygulamanızı dağıtır ve hello hata ayıklayıcı tooall uygulama örnekleri ekleyin. Kullanabileceğiniz **Ctrl + F5** toodeploy uygulamanın hata ayıklama veya olmadan tooa yerel yayımlayarak veya hello kullanarak uzak küme yayımlama profili. Daha fazla bilgi için bkz: [Visual Studio kullanarak bir uygulama tooa uzaktan küme yayımlama](service-fabric-publish-app-remote-cluster.md).

### <a name="application-debug-mode"></a>Uygulama hata ayıklama modu
Visual Studio sağlamak adlı bir özellik **uygulama hata ayıklama modu**, Visual stüdyoları toohandle uygulama dağıtımı hata ayıklama bir parçası olarak nasıl istediğiniz kontrol eder.

#### <a name="tooset-hello-application-debug-mode-property"></a>tooset hello uygulama hata ayıklama modu özelliği
1. Merhaba Service Fabric uygulaması projenin (*.sfproj) üzerinde kısayol menüsünü seçin **özellikleri** (veya tuşuna hello **F4** anahtar).
2. Merhaba, **özellikleri** penceresinde, kümesi hello **uygulama hata ayıklama modu** özelliği.

![Uygulama hata ayıklama modu özelliğini ayarlayın][debugmodeproperty]

#### <a name="application-debug-modes"></a>Uygulama hata ayıklama modu

1. **Uygulamayı yenileyin** Bu mod tooquickly değişiklik sağlar ve hata ayıklama sırasında statik web dosyaları düzenleme destekler ve kod hata ayıklama. Yerel geliştirme kümenizi ise bu modu yalnızca çalışır [1 düğümü modunu](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).
2. **Uygulamayı kaldırmak** nedenler hello uygulama toobe hello hata ayıklama oturumu bittikten sonra kaldırılır.
3. **Yükseltme otomatik** Merhaba uygulaması hello hata ayıklama oturumu sona erdiğinde toorun devam eder. Merhaba sonraki hata ayıklama oturumu hello dağıtım yükseltme olarak kabul eder. Merhaba yükseltme işlemi önceki bir hata ayıklama oturumunda girdiğiniz herhangi bir veriyi korur.
4. **Uygulama tutmak** hello zaman hello kümede çalışan hello uygulama tutar hata ayıklama oturumu sona erer. Merhaba başlangıcında hello sonraki hata ayıklama oturumu, Merhaba uygulaması kaldırılır.

İçin **otomatik yükseltme** hello uygulama yükseltme özelliklerini Service Fabric uygulayarak veriler korunur. Uygulamalar ve gerçek bir ortamda bir yükseltme nasıl yerine getirmeyebilir yükseltme hakkında daha fazla bilgi için bkz: [Service Fabric uygulama yükseltme](service-fabric-application-upgrade.md).

## <a name="add-a-service-tooyour-service-fabric-application"></a>Hizmet tooyour Service Fabric uygulaması ekleyin
Yeni hizmetler tooyour uygulama tooextend işlevselliğini ekleyebilirsiniz.  Merhaba hizmeti uygulama paketinizi bulunur tooensure eklemek hello hizmeti hello aracılığıyla **yeni Fabric hizmeti...**  menü öğesi.

![Yeni bir Service Fabric hizmeti ekleyin][newservice]

Bir Service Fabric proje türü tooadd tooyour uygulaması'nı seçin ve hello hizmeti için bir ad belirtin.  Bkz: [hizmetiniz için bir çerçeve seçme](service-fabric-choose-framework.md) hangi hizmet karar toohelp toouse yazın.

![Bir Service Fabric hizmeti proje türü tooadd tooyour uygulamasını seçin][addserviceproject]

Merhaba yeni hizmet tooyour çözümü ve mevcut uygulama paketi eklenir. Merhaba hizmeti başvuruları ve varsayılan hizmet örneği eklenen toohello uygulama bildirimi olacaktır, neden hello hizmet toobe oluşturulan ve hello başlattığınızda hello uygulamayı dağıtmak başlatıldı.

![Merhaba yeni hizmet tooyour uygulama bildirimi eklenir][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a>Service Fabric uygulamanızı paketleme
toodeploy hello uygulama ve kendi Hizmetleri tooa küme, toocreate bir uygulama paketi gerekir.  Merhaba paket hello uygulama bildirimi, hizmet bildirimlerini ve diğer gerekli dosyaları belirli bir düzende düzenler.  Visual Studio ayarlayan ve hello 'pkg' dizini için hello uygulama projenin klasöründe hello paketini yönetir.  Tıklatarak **paket** hello gelen **uygulama** bağlam menüsü oluşturur veya güncelleştirmeleri hello uygulama paketi.

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a>Uygulamalar ve uygulama türleri bulut Gezgini'ni kullanarak kaldırma
Merhaba başlatabilirsiniz bulut Gezgini'ni kullanarak Visual Studio içinden temel küme yönetim işlemlerini gerçekleştirebilirsiniz **Görünüm** menüsü. Örneğin, uygulamaları silin ve yerel veya uzak kümelerde uygulama türleri sağlamasını.

![Bir uygulamayı kaldırma][removeapplication]

> [!TIP]
> Daha zengin küme yönetim işlevselliği için bkz: [Service Fabric Explorer ile kümenizi görselleştirme](service-fabric-visualizing-your-cluster.md).
>
>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Sonraki adımlar
* [Service Fabric uygulama modeli](service-fabric-application-model.md)
* [Service Fabric uygulama dağıtımı](service-fabric-deploy-remove-applications.md)
* [Birden çok ortamlar için uygulama parametreleri yönetme](service-fabric-manage-multiple-environment-app-configuration.md)
* [Service Fabric uygulamanızı hata ayıklama](service-fabric-debugging-your-application.md)
* [Service Fabric Explorer kullanarak kümenizi Görselleştirme](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png