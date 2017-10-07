---
title: "Service Fabric tek başına Küme dağıtımı hazırlık aaaAzure | Microsoft Docs"
description: "Hello küme yapılandırmasını oluşturma, toobe, bir üretim iş yükü işleme için amacını küme önceki toodeploying olarak kabul ve belgeleri toopreparing hello ortamı ilgili."
services: service-fabric
documentationcenter: .net
author: maburlik
manager: timlt
editor: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 1/17/2017
ms.author: maburlik;chackdan
ms.openlocfilehash: e503c61a64b408af3f22bd75ab02f1c34ac9f380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
<a id="preparemachines"></a>

## <a name="plan-and-prepare-your-service-fabric-standalone-cluster-deployment"></a>Planlama ve Service Fabric tek başına küme dağıtımınızı hazırlama
Merhaba, küme oluşturmadan önce aşağıdaki adımları gerçekleştirin.

### <a name="step-1-plan-your-cluster-infrastructure"></a>Adım 1: küme altyapınızı planlama
Küme toosurvive istediğiniz hataları ne tür hello karar vermem, sahip olduğunuz makinelerde Service Fabric kümesi hakkında toocreate demektir. Örneğin, ayrı güç satırları gerekiyor mu yoksa Internet bağlantıları toothese makineler sağlanan? Ayrıca, bu makinelerin hello fiziksel güvenlik göz önünde bulundurun. Merhaba makineler bulunduğu ve erişim toothem gerek duyan? Bu kararlar yaptıktan sonra (adım 4'e bakın) çeşitli hata etki alanlarını hello makineler toohello mantıksal olarak eşleyebilirsiniz. Üretim kümeleri için planlama hello altyapı test kümeleri için daha daha karmaşıktır.

### <a name="step-2-prepare-hello-machines-toomeet-hello-prerequisites"></a>2. adım: hello makineler toomeet hello Önkoşullar hazırlayın.
Tooadd toohello küme istediğiniz her makine için Önkoşullar:

* En az 16 GB RAM önerilir.
* 40 GB kullanılabilir disk alanı en az önerilir.
* 4 çekirdek veya daha fazla CPU önerilir.
* Bağlantı tooa güvenli ağlar da tüm makineler için.
* Windows Server 2012 R2 veya Windows Server 2016. 
* [.NET framework 4.5.1 veya üzeri](https://www.microsoft.com/download/details.aspx?id=40773), tam yükleme.
* [Windows PowerShell 3.0](https://msdn.microsoft.com/powershell/scripting/setup/installing-windows-powershell).
* Merhaba [RemoteRegistry hizmeti](https://technet.microsoft.com/library/cc754820) tüm hello makinelerde çalışıyor olması gerekir.

Merhaba dağıtma ve hello küme yapılandırma Küme Yöneticisi olmalıdır [yönetici ayrıcalıkları](https://social.technet.microsoft.com/wiki/contents/articles/13436.windows-server-2012-how-to-add-an-account-to-a-local-administrator-group.aspx) hello makinelerinin her biri. Service Fabric’i bir etki alanı denetleyicisine yükleyemezsiniz.

### <a name="step-3-determine-hello-initial-cluster-size"></a>3. adım: hello ilk küme boyutu belirleme
Bir tek başına Service Fabric kümedeki her düğümde hello hizmeti çalışma zamanı dağıtılan ve hello küme üyesi olan doku sahiptir. Tipik bir üretim dağıtımında, yoktur işletim sistemi örneği başına tek bir düğüm (fiziksel veya sanal). Merhaba küme boyutu, iş gereksinimlerinize göre belirlenir. Ancak, üç düğümü (makineler ya da sanal makineleri) en düşük küme boyutunu olması gerekir.
Geliştirme amaçlı verilen makinede birden fazla düğüm olabilir. Bir üretim ortamında Service Fabric fiziksel veya sanal makine başına yalnızca bir düğüm destekler.

### <a name="step-4-determine-hello-number-of-fault-domains-and-upgrade-domains"></a>Adım 4: hello hata etki alanlarının sayısını belirlemek ve etki alanlarını yükseltme
A *hata etki alanı* (FD) hatası fiziksel birimidir ve hello veri merkezlerinde doğrudan ilgili toohello fiziksel altyapısıdır. Hata etki alanı tek hata noktası paylaşan donanım bileşenleri (bilgisayarlar, anahtarları, ağlar ve daha fazla) oluşur. Hata etki alanları ve raflarının arasında 1:1 eşleme olsa da, geniş konuşarak, her bir rafa hata etki alanı kabul edilebilir. Kümenizdeki düğümlerin Hello değerlendirirken hello düğümleri arasında en az üç hata etki alanlarını dağıtılması önerilir.

ClusterConfig.json içinde FDs belirttiğinizde, her FD için hello ad seçebilirsiniz. Service Fabric hiyerarşik FDs destekler, bu nedenle altyapı topolojinizi bunlara yansıtabilirsiniz.  Örneğin, FDs aşağıdaki hello geçerlidir:

* "faultDomain": "fd: / raf1/Room1/MAKİNE1"
* "faultDomain": "fd: / FD1"
* "faultDomain": "fd: / Room1/raf1/PDU1/M1"

Bir *yükseltme etki alanı* (UD) olan bir mantıksal birim düğümlerinin. Diğer UDs düğümler kullanılabilir tooserve istekleri kalırken Service Fabric bağımsızlıklar yükseltmeleri sırasında (Uygulama yükseltme veya Küme yükseltme), bir UD tüm düğümlerde tooperform hello yükseltme alınır. bunları bir yapmanız gereken şekilde hello makinelerinizi üzerinde gerçekleştirdiğiniz bellenim yükseltmeleri UDs, getirmiyor birer birer makine.

Bu kavramlar hakkında en basit yolu toothink Hello planlanmamış hatası ve UDs planlı bakım hello birimi olarak hello birimi tooconsider FDs gibidir.

ClusterConfig.json içinde UDs belirttiğinizde, her UD için hello ad seçebilirsiniz. Örneğin, adları aşağıdaki hello geçerlidir:

* "upgradeDomain": "UD0"
* "upgradeDomain": "UD1A"
* "upgradeDomain": "DomainRed"
* "upgradeDomain": "Mavi"

Yükseltme etki alanları ve hata etki alanları hakkında daha ayrıntılı bilgi için bkz: [Service Fabric kümesi açıklayan](service-fabric-cluster-resource-manager-cluster-description.md).

### <a name="step-5-download-hello-service-fabric-standalone-package-for-windows-server"></a>5. adım: Windows Server için hello Service Fabric tek başına yükleme paketini indirme
[Bağlantı - Service Fabric tek başına paketi - Windows Server karşıdan](http://go.microsoft.com/fwlink/?LinkId=730690) ve hello paketin sıkıştırmasını açın, ya da tooa dağıtım makine başka bir deyişle hello Küme parçası değil veya tooone hello makinelerin, kümenin bir parçası olur.

### <a name="step-6-modify-cluster-configuration"></a>6. adım: küme yapılandırmasını Değiştir
tek başına küme toocreate hello küme hello belirtimi tanımlayan bir tek başına küme yapılandırması ClusterConfig.json dosyası, toocreate sahip. Merhaba yapılandırma dosyası hello bağlantı aşağıda bulunan hello şablonları temel alabilir. <br>
[Tek başına küme yapılandırmaları](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

Bu dosyadaki hello bölümleri hakkında daha fazla bilgi için bkz: [tek başına Windows kümesi için yapılandırma ayarlarını](service-fabric-cluster-manifest.md).

İndirdiğiniz hello paketinden hello ClusterConfig.json dosyalarından birini açın ve ayarlar aşağıdaki hello değiştirin:
| **Yapılandırma ayarı** | **Açıklama** |
| --- | --- |
| **NodeTypes** |Düğüm türleri tooseparate izin Küme düğümlerinizi çeşitli gruplar. Bir küme en az bir NodeType olması gerekir. Bir gruptaki tüm düğümleri ortak özellikleri aşağıdaki hello vardır: <br> **Ad** -hello düğüm türü adı budur. <br>**Uç nokta bağlantı noktaları** - bu çeşitli son bu düğüm türü ile ilişkili noktalarını (bağlantı noktaları) adlandırılır. Bu bildiriminde başka bir şey ile çakışmadığından sürece istiyor ve zaten değil hello makine/VM üzerinde çalışan başka bir uygulama tarafından kullanılmakta olan bağlantı noktası numarası kullanabilirsiniz. <br> **Yerleşim özellikleri** -bunlar kısıtlamalarından hello sistem hizmetleri veya hizmetleriniz için kullandığınız bu düğüm türü için özellikleri açıklar. Bu özellikler için belirli bir düğümün ek meta veri sağlayan kullanıcı tanımlı anahtar/değer çiftleridir. Düğüm özellikleri örnekleri, bir sabit sürücü veya ekran kartı, hello sayısı dağılımı sabit sürücü, çekirdek ve diğer fiziksel özellikler hello düğüm olup olacaktır. <br> **Kapasiteleri** -düğüm kapasiteleri tanımlar hello adı ve belirli bir kaynak miktarı belirli bir düğüme tüketimi için kullanılabilir olduğunu. Örneğin, bir düğümü "MemoryInMb" adlı bir ölçüm için kapasiteye sahip olduğundan ve varsayılan olarak 2048 MB kullanılabilir olduğunu tanımlayabilir. Bu kapasiteleri kaynaklarla hello kullanılabilir tutarlar gerekli sahip belirli miktarda kaynağı gerektiren hizmetleri hello düğümlere yerleştirilir çalışma zamanı tooensure sırasında kullanılır.<br>**IsPrimary** - birden fazla NodeType tanımlı olun tek hello değerle tooprimary ayarlanır varsa *doğru*, burada Çalıştır hello Sistem Hizmetleri olduğu. Diğer tüm düğüm türleri toohello değerinin ayarlanması *false* |
| **Düğümler** |Bunlar (düğüm türü, düğüm adı, IP adresi, hata etki alanı ve yükseltme etki alanı hello düğümünün) hello kümesinin parçası olan hello düğümlerinin her biri için hello ayrıntılar verilmektedir. Merhaba makinelerin IP adreslerini burada listelenen gerek toobe oluşturulan hello küme toobe istediğiniz. <br> Merhaba kullanıyorsanız, aynı IP adresi tüm hello düğümler için bir kutusu küme, test amacıyla kullanabileceğiniz oluşturulur. Bir çalıştırma kümeleri üretim iş yükleri dağıtmak için kullanmayın. |

Merhaba küme yapılandırması tüm ayarları yapılandırılmış toohello ortamı aldıktan sonra (adım 7) hello küme ortamında sınanabilir.

<a id="environmentsetup"></a>

### <a name="step-7-environment-setup"></a>7. Adım. Ortam kurulumu

Bir Küme Yöneticisi bir Service Fabric tek başına küme yapılandırdığında, hello ihtiyaçlarını ölçütleri aşağıdaki hello ile ayarlanan toobe ortamıdır: <br>
1. Merhaba küme oluşturma hello kullanıcı düğümleriyle hello küme yapılandırma dosyasında listelenen yönetici düzeyi güvenlik ayrıcalıkları tooall makineler sahip olmalıdır.
2. Her küme düğümü makine yanı sıra hangi hello Küme oluşturulduktan makine gerekir:
* Service Fabric SDK kaldırdınız
* Service Fabric çalışma zamanı modülünün kaldırıldı 
* Merhaba Windows Güvenlik Duvarı hizmetini (mpssvc) etkinleştirdikten
* Merhaba Uzak Kayıt Hizmeti (remoteregistry) etkinleştirdiniz mi
* Dosya Paylaşımı (SMB) etkin
* Gerekli bağlantı noktaları açıldı, küme yapılandırması bağlantı noktalarını temel alarak sahip
* Sahip Windows SMB ve uzak kayıt defteri hizmeti için açılan gerekli bağlantı noktaları: 135 ve 137, 138, 139 ve 445
* Ağ bağlantısı tooone sahip başka bir
3. Hiçbir hello küme düğümü makinenin bir etki alanı denetleyicisi olmalıdır.
4. Dağıtılan hello küme toobe güvenli bir küme ise, Önkoşullar yerleştirin ve hello yapılandırma karşı doğru şekilde yapılandırıldığından bulunan hello gerekli güvenlik doğrulayın.
5. Merhaba küme makineler Internet erişilebilir değilse hello kümesi hello aşağıdaki yapılandırma kümesi:
* Telemetri devre dışı bırak: altında *özellikleri* ayarlamak *"enableTelemetry": yanlış*
* Otomatik yapı sürümü indirme & destek sonuna hello geçerli küme sürümünün dolmak üzere bildirimleri devre dışı bırak: altında *özellikleri* ayarlamak *"fabricClusterAutoupgradeEnabled": yanlış*
* Ağ Internet erişimi sınırlı toowhite listelenen etki alanları, alternatif olarak hello etki alanları aşağıdaki Otomatik yükseltme için gereklidir: go.microsoft.com download.microsoft.com

6. Uygun Service Fabric virüsten koruma Dışlamalar ayarlayın:

| **Virüsten koruma dışlanan dizinler** |
| --- |
| Program Files\Microsoft Service Fabric |
| FabricDataRoot (küme yapılandırmasından) |
| FabricLogRoot (küme yapılandırmasından) |

| **Virüsten koruma hariç tutulan işlemler** |
| --- |
| Fabric.exe |
| FabricHost.exe |
| FabricInstallerService.exe |
| FabricSetup.exe |
| FabricDeployer.exe |
| ImageBuilder.exe |
| FabricGateway.exe |
| FabricDCA.exe |
| FabricFAS.exe |
| FabricUOS.exe |
| FabricRM.exe |
| FileStoreService.exe |

### <a name="step-8-validate-environment-using-testconfiguration-script"></a>8. adım. TestConfiguration komut dosyası kullanarak ortamı doğrula
Merhaba TestConfiguration.ps1 betik hello tek başına paketinde bulunabilir. Bu en iyi yöntemler Çözümleyicisi toovalidate bazı hello ölçütler yukarıdaki kullanılan ve bir küme belirli bir ortamda dağıtılabilir sağlamlık onay toovalidate kullanılmalıdır. Herhangi bir hata varsa, toohello listesi altında bakın [ortam Kurulumu](service-fabric-cluster-standalone-deployment-preparation.md) sorun giderme. 

Bu komut dosyası düğümleriyle hello küme yapılandırma dosyasında listelenen yönetici erişimi tooall hello makinelerin bulunduğu herhangi bir makinede çalıştırılabilir. Bu komut dosyasını çalıştırmak hello makine toobe hello kümesinin parçası yok.

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
Running Best Practices Analyzer...
Best Practices Analyzer completed successfully.


LocalAdminPrivilege        : True
IsJsonValid                : True
IsCabValid                 : True
RequiredPortsOpen          : True
RemoteRegistryAvailable    : True
FirewallAvailable          : True
RpcCheckPassed             : True
NoConflictingInstallations : True
FabricInstallable          : True
Passed                     : True
```

Şu anda bu bağımsız olarak yapılan toobe nedenle bu yapılandırmayı test modül hello güvenlik yapılandırması doğrulamaz.  

> [!NOTE]
> Sürekli olarak iyileştirmeler toomake Bu modülün daha sağlam yapıyoruz, bu nedenle bir hatalı veya eksik olduğunu düşündüğünüz büyük-küçük harf olmayan şu anda yakalanan tarafından TestConfiguration varsa, lütfen aracılığıyla bize bizim [destek kanalları](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).   
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* [Windows Server çalıştıran tek başına kümesi oluşturma](service-fabric-cluster-creation-for-windows-server.md)
