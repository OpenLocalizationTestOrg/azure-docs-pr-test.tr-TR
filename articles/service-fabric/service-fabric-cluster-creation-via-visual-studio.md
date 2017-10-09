---
title: "Visual Studio kullanarak Service Fabric kümesi aaaSetting | Microsoft Docs"
description: "Service Fabric yukarı tooset nasıl küme Visual Studio'da bir Azure kaynak grubu projesi tarafından oluşturulan Azure Resource Manager şablonu kullanarak açıklar"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: adegeo
editor: 
ms.assetid: bd2c0511-36c9-4828-8dc3-69e4b6a70567
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/21/2017
ms.author: mikhegn
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: adb0dd2169a28b46e832c6f06c998cbed0c473f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a>Visual Studio kullanarak bir Service Fabric kümesi ayarlayın
Bu makalede, Azure Service Fabric yukarı tooset nasıl küme Visual Studio ve Azure Resource Manager şablonu kullanarak açıklanmaktadır. Bir Visual Studio Azure kaynak grubu projesi toocreate hello şablonu kullanacağız. Merhaba şablonu oluşturulduktan sonra dağıtılabilir doğrudan tooAzure Visual Studio'dan. Ayrıca bir komut dosyasından veya sürekli tümleştirme (CI) tesis parçası olarak kullanılabilir.

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a>Bir Azure kaynak grubu projesi kullanarak bir Service Fabric kümesi şablonu oluşturma
tooget başlatıldı, Visual Studio'yu açın ve bir Azure kaynak grubu projesi oluşturun (hello kullanılabilir **bulut** klasörü):

![Seçili Azure kaynak grubu projesi ile yeni proje iletişim kutusu][1]

Bu proje için yeni bir Visual Studio çözümü oluşturun veya varolan bir çözümü tooan ekleyin.

> [!NOTE]
> Hello Azure kaynak grubu projesi hello bulut düğümü altında görmüyorsanız hello Azure SDK'sı yok. Web Platformu yükleyicisi başlatın ([şimdi yüklemek](http://www.microsoft.com/web/downloads/platform.aspx) henüz yapmadıysanız) ve ".NET için Azure SDK'sı" ve Visual Studio sürümünüzle uyumlu yükleme hello sürüm için arama yapın.
> 
> 

Visual Studio hello Tamam düğmesine basın sonra toocreate istediğiniz tooselect hello Resource Manager şablonu ister:

![Azure şablonu iletişim kutusu seçili Service Fabric kümesi şablonla seçin][2]

İsabet hello Tamam düğmesi ve Hello Service Fabric kümesi şablonu yeniden seçin. Merhaba proje ve hello Resource Manager şablonu şimdi oluşturuldu.

## <a name="prepare-hello-template-for-deployment"></a>Merhaba şablonu dağıtımı için hazırlama
Dağıtılan toocreate hello küme Hello şablonudur önce gerekli hello şablon parametreleri için değerler sağlamanız gerekir. Bu parametre değerleri hello salt okunurdur `ServiceFabricCluster.parameters.json` hello dosyasını `Templates` hello kaynak grubu projesi klasörü. Merhaba dosyasını açın ve değerleri aşağıdaki hello sağlayın:

| Parametre adı | Açıklama |
| --- | --- |
| adminUserName |Service Fabric makineler (düğümler) hello yönetici hesabı adı Hello. |
| certificateThumbprint |Merhaba küme korur hello sertifikanın parmak izini hello. |
| sourceVaultResourceId |Merhaba *kaynak kimliği* hello anahtar kasasının hello küme korur hello sertifikanın depolandığı. |
| certificateUrlValue |Merhaba küme güvenlik sertifikası Hello URL'si. |

Merhaba Visual Studio Service Fabric Resource Manager şablonu bir sertifika tarafından korunan güvenli bir küme oluşturur. Bu sertifika hello tarafından tanımlanan üç şablon parametreleri en son (`certificateThumbprint`, `sourceVaultValue`, ve `certificateUrlValue`), ve bunu bulunmalıdır bir **Azure anahtar kasası**. Nasıl toocreate hello küme güvenlik sertifikası ile ilgili daha fazla bilgi için bkz: [Service Fabric kümesi güvenlik senaryoları](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) makalesi.

## <a name="optional-change-hello-cluster-name"></a>İsteğe bağlı: hello küme adını değiştirin
Her Service Fabric kümesi bir adı vardır. Azure'da bir Fabric kümesi oluşturduğunuzda, küme adı (hello Azure bölgesi ile birlikte) belirler hello kümesi için hello etki alanı adı sistemi (DNS) ad. Örneğin, küme adı, `myBigCluster`ve hello yeni küme barındıracak hello kaynak grubu (Azure bölgesi) konumunu hello Doğu ABD, hello kümenin hello DNS adı olacaktır `myBigCluster.eastus.cloudapp.azure.com`.

Varsayılan olarak hello küme adı otomatik olarak oluşturulur ve bir rastgele soneki tooa "Küme" önek ekleyerek benzersiz yapılan. Bu çok kolay toouse hello şablonunun parçası olarak kolaylaştırır bir **sürekli tümleştirme** (CI) sistem. Toouse istiyorsanız, küme, anlamlı tooyou olan bir için belirli bir ad hello hello değerini `clusterName` hello Resource Manager şablonu dosyasındaki değişken (`ServiceFabricCluster.json`) seçilen tooyour adı. Bu dosyada bulunan tanımlanan hello ilk değişkenidir.

## <a name="optional-add-public-application-ports"></a>İsteğe bağlı: genel uygulama bağlantı noktaları ekleme
Dağıtmadan önce toochange hello ortak uygulama bağlantı noktaları için hello küme isteyebilirsiniz. Varsayılan olarak, yalnızca iki ortak TCP bağlantı noktalarını (80 ve 8081) hello şablonu açar. Daha fazla bilgi için uygulamalarınızı gerekiyorsa, hello şablonunda hello Azure yük dengeleyici tanımını değiştirin. Merhaba tanımı hello ana şablon dosyasında depolanan (`ServiceFabricCluster.json`). Bu dosyayı açın ve arama `loadBalancedAppPort`. Her bağlantı noktası üç yapılar ile ilişkilidir:

1. Başlangıç bağlantı noktası için hello TCP bağlantı noktası değeri tanımlayan Şablon değişkeni:
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. A *araştırma* ne sıklıkta ve ne kadar süreyle hello için Azure yük dengeleyici toouse belirli bir hizmet yapı düğümü başarısız olmadan önce bir tooanother üzerinde çalışır. tanımlar. Merhaba araştırmalar hello yük dengeleyici kaynak bir parçasıdır. Merhaba ilk varsayılan uygulama bağlantı noktası için hello araştırma tanımı aşağıda verilmiştir:
   
    ```json
    {
        "name": "AppPortProbe1",
        "properties": {
            "intervalInSeconds": 5,
            "numberOfProbes": 2,
            "port": "[variables('loadBalancedAppPort1')]",
            "protocol": "Tcp"
        }
    }
    ```
3. A *Yük Dengeleme kuralı* , bağlar, birlikte hello bağlantı noktası ve hangi etkinleştirir Yük Dengeleme Service Fabric küme düğümleri kümesi boyunca hello araştırma:
   
    ```json
    {
        "name": "AppPortLBRule1",
        "properties": {
            "backendAddressPool": {
                "id": "[variables('lbPoolID0')]"
            },
            "backendPort": "[variables('loadBalancedAppPort1')]",
            "enableFloatingIP": false,
            "frontendIPConfiguration": {
                "id": "[variables('lbIPConfig0')]"
            },
            "frontendPort": "[variables('loadBalancedAppPort1')]",
            "idleTimeoutInMinutes": 5,
            "probe": {
                "id": "[concat(variables('lbID0'),'/probes/AppPortProbe1')]"
            },
            "protocol": "Tcp"
        }
    }
    ```
   Daha fazla bağlantı noktaları toodeploy toohello küme planlama hello uygulamaları ihtiyacınız varsa, bunları oluşturma ek araştırma ve Yük Dengeleme kuralı tanımlarına göre ekleyebilirsiniz. Hakkında daha fazla bilgi için Resource Manager şablonları aracılığıyla Azure yük dengeleyici ile toowork bkz [bir şablonu kullanarak bir iç yük dengeleyici oluşturmaya başlamak](../load-balancer/load-balancer-get-started-ilb-arm-template.md).

## <a name="deploy-hello-template-by-using-visual-studio"></a>Visual Studio kullanarak Hello şablonu dağıtma
Kaydettiğiniz sonra tüm gerekli parametre değerleri hello`ServiceFabricCluster.param.dev.json` dosya, hazır toodeploy hello şablon ve çalıştığınız Service Fabric kümesi oluşturun. Visual Studio Çözüm Gezgini'nde Hello kaynak grubu projesine sağ tıklayın ve seçin **dağıtma | Yeni dağıtım...** . Gerekirse, Visual Studio hello gösterir, **tooResource grubu dağıtma** tooauthenticate tooAzure soran iletişim kutusunda:

![TooResource Grup iletişim dağıtma][3]

Merhaba iletişim kutusu hello küme ve yeni bir seçenek toocreate hello verir için mevcut bir Resource Manager kaynak grubu seçmenize olanak sağlar. Normal algılama toouse Service Fabric kümesi için farklı bir kaynak grubu sağlar.

Visual Studio hello Dağıt düğmesi isabet sonra tooconfirm hello şablon parametre değerlerini ister. İsabet hello **kaydetmek** düğmesi. Bir parametre kalıcı bir değere sahip değil: hello küme hello yönetici hesabı parolası. Visual Studio için bir tane istediğinde tooprovide bir parola değeri gerekir.

> [!NOTE]
> Azure SDK 2.9 ile başlayarak, Visual Studio okuma parolalardan destekler **Azure anahtar kasası** dağıtımı sırasında. Merhaba şablon parametreleri iletişim kutusunda bu hello fark `adminPassword` parametresi metin kutusunun sağ hello küçük bir "anahtarı" simgesi bulunur. Bu simge hello küme için yönetici parolasını hello olarak tooselect var olan bir anahtar kasası gizliliği sağlar. Yalnızca anahtar kasanızı hello Gelişmiş erişim ilkelerindeki şablon dağıtımı için Azure Resource Manager erişimini etkinleştirmek emin toofirst yapın. 
> 
> 

Merhaba dağıtım işlemi hello Visual Studio çıktı penceresinde hello ilerlemesini izleyebilirsiniz. Merhaba şablon dağıtımı tamamlandıktan sonra yeni küme hazır toouse değil!

> [!NOTE]
> PowerShell hiçbir zaman kullanılan tooadminister Azure şimdi kullandığınız hello makineden olduysa, küçük bir temizlik toodo gerekir.
> 
> 1. Merhaba çalıştırarak scripting PowerShell'i etkinleştirme [ `Set-ExecutionPolicy` ](https://technet.microsoft.com/library/hh849812.aspx) komutu. Geliştirme makineler için "sınırsız" ilke genellikle kabul edilebilir.
> 2. Karar olup olmadığını tooallow tanılama veri koleksiyonundan Azure PowerShell komutlarını ve Çalıştır [ `Enable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619303.aspx) veya [ `Disable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619236.aspx) gerektiği. Bu gereksiz istemleri şablon dağıtımı sırasında kaçının.
> 
> 

Herhangi bir hata varsa, toohello Git [Azure portal](https://portal.azure.com/) ve için dağıtılan açık hello kaynak grubu. Tıklatın **tüm ayarları**, ardından **dağıtımları** hello ayarları dikey penceresinde. Başarısız bir kaynak grubu dağıtım ayrıntılı tanılama bilgisi var. bırakır.

> [!NOTE]
> Service Fabric kümeleri belirli sayıda düğüm toobe toomaintain kullanılabilirliği gerektirir ve durumunu - başvurulan tooas "çekirdek Bakımı" koru İlk yapmadığınız sürece bu nedenle, tüm hello makineler hello kümedeki aşağı güvenli tooshut erişilebilir bir [tam yedekleme, durumunun](service-fabric-reliable-services-backup-restore.md).
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* [Service Fabric kümesi Hello Azure portal kullanarak ayarlama hakkında bilgi edinin](service-fabric-cluster-creation-via-portal.md)
* [Bilgi nasıl toomanage ve Visual Studio kullanarak Service Fabric uygulamaları dağıtma](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
