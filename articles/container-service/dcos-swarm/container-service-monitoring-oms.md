---
title: "aaaMonitor Azure DC/OS kümesi - Operations Management | Microsoft Docs"
description: "Microsoft Operations Management Suite ile Azure kapsayıcı hizmeti DC/OS kümesi izleyin."
services: container-service
documentationcenter: 
author: keikhara
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 11/17/2016
ms.author: keikhara
ms.custom: mvc
ms.openlocfilehash: 0ebfa3ba3cef8f0205b15731b0e91f5b304bc8fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a>Operations Management Suite ile Azure kapsayıcı hizmeti DC/OS kümesi izleme

Microsoft Operations Management Suite (OMS), şirket içi ve bulut altyapınızı yönetmenize ve korumanıza yardımcı olan, Microsoft'un bulut tabanlı BT yönetim çözümüdür. Kapsayıcı, bir çözümde hello kapsayıcı envanterini görüntüleme, performans ve günlükleri tek bir konumda yardımcı olan OMS günlük analizi çözümüdür. Denetim, merkezi konumda hello günlükleri görüntüleyerek kapsayıcıları sorun giderme ve bir ana bilgisayar üzerindeki fazladan kapsayıcı tüketen gürültülü bulabilirsiniz.

![](media/container-service-monitoring-oms/image1.png)

Kapsayıcı çözüm hakkında daha fazla bilgi için lütfen toothe bakın [kapsayıcı çözüm günlük analizi](../../log-analytics/log-analytics-containers.md).

## <a name="setting-up-oms-from-hello-dcos-universe"></a>OMS hello DC/OS universe'ten ayarlama


Bu makalede bir DC/OS ayarladıktan ve basit bir web kapsayıcı uygulamaları hello kümede dağıtmış olan varsayar.

### <a name="pre-requisite"></a>Önkoşul
- [Microsoft Azure aboneliği](https://azure.microsoft.com/free/) -bu ücretsiz alabilirsiniz.  
- Microsoft OMS çalışma Kurulumu - bkz aşağıda "Adım 3"
- [DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) yüklü.

1. Merhaba DC/OS panosunda Universe ve 'aşağıda gösterildiği gibi OMS' araması tıklayın.

![](media/container-service-monitoring-oms/image2.png)

2. **Yükle**'ye tıklayın. Merhaba OMS sürüm bilgilerle yukarı pop görürsünüz ve bir **paket yükleme** veya **gelişmiş yükleme** düğmesi. Tıkladığınızda **gelişmiş yükleme**, hangi müşteri adayları, toohello **OMS belirli yapılandırma özellikleri** sayfası.

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. Burada, tooenter hello sizden istenir `wsid` (OMS çalışma alanı kimliği hello) ve `wskey` (Merhaba OMS birincil anahtar hello çalışma alanı kimliği için). Her iki tooget `wsid` ve `wskey` OMS hesabı toocreate gerek <https://mms.microsoft.com>. Lütfen başlangıç adımları toocreate bir hesap izleyin. Merhaba hesabı oluşturulurken tamamladıktan sonra tooobtain gerekir, `wsid` ve `wskey` tıklayarak **ayarları**, ardından **bağlı kaynakları**ve ardından **Linux sunucuları** , aşağıda gösterildiği gibi.

 ![](media/container-service-monitoring-oms/image5.png)

4. İstediğiniz ve hello 'Gözden geçirin ve yükleyin' düğmesini tıklatın hello numara, OMS örneği seçin. Genellikle, toohave hello sayısının OMS örnekleri eşit toohello Aracısı kümenizdeki sahip VM'in isteyeceksiniz. Linux için OMS aracısının toocollect bilgilerini izleme ve günlük bilgilerini istiyorsa, her bir VM üzerinde tek tek kapsayıcıları yükler gibidir.

## <a name="setting-up-a-simple-oms-dashboard"></a>Basit bir OMS Pano ayarlama

Linux hello VM'ler için hello OMS Aracısı yüklendiğinde sonraki hello OMS Pano yukarı tooset adımdır. Var olan iki yolu toodo bu: OMS portalında veya Azure portalı.

### <a name="oms-portal"></a>OMS portalı 

Toohello OMS portalında oturum (<https://mms.microsoft.com>) ve Git toohello **çözüm Galerisi**.

![](media/container-service-monitoring-oms/image6.png)

Hello olduğunuzda **çözüm Galerisi**seçin **kapsayıcıları**.

![](media/container-service-monitoring-oms/image7.png)

Merhaba kapsayıcı çözüm seçtikten sonra hello OMS Genel Bakış Panosu sayfasında döşeme hello görürsünüz. Alınan hello kapsayıcı verileri dizini oluşturulduktan sonra göreceğiniz hello döşeme çözüm görünümü döşeme hakkında bilgi ile doldurulur.

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a>Azure Portal 

Oturum açma tooAzure portalında <https://portal.microsoft.com/>. Git **Market**seçin **izleme + Yönetim** tıklatıp **bkz tüm**. Yazın `containers` arama. "Kapsayıcıları" Merhaba arama sonuçlarında görürsünüz. Seçin **kapsayıcıları** tıklatıp **oluşturma**.

![](media/container-service-monitoring-oms/image9.png)

Tıkladığınızda **oluşturma**, onu için çalışma alanınızda sorar. Çalışma alanınızı seçin veya bir yoksa yeni bir çalışma alanı oluşturun.

![](media/container-service-monitoring-oms/image10.PNG)

Çalışma alanınızı seçtikten sonra tıklatın **oluşturma**.

![](media/container-service-monitoring-oms/image11.png)

Merhaba OMS kapsayıcı çözüm hakkında daha fazla bilgi için lütfen toothe bakın [kapsayıcı çözüm günlük analizi](../../log-analytics/log-analytics-containers.md).

### <a name="how-tooscale-oms-agent-with-acs-dcos"></a>Nasıl tooscale OMS Aracısı ACS DC/OS ile 

Yüklü toohave OMS Aracısı hello gerçek düğüm sayısı yetersiz gerekir ya da daha fazla VM ekleyerek VMSS ölçekleme durumda hello ölçeklendirme tarafından yapabilirsiniz `msoms` hizmet.

TooMarathon veya hello DC/OS kullanıcı Arabirimi Hizmetleri sekmesine gidin ve düğüm sayınız ölçeklendirin.

![](media/container-service-monitoring-oms/image12.PNG)

Bu hello OMS Aracısı henüz dağıtmadıysanız tooother düğümler dağıtır.

## <a name="uninstall-ms-oms"></a>MS OMS kaldırma

toouninstall MS OMS hello aşağıdaki komutu girin:

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a>Bize bildirin!!!
Neler çalışır? Eksik nedir? Başka ne için bu toobe sizin için yararlı ihtiyacınız var? Konumundaki bize bildirin <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.

## <a name="next-steps"></a>Sonraki adımlar

 Kapsayıcılarınızı, OMS toomonitor ayarladığınız göre[kapsayıcı panonuz bkz](../../log-analytics/log-analytics-containers.md).
