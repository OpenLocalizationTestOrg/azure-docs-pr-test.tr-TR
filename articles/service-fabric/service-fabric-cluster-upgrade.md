---
title: "Azure Service Fabric kümesi aaaUpgrade | Microsoft Docs"
description: "Merhaba Service Fabric kod ve/veya küme güncelleştirme modunda, sertifikaları, uygulama bağlantı noktaları, işletim sistemi yamalarını yapılması ekleme yükseltme ayarı dahil olmak üzere bir Service Fabric kümesi çalıştıran yapılandırma yükseltin ve benzeri. Merhaba yükseltme gerçekleştirildiğinde beklentilerinizin ne?"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 15190ace-31ed-491f-a54b-b5ff61e718db
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/10/2017
ms.author: chackdan
ms.openlocfilehash: 94ac3833ec0810f79de06ecb50f254028fa90408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-an-azure-service-fabric-cluster"></a>Azure Service Fabric kümesi yükseltme
> [!div class="op_single_selector"]
> * [Azure küme](service-fabric-cluster-upgrade.md)
> * [Tek başına küme](service-fabric-cluster-upgrade-windows-server.md)
> 
> 

Tüm modern, upgradability tasarlama anahtar tooachieving uzun vadeli başarı ürününüzün sistemidir. Azure Service Fabric kümesi sahip, ancak kısmen Microsoft tarafından yönetilen bir kaynaktır. Bu makalede, otomatik olarak yönetilir ve ne kendiniz yapılandırabileceğiniz anlatılmaktadır.

## <a name="controlling-hello-fabric-version-that-runs-on-your-cluster"></a>Kümenizde çalışan hello yapı sürümünü denetleme
Microsoft tarafından yayımlanan veya küme toobe istediğiniz desteklenen fabric sürümü seçebileceğiniz gibi yükseltmeler küme tooreceive otomatik dokunuz ayarlayabilirsiniz.

Ayar hello "upgrademode öğesinin" Küme yapılandırmasına hello portal ya da canlı bir küme oluşturma hello zaman Resource Manager veya sonraki bir sürümü kullanılarak tarafından bunu 

> [!NOTE]
> Desteklenen fabric sürümü her zaman çalışması kümenizi emin tookeep olun. Gibi ve biz hello service fabric yeni bir sürümü sunmaktan zaman hello önceki sürümü en az 60 gün o tarihten sonra destek sona ermesi için işaretlenir. Merhaba hello yeni sürümler duyurulur [hello service fabric ekip blogunda](https://blogs.msdn.microsoft.com/azureservicefabric/). Merhaba yeni sürüm kullanılabilir toochoose ise. 
> 
> 

14 gün önceki toohello bitiş hello sürümü kümenizi çalışıyor, sistem durumu olayı, sistem durumu uyarısı kümenizi koyan oluşturulur. tooa desteklenen yapı sürümü'ı yükseltmeden hello küme bir uyarı durumunda kalır.

### <a name="setting-hello-upgrade-mode-via-portal"></a>Portal aracılığıyla hello yükseltme modunu ayarlama
Merhaba kümesi oluştururken hello küme tooautomatic veya el ile ayarlayabilirsiniz.

![Create_Manualmode][Create_Manualmode]

Veya, canlı bir kümede el ile hello kullanarak yönetebileceğiniz deneyimi hello küme tooautomatic ayarlayabilirsiniz. 

#### <a name="upgrading-tooa-new-version-on-a-cluster-that-is-set-toomanual-mode-via-portal"></a>Yükseltme tooa yeni sürüm bir kümede tooManual modu Portalı aracılığıyla ayarlanır.
tooupgrade tooa yeni sürümü, tek toodo ihtiyacınız olan hello kullanılabilir sürüm hello aşağı açılır listeden seçin ve kaydedin. Merhaba Fabric yükseltmesi otomatik olarak koparılan. Merhaba küme sistem durumu ilkeleri (düğüm durumu ve tüm hello hello kümede çalışan uygulamaları hello durumu birleşimi) bağlı tooduring hello yükseltme.

Merhaba küme sistem durumu ilkeleri karşılanmazsa hello yükseltme geri alınır. Bu belge tooread konusunda daha fazla aşağı tooset bu özel sistem durumu ilkeleri. 

Merhaba geri alma sonuçlandı hello sorunları çözümledik. sonra tooinitiate hello yükseltme yeniden öncekiyle aynı adımları aşağıdaki hello tarafından gerekir.

![Manage_Automaticmode][Manage_Automaticmode]

### <a name="setting-hello-upgrade-mode-via-a-resource-manager-template"></a>Resource Manager şablonu aracılığıyla hello yükseltme modunu ayarlama
"Upgrademode öğesinin" yapılandırma toohello Microsoft.ServiceFabric/clusters kaynak tanımı hello ve kümesi hello "clusterCodeVersion" tooone Merhaba, aşağıda gösterildiği gibi desteklenen doku sürümleri ve hello şablonu dağıtmak ekleyin. "Elle" veya "Otomatik" Hello "upgrademode öğesinin" için geçerli değerler şunlardır

![ARMUpgradeMode][ARMUpgradeMode]

#### <a name="upgrading-tooa-new-version-on-a-cluster-that-is-set-toomanual-mode-via-a-resource-manager-template"></a>Resource Manager şablonu aracılığıyla tooManual modunu ayarlama bir kümede tooa yeni sürümüne yükseltme.
Merhaba küme el ile modunda tooupgrade tooa yeni sürümü, olduğunda hello "clusterCodeVersion" tooa desteklenen sürüm değiştirin ve dağıtın. Merhaba dağıtım hello şablonunun hello Fabric yükseltmesi kicks başlayacağı zamana otomatik olarak. Merhaba küme sistem durumu ilkeleri (düğüm durumu ve tüm hello hello kümede çalışan uygulamaları hello durumu birleşimi) bağlı tooduring hello yükseltme.

Merhaba küme sistem durumu ilkeleri karşılanmazsa hello yükseltme geri alınır. Bu belge tooread konusunda daha fazla aşağı tooset bu özel sistem durumu ilkeleri. 

Merhaba geri alma sonuçlandı hello sorunları çözümledik. sonra tooinitiate hello yükseltme yeniden öncekiyle aynı adımları aşağıdaki hello tarafından gerekir.

### <a name="get-list-of-all-available-version-for-all-environments-for-a-given-subscription"></a>Belirli bir aboneliğe için tüm ortamlar için tüm kullanılabilir sürüm listesini al
Çalıştır komutunu aşağıdaki hello ve çıktı benzer toothis almanız gerekir.

"supportExpiryUtc" söyler, zaman belirli bir yayın doluyor veya süresi dolmuş. Merhaba en son sürüm geçerli bir tarih yok - değerine sahip "9999-12-31T23:59:59.9999999", yalnızca başka bir deyişle, hello sona erme tarihi henüz ayarlanmadı.

```REST
GET https://<endpoint>/subscriptions/{{subscriptionId}}/providers/Microsoft.ServiceFabric/locations/{{location}}/clusterVersions?api-version=2016-09-01

Example: https://management.azure.com/subscriptions/1857f442-3bce-4b96-ad95-627f76437a67/providers/Microsoft.ServiceFabric/locations/eastus/clusterVersions?api-version=2016-09-01

Output:
{
                  "value": [
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/5.0.1427.9490",
                      "name": "5.0.1427.9490",
                      "type": "Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.0.1427.9490",
                        "supportExpiryUtc": "2016-11-26T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.0.1427.9490",
                      "name": "5.1.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.1.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.4.1427.9490",
                      "name": "4.4.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "4.4.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Linux"
                      }
                    }
                  ]
                }


```

## <a name="fabric-upgrade-behavior-when-hello-cluster-upgrade-mode-is-automatic"></a>Merhaba Küme yükseltme modu otomatik olduğunda doku yükseltme davranışı
Microsoft hello fabric kod ve Azure bir kümede çalışan yapılandırma bulundurur. Biz gerektiği ölçüde temeline göre otomatik izlenen yükseltme toohello yazılım gerçekleştirin. Bu yükseltme, kod, yapılandırma veya her ikisi de olabilir. Uygulamanız herhangi bir etkisi veya düşük etkili toothese yükseltmeler son yükselmesine emin toomake, biz aşamaları aşağıdaki hello hello yükseltmeleri gerçekleştirin:

### <a name="phase-1-an-upgrade-is-performed-by-using-all-cluster-health-policies"></a>1. Aşama: Tüm küme sistem durumu ilkeleri kullanarak yükseltme gerçekleştirilir
Bu aşamasında, aynı anda tek bir yükseltme etki alanı hello yükseltme devam ve hello kümede çalışan hello uygulamalar toorun herhangi kesinti olmadan devam eder. Merhaba küme sistem durumu ilkeleri (düğüm durumu ve tüm hello hello kümede çalışan uygulamaları hello durumu birleşimi) bağlı tooduring hello yükseltme.

Merhaba küme sistem durumu ilkeleri karşılanmazsa hello yükseltme geri alınır. Daha sonra bir e-posta hello aboneliğin toohello sahibi gönderilir. Merhaba e-posta bilgisinden hello içerir:

* Bildirim biz tooroll geri Küme yükseltme vardı.
* Varsa önerilen düzeltici eylemler.
* Merhaba gün sayısı (biz Aşama 2 yürütme kadar n)

Biz tooexecute hello herhangi bir yükseltmesinin altyapı nedenlerden dolayı başarısız olduysa aynı yükseltme birkaç kez daha deneyin. Merhaba sonra n gün başlangıç tarihi hello e-posta gönderildi, tooPhase 2 ilerlemeden.

Merhaba küme sistem durumu ilkeleri karşılanıyorsa hello yükseltme başarılı olarak kabul ve tam olarak işaretlenmiş. Bu aşamada bu hello ilk yükseltme veya hello yükseltme tekrar bölümlerini hiçbirini sırasında meydana gelebilir. Hiçbir e-posta onayı başarılı bir çalışma yoktur. Bu, çok fazla e-postaların bir e-postayı--bir özel durum toonormal görülmelidir gönderme tooavoid olur. Uygulama kullanılabilirliği etkilemeden hello Küme yükseltme toosucceed çoğunu bekliyoruz.

### <a name="phase-2-an-upgrade-is-performed-by-using-default-health-policies-only"></a>2. Aşama: Yalnızca varsayılan sistem durumu ilkeleri kullanarak yükseltme gerçekleştirilir
Merhaba sistem durumu ilkeleri bu aşamasında, hello hello yükseltme başında sağlıklı uygulama hello sayısı için aynı hello yükseltme işleminin süresi hello hello kalmasını bir şekilde ayarlanır. 1. aşaması, olduğu gibi aynı anda tek bir yükseltme etki alanı hello Aşama 2 Yükseltme devam ve hello kümede çalışan hello uygulamalar toorun herhangi kesinti olmadan devam eder. Merhaba küme durumu (düğüm durumu ve tüm hello kümede çalışan uygulamaları hello hello durumu birleşimi) bağlı toofor hello hello yükseltme süresince ilkelerdir.

Merhaba küme sistem durumu ilkeleri yürürlükte karşılanmazsa hello yükseltme geri alınır. Daha sonra bir e-posta hello aboneliğin toohello sahibi gönderilir. Merhaba e-posta bilgisinden hello içerir:

* Bildirim biz tooroll geri Küme yükseltme vardı.
* Varsa önerilen düzeltici eylemler.
* Merhaba gün sayısı (biz aşama 3 yürütme kadar n)

Biz tooexecute hello herhangi bir yükseltmesinin altyapı nedenlerden dolayı başarısız olduysa aynı yükseltme birkaç kez daha deneyin. Birkaç gün n gün hazır olduğunuzda önce anımsatıcı e-posta gönderilir. Merhaba sonra n gün başlangıç tarihi hello e-posta gönderildi, tooPhase 3 ilerlemeden. size Aşama 2'de göndereceğiz hello e-postaları ciddi alınması ve düzeltici eylemler alınması gerekir.

Merhaba küme sistem durumu ilkeleri karşılanıyorsa hello yükseltme başarılı olarak kabul ve tam olarak işaretlenmiş. Bu aşamada bu hello ilk yükseltme veya hello yükseltme tekrar bölümlerini hiçbirini sırasında meydana gelebilir. Hiçbir e-posta onayı başarılı bir çalışma yoktur.

### <a name="phase-3-an-upgrade-is-performed-by-using-aggressive-health-policies"></a>3. Aşama: Agresif sistem durumu ilkeleri kullanarak yükseltme gerçekleştirilir
Bu sistem durumu ilkeleri bu aşamasında, hello uygulamaları hello durumunu yerine hello yükseltme tamamlanmasından sağlamıştır. Bu aşamada çok az sayıda Küme yükseltme sonlanır. Kümenizi toothis aşaması alırsa, uygulamanızın bozulur ve/veya kullanılabilirlik kaybına olduğunu şansı yoktur.

Benzer toohello diğer iki aşama, aşama 3 yükseltmeler, aynı anda tek bir yükseltme etki alanı geçin.

Merhaba küme sistem durumu ilkeleri karşılanmazsa hello yükseltme geri alınır. Biz tooexecute hello herhangi bir yükseltmesinin altyapı nedenlerden dolayı başarısız olduysa aynı yükseltme birkaç kez daha deneyin. Böylece, destek ve/veya yükseltmeler almayacaksınız bundan sonra hello küme, sabitlenir.

Bu bilgileri içeren bir e-posta toohello abonelik sahibi, hello eylemlerden gönderilir. Tüm küme tooget aşama 3 başarısız olduğu bir duruma bekliyoruz değil.

Merhaba küme sistem durumu ilkeleri karşılanıyorsa hello yükseltme başarılı olarak kabul ve tam olarak işaretlenmiş. Bu aşamada bu hello ilk yükseltme veya hello yükseltme tekrar bölümlerini hiçbirini sırasında meydana gelebilir. Hiçbir e-posta onayı başarılı bir çalışma yoktur.

## <a name="cluster-configurations-that-you-control"></a>Denetim küme yapılandırmaları
Ayrıca toohello özelliği tooset hello Küme yükseltme modu, canlı bir küme üzerinde değiştirebileceğiniz hello yapılandırmalar şunlardır.

### <a name="certificates"></a>Sertifikalar
Yeni ekleyebilir veya sertifikaları hello küme ve istemci hello Portalı aracılığıyla kolayca silebilirsiniz. Çok başvuran[ayrıntılı yönergeler için bu belgenin](service-fabric-cluster-security-update-certs-azure.md)

![Sertifika parmak izlerini hello Azure portal gösteren ekran görüntüsü.][CertificateUpgrade]

### <a name="application-ports"></a>Uygulama bağlantı noktaları
Uygulama bağlantı noktalarını hello düğüm türü ile ilişkili hello yük dengeleyici kaynak özelliklerini değiştirerek değiştirebilirsiniz. Resource Manager PowerShell doğrudan kullanabilirsiniz veya hello portalı kullanabilirsiniz.

bir düğüm türü içindeki tüm sanal makineleri üzerinde yeni bir bağlantı noktası tooopen hello aşağıdaki:

1. Yeni bir araştırma toohello uygun yük dengeleyici ekleyin.
   
    Merhaba portalını kullanarak kümenizi dağıttıysanız hello yük dengeleyici "LB-adının hello kaynak grubu nodetypename-adlı" adlı her düğüm türü için bir tane. Merhaba yük dengeleyici adları yalnızca bir kaynak grubunda benzersiz olduğundan, bunlar için belirli bir kaynak grubu altında arama en iyisidir.
   
    ![Bir araştırma tooa ekleme gösteren ekran görüntüsü yük dengeleyici hello Portalı'nda.][AddingProbes]
2. Yeni bir kural toohello yük dengeleyiciye ekleyin.
   
    Aynı hello önceki adımda oluşturduğunuz hello araştırma kullanarak yük dengeleyici yeni bir kural toohello ekleyin.
   
    ![Yeni bir kural tooa yük dengeleyici hello Portalı'nda ekleniyor.][AddingLBRules]

### <a name="placement-properties"></a>Yerleşim özellikleri
Her hello düğüm türleri için uygulamalarınızda toouse istediğiniz özel yerleşim özellikleri ekleyebilirsiniz. NodeType açıkça eklemeden kullanabileceğiniz varsayılan bir özelliktir.

> [!NOTE]
> Düğüm özellikleri kısıtlamalarından hello kullanımı ile ilgili ayrıntılar için ve nasıl toodefine bunları başvuruda hello Service Fabric kümesi Resource Manager belge "Yerleştirme kısıtlamaları ve düğüm özellikleri" bölümünde toohello üzerinde [açıklayan bilgisayarınızı küme ](service-fabric-cluster-resource-manager-cluster-description.md).
> 
> 

### <a name="capacity-metrics"></a>Kapasite ölçümleri
Her hello düğüm türleri için uygulamaları tooreport yükleme toouse istediğiniz özel kapasite ölçümleri ekleyebilirsiniz. Kapasite ölçümleri tooreport yükü hello kullanımı hakkında daha fazla bilgi için üzerinde toohello Service Fabric kümesi Resource Manager belgeleri başvuran [açıklayan bilgisayarınızı küme](service-fabric-cluster-resource-manager-cluster-description.md) ve [ölçümleri ve yük](service-fabric-cluster-resource-manager-metrics.md).

### <a name="fabric-upgrade-settings---health-polices"></a>Fabric yükseltme ayarları - sistem durumu ilkeleri
Fabric yükseltmesi için özel sistem durumu ilkeleri belirtebilirsiniz. Fabric yükseltmelerinin küme tooAutomatic ayarladıysanız, bu ilkeler uygulanan toohello Aşama 1 hello otomatik fabric yükseltmelerinin alın.
Yükseltmeler, kümeniz için el ile doku ayarladıysanız bu ilkelerin her zaman uygulanacağını sonra hello sistem tookick hello fabric yükseltmesi kümenizdeki kapalı tetikleme yeni bir sürümünü seçin. Merhaba ilkelerini geçersiz kılmaz hello Varsayılanları kullanılır.

Merhaba özel sistem durumu ilkeleri belirtin veya Gelişmiş yükseltme ayarlarını hello seçerek hello "fabric yükseltmesi" dikey penceresinde hello geçerli ayarlarında gözden geçirin. Resim nasıl üzerinde aşağıdaki hello gözden geçirin. 

![Özel sistem durumu ilkeleri yönetme][HealthPolices]

### <a name="customize-fabric-settings-for-your-cluster"></a>Yapı ayarları kümeniz için özelleştirme
Çok başvuran[hizmet doku küme yapı ayarları](service-fabric-cluster-fabric-settings.md) ne ve bunları nasıl özelleştirebilirsiniz.

### <a name="os-patches-on-hello-vms-that-make-up-hello-cluster"></a>İşletim sistemi düzeltme eklerinin hello hello küme olun VM'ler
Çok başvuran[düzeltme eki Orchestration uygulama](service-fabric-patch-orchestration-application.md) dağıtılabilecek, küme tooinstall düzeltme eklerini Windows Update'ten üzerinde hello Hizmetleri kullanılabilir tüm hello zaman tutma orchestrated bir biçimde. 

### <a name="os-upgrades-on-hello-vms-that-make-up-hello-cluster"></a>İşletim sistemi yükseltmeleri hello hello küme olun VM'ler hakkında
Merhaba işletim sistemi görüntüsü hello kümesinin hello sanal makinelerde yükseltmeniz gerekir, aynı anda bir VM yapmalısınız. Sorumlu olduğunuz bu yükseltmeyi--var. şu anda bu Otomasyon.

## <a name="next-steps"></a>Sonraki adımlar
* Bilgi nasıl toocustomize hello bazıları [hizmet doku küme yapı ayarları](service-fabric-cluster-fabric-settings.md)
* Nasıl çok öğrenin[kümenizi ölçeğini](service-fabric-cluster-scale-up-down.md)
* Hakkında bilgi edinin [uygulama yükseltme](service-fabric-application-upgrade.md)

<!--Image references-->
[CertificateUpgrade]: ./media/service-fabric-cluster-upgrade/CertificateUpgrade2.png
[AddingProbes]: ./media/service-fabric-cluster-upgrade/addingProbes2.PNG
[AddingLBRules]: ./media/service-fabric-cluster-upgrade/addingLBRules.png
[HealthPolices]: ./media/service-fabric-cluster-upgrade/Manage_AutomodeWadvSettings.PNG
[ARMUpgradeMode]: ./media/service-fabric-cluster-upgrade/ARMUpgradeMode.PNG
[Create_Manualmode]: ./media/service-fabric-cluster-upgrade/Create_Manualmode.PNG
[Manage_Automaticmode]: ./media/service-fabric-cluster-upgrade/Manage_Automaticmode.PNG
