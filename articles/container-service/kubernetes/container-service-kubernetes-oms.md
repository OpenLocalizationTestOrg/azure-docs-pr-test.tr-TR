---
title: "aaaMonitor Azure Kubernetes küme - Operations Management | Microsoft Docs"
description: "Microsoft Operations Management Suite kullanarak Azure kapsayıcı hizmeti kümesinde Kubernetes izleme"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: 7474ee1571134ffe43ff8e4041cf5a64f5635bb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a>İzleyici bir Azure kapsayıcı hizmeti kümesi Microsoft Operations Management Suite (OMS)

## <a name="prerequisites"></a>Ön koşullar
Bu kılavuz, sahibi olduğunuzu varsayar [Azure kapsayıcı hizmeti kullanarak Kubernetes küme oluşturulan](container-service-kubernetes-walkthrough.md).

Ayrıca, hello sahibi olduğunuzu varsayar `az` Azure CLI ve `kubectl` araçları yüklü.

Merhaba varsa test edebilirsiniz `az` çalıştırarak yüklü aracı:

```console
$ az --version
```

Merhaba yoksa `az` yüklü, aracı yönergeler vardır [burada](https://github.com/azure/azure-cli#installation).  
Alternatif olarak, kullanabileceğiniz [Azure bulut Kabuk](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), hello olan `az` Azure CLI ve `kubectl` Araçları zaten yüklenmiş.  

Merhaba varsa test edebilirsiniz `kubectl` çalıştırarak yüklü aracı:

```console
$ kubectl version
```

Sahip değilseniz `kubectl` yüklü çalıştırabilirsiniz:
```console
$ az acs kubernetes install-cli
```

kubectl aracına kubernetes anahtarları varsa tootest çalıştırabilirsiniz:
```console
$ kubectl get nodes
```

Merhaba, komut hataları, kubectl aracına tooinstall kubernetes küme anahtarları gerekiyor. Bu komutu aşağıdaki hello ile yapabilirsiniz:
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a>Operations Management Suite (OMS) ile izleme kapsayıcıları

Microsoft Operations Management (OMS) yönetmenize ve şirket içi korumak ve altyapı bulut yardımcı olan Microsoft'un bulut tabanlı BT yönetimi çözümüdür. Kapsayıcı, bir çözümde hello kapsayıcı envanterini görüntüleme, performans ve günlükleri tek bir konumda yardımcı olan OMS günlük analizi çözümüdür. Denetim, merkezi konumda hello günlükleri görüntüleyerek kapsayıcıları sorun giderme ve bir ana bilgisayar üzerindeki fazladan kapsayıcı tüketen gürültülü bulabilirsiniz.

![](media/container-service-monitoring-oms/image1.png)

Kapsayıcı çözüm hakkında daha fazla bilgi için lütfen toothe bakın [kapsayıcı çözüm günlük analizi](../../log-analytics/log-analytics-containers.md).

## <a name="installing-oms-on-kubernetes"></a>OMS Kubernetes üzerinde yükleme

### <a name="obtain-your-workspace-id-and-key"></a>Çalışma alanı kimliği ve anahtarı edinin
Merhaba OMS Aracısı tootalk toohello hizmeti için bir çalışma alanı kimliği ve çalışma alanı anahtarı ile yapılandırılmış toobe gerekir. Hesap tooget hello çalışma alanı kimliği ve anahtarı toocreate bir OMS ihtiyacınız adresindeki <https://mms.microsoft.com>. Lütfen başlangıç adımları toocreate bir hesap izleyin. Merhaba hesabı oluşturulurken tamamladıktan sonra tooobtain kimliği ve anahtarı tıklayarak ihtiyacınız **ayarları**, ardından **bağlı kaynakları**ve ardından **Linux sunucuları**, aşağıda gösterildiği gibi.

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-hello-oms-agent-using-a-daemonset"></a>Bir DaemonSet kullanarak hello OMS aracı yükleme
DaemonSets Kubernetes toorun tarafından kullanılan bir kapsayıcı hello kümedeki her ana bilgisayarda tek bir örneği.
Bunlar izleme aracıları çalıştırmak için mükemmel.

Merhaba işte [DaemonSet YAML dosya](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes). Kaydedin tooa dosya adlı `oms-daemonset.yaml` ve hello yer tutucu değerlerini değiştirme `WSID` ve `KEY` çalışma alanı kimliği ve anahtarı hello dosyasında.

Çalışma alanı kimliği ve anahtarı toohello DaemonSet yapılandırma ekledikten sonra kümenizdeki hello ile Merhaba OMS Aracısı yükleyebilirsiniz `kubectl` komut satırı aracı:

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-hello-oms-agent-using-a-kubernetes-secret"></a>Merhaba OMS Aracısı Kubernetes gizli anahtarı kullanarak yükleme
tooprotect OMS çalışma alanı kimliği ve anahtarı Kubernetes gizli DaemonSet YAML dosyasının bir parçası olarak kullanabilirsiniz.

 - Merhaba komut dosyası, gizli şablon dosyası ve hello DaemonSet YAML dosya kopyalama (gelen [depo](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) ve üzerinde hello olduklarından emin olmak aynı dizin. 
      - Komut dosyası - gizli gen.sh üretiliyor gizli
      - Gizli şablon - gizli template.yaml
   - DaemonSet YAML dosyası - omsagent ds secrets.yaml
 - Merhaba komut dosyasını çalıştırın. Merhaba betik Merhaba OMS çalışma alanı kimliği ve birincil anahtar sorar. Lütfen, Ekle ve çalıştırabilirsiniz şekilde hello betik gizli yaml dosyası oluşturur.   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - Merhaba gizli pod hello aşağıdakini çalıştırarak oluşturun:``` kubectl create -f omsagentsecret.yaml ```
 
   - toocheck, Hello aşağıdaki komutu çalıştırın: 

   ``` 
   root@ubuntu16-13db:~# kubectl get secrets
   NAME                  TYPE                                  DATA      AGE
   default-token-gvl91   kubernetes.io/service-account-token   3         50d
   omsagent-secret       Opaque                                2         1d
   root@ubuntu16-13db:~# kubectl describe secrets omsagent-secret
   Name:           omsagent-secret
   Namespace:      default
   Labels:         <none>
   Annotations:    <none>

   Type:   Opaque

   Data
   ====
   WSID:   36 bytes
   KEY:    88 bytes 
   ```
 
  - Arka plan programı kümesi çalıştırarak, omsagent oluşturma``` kubectl create -f omsagent-ds-secrets.yaml ```

### <a name="conclusion"></a>Sonuç
İşte bu kadar! Birkaç dakika sonra tooyour OMS Pano akan mümkün toosee veriler olmalıdır.
