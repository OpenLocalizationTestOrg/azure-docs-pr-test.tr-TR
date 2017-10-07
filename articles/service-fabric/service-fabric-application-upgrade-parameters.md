---
title: "Uygulama yükseltme: yükseltme parametreleri | Microsoft Docs"
description: "Parametreleri ilgili tooupgrading sistem durumu denetimleri tooperform ve ilkeleri tooautomatically geri hello yükseltme de dahil olmak üzere bir Service Fabric uygulaması açıklar."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a4170ac6-192e-44a8-b93d-7e39c92a347e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: abd0ba48c223be9aa0909c7a0100ba5986430db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-upgrade-parameters"></a>Uygulama yükseltme parametreleri
Bu makalede Azure Service Fabric uygulama yükseltme sırasında hello uygulamak çeşitli parametreleri hello açıklanmaktadır. Merhaba parametreleri hello adı ve hello uygulama sürümünü içerir. Merhaba zaman aşımları ve hello yükseltme sırasında uygulanan sistem durumu denetimlerini denetleme düğmelerini oldukları ve bir yükseltme başarısız olduğunda uygulanması gereken hello ilkeleri belirtin.

<br>

| Parametre | Açıklama |
| --- | --- |
| ApplicationName |Yükseltiliyor hello uygulamanın adı. Örnekler: fabric: / VisualObjects, fabric: / ClusterMonitor |
| TargetApplicationTypeVersion |Yükseltme hedeflerini hello hello uygulama türü sürümü Hello. |
| FailureAction |Merhaba yükseltme başarısız olduğunda Service Fabric tarafından gerçekleştirilen hello eylem. Merhaba uygulaması toohello güncelleştirme öncesi sürüm (rollback) geri alınması veya hello yükseltme hello geçerli yükseltme etki alanında durdurulmuş olabilir. Merhaba ikinci durumda, hello yükseltme de değiştirilen tooManual moddur. Geri alma ve el ile izin verilen değerleri şunlardır. |
| HealthCheckWaitDurationSec |Service Fabric Merhaba uygulaması hello durumunu değerlendirir önce hello yükselttikten sonra (saniye cinsinden) hello zaman toowait hello yükseltme etki alanında bitirdi. Bu sürenin sağlıklı değerlendirilebilir önce uygulamanın çalıştırılması hello zaman olarak kabul edilebilir. Merhaba sistem durumu denetimi başarılı olursa, toohello sonraki yükseltme etki alanına hello yükseltme işlemi devam eder.  Hello sistem durumu denetimi başarısız olursa, Service Fabric (Merhaba UpgradeHealthCheckInterval) için bir aralığı hello sistem durumu denetimi yeniden denemeden önce yeniden hello HealthCheckRetryTimeout ulaşılana kadar bekler. Merhaba varsayılan ve önerilen değer 0 ise saniyeyi ifade eder. |
| HealthCheckRetryTimeoutSec |Service Fabric hello yükseltme başarısız olarak bildirme önce tooperform sistem durumu değerlendirmesi devam hello süresi (saniye cinsinden). Merhaba, 600 saniye varsayılandır. Bu süre HealthCheckWaitDuration ulaşıldıktan sonra başlar. Bu HealthCheckRetryTimeout içinde Service Fabric hello uygulama sistem durumunun birden fazla sistem durumu denetimi gerçekleştirebilir. Merhaba varsayılan değer 10 dakikadır ve uygulamanız için uygun şekilde özelleştirilmiş. |
| HealthCheckStableDurationSec |Uygulama hello hello süresi (saniye) tooverify taşıma toohello sonraki yükseltme etki alanına önce kararlı olduğundan veya hello Yükseltme tamamlanıyor. Hello sistem durumu denetimi gerçekleştirildikten sonra bu bekleme süresi algılanamadı kullanılan tooprevent değişiklikleri sistem durumu doğru olur. Merhaba varsayılan değer 120 saniye ve uygulamanız için uygun şekilde özelleştirilmiş. |
| UpgradeDomainTimeoutSec |Tek bir yükseltme etki alanına yükseltmek için en uzun süre (saniye cinsinden). Bu zaman aşımı ulaşılırsa hello yükseltme durdurur ve UpgradeFailureAction hello ayarı dayanan devam eder. Merhaba varsayılan değer: hiçbir zaman (sınırsız) ve uygulamanız için uygun şekilde özelleştirilebilir. |
| UpgradeTimeout |Merhaba tüm yükseltme için geçerli bir zaman aşımı (saniye cinsinden). Bu zaman aşımı ulaştıysanız, yükseltme durakları hello ve UpgradeFailureAction tetiklenir. Merhaba varsayılan değer: hiçbir zaman (sınırsız) ve uygulamanız için uygun şekilde özelleştirilebilir. |
| UpgradeHealthCheckInterval |Sistem durumu hello hello sıklığı denetlenir. Bu parametre hello hello ClusterManager bölümünde belirtilen *küme* *bildirim*ve hello yükseltme cmdlet'inin bir parçası olarak belirtilmemiş. Merhaba varsayılan değer 60 saniyedir. |

<br>

## <a name="service-health-evaluation-during-application-upgrade"></a>Uygulama yükseltme sırasında hizmet sistem durumu değerlendirmesi
<br>
Merhaba sistem durumu değerlendirme ölçütleri isteğe bağlıdır. Yükseltme başladığında hello sistem durumu değerlendirme ölçütleri belirtilmezse, Service Fabric hello ApplicationManifest.xml hello Uygulama örneğinin belirtilen hello uygulama sistem durumu ilkeleri kullanır.

<br>

| Parametre | Açıklama |
| --- | --- |
| ConsiderWarningAsError |Varsayılan değer False olur. Merhaba uygulaması için Hello uyarı sistem durumu olayları hello uygulama yükseltmesi sırasında hello durumunu değerlendirilirken hata olarak işler. Uyarı olayları olsa bile hello yükseltme devam edebilmeniz için varsayılan olarak, Service Fabric uyarı sistem durumu olayları toobe hataları (hatalar) değerlendirmez. |
| MaxPercentUnhealthyDeployedApplications |Varsayılan ve önerilen değer: 0. Dağıtılan uygulamalar Hello sayısını belirtin (Merhaba bkz [sistem bölümü](service-fabric-health-introduction.md)), olabilir sağlıksız Merhaba uygulaması sağlıksız olarak değerlendirilir ve başarısız hello yükseltmeden önce. Bu parametre hello uygulama sağlığını hello düğümde tanımlar ve yükseltme sırasında sorunlarını algılamaya yardımcı olur. Genellikle, Merhaba uygulaması hello çoğaltmalarının yük dengeli toohello hello uygulama tooappear sağlıklı, böylece hello yükseltme tooproceed izin veren diğer düğümün alın. Service Fabric, katı MaxPercentUnhealthyDeployedApplications sağlık durumunu belirterek hello uygulama paketle ilgili bir sorun hızla algılayabilir ve başarısız hızlı yükseltme oluşturulmasını sağlamak. |
| MaxPercentUnhealthyServices |Varsayılan ve önerilen değer: 0. Merhaba uygulaması kötü olarak değerlendirilir ve hello yükseltme başarısız olduğunda önce sağlıksız hello uygulama örneğinde Hizmetleri Hello sayısını belirtin. |
| MaxPercentUnhealthyPartitionsPerService |Varsayılan ve önerilen değer: 0. Bölümler Hello sayısını hello hizmet sağlıksız kabul edilmeden önce sağlıksız bir hizmet belirtin. |
| MaxPercentUnhealthyReplicasPerPartition |Varsayılan ve önerilen değer: 0. Merhaba bölüm sağlıksız kabul edilmeden önce sağlıksız bölümünde çoğaltmaları Hello sayısını belirtin. |
| UpgradeReplicaSetCheckTimeout |**Durum bilgisiz hizmet**--tek bir yükseltme etki alanında Service Fabric hello hizmeti ek örneklerini kullanılabilir tooensure çalışır. Merhaba hedef örnek sayısı birden fazla ise, Service Fabric birden fazla örneği toobe kullanılabilir tooa en büyük zaman aşımı değeri bekler. Bu zaman aşımı hello UpgradeReplicaSetCheckTimeout özelliğini kullanarak belirtilir. Merhaba zaman aşımı süresi dolarsa, Service Fabric hizmeti örneklerinin sayısını hello bakılmaksızın hello yükseltme devam eder. Merhaba hedef örnek sayısı ise, Service Fabric beklememek ve hemen hello yükseltme işlemine devam eder. **Durum bilgisi olan hizmet**--tek bir yükseltme etki alanında Service Fabric çoğaltma hello tooensure çalışır bir çekirdek olarak ayarlanmış. Service Fabric tooa en büyük zaman aşımı değerini (Merhaba UpgradeReplicaSetCheckTimeout özelliği tarafından belirtilen), kullanılabilir bir çekirdek toobe bekler. Merhaba zaman aşımı süresi dolarsa, Service Fabric hello yükseltme, çekirdek bağımsız olarak devam eder. Bu ayar kümesi olarak hiçbir zaman (İleri sunulurken sonsuz) ve 900 saniye olan zaman geri alınıyor. |
| ForceRestart |Bir yapılandırma veya veri paketi hello servis kodu güncelleştirmeden güncelleştirirseniz yalnızca hello ForceRestart özelliği tootrue ayarlandıysa hello hizmeti yeniden başlatılır. Merhaba güncelleştirme tamamlandığında, Service Fabric hello hizmeti, yeni bir yapılandırma paketi veya veri paketi kullanılabilir olduğunu bildirir. Merhaba hizmet hello değişiklikleri uygulamak için sorumludur. Gerekirse, hello hizmetini kendisini yeniden başlatabilirsiniz. |

<br>
<br>
Merhaba MaxPercentUnhealthyServices, MaxPercentUnhealthyPartitionsPerService ve MaxPercentUnhealthyReplicasPerPartition ölçütlerini hizmet türü için bir uygulama örneği başına belirtilebilir. Bu parametreleri başına hizmet ayarı için bir uygulama toocontain farklı Hizmetleri farklı değerlendirme ilkeleriyle türlerine izin verir. Örneğin, bir durum bilgisi olmayan ağ geçidi hizmet türü belirli uygulama örneği için bir durum bilgisi olan Altyapısı hizmeti türünden farklı bir MaxPercentUnhealthyPartitionsPerService sahip olabilir.

## <a name="next-steps"></a>Sonraki adımlar
[Uygulama kullanarak Visual Studio yükseltme](service-fabric-application-upgrade-tutorial.md) Visual Studio kullanarak bir uygulama yükseltme yol gösterir.

[Uygulama Powershell kullanarak yükseltme](service-fabric-application-upgrade-tutorial-powershell.md) PowerShell kullanarak bir uygulama yükseltme yol gösterir.

[Linux'ta Service Fabric CLI kullanarak uygulamanızı yükseltme](service-fabric-application-lifecycle-sfctl.md#upgrade-application) Service Fabric CLI kullanarak bir uygulama yükseltme yoluyla anlatılmaktadır.

[Service Fabric Eclipse eklentisi kullanarak uygulamanızı yükseltme](service-fabric-get-started-eclipse.md#upgrade-your-service-fabric-java-application)

Uygulama yükseltme öğrenme tarafından uyumlu hale getirmek nasıl toouse [veri seri hale getirme](service-fabric-application-upgrade-data-serialization.md).

Uygulamanız çok başvurarak yükseltirken toouse işlevselliği nasıl Gelişmiş öğrenin[Gelişmiş konular](service-fabric-application-upgrade-advanced.md).

Toohello adımlarda başvurarak uygulama yükseltmeleri sık karşılaşılan sorunları düzeltmek [sorun giderme uygulama yükseltmelerini](service-fabric-application-upgrade-troubleshooting.md).
