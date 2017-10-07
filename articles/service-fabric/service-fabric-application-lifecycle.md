---
title: "Service Fabric aaaApplication çevriminin | Microsoft Docs"
description: "Geliştirme, dağıtma, test, yükseltme, koruma ve Service Fabric uygulamaları kaldırma açıklar."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 08837cca-5aa7-40da-b087-2b657224a097
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/14/2017
ms.author: ryanwi
ms.openlocfilehash: 36cd6081010e83cb8226c8f85d1e912ac9eebd00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-lifecycle"></a>Service Fabric uygulama yaşam döngüsü
Diğer platformlar ile Azure Service Fabric bir uygulamada genellikle aşamaları aşağıdaki hello geçtikçe: tasarım, geliştirme, test, dağıtım, yükseltme, Bakım ve kaldırma. Service Fabric, bulut uygulamalarından geliştirme aşamasından dağıtım, günlük yönetim ve Bakım tooeventual yetkisini hello tam uygulama yaşam döngüsü için birinci sınıf destek sağlar. Merhaba hizmet modeli hello uygulama yaşam döngüsü, bağımsız olarak birçok farklı roller tooparticipate sağlar. Bu makalede hello API'leri genel bir bakış ve hello hello Service Fabric uygulama yaşam döngüsü aşamaları boyunca hello farklı rolleri tarafından nasıl kullanıldıkları sağlar.

Merhaba aşağıdaki Microsoft Virtual Academy video açıklar nasıl toomanage, uygulama yaşam döngüsü:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=My3Ka56yC_6106218965">
<img src="./media/service-fabric-application-lifecycle/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="service-model-roles"></a>Hizmet modeli rolleri
Merhaba hizmet modeli rolü şunlardır:

* **Hizmet Geliştirici**: başka bir amaçla ve hello birçok uygulamada kullanılan modüler ve genel hizmetler geliştirdiği uygulamalarla aynı türde veya farklı tür. Örneğin, bir sıra hizmeti gişe uygulaması (Yardım Masası) veya bir e-ticaret uygulaması (alışveriş sepeti) oluşturmak için kullanılabilir.
* **Uygulama geliştiricisi**: uygulamaları hizmetleri toosatisfy koleksiyonu tümleştirerek belirli özel gereksinimler ya da senaryoları oluşturur. "Örneğin, bir e-ticaret Web sitesi JSON durum bilgisi olmayan ön uç hizmeti," tümleştirmek "Artırma durum bilgisi olan hizmeti" ve "Sırası durum bilgisi olan hizmeti" toobuild auctioning çözümünü.
* **Uygulama Yöneticisi**: kararları hello uygulama yapılandırması (Merhaba yapılandırma şablonu parametreleri doldurma), (tooavailable kaynakları eşleme) dağıtım ve hizmet kalitesi sağlar. Örneğin, bir uygulama Yöneticisi Merhaba uygulaması hello dil yerel (İngilizce hello Amerika Birleşik Devletleri veya için Japonca örneğin Japonya için) karar verir. Farklı bir dağıtılmış uygulama farklı ayarlara sahip olabilir.
* **İşleç**: hello uygulama yapılandırması ve hello Uygulama Yöneticisi tarafından belirtilen gereksinimleri temelinde uygulamaları dağıtır. Örneğin, bir işleç sağlar ve hello uygulama dağıtır ve Azure'da çalıştığını sağlar. İşleçler uygulama sağlık ve performans bilgilerini izlemek ve gerektiği gibi hello fiziksel altyapı sürdürün.

## <a name="develop"></a>Geliştirme
1. A *Hizmet Geliştirici* hizmetlerini hello kullanarak farklı türlerde geliştirir [Reliable Actors](service-fabric-reliable-actors-introduction.md) veya [Reliable Services](service-fabric-reliable-services-introduction.md) programlama modeli.
2. A *Hizmet Geliştirici* bildirimli olarak geliştirilen hello hizmet türlerini bir veya daha fazla kod, yapılandırma ve veri paketlerini oluşan bir hizmet bildirim dosyasında açıklar.
3. Bir *uygulama geliştiricisi* farklı hizmet türlerini kullanarak bir uygulama oluşturur.
4. Bir *uygulama geliştiricisi* bildirimli olarak hello uygulama türü uygulama bildiriminde hello hizmet bildirimlerini hello bağlı Hizmetleri başvuran uygun şekilde geçersiz kılma ve kümesini parametreleştirme tarafından açıklanır farklı yapılandırma ve dağıtım ayarlarını hello bağlı hizmetleri.

Bkz: [Reliable Actors ile çalışmaya başlama](service-fabric-reliable-actors-get-started.md) ve [Reliable Services ile çalışmaya başlama](service-fabric-reliable-services-quick-start.md) örnekleri için.

## <a name="deploy"></a>Dağıtma
1. Bir *Uygulama Yöneticisi* belirlenmek hello uygulama türü tooa belirli uygulama dağıtılan toobe tooa Service Fabric kümesi hello hello uygun parametreleri belirterek **ApplicationType**hello uygulama bildiriminde öğesi.
2. Bir *işleci* karşıya hello kullanarak uygulama paketi toohello küme Image store hello [ **CopyApplicationPackage** yöntemi](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_CopyApplicationPackage_System_String_System_String_System_String_) veya hello [  **Kopya ServiceFabricApplicationPackage** cmdlet](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps). Merhaba uygulama paketi hello uygulama bildirimi ve hizmet paketleri hello koleksiyonunu içerir. Service Fabric uygulamaları hello uygulama paketinden bir Azure blob depolama veya hello Service Fabric sistem hizmeti olabilen hello görüntü deposunda depolanan dağıtır.
3. Merhaba *işleci* hello uygulama türü hello kullanarak hello karşıya yüklenen uygulama paketinden hello hedef kümedeki hazırlar [ **ProvisionApplicationAsync** yöntemi](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_ProvisionApplicationAsync_System_String_System_TimeSpan_System_Threading_CancellationToken_), hello [ **Register-ServiceFabricApplicationType** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/register-servicefabricapplicationtype), veya hello [ **bir uygulama sağlama** REST işlemini](https://docs.microsoft.com/rest/api/servicefabric/provision-an-application).
4. Merhaba uygulaması sağlama sonra bir *işleci* başlatır hello tarafından sağlanan hello parametrelerle uygulama hello *Uygulama Yöneticisi* hello kullanarak [  **CreateApplicationAsync** yöntemi](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_CreateApplicationAsync_System_Fabric_Description_ApplicationDescription_System_TimeSpan_System_Threading_CancellationToken_), hello [ **yeni ServiceFabricApplication** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/new-servicefabricapplication), veya hello [ **oluştur Uygulama** REST işlemini](https://docs.microsoft.com/rest/api/servicefabric/create-an-application).
5. Merhaba uygulama dağıtıldıktan sonra bir *işleci* kullanır hello [ **CreateServiceAsync** yöntemi](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient#System_Fabric_FabricClient_ServiceManagementClient_CreateServiceAsync_System_Fabric_Description_ServiceDescription_System_TimeSpan_System_Threading_CancellationToken_), hello [  **ServiceFabricService yeni** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/new-servicefabricservice), veya hello [ **hizmet oluşturma** REST işlemini](https://docs.microsoft.com/rest/api/servicefabric/create-a-service) toocreate yeni hizmeti örnekleri hello uygulama için temel kullanılabilir hizmet türleri.
6. Merhaba uygulaması hello Service Fabric kümesi şu anda çalışıyor.

Bkz: [bir uygulamayı dağıtmak](service-fabric-deploy-remove-applications.md) örnekleri için.

## <a name="test"></a>Test etme
1. Toohello yerel geliştirme küme veya test kümesi dağıttıktan sonra bir *Hizmet Geliştirici* çalıştırır hello kullanarak yerleşik yük devretme testi senaryosu hello [ **FailoverTestScenarioParameters** ](https://docs.microsoft.com/dotnet/api/system.fabric.testability.scenario.failovertestscenarioparameters#System_Fabric_Testability_Scenario_FailoverTestScenarioParameters) ve [ **FailoverTestScenario** ](https://docs.microsoft.com/dotnet/api/system.fabric.testability.scenario.failovertestscenario#System_Fabric_Testability_Scenario_FailoverTestScenario) sınıfları veya hello [ **Invoke-ServiceFabricFailoverTestScenario** cmdlet'i ](/powershell/module/servicefabric/invoke-servicefabricfailovertestscenario?view=azureservicefabricps). Merhaba yük devretme testi senaryosu belirtilen bir hizmeti hala kullanılabilir ve çalışıyor olduğunu önemli geçişler ve yük devretme işlemlerini tooensure çalışır.
2. Merhaba *Hizmet Geliştirici* çalıştırır hello kullanarak yerleşik chaos testi senaryosu hello sonra [ **ChaosTestScenarioParameters** ](https://docs.microsoft.com/dotnet/api/system.fabric.testability.scenario.chaostestscenarioparameters#System_Fabric_Testability_Scenario_ChaosTestScenarioParameters) ve [  **ChaosTestScenario** ](https://docs.microsoft.com/dotnet/api/system.fabric.testability.scenario.chaostestscenario#System_Fabric_Testability_Scenario_ChaosTestScenario) sınıfları veya hello [ **Invoke-ServiceFabricChaosTestScenario** cmdlet](/powershell/module/servicefabric/invoke-servicefabricchaostestscenario?view=azureservicefabricps). Merhaba chaos testi senaryosu birden çok düğüm, kod paketi ve çoğaltma hataları rastgele hello kümesine uygulanmasını.
3. Merhaba *Hizmet Geliştirici* [hizmeti hizmeti iletişimi testleri](service-fabric-testability-scenarios-service-communication.md) hello küme geçici birincil çoğaltmalara taşıma sınama senaryolarını yazarak.

Bkz: [giriş toohello hata analizi hizmeti](service-fabric-testability-overview.md) daha fazla bilgi için.

## <a name="upgrade"></a>Yükseltme
1. A *Hizmet Geliştirici* hello bağlı Hizmetleri örneği hello uygulamasının güncelleştirir ve/veya hataları düzeltir ve hello hizmet bildirimi yeni bir sürümünü sağlar.
2. Bir *uygulama geliştiricisi* geçersiz kılar ve hello tutarlı Hizmetleri hello yapılandırma ve dağıtım ayarlarının parameterizes ve hello uygulama bildirimi yeni bir sürümünü sağlar. Hello uygulama geliştiricisi sonra hello uygulamasına hello yeni sürümlerini hello hizmet bildirimleri bir araya getirir ve güncelleştirilmiş uygulama paketi hello uygulama türü yeni bir sürümünü sağlar.
3. Bir *Uygulama Yöneticisi* hello uygun parametreleri güncelleştirerek hello hedef uygulamaya hello uygulama türü hello yeni sürümünü içerir.
4. Bir *işleci* karşıya hello güncelleştirilmiş uygulama paketi toohello küme Image store hello kullanarak [ **CopyApplicationPackage** yöntemi](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_CopyApplicationPackage_System_String_System_String_System_String_) veya hello [ **Kopya ServiceFabricApplicationPackage** cmdlet](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps). Merhaba uygulama paketi hello uygulama bildirimi ve hizmet paketleri hello koleksiyonunu içerir.
5. Bir *işleci* hükümleri hello kullanarak hello hedef kümedeki hello uygulamanın yeni sürümü hello [ **ProvisionApplicationAsync** yöntemi](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_ProvisionApplicationAsync_System_String_System_TimeSpan_System_Threading_CancellationToken_), hello [ **Register-ServiceFabricApplicationType** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/register-servicefabricapplicationtype), veya hello [ **bir uygulama sağlama** REST işlemini](https://docs.microsoft.com/rest/api/servicefabric/provision-an-application).
6. Bir *işleci* yükseltmeler hello hedef uygulama toohello yeni sürümü hello kullanarak [ **UpgradeApplicationAsync** yöntemi](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_UpgradeApplicationAsync_System_Fabric_Description_ApplicationUpgradeDescription_System_TimeSpan_System_Threading_CancellationToken_), hello [  **Başlangıç ServiceFabricApplicationUpgrade** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/start-servicefabricapplicationupgrade), veya hello [ **uygulama yükseltme** REST işlemini](https://docs.microsoft.com/rest/api/servicefabric/upgrade-an-application).
7. Bir *işleci* denetimleri hello hello kullanarak yükseltme sürecini [ **GetApplicationUpgradeProgressAsync** yöntemi](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_GetApplicationUpgradeProgressAsync_System_Uri_System_TimeSpan_System_Threading_CancellationToken_), hello [  **Get-ServiceFabricApplicationUpgrade** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricapplicationupgrade), veya hello [ **uygulama yükseltme ilerleme durumunu alma** REST işlemini](https://docs.microsoft.com/rest/api/servicefabric/get-the-progress-of-an-application-upgrade1).
8. Gerekirse, hello *işleci* değiştirir ve hello kullanarak hello geçerli uygulama yükseltmesi hello parametrelerinin yeniden uygular [ **UpdateApplicationUpgradeAsync** yöntemi](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_UpdateApplicationUpgradeAsync_System_Fabric_Description_ApplicationUpgradeUpdateDescription_System_TimeSpan_System_Threading_CancellationToken_), Merhaba [ **güncelleştirme ServiceFabricApplicationUpgrade** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/update-servicefabricapplicationupgrade), veya hello [ **güncelleştirme uygulama yükseltme** REST işlemini](https://docs.microsoft.com/rest/api/servicefabric/update-an-application-upgrade).
9. Gerekirse, hello *işleci* hello kullanarak hello geçerli uygulama yükseltmeyi geri alındığında [ **RollbackApplicationUpgradeAsync** yöntemi](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_RollbackApplicationUpgradeAsync_System_Uri_System_TimeSpan_System_Threading_CancellationToken_), hello [ **Başlangıç ServiceFabricApplicationRollback** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/start-servicefabricapplicationrollback), veya hello [ **geri alma uygulama yükseltme** REST işlemini](https://docs.microsoft.com/rest/api/servicefabric/rollback-an-application-upgrade).
10. Service Fabric hello kullanılabilirliğini bağlı hizmetlerinin kaybetmeden hello kümede çalışan hello hedef uygulama yükseltir.

Merhaba bkz [uygulaması yükseltme Öğreticisi](service-fabric-application-upgrade-tutorial.md) örnekleri için.

## <a name="maintain"></a>Koru
1. İşletim sistemi yükseltildikten ve düzeltme ekleri için Service Fabric hello Azure altyapı tooguarantee hello kümede çalışan tüm hello uygulamaların kullanılabilirliğini ile arabirimleri.
2. Yükseltme ve düzeltme eklerini toohello Service Fabric platform için Service Fabric kendisini hello kümede çalışan hello uygulamalardan herhangi biri kullanılabilirliğini kaybetmeden yükseltir.
3. Bir *Uygulama Yöneticisi* hello eklenmesi veya bir küme düğümünden kaldırılması geçmiş kapasite kullanım verileri ve öngörülen ileri tarihli talebi çözümleme sonra onaylar.
4. Bir *işleci* ekler ve hello tarafından belirtilen düğümleri kaldırır *Uygulama Yöneticisi*.
5. Tooor varolan düğümleri hello kümeden kaldırılmış yeni düğümler eklendiğinde, Service Fabric otomatik olarak yükle-hello küme tooachieve en iyi performans tüm düğümler üzerinde çalışan uygulamalar hello dengeler.

## <a name="remove"></a>Kaldır
1. Bir *işleci* hello kümede çalışan bir hizmeti belirli bir örneği hello tüm uygulama hello kullanarak kaldırmadan silebilirsiniz [ **DeleteServiceAsync** yöntemi](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient#System_Fabric_FabricClient_ServiceManagementClient_DeleteServiceAsync_System_Fabric_Description_DeleteServiceDescription_System_TimeSpan_System_Threading_CancellationToken_) , hello [ **Kaldır ServiceFabricService** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/remove-servicefabricservice), veya hello [ **hizmet silme** REST işlemini](https://docs.microsoft.com/rest/api/servicefabric/delete-a-service).  
2. Bir *işleci* uygulama örneğini ve tüm hizmetlerinin hello kullanarak silebilirsiniz [ **DeleteApplicationAsync** yöntemi](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_DeleteApplicationAsync_System_Fabric_Description_DeleteApplicationDescription_System_TimeSpan_System_Threading_CancellationToken_), hello [ **Kaldır ServiceFabricApplication** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/remove-servicefabricapplication), veya hello [ **uygulama Sil** REST işlemini](https://docs.microsoft.com/rest/api/servicefabric/delete-an-application).
3. Merhaba uygulama ve Hizmetleri durdurduktan sonra hello *işleci* hello uygulama türü hello kullanarak sağlamasını [ **UnprovisionApplicationAsync** yöntemi](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_UnprovisionApplicationAsync_System_String_System_String_System_TimeSpan_System_Threading_CancellationToken_), Merhaba [ **Unregister-ServiceFabricApplicationType** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/unregister-servicefabricapplicationtype), veya hello [ **uygulama sağlamasını** REST işlemini](https://docs.microsoft.com/rest/api/servicefabric/unprovision-an-application). Sağlama geri alınıyor hello uygulama türü hello uygulama paketi görüntü hello kaldırmaz. Merhaba uygulama paketini el ile kaldırmanız gerekir.
4. Bir *işleci* kaldırır hello uygulama paketinden hello hello kullanarak görüntü [ **RemoveApplicationPackage** yöntemi](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_RemoveApplicationPackage_System_String_System_String_) veya hello [ **Kaldır ServiceFabricApplicationPackage** cmdlet](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps).

Bkz: [bir uygulamayı dağıtmak](service-fabric-deploy-remove-applications.md) örnekleri için.

## <a name="next-steps"></a>Sonraki adımlar
Geliştirme hakkında daha fazla bilgi için test ve Service Fabric uygulamaları ve Hizmetleri yönetme bakın:

* [Reliable Actors](service-fabric-reliable-actors-introduction.md)
* [Reliable Services](service-fabric-reliable-services-introduction.md)
* [Bir uygulamayı dağıtma](service-fabric-deploy-remove-applications.md)
* [Uygulama yükseltme](service-fabric-application-upgrade.md)
* [Test Edilebilirlik genel bakış](service-fabric-testability-overview.md)
