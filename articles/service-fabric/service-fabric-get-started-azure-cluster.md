---
title: "Azure Service Fabric kümesi aaaSet | Microsoft Docs"
description: "Hızlı başlangıç- Azure’da bir Windows veya Linux Service Fabric kümesi oluşturun."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 13c60e293d19d607bb41ee4859706508c219a833
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a>Azure’da ilk Service Fabric kümenizi oluşturma
[Service Fabric kümesi](service-fabric-deploy-anywhere.md), mikro hizmetlerin dağıtılıp yönetildiği, ağa bağlı bir sanal veya fiziksel makine kümesidir. Bu hızlı başlangıç toocreate hello Windows veya Linux çalıştıran beş düğümlü bir küme, yardımcı [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) veya [Azure portal](http://portal.azure.com) yalnızca birkaç dakika içinde.  

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.


## <a name="use-hello-azure-portal"></a>Hello Azure portalını kullanın

Azure Portalı ' toohello oturum [http://portal.azure.com](http://portal.azure.com).

### <a name="create-hello-cluster"></a>Merhaba kümesi oluşturma

1. Merhaba tıklatın **yeni** düğmesi hello sol üst köşesinin hello Azure portalı üzerinde bulunamadı.
2. Seçin **işlem** hello gelen **yeni** dikey ve ardından **Service Fabric kümesi** hello gelen **işlem** dikey.
3. Service Fabric Hello dolgu **Temelleri** formu. İçin **işletim sistemi**seçin Windows veya Linux istediğiniz küme düğümleri toorun hello hello sürümü. Merhaba kullanıcı adı ve parola buraya girilen toohello sanal makinede kullanılan toolog olur. **Kaynak grubu** için yeni bir tane oluşturun. Kaynak grubu, Azure kaynaklarının oluşturulup toplu olarak yönetildiği bir mantıksal kapsayıcıdır. İşlem tamamlandığında **Tamam**’a tıklayın.

    ![Küme kurulumu çıktısı][cluster-setup-basics]

4. Merhaba dolgu **küme yapılandırması** formu.  **Düğüm türü sayısı** için "1" değerini girin.

5. Seçin **düğüm türü 1 (birincil)** ve hello doldurun **düğüm türü yapılandırması** formu.  Düğüm türü adı girin ve hello [dayanıklılık katmanı](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) çok "Bronz."  VM boyutunu seçin.

    Bu tür VM'ler için diğer ayarları hello ve hello VM boyutu, VM'ler, özel uç noktaları, düğüm türleri tanımlayın. Tanımlanan her bir düğüm türünde kullanılan toodeploy ve yönetilen sanal makineleri bir küme olarak olan ayrı sanal makine ölçek kümesi olarak ayarlanır. Her düğüm türünün ölçeği birbirinden bağımsız olarak artırılabilir veya azaltılabilir, her düğüm türünde farklı bağlantı noktası kümeleri açık olabilir ve farklı kapasite ölçümleri yapılabilir.  Merhaba ilk ya da birincil düğüm türü burada Service Fabric Sistem Hizmetleri barındırılır ve beş veya daha fazla VM olmalıdır ' dir.

    Herhangi bir üretim dağıtımı için [kapsite planlaması](service-fabric-cluster-capacity.md) önemli bir adımdır.  Ancak, bu hızlı başlangıçta uygulama çalıştırmadığınız için bir *DS1_v2 Standart* VM boyutu seçin.  Merhaba "Gümüş" seçin [güvenilirlik katmanı](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) ve bir ilk sanal makine ölçek kümesi kapasitesi 5.  

    Merhaba küme üzerinde çalışan uygulamalar ile bağlantı kurabilmesi için özel uç noktaları hello Azure yük dengeleyici bağlantı noktalarını açın.  Yukarı bağlantı noktası 80 ve 8172 "80, 8172" tooopen girin.

    Merhaba denetleme **Gelişmiş ayarları Yapılandır** TCP/HTTP yönetim uç noktaları, uygulama bağlantı noktası aralıkları özelleştirmek için kullanılan kutusunu [kısıtlamalarından](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), ve [kapasitesi Özellikler](service-fabric-cluster-resource-manager-metrics.md).    

    **Tamam**’ı seçin.

6. Merhaba, **küme yapılandırması** formunda, ayarlamak **tanılama** çok**üzerinde**.  Bu Hızlı Başlangıç, tooenter herhangi gerekmez [ayarı doku](service-fabric-cluster-fabric-settings.md) özellikleri.  İçinde **Fabric sürümü**seçin **otomatik** yükseltme modu böylece Microsoft hello küme çalışan hello doku kodu hello sürümünü otomatik olarak güncelleştirir.  Başlangıç modu çok ayarlamak**el ile** çok istiyorsanız[desteklenen bir sürüm seçin](service-fabric-cluster-upgrade.md) tooupgrade için. 

    ![Düğüm türü yapılandırması][node-type-config]

    **Tamam**’ı seçin.

7. Merhaba dolgu **güvenlik** formu.  Bu hızlı başlangıç için **Güvenli olmayan**’ı seçin.  Yüksek oranda olan herkes anonim olarak tooan güvenli olmayan küme bağlanabilir ve yönetim işlemleri beri toocreate üretim iş yükleri için güvenli bir küme ancak önerilir.  

    Sertifikaları Service Fabric tooprovide kimlik doğrulama ve şifreleme toosecure içinde kullanılan bir küme ve kendi uygulamalarına çeşitli yönlerini. Sertifikaların Service Fabric’te kullanılmasıyla ilgili daha fazla bilgi için bkz. [Service Fabric kümesi güvenlik senaryoları](service-fabric-cluster-security.md).  Azure Active Directory veya sertifikaları kurma tooset uygulama güvenliği için kullanarak tooenable kullanıcı kimlik doğrulaması [bir Resource Manager şablonu bir küme oluşturmak](service-fabric-cluster-creation-via-arm.md).

    **Tamam**’ı seçin.

8. Gözden geçirme hello Özet.  Toodownload isterseniz hello ayarlarından yerleşik bir Resource Manager şablonu girdiğiniz, seçin **karşıdan şablonu ve parametre**.  Seçin **oluşturma** toocreate hello küme.

    Merhaba oluşturma ilerlemesi hello Bildirimlerde görebilirsiniz. (Hello durum çubuğu, ekranınızın sağ üst hello en yakın hello "zil" simgesine tıklayın.) Tıkladıysanız **PIN tooStartboard** gördüğünüz hello küme oluştururken **Service Fabric kümesi dağıtma** toohello sabitlenmiş **Başlat** Panosu.

### <a name="view-cluster-status"></a>Küme durumunu görüntüleme
Kümenizi oluşturduktan sonra kümenizde hello inceleyebilirsiniz **genel bakış** dikey penceresinde hello portal. Şimdi kümenizi hello kümenin ortak uç noktası ve bağlantı tooService Fabric Explorer dahil olmak üzere hello panosundaki hello ayrıntılarını görebilirsiniz.

![Küme durumu][cluster-status]

### <a name="visualize-hello-cluster-using-service-fabric-explorer"></a>Service Fabric explorer'ı kullanarak hello küme Görselleştirme
[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md), kümenizi görselleştirmek ve uygulamaları yönetmek için iyi bir araçtır.  Service Fabric Explorer hello kümede çalışan bir hizmettir.  Merhaba tıklayarak bir web tarayıcısı kullanarak erişim **Service Fabric Explorer** bağlantı hello kümesinin **genel bakış** hello portalında sayfası.  Merhaba adresini doğrudan hello tarayıcısına girebilirsiniz: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Gezgini](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)

Merhaba küme Panosu uygulama ve düğüm durumu özetini dahil olmak üzere kümenizi genel bir bakış sağlar. Merhaba düğümü görünüm hello küme hello fiziksel düzenini gösterir. Belirli bir düğümde, hangi uygulamalara kod dağıtıldığını denetleyebilirsiniz.

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-toohello-cluster-using-powershell"></a>PowerShell kullanarak toohello kümesine bağlanın
Bu hello küme PowerShell kullanarak bağlanarak çalışıp çalışmadığını denetleyin.  Merhaba ServiceFabric PowerShell modülü ile Merhaba yüklü [Service Fabric SDK](service-fabric-get-started.md).  Merhaba [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet'i bir bağlantı toohello kümesi oluşturur.   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
Bkz: [Bağlan tooa güvenli küme](service-fabric-connect-to-secure-cluster.md) bağlanan tooa kümenin diğer örnekler için. Bağlantı toohello küme sonra hello kullanmak [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay hello küme ve durum bilgilerini her düğüm için düğüm listesi. Her düğüm için **HealthState** değerinin *OK* olması gerekir.

```powershell
PS C:\Users\sfuser> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName     IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- --------     --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     _nodetype1_2 10.0.0.6        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_1 10.0.0.5        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_0 10.0.0.4        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_4 10.0.0.8        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_3 10.0.0.7        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
```

### <a name="remove-hello-cluster"></a>Merhaba küme Kaldır
Service Fabric kümesi diğer Azure kaynaklarını toohello küme kaynağı kendisi ayrıca oluşur. Toocompletely silmek için Service Fabric kümesi tüm kaynakları, yapılan hello toodelete de olması gerekir. Merhaba en basit yolu toodelete hello küme içereceği tükettiği tüm hello kaynakları ise toodelete hello kaynak grubu. Diğer yolları toodelete bir küme veya toodelete bazı (ancak tüm) hello kaynakları bir kaynak grubunda görmek için [bir küme silme](service-fabric-cluster-delete.md)

Hello Azure portalında bir kaynak grubunda Sil:
1. Toodelete istediğiniz toohello Service Fabric kümesi gidin.
2. Merhaba tıklatın **kaynak grubu** hello küme essentials sayfasında adı.
3. Merhaba, **kaynak grubu Essentials** sayfasında, **kaynak grubu Sil** ve bu sayfa toocomplete hello hello kaynak grubunun silinmesi üzerinde hello yönergeleri izleyin.
    ![Merhaba kaynak grubunu silme][cluster-delete]


## <a name="use-azure-powershell-toodeploy-a-secure-cluster"></a>Azure Powershell toodeploy güvenli bir küme kullanın
1. Merhaba karşıdan [Azure Powershell modülü sürüm 4.0 veya üstü](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) makinenizde.

2. Çalışma hello komut aşağıdaki gibi Windows PowerShell penceresini açın. 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    Bir çıkış benzer toohello aşağıdaki görmeniz gerekir.

    ![ps-list][ps-list]

3. Oturum açma tooAzure ve toocreate hello kümenin istediğinizi seçin hello abonelik toowhich

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. Komut toonow aşağıdaki çalışma hello güvenli bir küme oluşturur. Toocustomize hello parametreleri unutmayın. 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also hello name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    Merhaba komutu herhangi bir yere hello ucunda 10 dakika too30 dakika toocomplete gelen alabilir, bir çıktı benzer toohello aşağıdaki almanız gerekir. Merhaba çıktı hello sertifikası, hello olduğu için yüklenen KeyVault hakkında bilgi sahiptir ve burada hello sertifika kopyalanır yerel klasör hello. 

    ![ps-out][ps-out]

5. Merhaba tüm çıktı kopyalayın ve toorefer tooit ihtiyacımız gibi tooa metin dosyasına kaydedin. Merhaba çıktısını bilgisinden hello not edin. 

    - **CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx
    - **CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10
    - **ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080
    - **ClientConnectionEndpointPort** : 19000

### <a name="install-hello-certificate-on-your-local-machine"></a>Merhaba sertifika yerel makinenize yükleyin
  
tooconnect toohello küme hello geçerli kullanıcının (My) kişisel deposuna hello tooinstall hello sertifikası gerekir. 

PowerShell aşağıdaki hello çalıştırın

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\hello name of hello cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

Hazır tooconnect tooyour güvenli küme sunulmuştur.

### <a name="connect-tooa-secure-cluster"></a>Tooa güvenli kümesine bağlanın 

PowerShell komut tooconnect tooa güvenli küme aşağıdaki hello çalıştırın. Merhaba sertifika ayrıntıları kullanılan tooset hello kümesi olan bir sertifika ile eşleşmesi gerekir. 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


Aşağıdaki örnekte gösterildiği hello hello parametreleri tamamlandı: 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

Bağlı ve hello küme sağlıklı olduğundan komut toocheck aşağıdaki hello çalıştırın.

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-tooyour-cluster-from-visual-studio"></a>Visual Studio, uygulamaları tooyour kümenizden yayımlama

Bir Azure küme ayarlama, Visual Studio'dan uygulamaları tooit aşağıdaki hello tarafından yayımlayabilirsiniz [Yayımla tooan küme](service-fabric-publish-app-remote-cluster.md) belge. 

### <a name="remove-hello-cluster"></a>Merhaba küme Kaldır
Bir küme diğer Azure kaynaklarını toohello küme kaynağı kendisi ayrıca oluşur. Merhaba en basit yolu toodelete hello küme içereceği tükettiği tüm hello kaynakları ise toodelete hello kaynak grubu. 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a>Sonraki adımlar
Geliştirme küme ayarlama, hello aşağıdakileri deneyin:
* [Merhaba Portalı'nda güvenli küme oluşturma](service-fabric-cluster-creation-via-portal.md)
* [Şablondan küme oluşturma](service-fabric-cluster-creation-via-arm.md) 
* [PowerShell kullanarak uygulama dağıtma](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
