---
title: "aaaAzure kapsayıcı örnekleri ve kapsayıcı düzenleme"
description: "Azure kapsayıcı örnekleri kapsayıcı orchestrators ile nasıl etkileşim anlama"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 69a39edc6f14d885c1ac300990ed1399002ccfee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a>Azure kapsayıcı örnekleri ve kapsayıcı orchestrators

Kendi küçük boyutu ve uygulama yönlendirme nedeniyle kapsayıcıları Çevik teslim ortamları ve mikro hizmet tabanlı mimariler için uygundur. Başlangıç görevini otomatikleştirmek ve çok sayıda kapsayıcıları ve nasıl etkileşim kurduklarını yönetme olarak bilinir *orchestration*. Popüler kapsayıcı orchestrators dahil Kubernetes, DC/OS ve tümü hello kullanılabilir Docker Swarm, [Azure kapsayıcı hizmeti](https://docs.microsoft.com/azure/container-service/).

Bazı zamanlama özellikleri orchestration platformlarının temel hello Azure kapsayıcı örnekleri sağlar, ancak bu platformlar sağlar ve hatta bunları tamamlayıcı olabilir hello yüksek değerli hizmetleri kapsamaz. Bu makalede hello kapsamını ne Azure kapsayıcı örnekleri işler ve kapsayıcı orchestrators ile nasıl tam etkileşebilir açıklanmaktadır.

## <a name="traditional-orchestration"></a>Geleneksel düzenleme

orchestration standart tanımını Hello hello aşağıdaki görevleri içerir:

- **Zamanlama**: verilen bir kapsayıcı görüntüsü ve bir kaynak isteği, hangi toorun hello kapsayıcısı üzerinde uygun bir makine bulunamadı.
- **Benzeşim/Anti-affinity**: kapsayıcıları bir dizi diğer (performans için) yakındaki veya yeterince kadar parçalayın (kullanılabilirlik için) çalışması gerektiğini belirtmek.
- **Sistem durumu izleme**: kapsayıcı hatalarını ve otomatik olarak izlemek yeniden zamanlayabilirsiniz.
- **Yük devretme**: her makinede çalışan izlemek ve başarısız makineler toohealthy düğümleri kapsayıcılardan yeniden zamanlayın.
- **Ölçeklendirme**: ekleyin veya kapsayıcı örnekleri toomatch isteğe bağlı, el ile veya otomatik olarak kaldırın.
- **Ağ**: birden çok ana bilgisayar makine genelinde kapsayıcıları toocommunicate düzenlemekten bir katman ağ sağlar.
- **Hizmet bulma**: ana makineler arasında taşımak ve IP adreslerini değiştirmek gibi bile kapsayıcıları toolocate birbirine otomatik olarak etkinleştirin.
- **Uygulama yükseltme Eşgüdümlü**: kapsayıcı yükseltmeler tooavoid uygulama kesinti yönetebilir ve bir sorun yaşanırsa geri alma etkinleştirebilir.

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a>Azure kapsayıcı örnekleri düzenlemesini: bir katmanlı yaklaşımın

Tüm hello zamanlama sağlayan bir katmanlı yaklaşımın tooorchestration Azure kapsayıcı örnekleri sağlar ve yönetim özellikleri, orchestrator platformları toomanage çok kapsayıcı görevler, en üstünde olanak tanırken, tek bir kapsayıcı toorun gerekli.

Azure tarafından tüm altyapı kapsayıcı örnekleri için temel alınan hello yönetilir çünkü bir orchestrator platformu hangi toorun uygun ana makinede tek bir kapsayıcı bulma ile tooconcern kendisini gerekmez. bir her zaman kullanılabilir hello bulutun Hello esneklik sağlar. Bunun yerine, hello orchestrator hello geliştirilmesini ölçeklendirme dahil olmak üzere birden çok kapsayıcı mimarileri ve Eşgüdümlü yükseltmeleri basitleştirmek hello görevlerde odaklanabilirsiniz.



## <a name="potential-scenarios"></a>Olası senaryolar

Azure kapsayıcı örnekleri ile orchestrator tümleştirme hala nascent olsa da, birkaç farklı ortamlarda ortaya çıkan düşündüğünüz:

### <a name="orchestration-of-container-instances-exclusively"></a>Orchestration kapsayıcı örneklerinin özel olarak

Hızlı Başlat ve fatura hello tarafından ikinci, özel olarak üzerinde bağlı bir ortam Azure kapsayıcı örnekleri sunar hello en hızlı yolu tooget başlatıldı ve yüksek oranda değişken iş yükleri ile toodeal.

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a>Kapsayıcı örnekleri ve sanal makineleri kapsayıcılarında birleşimi

Uzun süre çalışan için ayrılmış sanal makine bir kümede kapsayıcıları yönetme kararlı iş yükleri, genellikle hello aynı kapsayıcı örnekleriyle çalışan kapsayıcılar daha ucuz olacaktır. Ancak, kapsayıcı örnekleri hızlı bir şekilde genişletme ve beklenmeyen veya kısa süreli ani kullanımı ile genel kapasitesini toodeal daraltılırken için harika bir çözüm sunar. Sanal makine kümenizdeki hello sayısı ölçeğini, yerine daha sonra bu makinelere ek kapsayıcıları dağıtma, hello orchestrator yalnızca hello ek kapsayıcıları kapsayıcı örnekleri kullanılarak zamanlayabilir ve bunlar olduğunuzda silin yok artık gerekli.

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a>Örnek uygulama: Kubernetes için Azure kapsayıcı örnekleri Bağlayıcısı

nasıl kapsayıcı orchestration platformları tümleştirebilir Azure kapsayıcı örnekleriyle toodemonstrate, biz başlatıldı yapı bir [Kubernetes için örnek Bağlayıcısı][aci-connector-k8s]. 

Merhaba Kubernetes taklit için bağlayıcı hello [kubelet] [ kubelet-doc] sınırsız kapasiteye sahip bir düğüm olarak kaydetme ve hello oluşturulmasını göndermeyi [pod'ları] [ pod-doc] Azure kapsayıcı durumlarda kapsayıcı grupları olarak. 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

Diğer orchestrators bağlayıcılarının platform temelleri toocombine hello güç hello orchestrator API'si hello hızı ile ve Azure kapsayıcı örnekleri kapsayıcılarında yönetme Basitlik ile benzer şekilde tümleşik oluşturulabilir.

> [!WARNING]
> Kubernetes için ACI bağlayıcı hello *Deneysel* ve üretimde kullanılmamalıdır.

## <a name="next-steps"></a>Sonraki adımlar

İlk kapsayıcı hello kullanarak Azure kapsayıcı örnekleri ile oluşturmak [Hızlı Başlangıç Kılavuzu](container-instances-quickstart.md).

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/