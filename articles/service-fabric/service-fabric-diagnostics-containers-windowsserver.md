---
title: "aaaAzure Service Fabric kapsayıcıları izleme ve tanılama | Microsoft Docs"
description: "Bilgi nasıl toomonitor ve Microsoft Azure Service Fabric üzerinde OMS'ın kapsayıcıları çözümüyle bağımsızlıklar kapsayıcıları tanılayın."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/10/2017
ms.author: dekapur
ms.openlocfilehash: cd79111cf78b9d76a60d489bb9953587aa06186d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-windows-server-containers-with-oms"></a>Windows Server kapsayıcıları OMS ile izleme

## <a name="oms-containers-solution"></a>OMS kapsayıcıları çözümü

Merhaba Operations Management Suite (OMS) ekip tanılama kapsayıcıları çözüm ve kapsayıcıları için izleme yayımladı. Kendi Service Fabric yanı sıra, bu çözüm Service Fabric bağımsızlıklar harika aracı toomonitor kapsayıcı dağıtımlarını çözümüdür. Aşağıda, hangi hello Pano hello çözümde benzer basit bir örnek verilmiştir:

![Temel OMS Panosu](./media/service-fabric-diagnostics-containers-windowsserver/oms-containers-dashboard.png)

Farklı türde hello OMS günlük analizi aracında sorgulanabilir günlükleri de toplar ve kullanılan toovisualize herhangi bir ölçümleri veya oluşturulan olaylar olabilir. toplanan hello günlük türleri şunlardır:

1. ContainerInventory: kapsayıcı konumunu, adı ve görüntüleri hakkında bilgi gösterir
2. ContainerImageInventory: bilgi kimlikleri veya boyutları dahil olmak üzere, dağıtılan görüntüler hakkında
3. ContainerLog: belirli hata günlüklerini, docker günlükleri (stdout, vb.) ve diğer girişleri
4. ContainerServiceLog: çalıştırılmış docker arka plan programı komutları
5. Perf: kapsayıcı dahil olmak üzere performans sayaçlarını cpu, bellek, ağ trafiğini, disk g/ç ve hello özel ölçümleri makineler ana bilgisayar

Bu makalede hello adımları gerekli tooset kapsayıcı kümeniz için izleme yukarı kapsar. OMS'ın kapsayıcıları çözüm hakkında daha fazla toolearn kullanıma kendi [belgelerine](../log-analytics/log-analytics-containers.md).

## <a name="1-set-up-a-service-fabric-cluster"></a>1. Bir Service Fabric kümesi

Bulunan hello Azure Resource Manager şablonunu kullanarak bir küme oluşturmak [burada](https://github.com/dkkapur/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Sample). Benzersiz bir OMS çalışma ad tooadd emin olun. Bu şablon hello Önizleme'de bir küme oluşturmak toodeploying hizmet üretimde kullanılamaz ve olamaz anlamına tooa farklı Service Fabric sürüm yükseltme dokusu (v255.255) de varsayılan olarak ayarlanır. Bu şablon için toouse karar verirseniz uzun vadeli veya üretim kullanın, hello sürüm tooa kararlı sürüm numarasını değiştirin.

Merhaba küme ayarlandıktan sonra hello uygun sertifika yüklediyseniz ve mümkün tooconnect toohello küme olduğundan emin olun onaylayın.

Kaynak grubunuzun doğru başlık toohello tarafından ayarlandığını onaylayın [Azure portal](https://portal.azure.com/) ve hello dağıtım bulma. Merhaba kaynak grubunun tüm hello Service Fabric kaynakları içeren ve Service Fabric çözüm yanı sıra, bir günlük analizi çözüm de gerekir.

Var olan bir Service Fabric kümesi değiştirmek için:
* Tanılama etkinleştirilmiş olduğunu doğrulayın (Aksi takdirde, aracılığıyla etkinleştirmek [hello sanal makine ölçek kümesi güncelleştirme](/rest/api/virtualmachinescalesets/create-or-update-a-set))
* "Service Fabric Analytics" Çözüm hello Azure Market üzerinden oluşturarak bir OMS çalışma alanı Ekle
* Hello Service Fabric çözüm toopick tablolardaki verileri (WAD tarafından ayarlanır) hello uygun Azure Storage yukarı Hello veri kaynağının küme hello kaynak grubu hello düzenleme
* Merhaba aracısı olarak ekleme bir [uzantısı toohello sanal makine ölçek kümesi](/powershell/module/azurerm.compute/add-azurermvmssextension) PowerShell aracılığıyla veya hello sanal makine ölçek kümesi (yukarıdaki gibi aynı bağlantı, toomodify hello Resource Manager şablonu) güncelleştirme

## <a name="2-deploy-a-container"></a>2. Bir kapsayıcı dağıtma

Merhaba küme hazır olduğundan ve ona erişebildiğinizden emin onayladıktan sonra bir kapsayıcı tooit dağıtın. Merhaba şablon tarafından kümesi olarak toouse hello Önizleme sürümü seçerseniz, Service Fabric'ın yeni docker de keşfedebilirsiniz işlevselliği oluşturun. İlk kez bir kapsayıcı görüntüsü hello aklınızda ayı dağıtılan tooa küme, boyutuna bağlı olarak birkaç dakika toodownload hello görüntü alır.

## <a name="3-add-hello-containers-solution"></a>3. Merhaba kapsayıcılara çözüme ekleyin

İçinde Azure portal Merhaba, kapsayıcıları kaynak oluşturma (altında hello izleme + yönetim kategorisi) Azure Market üzerinden. 

![Kapsayıcıları çözüm ekleme](./media/service-fabric-diagnostics-containers-windowsserver/containers-solution.png)

Merhaba oluşturma adımda bir OMS çalışma ister. Yukarıdaki hello dağıtımı ile oluşturulmuş bir Hello seçin. Bu adım, OMS çalışma kapsayıcıları çözümünüzde ekler ve hello şablon tarafından dağıtılan hello OMS aracısı tarafından otomatik olarak algılanır. Merhaba Aracısı Merhaba kapsayıcılara işlemler hello kümedeki üzerinde veri toplamayı başlatılır ve yaklaşık 10-15 dakika içinde hello çözüm hello Pano yukarıdaki hello görüntüsü olduğu gibi verilerle yukarı hafif görmeniz gerekir.

## <a name="4-next-steps"></a>4. Sonraki adımlar

OMS hello çalışma toomake içinde çeşitli araçları daha kullanışlı, sizin için sunar. Seçenekler toocustomize hello çözüm tooyour gereksinimlerini aşağıdaki hello keşfedin:
- Merhaba ile familiarized [günlük arama ve sorgulama](../log-analytics/log-analytics-log-searches.md) günlük analizi bir parçası olarak sunulan özellikler
- Merhaba OMS Aracısı toopick belirli performans sayaçlarını yukarı yapılandırın (toohello çalışma giriş Git > ayarları > veri > Windows performans sayaçlarını)
- Yukarı OMS tooset yapılandırma [uyarı otomatik](../log-analytics/log-analytics-alerts.md) kuralları tooaid algılama ve tanılama
