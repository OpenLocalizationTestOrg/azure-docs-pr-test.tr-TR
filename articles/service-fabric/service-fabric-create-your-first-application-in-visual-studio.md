---
title: "C# ile Azure Service Fabric güvenilir hizmet aaaCreate"
description: "Visual Studio ile, Azure Service Fabric üzerinde derlenmiş bir Güvenilir Hizmet uygulaması oluşturun, dağıtım ve hatalarını ayıklayın."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 740c866da6e639219b529fe92ed63cbeaa702a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a>İlk C# Service Fabric durum bilgisi olan reliable services uygulamanızı oluşturma

Bilgi nasıl toodeploy ilk Service Fabric uygulamanızı .NET Windows için yalnızca birkaç dakika içinde. Tamamladığınızda, güvenilir hizmet uygulamasıyla çalışan bir yerel kümeniz olacaktır.

## <a name="prerequisites"></a>Ön koşullar

Başlamadan önce [geliştirme ortamınızı ayarladığınızdan](service-fabric-get-started.md) emin olun. Bu, hello Service Fabric SDK ve Visual Studio 2017 veya 2015 yüklenmesini içerir.

## <a name="create-hello-application"></a>Merhaba uygulaması oluşturma

Visual Studio'yu **yönetici** olarak başlatın.

`CTRL`+`SHIFT`+`N` ile bir proje oluşturun

Merhaba, **yeni proje** iletişim kutusunda, seçin **bulut > Service Fabric uygulaması**.

Ad Merhaba uygulaması **MyApplication** ve basın **Tamam**.

   
![Visual Studio'da yeni proje iletişim kutusu][1]

Service Fabric uygulaması herhangi bir türde hello sonraki iletişim kutusundan oluşturabilirsiniz. Bu Hızlı Başlangıç için **Durum Bilgisi Olan Hizmet**'i seçin.

Ad hello hizmeti **Mystatefulservice'ten** ve basın **Tamam**.

![Visual Studio'da yeni hizmet iletişim kutusu][2]


Visual Studio hello uygulama projesi ve hello durum bilgisi olan hizmet projesi oluşturur ve bunları Çözüm Gezgini'nde görüntüler.

![Durum bilgisi olan hizmeti içeren uygulama oluşturulduktan sonra Çözüm Gezgini][3]

Merhaba uygulama projesi (**MyApplication**) herhangi bir kod doğrudan içermiyor. Bunun yerine, bir dizi hizmet projesine başvuru sağlar. Ayrıca, bunlardan farklı olarak üç tür içerik daha barındırır:

* **Yayımlama profilleri**  
Toodifferent ortamları dağıtmak için profiller.

* **Betikler**  
Uygulamanızı dağıtmak/yükseltmek için PowerShell betiği.

* **Uygulama tanımı**  
Merhaba ApplicationManifest.xml dosyası altında içerir *ApplicationPackageRoot* uygulamanızın birleşim açıklar. İlişkili uygulama parametreleri dosyalarını olan altında *ApplicationParameters*, hangi kullanılan toospecify ortama özel parametreler olabilir. Yayımlama profili dağıtım tooa sırasında belirli bir ortamın hello belirtilen bir uygulama parametre dosyası ilişkili visual Studio seçer.
    
Merhaba hizmet projesi Merhaba içeriğine genel bakış için bkz: [Reliable Services ile çalışmaya başlama](service-fabric-reliable-services-quick-start.md).

## <a name="deploy-and-debug-hello-application"></a>Dağıtma ve hello uygulamanızın hatalarını ayıklama

Artık bir uygulamanız olduğuna göre uygulamayı çalıştırın.

Visual Studio'da basın `F5` hata ayıklama için toodeploy Merhaba uygulaması.

>[!NOTE]
>Merhaba ilk kez çalıştırma ve yerel olarak hello uygulamayı Visual Studio dağıtmak hata ayıklama için yerel bir küme oluşturur. Bu işlem biraz zaman alabilir. Merhaba küme oluşturma durumunu hello Visual Studio çıktı penceresinde görüntülenir.

Merhaba küme hazır olduğunda, uygulamadan hello SDK ile dahil hello yerel küme sistemi Tepsisi Yöneticisi bir bildirim alır.
   
![Yerel küme sistemi tepsisi bildirimi][4]

Bir kez hello uygulama başladığında Visual Studio otomatik olarak hello getirir **Tanılama Olay Görüntüleyicisi'ni**, burada, Hizmetleri'nden izleme çıktısını görebilirsiniz.
   
![Tanılama olayları görüntüleyicisi][5]

Merhaba kullandık durum bilgisi olan hizmet şablonu yalnızca bir sayaç değeri hello artırma gösterir `RunAsync` yöntemi **MyStatefulService.cs**.

Merhaba olayları toosee birini hello düğümü hello kod çalıştığı dahil olmak üzere daha fazla ayrıntı genişletin. Bu durumda, \_Node\_2 genişletilir ancak makinenize göre değişiklik gösterebilir.
   
![Tanılama olayları görüntüleyicisi ayrıntıları][6]

Merhaba yerel küme tek bir makinede barındırılan beş düğüm içerir. Üretim ortamında, her düğüm ayrı fiziksel veya sanal makinelerde barındırılır. Visual Studio hello uygulanması sırasında makine toosimulate hello kaybı hata ayıklayıcı hello aynı saat, hello yerel kümede hello düğümlerinden biri aşağı atalım.

Merhaba, **Çözüm Gezgini** penceresi açık **MyStatefulService.cs**. 

Hello bulur `RunAsync` yöntemi ve hello yönteminin hello ilk satırında bir kesme noktası ayarlama.

![Durum bilgisi olan hizmetin RunAsync yönteminde kesme noktası ayarlama][7]

Merhaba başlatma **Service Fabric Explorer** hello üzerinde sağ tıklanarak aracı **yerel Küme Yöneticisi** sistem tepsisi uygulaması ve **yerel kümeyi Yönet**.

![Hello yerel Küme Yöneticisi ' Service Fabric Explorer'ı başlatın][systray-launch-sfx]

[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) kümenin görsel bir gösterimini sağlar. Dağıtılan uygulamalar tooit hello kümesi ve onu oluşturan fiziksel düğümlerin hello kümesini içerir.

Merhaba sol bölmesinde **küme > düğümler** ve kodunuzun çalıştığı Bul hello düğüm.

Tıklatın **Eylemler > devre dışı bırak (yeniden)** makinenin yeniden başlatılması toosimulate.

![Service Fabric Explorer'da bir düğümü durdurma][sfx-stop-node]

Kısa bir süre içinde isabetini göreceksiniz tooanother yaptığınız işlem bir düğüme sorunsuz bir şekilde hello hesaplama başarısız olarak Visual Studio'da isabet.


Ardından, toohello Tanılama Olayları Görüntüleyicisi dönün ve hello iletileri gözlemleyin. Merhaba olaylar gerçekte farklı bir düğümden geliyor olsa bile hello sayacın artmaya devam.

![Yük devretme sonrası tanılama olayları görüntüleyicisi][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-hello-local-cluster-optional"></a>Merhaba yerel küme (isteğe bağlı) temizleme

Bu yerel kümenin gerçek olduğunu unutmayın. Merhaba hata ayıklayıcı durdurma uygulama örneğinizi kaldırır ve hello uygulama türü kaydını siler. Ancak, hello küme toorun hello arka planda devam eder. Hazır toostop hello yerel küme olduğunuzda, birkaç seçenek vardır.

### <a name="keep-application-and-trace-data"></a>Uygulamayı ve izleme verilerini koruma

Merhaba üzerinde sağ tıklayarak Hello kümeyi kapatın **yerel Küme Yöneticisi** sistem tepsisi uygulaması ve ardından **yerel kümeyi Durdur**.

### <a name="delete-hello-cluster-and-all-data"></a>Merhaba küme ve tüm verileri silme

Merhaba üzerinde sağ tıklayarak Hello kümesini kaldırmak **yerel Küme Yöneticisi** sistem tepsisi uygulaması ve ardından **yerel kümeyi Kaldır**. 

Bu seçeneği seçerseniz, Visual Studio hello küme hello çalıştırma hello uygulama sonraki sefer yeniden. Bir süredir toouse hello yerel küme planlamıyorsanız veya tooreclaim kaynakları gerekiyorsa bu seçeneği belirleyin.

## <a name="next-steps"></a>Sonraki adımlar
[Reliable services](service-fabric-reliable-services-introduction.md) hakkındaki diğer yazıları okuyun.
<!-- Image References -->

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: ./media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: ./media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: ./media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: ./media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
