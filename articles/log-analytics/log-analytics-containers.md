---
title: "aaaContainer Azure günlük analizi izleme çözümüne | Microsoft Docs"
description: "Hello günlük analizi kapsayıcı izleme çözümünde görüntülemenize ve Docker ve Windows yönetmenize yardımcı olur kapsayıcı konakları tek bir konumda."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e1e4b52b-92d5-4bfa-8a09-ff8c6b5a9f78
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte;banders
ms.openlocfilehash: 2eed1dd81c22faef78a375fca3ebece9e5300c09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a>Kapsayıcı izleme çözümüne günlük analizi

![Kapsayıcıları simgesi](./media/log-analytics-containers/containers-symbol.png)

Tooset ayarlama ve kullanma görüntülemenize ve Docker ve Windows yönetmenize yardımcı olan günlük analizi kapsayıcı izleme çözümünde nasıl hello bu makalede tek bir konumda kapsayıcı konakları. Docker olan yazılım sanallaştırma sistemi kullanılan yazılım dağıtım tootheir BT otomatikleştirmek toocreate kapsayıcıları altyapı.

Merhaba, çalışan kapsayıcılar, çalıştırdıkları, hangi kapsayıcı görüntü çözüm gösterir ve kapsayıcıları çalıştırdığı. Kapsayıcılar ile kullanılan komutları gösteren ayrıntılı denetim bilgileri görüntüleyebilirsiniz. Ve görüntüleme ve tooremotely görünümü Docker veya Windows konakları gerek kalmadan merkezi günlükleri arama yaparak kapsayıcıları giderebilirsiniz. Bir ana bilgisayar üzerindeki gürültülü ve alan üst limiti aşan kaynakları olabilir kapsayıcıları bulabilirsiniz. Ve merkezi CPU, bellek, depolama ve ağ kullanımı ve performans bilgilerini kapsayıcıları için görüntüleyebilirsiniz. Windows çalıştıran bilgisayarlarda, merkezileştirme ve Windows Server günlüklerinden karşılaştırmak Hyper-V ve Docker kapsayıcıları. Merhaba çözüm kapsayıcı orchestrators aşağıdaki hello destekler:

- Docker Swarm
- DC/OS
- Kubernetes
- Service Fabric
- Red Hat OpenShift


Merhaba Aşağıdaki diyagramda çeşitli kapsayıcı konakları ve OMS aracılarla arasında hello ilişkiler gösterilmektedir.

![Kapsayıcıları diyagramı](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a>Sistem gereksinimleri

Başlamadan önce hello önkoşulları karşılaması ayrıntıları tooverify aşağıdaki hello gözden geçirin.

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a>Kapsayıcı izleme çözümü desteklemek için Docker Orchestrator ve işletim sistemi platformu
Merhaba aşağıdaki tabloda ana hatlarını Docker düzenleme ve işletim sistemi izleme desteği kapsayıcı envanter, performans ve günlük analizi ile günlükleri hello.   

| | ACS | Linux | Windows | Kapsayıcı<br>Stok | Görüntü<br>Stok | Node<br>Stok | Kapsayıcı<br>Performans | Kapsayıcı<br>Olay | Olay<br>Günlük | Kapsayıcı<br>Günlük |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| Kubernetes | &#8226; | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; |
| Mesosphere<br>DC/OS | &#8226; | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226;| &#8226; | &#8226; | &#8226; |
| Docker<br>Swarm | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |
| Hizmet<br>Yapı | | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; |
| Red Hat Aç<br>Kaydırma | | &#8226; | | &#8226; | &#8226;| &#8226; | &#8226; | &#8226; | | &#8226; |
| Windows Server<br>(tek başına) | | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |
| Linux Sunucu<br>(tek başına) | | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |


### <a name="docker-versions-supported-on-linux"></a>Linux üzerinde desteklenen docker sürümleri

- Docker 1.11 too1.13
- Docker CE ve EE v17.06

### <a name="x64-linux-distributions-supported-as-container-hosts"></a>x64 kapsayıcı konakları olarak desteklenen Linux dağıtımları

- Ubuntu 14.04 LTS ve 16.04 LTS
- CoreOS(stable)
- Amazon Linux 2016.09.0
- openSUSE 13.2
- openSUSE LEAP 42.2
- CentOS 7.2 ve 7.3
- SLES 12
- RHEL 7.2 ve 7.3
- Red Hat OpenShift kapsayıcı Platform (OCP) 3.4 ve 3.5
- ACS Mesosphere DC/OS 1.7.3 too1.8.8
- ACS Kubernetes 1.4.5 too1.6
- ACS Docker Swarm

### <a name="supported-windows-operating-system"></a>Desteklenen Windows işletim sistemi

- Windows Server 2016
- Windows 10 Anniversary Edition (Professional veya Enterprise)

### <a name="docker-versions-supported-on-windows"></a>Windows'da desteklenen docker sürümleri

- Docker 1.12 ve 1.13
- Docker 17.03.0 ve sonraki sürümler

## <a name="installing-and-configuring-hello-solution"></a>Yükleme ve yapılandırma hello çözümü
Bilgi tooinstall aşağıdaki hello kullanın ve hello çözüm yapılandırın.

1. Merhaba kapsayıcı izleme çözümü tooyour OMS çalışma alanından eklemek [Azure Market](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) veya açıklanan hello işlemi kullanarak [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).

2. Yükleyin ve Docker bir OMS Aracısı ile kullanın.  İşletim sistemi temelinde, yöntemleri aşağıdaki hello seçebilirsiniz:

  * Desteklenen Linux işletim sistemlerinde yüklemek ve Docker çalıştırın ve ardından yükleyin ve hello yapılandırın [Linux için OMS aracısının](log-analytics-agent-linux.md).  
  * CoreOS üzerinde Linux için hello OMS Aracısı çalıştırılamıyor. Bunun yerine, Linux için hello OMS Aracısı kapsayıcılı sürümünü çalıştırın. Gözden geçirme [CoreOS dahil olmak üzere Linux kapsayıcı konakları](#for-all-linux-container-hosts-including-coreos) veya [CoreOS dahil olmak üzere Azure kamu Linux kapsayıcı konakları](#for-all-azure-government-linux-container-hosts-including-coreos) Azure Bulutu kapsayıcılarında ile çalışıyorsanız.
  * Windows Server 2016 ve Windows 10, hello Docker altyapısına ve istemcisi yükleme Aracısı toogather bilgi bağlanın ve tooLog Analytics gönderebilirsiniz.  

### <a name="container-services"></a>Kapsayıcı hizmetlerini

- Red Hat OpenShift ortamınız varsa, gözden [bir OMS Aracısı Red Hat OpenShift için yapılandırma](#configure-an-oms-agent-for-red-hat-openshift).
- Hello Azure kapsayıcı hizmeti kullanarak Kubernetes kümeniz varsa, gözden [Microsoft Operations Management Suite (OMS) Azure kapsayıcı hizmeti kümesini izlemek](../container-service/kubernetes/container-service-kubernetes-oms.md).
- Bir Azure kapsayıcı hizmeti DC/OS kümeniz varsa, altında daha fazla bilgi [Operations Management Suite ile Azure kapsayıcı hizmeti DC/OS kümesi izlemek](../container-service/dcos-swarm/container-service-monitoring-oms.md).
- Bir Docker Swarm modu ortamınız varsa, altında daha fazla bilgi [Docker Swarm için bir OMS Aracısı Yapılandırma](#configure-an-oms-agent-for-docker-swarm).
- Service Fabric ile kapsayıcılar kullanıyorsa, hakkında daha fazla bilgi edinin [Azure Service Fabric genel bakış](../service-fabric/service-fabric-overview.md).
- Gözden geçirme hello [Docker altyapısına Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) hakkında ek bilgi için makalenin tooinstall ve Windows çalıştıran bilgisayarlarda, Docker altyapılarını yapılandırın.

> [!IMPORTANT]
> Docker çalıştırmalıdır **önce** hello yüklemek [Linux için OMS aracısının](log-analytics-agent-linux.md) kapsayıcı konaklarda. Docker yüklemeden önce hello Aracısı zaten yüklediyseniz, Linux için tooreinstall hello OMS Aracısı gerekir. Merhaba Docker hakkında daha fazla bilgi için bkz: [Docker Web sitesi](https://www.docker.com).


## <a name="linux-container-hosts"></a>Linux kapsayıcı konakları

Docker yükledikten sonra kapsayıcı konak tooconfigure hello aracınızı Docker ile kullanılmak için ayarları aşağıdaki hello kullanın. Öncelikle, OMS çalışma alanı kimliği ve hello Azure portalında bulabilirsiniz anahtarınızı gerekir. Çalışma alanınızda tıklatın **Hızlı Başlangıç** > **bilgisayarlar** tooview, **çalışma alanı kimliği** ve **birincil anahtar**.  Kopyalayın ve her ikisi de, sık kullanılan düzenleyicisine yapıştırın.

### <a name="for-all-linux-container-hosts-except-coreos"></a>Tüm Linux kapsayıcı ana bilgisayarlar için CoreOS dışında

- Daha fazla bilgi ve nasıl tooinstall hello OMS Aracısı Linux için adımlar için bkz: [, Linux bilgisayarları tooOperations Yönetim Paketi (OMS) bağlantı](log-analytics-agent-linux.md).

### <a name="for-all-linux-container-hosts-including-coreos"></a>CoreOS dahil olmak üzere tüm Linux kapsayıcı ana bilgisayarlar için

Merhaba OMS kapsayıcı toomonitor istediğiniz başlatın. Değiştirin ve aşağıdaki örneğine hello kullanın:

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a>CoreOS dahil olmak üzere tüm Azure kamu Linux kapsayıcı ana bilgisayarlar için

Merhaba OMS kapsayıcı toomonitor istediğiniz başlatın. Değiştirin ve aşağıdaki örneğine hello kullanın:

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-tooone-in-a-container"></a>Bir kapsayıcıda yüklü bir Linux Aracısı tooone kullanarak değiştirme
Daha önce yüklenmiş doğrudan hello Aracısı kullanılan ve isterseniz önce yapmalısınız bir kapsayıcıda çalışan bir aracının tooinstead kullanmak Linux için hello OMS Aracısı kaldırın. Bkz: [kaldırma hello Linux için OMS aracısının](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) nasıl toosuccessfully kaldırma toounderstand hello Aracısı.  

### <a name="configure-an-oms-agent-for-docker-swarm"></a>Docker Swarm için OMS Aracısı'nı yapılandırma

Docker Swarm hakkında genel bir hizmet olarak hello OMS Aracısı çalıştırabilirsiniz. Bilgi toocreate bir OMS Aracısı hizmeti aşağıdaki hello kullanın. Tooinsert OMS çalışma alanı kimliği ve birincil anahtar gerekir.

- Merhaba aşağıdaki hello ana düğümde çalıştırın.

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a>Red Hat OpenShift bir OMS Aracısı'nı yapılandırma
Üç yolu tooadd hello OMS Aracısı tooRed Hat OpenShift toostart kapsayıcı izleme veri toplama vardır.

* [Linux için Hello OMS Aracısı yükleme](log-analytics-agent-linux.md) doğrudan her bir düğümde OpenShift  
* [Log Analytics VM uzantısı etkinleştirmek](log-analytics-azure-vm-extension.md) Azure'da bulunan her bir OpenShift düğümüne  
* Bir OpenShift arka plan programı kümesi olarak Hello OMS Aracısı yükleme  

Bu bölümde biz bir OpenShift arka plan programı kümesi olarak hello adımları gerekli tooinstall hello OMS Aracısı kapsar.  

1. Toohello OpenShift ana düğüm ve kopyalama hello yaml dosya üzerinde oturum [ocp omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) github'dan tooyour ana düğüm ve hello değerini OMS çalışma alanı Kimliğinizi ve birincil anahtarınız ile değiştirin.
2. Aşağıdaki komutları toocreate hello bir proje için OMS çalıştırın ve hello kullanıcı hesabı ayarlayın.

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. toodeploy hello arka plan programı kümesi hello aşağıdakileri çalıştırın:

    `oc create -f ocp-omsagent.yaml`

5. yapılandırıldığı tooverify ve doğru şekilde çalıştığını hello aşağıdakileri yazın:

    `oc describe daemonset omsagent`  

    ve hello çıktı aşağıdakine benzemelidir:

    ```
    [ocpadmin@khm-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

Toouse gizli toosecure OMS çalışma alanı kimliği ve birincil anahtar hello OMS Aracısı arka plan programı kümesi yaml dosyası kullanıldığında isterseniz, hello aşağıdaki adımları gerçekleştirin.

1. Toohello OpenShift ana düğüm ve kopyalama hello yaml dosya üzerinde oturum [ocp ds omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) ve komut dosyası oluşturuluyor gizli [ocp secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) github'dan.  Bu komut dosyası için OMS çalışma alanı kimliği ve birincil anahtar toosecure hello gizli yaml dosyası oluşturur, bilgi secrete.  
2. Aşağıdaki komutları toocreate hello bir proje için OMS çalıştırın ve hello kullanıcı hesabı ayarlayın. komut dosyası oluşturuluyor hello gizli ister OMS çalışma alanı Kimliğiniz için <WSID> ve birincil anahtar <KEY> ve isteğe bağlı olarak tamamlandıktan sonra hello ocp-secret.yaml dosyası oluşturur.  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. Merhaba gizli dosya hello aşağıdakini çalıştırarak dağıtın:

    `oc create -f ocp-secret.yaml`

5. Dağıtım hello aşağıdakini çalıştırarak doğrulayın:

    `oc describe secret omsagent-secret`  

    ve hello çıktı aşağıdakine benzemelidir:  

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

6. Merhaba OMS Aracısı arka plan programı kümesi yaml dosya hello aşağıdakini çalıştırarak dağıtın:

    `oc create -f ocp-ds-omsagent.yaml`  

7. Dağıtım hello aşağıdakini çalıştırarak doğrulayın:

    `oc describe ds oms`

    ve hello çıktı aşağıdakine benzemelidir:

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe secret omsagent-secret  
    Name:           omsagent-secret  
    Namespace:      omslogging  
    Labels:         <none>  
    Annotations:    <none>  

    Type:   Opaque  

     Data  
     ====  
     KEY:    89 bytes  
     WSID:   37 bytes  
    ```

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a>Gizli bilgilerinizi Docker Swarm ve Kubernetes için güvenli

Docker Swarm ve Kubernetes kapsayıcı hizmetlerini için gizli OMS çalışma alanı Kimliğinizi ve birincil anahtarlar güvenliğini sağlayabilirsiniz.

#### <a name="secure-secrets-for-docker-swarm"></a>Docker Swarm için güvenli parolaları

Çalışma alanı kimliği ve birincil anahtar için Hello gizli anahtar oluşturulduktan sonra Docker Swarm için hello çalıştırabilirsiniz OMSagent için hello Docker hizmeti oluşturun. Bilgi toocreate aşağıdaki hello gizli bilgilerinizi kullanın.

1. Merhaba aşağıdaki hello ana düğümde çalıştırın.

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. Gizli düzgün bir şekilde oluşturulduğundan emin olun.

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. Komut toomount hello gizli toohello aşağıdaki çalışma hello OMS Aracısı kapsayıcılı.

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a>Yaml dosyalarla Kubernetes için güvenli parolaları

Kubernetes için çalışma alanı kimliği ve birincil anahtar için bir komut toogenerate hello gizli yaml dosyasını kullanın. Merhaba, [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) sayfasında, gizli bilgileri olan veya olmayan kullanabileceğiniz dosyaları vardır.

- Merhaba varsayılan OMS Aracısı DaemonSet gizli bilgileri (omsagent.yaml) yok
- Merhaba OMS Aracısı DaemonSet yaml dosya gizli oluşturma betikleri toogenerate hello gizli yaml (omsagentsecret.yaml) dosyası ile gizli bilgileri (omsagent-ds-secrets.yaml) kullanır.

Toocreate omsagent DaemonSets ile veya olmadan gizli seçebilirsiniz.

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a>Varsayılan OMSagent DaemonSet yaml dosya gizlilikler olmadan

- Merhaba varsayılan OMS Aracısı DaemonSet yaml dosyası için hello yerine `<WSID>` ve `<KEY>` tooyour WSID ve anahtarı. Merhaba dosya tooyour ana düğümü ve çalışma hello aşağıdakileri kopyalayın:

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a>Varsayılan OMSagent DaemonSet yaml dosya gizli

1. toouse OMS Aracısı gizli bilgileri kullanarak DaemonSet hello gizli önce oluşturun.
    1. Hello komut dosyası ve gizli şablon dosyası kopyalayabilir ve üzerinde hello olduklarından emin olmak aynı dizin.
        - Komut dosyası - gizli gen.sh üretiliyor gizli
        - Gizli şablon - gizli template.yaml
    2. Aşağıdaki örnek hello gibi Hello komut dosyasını çalıştırın. OMS çalışma alanı kimliği ve birincil anahtar Hello betik Merhaba sorar ve bunları girdikten sonra onu çalıştırabilmeniz için hello betik gizli yaml dosyası oluşturur.   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. Merhaba gizli pod hello aşağıdakini çalıştırarak oluşturun:
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. tooverify, Hello aşağıdaki komutu çalıştırın:

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        Çıktı aşağıdakine benzemelidir:

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        Çıktı aşağıdakine benzemelidir:

        ```
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

    5. Arka plan programı kümesi çalıştırarak, omsagent oluşturma``` sudo kubectl create -f omsagent-ds-secrets.yaml ```

2. OMS Aracısı DaemonSet çalıştığından, o hello aşağıdaki benzer toohello doğrulayın:

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


Kubernetes için çalışma alanı kimliği ve birincil anahtar için bir komut dosyası toogenerate hello gizli yaml dosyasını kullanın. Merhaba örnek bilgilerle aşağıdaki kullanım hello [omsagent yaml dosya](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure gizli bilgilerinizi.

```
keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
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

## <a name="windows-container-hosts"></a>Windows kapsayıcı konakları

### <a name="preparation-before-installing-windows-agents"></a>Windows aracıları yüklemeden önce hazırlama

Windows çalıştıran bilgisayarlarda aracılar yüklemeden önce tooconfigure hello Docker hizmet gerekir. Hello yapılandırma, izleme için Docker TCP yuva hello aracıları hello Docker arka plan programı uzaktan erişebilmesi için hello Windows aracı veya hello günlük analizi sanal makine uzantısı toouse hello ve toocapture verileri sağlar.

#### <a name="toostart-docker-and-verify-its-configuration"></a>toostart Docker ve yapılandırmasını doğrulayın

Windows Server için adlandırılmış TCP yukarı adımlar tooset vardır:

1. Windows PowerShell'de TCP kanal ve adlandırılmış kanal etkinleştirin.

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. Docker hello yapılandırma dosyası TCP kanal için yapılandırmak ve adlandırılmış. Merhaba yapılandırma dosyası C:\ProgramData\docker\config\daemon.json bulunur.

    Merhaba daemon.json dosyasında hello aşağıdaki gerekir:

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

İle Windows kapsayıcıları kullanılan hello Docker arka plan programı yapılandırma hakkında daha fazla bilgi için bkz: [Docker altyapısına Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).


### <a name="install-windows-agents"></a>Windows aracılarını yükleme

tooenable Windows ve Hyper-V kapsayıcı izleme, kapsayıcı konaklar Windows bilgisayarlarda hello Microsoft İzleme Aracısı'nı (MMA) yükleyin. Şirket içi ortamınızda Windows çalıştıran bilgisayarlar için bkz: [bağlanmak Windows bilgisayarları tooLog Analytics](log-analytics-windows-agents.md). Sanal makineler için Azure'da çalışan bağlanmak bunları tooLog Analytics hello kullanarak [sanal makine uzantısı](log-analytics-azure-vm-extension.md).

Service Fabric üzerinde çalışan Windows kapsayıcıları izleyebilirsiniz. Ancak, yalnızca [Azure'da çalışan sanal makineler](log-analytics-azure-vm-extension.md) ve [şirket içi ortamınızda Windows çalıştıran bilgisayarlar](log-analytics-windows-agents.md) için Service Fabric şu anda desteklenmiyor.

Bu hello kapsayıcı izlemesi çözümü Windows için doğru ayarlandığını doğrulayabilirsiniz. Merhaba Yönetim Paketi yükleme düzgün olup toocheck arayın *ContainerManagement.xxx*. Merhaba dosyaları hello C:\Program Files\Microsoft Monitoring Agent\Agent\Health hizmet State\Management paketleri klasörde olmalıdır.


## <a name="solution-components"></a>Çözüm bileşenleri

Windows aracılarının kullanıyorsanız, bu çözüme ekleyin ardından hello aşağıdaki Yönetim Paketi her bilgisayara bir aracı ile yüklenir. Hiçbir yapılandırma ve Bakım hello Yönetim Paketi için gereklidir.

- *ContainerManagement.xxx* C:\Program Files\Microsoft Monitoring Agent\Agent\Health hizmet State\Management paketlerinde yüklü

## <a name="container-data-collection-details"></a>Kapsayıcı veri toplama ayrıntıları
Merhaba kapsayıcı izlemesi çözümü kapsayıcı konakları ve etkinleştirmeniz aracıları kullanarak kapsayıcıları çeşitli performans ölçümleri ve günlük verilerini toplar.

Verileri üç dakikada şu Aracısı türlerini hello tarafından toplanır.

- [Linux için OMS Aracısı](log-analytics-linux-agents.md)
- [Windows Aracısı](log-analytics-windows-agents.md)
- [Log Analytics VM uzantısı](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a>Kapsayıcı kayıtlarını

Merhaba aşağıdaki tabloda hello kapsayıcı izlemesi çözümü ve günlük arama sonuçlarında görünecek hello veri türleri tarafından toplanan kayıtları örnekleri gösterilmektedir.

| Veri türü | Günlük arama veri türü | Alanları |
| --- | --- | --- |
| Konaklar ve kapsayıcıları için performans | `Type=Perf` | Bilgisayar, ObjectName, CounterName &#40; % işlemci zamanı, Disk MB okur, MB, bellek kullanımı MB Disk Yazar ağ Al bayt, ağ gönderme bayt, işlemci kullanımı sn, ağ &#41; CounterValue, TimeGenerated, sayaç yolu, SourceSystem |
| Kapsayıcı envanteri | `Type=ContainerInventory` | TimeGenerated, bilgisayar, ContainerHostname, görüntü, ImageTag, ContainerState, ExitCode, EnvironmentVar, komutu, CreatedTime, StartedTime, FinishedTime, SourceSystem, Containerıd, ImageID kapsayıcı adı |
| Kapsayıcı görüntü envanteri | `Type=ContainerImageInventory` | TimeGenerated, bilgisayar, görüntü, ImageTag, ImageSize, VirtualSize, duraklatıldı, çalışıyor, durduruldu, başarısız, SourceSystem, ImageID, TotalContainer |
| Kapsayıcı günlük | `Type=ContainerLog` | TimeGenerated, bilgisayar, görüntü kimliği, LogEntrySource, LogEntry, SourceSystem, Containerıd kapsayıcı adı |
| Kapsayıcı hizmeti oturum açma | `Type=ContainerServiceLog`  | TimeGenerated, bilgisayar, TimeOfCommand, görüntü, komutu, SourceSystem, Containerıd |
| Kapsayıcı düğümü envanteri | `Type=ContainerNodeInventory_CL`| TimeGenerated, bilgisayar, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem|
| Kubernetes envanteri | `Type=KubePodInventory_CL` | TimeGenerated, bilgisayar, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem |
| Kapsayıcı işlemi | `Type=ContainerProcess_CL` | TimeGenerated, bilgisayar, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem |
| Kubernetes olayları | `Type=KubeEvents_CL` | TimeGenerated, bilgisayar, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, ileti |

Etiketleri eklenmiş çok*PodLabel* veri türleridir kendi özel etiketler. Merhaba eklenmiş PodLabel etiketleri hello tabloda gösterilen örnek verilmiştir. Bu nedenle, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` ortamınızı ait veri kümesinde farklı ve genel benzer `PodLabel_yourlabel_s`.


## <a name="monitor-containers"></a>İzleyici kapsayıcıları
Merhaba OMS portalında etkin hello çözüm aldıktan sonra hello **kapsayıcıları** döşeme kapsayıcı konakları ve ana bilgisayarlarda çalışan Merhaba kapsayıcılara hakkındaki özet bilgileri gösterir.

![Kapsayıcıları döşeme](./media/log-analytics-containers/containers-title.png)

Hello kutucuğu çalışıyor veya durdurulmuştur hello ortamı ve olup bunların başarısız, elinizde kaç kapsayıcıları genel bir bakış gösterilir.

### <a name="using-hello-containers-dashboard"></a>Merhaba kapsayıcılara panosunu kullanma
Merhaba tıklatın **kapsayıcıları** döşeme. Buradan düzenlenmiş görünümler görürsünüz:

- **Kapsayıcı olayları** -kapsayıcı durumu ve başarısız kapsayıcıları sahip bilgisayarları gösterir.
- **Kapsayıcı günlükleri** -kapsayıcı günlük dosyalarının zaman ve bilgisayarların bir listesini hello en yüksek sayıda günlük dosyaları ile oluşturulan bir grafik gösterir.
- **Kubernetes olayları** -zaman ve neden pod'ları oluşturulan hello olayları hello nedenleri listesini oluşturulan Kubernetes olayları bir grafiğini gösterir. *Bu veri kümesi yalnızca Linux ortamlarda kullanılır.*
- **Kubernetes Namespace stok** - gösterir hello sayısı ad alanları ve pod'ları ve hiyerarşileri gösterir. *Bu veri kümesi yalnızca Linux ortamlarda kullanılır.*
- **Kapsayıcı düğümü stok** -kapsayıcı düğümlerini/ana bilgisayarda kullanılan orchestration türleri hello sayısını gösterir. Merhaba bilgisayar/ana bilgisayar düğümleri de Merhaba kapsayıcılara sayısıyla listelenir. *Bu veri kümesi yalnızca Linux ortamlarda kullanılır.*
- **Kapsayıcı görüntüleri stok** -hello kullanılan kapsayıcı görüntüleri toplam sayısı ve resim türleri sayısını gösterir. Görüntü Hello sayısını da hello resim etiketi listelenir.
- **Kapsayıcıları durum** -çalışan kapsayıcılar olan düğümler/ana bilgisayarlar kapsayıcısı hello toplam sayısını gösterir. Bilgisayarları da ana çalışan hello sayısı tarafından listelenir.
- **Kapsayıcı işlem** -kapsayıcı işlemlerin zaman içinde çalışan bir çizgi grafiği gösterir. Kapsayıcılar, çalıştırarak da listelenen komutu/işlemi kapsayıcıları içinde. *Bu veri kümesi yalnızca Linux ortamlarda kullanılır.*
- **Kapsayıcı CPU performans** -hello ortalama CPU kullanımı düğümleri/barındıran bilgisayar için zaman içinde bir çizgi grafiği gösterir. Ayrıca listeleri hello bilgisayar düğümleri/ortalama CPU kullanımı tabanlı.
- **Kapsayıcı bellek performansı** -zaman içinde bir çizgi grafiği bellek kullanımını gösterir. Ayrıca bilgisayar bellek kullanımı örneği adına göre listeler.
- **Bilgisayar performansı** -gösterir hello Yüzde CPU performans zaman içerisinde, çizgi grafiklerde zaman ve megabayt boş disk alanı üzerinden bellek kullanımı yüzdesi Zamanla. Her satırda bir grafik tooview üzerinde daha fazla ayrıntı gelebilirsiniz.


Her hello Pano görsel bir toplanan veriler üzerinde çalıştırılan bir arama alanıdır.

![Kapsayıcıları Panosu](./media/log-analytics-containers/containers-dash01.png)

![Kapsayıcıları Panosu](./media/log-analytics-containers/containers-dash02.png)

Merhaba, **kapsayıcı durumu** alanında, aşağıda gösterildiği gibi hello üst bölmesinde tıklatın.

![Kapsayıcı durumu](./media/log-analytics-containers/containers-status.png)

Kapsayıcılarınızı hello durumu hakkındaki bilgileri görüntüleyen günlük arama açılır.

![Günlük arama kapsayıcıları için](./media/log-analytics-containers/containers-log-search.png)

Buradan, hello arama sorgusu toomodify düzenleyebilirsiniz, ilgilendiğiniz toofind hello özel bilgiler. Günlük aramaları hakkında daha fazla bilgi için bkz: [günlük analizi aramaları oturum](log-analytics-log-searches.md).

## <a name="troubleshoot-by-finding-a-failed-container"></a>Başarısız bir kapsayıcı bulma ile ilgili sorunları giderme

Günlük analizi kapsayıcı olarak işaretler **başarısız** sıfır olmayan çıkış kodu ile çıkıldı durumunda. Hello hataları ve hataları hello hello ortamında özetini görebilirsiniz **başarısız kapsayıcıları** alanı.

### <a name="toofind-failed-containers"></a>toofind kapsayıcıları başarısız oldu
1. Merhaba tıklatın **kapsayıcı durumu** alanı.  
   ![kapsayıcı durumu](./media/log-analytics-containers/containers-status.png)
2. Günlük arama açar ve Merhaba, kapsayıcıları durumunu izleyen benzer toohello görüntüler.  
   ![kapsayıcı durumu](./media/log-analytics-containers/containers-log-search.png)
3. Ardından, başarısız kapsayıcıları tooview ek bilgiler toplanır hello değerini tıklatın. Genişletme **daha fazla Göster** tooview hello görüntü kimliği  
   ![başarısız kapsayıcıları](./media/log-analytics-containers/containers-state-failed.png)  
4. Ardından, hello aşağıdaki hello arama sorgusu yazın. `Type=ContainerInventory <ImageID>`görüntü boyutu ve durduruldu ve başarısız resimlerinin sayısı gibi hello görüntü ayrıntılarını toosee.  
   ![başarısız kapsayıcıları](./media/log-analytics-containers/containers-failed04.png)

## <a name="search-logs-for-container-data"></a>Kapsayıcı verileri için arama günlüklerini
Belirli bir hata gidermeye çalışıyorsanız, ortamınızda oluştuğu toosee yardımcı olabilir. şu günlük türlerini hello tooreturn hello bilgileri sorgular oluşturmanıza yardımcı olur.


- **ContainerImageInventory** – resim kimlikleri veya boyutları gibi görüntü ve tooview görüntü bilgileri tarafından düzenlenmiş toofind bilgileri çalışırken bu türü kullanın.
- **ContainerInventory** – kapsayıcı konumunu, adlarını nedir ve ne hakkında bilgi almak istediğinizde bu türü kullanın çalıştırma kaynağınız görüntüler.
- **ContainerLog** – toofind belirli hata günlüğü bilgilerini ve girişleri istediğinizde bu türü kullanın.
- **ContainerNodeInventory_CL** kapsayıcıları burada bulunan konak/düğüm hakkında hello bilgi istediğinizde bu türü kullanın. Bu, Docker sürüm, orchestration türünü, depolama ve ağ bilgilerini sağlar.
- **ContainerProcess_CL** kullanma Bu tür tooquickly hello kapsayıcıda çalıştırılan hello işlemi konusuna bakın.
- **ContainerServiceLog** – hello Docker arka plan programı, Başlat, Durdur, silmek veya çekme komutları için toofind denetim izi bilgilerini çalışırken bu türü kullanın.
- **KubeEvents_CL** bu tür toosee hello Kubernetes olayları kullanın.
- **KubePodInventory_CL** toounderstand hello küme hiyerarşisi bilgileri istediğinizde bu türü kullanın.


### <a name="toosearch-logs-for-container-data"></a>kapsayıcı verilerini toosearch günlükleri
* Bildiğiniz bir görüntüyü yakın zamanda başarısız oldu ve hello Hata günlüklerini bulabilmelerini seçin. Başlat, görüntü ile çalışan bir kapsayıcı adı bularak bir **ContainerInventory** arama. Örneğin, arama`Type=ContainerInventory ubuntu Failed`  
    ![Ubuntu kapsayıcıları için arama](./media/log-analytics-containers/search-ubuntu.png)

  Merhaba kapsayıcının adını sonraki çok hello**adı**ve bu günlükleri arayın. Bu örnekte bu değer `Type=ContainerLog cranky_stonebreaker`’dur.

**Performans bilgilerini görüntüleme**

Tooconstruct sorguları başlayan olduğunda, ilk olası nedir toosee yardımcı olur. Örneğin, tüm performans verileri, yazarak geniş bir sorgu hello aşağıdaki try arama toosee sorgu.

```
Type=Perf
```

![kapsayıcıları performansı](./media/log-analytics-containers/containers-perf01.png)

Merhaba performans verileri, tooa belirli bir kapsayıcıya hello adını yazarak sorgunuzun sağ toohello görüyorsunuz kapsamını belirleyebilirsiniz.

```
Type=Perf <containerName>
```

Tek bir kapsayıcı için toplanan performans ölçümleri hello listesini gösterir.

![kapsayıcıları performansı](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a>Örnek günlük arama sorguları
Genellikle yararlı toobuild ortamınızın bir örnek veya iki ile başlayan ve bunları toofit değiştirme sorgular. Bir başlangıç noktası olarak ile Merhaba deneyebilirsiniz **örnek sorgular** alanı toohelp daha gelişmiş sorgular oluşturun.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Kapsayıcıları sorguları](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a>Arama sorguları günlük kaydetme
Sorguları kaydetme günlük analizi standart bir özelliktir. Bunları kaydederek yararlı buldunuz o gerekir gelecekte kullanım için kullanışlı.

Size kullanışlı bir sorgu oluşturduktan sonra tıklayarak Kaydet **Sık Kullanılanlar** hello sayfanın üst kısmındaki hello günlük arama. Kolayca daha sonra hello erişebildiğinizi sonra **My Pano** sayfası.

## <a name="next-steps"></a>Sonraki adımlar
* [Arama günlüklerini](log-analytics-log-searches.md) tooview ayrıntılı kapsayıcı verileri kaydeder.
