---
title: "aaaLoad Bakiye Azure Kubernetes kapsayıcılarında | Microsoft Docs"
description: "Harici olarak bağlayın ve Azure kapsayıcı Hizmeti'nde Kubernetes kümedeki birden çok kapsayıcı arasında Yük Dengelemesi."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kapsayıcılar, mikro hizmetler, Kubernetes, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 8073c8d3a015a53a532c326749571cb2582e1bac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a>Azure kapsayıcı hizmeti Kubernetes kümede Yük Dengelemesi kapsayıcıları 
Bu makalede, Azure kapsayıcı Hizmeti'nde Kubernetes kümedeki dengelemesini tanıtılır. Yük Dengeleme hello hizmeti için harici olarak erişilebilir bir IP adresi sağlar ve ağ trafiğini aracısını sanal makineleri çalıştıran hello pod'ları arasında dağıtır.

Kubernetes hizmet toouse ayarlayabilirsiniz [Azure yük dengeleyici](../../load-balancer/load-balancer-overview.md) toomanage dış (TCP) ağ trafiği. Ek bir yapılandırma olmadan Yük Dengeleme ve HTTP veya HTTPS trafiği veya daha Gelişmiş senaryolar yönlendirme mümkündür.

## <a name="prerequisites"></a>Ön koşullar
* [Kubernetes küme dağıtma](container-service-kubernetes-walkthrough.md) Azure kapsayıcı Hizmeti'nde
* [İstemci bağlantı](../container-service-connect.md) tooyour küme

## <a name="azure-load-balancer"></a>Azure yük dengeleyici

Varsayılan olarak, Azure kapsayıcı Hizmeti'nde dağıtılan Kubernetes küme hello Aracısı VM'ler için bir Internet'e yönelik Azure yük dengeleyici içerir. (Ayrı yük dengeleyici kaynak hello Yöneticisi VM'ler için yapılandırılır.) Azure yük dengeleyici katman 4 yük dengeleyici ' dir. Şu anda hello yük dengeleyici Kubernetes içinde yalnızca TCP trafiğini destekler.

Kubernetes hizmet oluşturulurken hello Azure yük dengeleyici tooallow erişim toohello hizmeti otomatik olarak yapılandırabilirsiniz. tooconfigure hello yük dengeleyici, kümesi hello hizmet `type` çok`LoadBalancer`. Aracı VM'ler (ve tersi yanıt trafiği için), bir ortak IP adresi ve bağlantı noktası numarası gelen hizmet trafiği toohello özel IP adresleri ve bağlantı noktası numaralarını hello pod'ları bir kural toomap Hello yük dengeleyici oluşturur. 

 Nasıl tooset hello Kubernetes hizmet gösteren iki örnek verilmiştir `type` çok`LoadBalancer`. (Artık gereksinim duyduğunuzda çalışırken hello örnekler sonra hello dağıtımları silin.)

### <a name="example-use-hello-kubectl-expose-command"></a>Örnek: Kullanım hello `kubectl expose` komutu 
Merhaba [Kubernetes izlenecek](container-service-kubernetes-walkthrough.md) nasıl bir örnek içerir tooexpose hello hizmetiyle `kubectl expose` komutu ve onun `--type=LoadBalancer` bayrağı. Merhaba adımlar şunlardır:

1. Yeni bir kapsayıcı dağıtımı başlatın. Örneğin, yeni bir dağıtım adlı komut başlatır aşağıdaki hello `mynginx`. Merhaba dağıtım hello Docker görüntü hello Nginx web sunucusu için temel üç kapsayıcı oluşur.

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. Merhaba kapsayıcılara çalıştığını doğrulayın. Örneğin, Merhaba kapsayıcılara ile sorgulama `kubectl get pods`, çıktı benzer toohello aşağıdakilere bakın:

    ![Nginx kapsayıcısı alma](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. çalıştırma tooconfigure hello yük dengeleyici tooaccept dış trafiğin toohello dağıtımı, `kubectl expose` ile `--type=LoadBalancer`. Merhaba aşağıdaki komutu hello Nginx sunucu bağlantı noktası 80 üzerinde sunar:

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. Tür `kubectl get svc` toosee hello hello kümedeki hello hizmetlerinin durumunu. Merhaba yük dengeleyici hello kuralı yapılandırırken hello `EXTERNAL-IP` Merhaba hizmet olarak görünür. `<pending>`. Birkaç dakika sonra hello dış IP adresi yapılandırılır: 

    ![Azure yük dengeleyici yapılandırma](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. Merhaba hizmet hello dış IP adresine erişebildiğinizi doğrulayın. Örneğin, gösterilen bir web tarayıcısı toohello IP adresini açın. Merhaba tarayıcı Merhaba kapsayıcılara birinde çalışan hello Nginx web sunucusu gösterir. Veya, çalışma hello `curl` veya `wget` komutu. Örneğin:

    ```
    curl 13.82.93.130
    ```

    Aşağıdakine benzer bir çıktı görmeniz gerekir:

    ![Erişim Nginx curl ile](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. hello Azure yük dengeleyici, Git toohello toosee hello yapılandırmasını [Azure portal](https://portal.azure.com).

7. Merhaba kaynak grubu için kapsayıcı hizmeti kümesini bulun ve hello yük dengeleyici hello Aracısı VM'ler için seçin. Adını olması hello hello kapsayıcı hizmeti ile aynı. (Yok hello yük dengeleyici hello ana düğüm için seçin, bir adı içeren hello **ana lb**.) 

    ![Kaynak grubundaki yük dengeleyici](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. Merhaba yük dengeleyici yapılandırması, toosee hello ayrıntılarını tıklatın **Yük Dengeleme kuralları** ve yapılandırılan hello kuralının hello adı.

    ![Yük Dengeleyici kuralları](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-hello-service-configuration-file"></a>Örnek: Belirtin `type: LoadBalancer` hello hizmet yapılandırma dosyası

JSON veya YAML Kubernetes kapsayıcı uygulama dağıtırsanız [hizmet yapılandırma dosyası](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), aşağıdaki satırı toohello hizmet belirtimi hello ekleyerek bir dış yük dengeleyici belirtin:

```YAML
 "type": "LoadBalancer"
``` 



Merhaba aşağıdaki adımları kullanın hello Kubernetes [Konuk örnek](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook). Bu örnek, Redis ve PHP Docker görüntülerini temel çok katmanlı web uygulamasıdır. Merhaba ön uç PHP sunucu hello Azure yük dengeleyici kullanan hello hizmet yapılandırma dosyasında belirtebilirsiniz.

1. Merhaba dosya indirme `guestbook-all-in-one.yaml` gelen [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one). 
2. Merhaba Gözat `spec` hello için `frontend` hizmet.
3. Merhaba satırı açıklamadan kaldırmasına `type: LoadBalancer`.

    ![Yük Dengeleyici Hizmeti Yapılandırması](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. Merhaba dosyasını kaydedin ve hello aşağıdaki komutu çalıştırarak hello uygulama dağıtabilirsiniz:

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. Tür `kubectl get svc` toosee hello hello kümedeki hello hizmetlerinin durumunu. Merhaba yük dengeleyici hello kuralı yapılandırırken hello `EXTERNAL-IP` Merhaba, `frontend` hizmeti görünür olarak `<pending>`. Birkaç dakika sonra hello dış IP adresi yapılandırılır: 

    ![Azure yük dengeleyici yapılandırma](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. Merhaba hizmet hello dış IP adresine erişebildiğinizi doğrulayın. Örneğin, bir web tarayıcısı toohello dış IP adresi hello hizmetinin açabilirsiniz.

    ![Dışarıdan erişim Konuk](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    Konuk girişleri ekleyebilirsiniz.

7. hello Azure yük dengeleyici, hello yük dengeleyici kaynak Gözat hello hello kümedeki toosee hello yapılandırmasını [Azure portal](https://portal.azure.com). Merhaba hello önceki örnekte adımlarına bakın.

### <a name="considerations"></a>Dikkat edilmesi gerekenler

* Merhaba yük dengeleyici kuralı oluşturulmasını olur zaman uyumsuz olarak ve sağlanan hello dengeleyici hakkında bilgi hello hizmetin içinde yayımlanan `status.loadBalancer` alan.
* Her hizmetin kendi hello yük dengeleyici sanal IP adresi otomatik olarak atanır.
* Bir DNS adı tarafından tooreach hello yük dengeleyici istiyorsanız hello kuralındaki IP adresi için bir DNS adı, etki alanı hizmeti sağlayıcısı toocreate ile çalışır.

## <a name="http-or-https-traffic"></a>HTTP veya HTTPS trafiği

tooload Bakiye HTTP veya HTTPS trafiği toocontainer web uygulamaları ve Aktarım Katmanı Güvenliği (TLS) için sertifikaları yönetme, hello Kubernetes kullanabileceğiniz [giriş](https://kubernetes.io/docs/user-guide/ingress/) kaynak. Bir giriş tooreach hello küme hizmetlerini gelen bağlantılara izin veren kuralları koleksiyonudur. Bir giriş kaynak toowork hello Kubernetes küme olmalıdır bir [giriş denetleyicisi](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) çalışıyor.

Azure kapsayıcı hizmeti Kubernetes giriş denetleyicisi otomatik olarak uygulamıyor. Çeşitli denetleyicisi uygulamalarını kullanılabilir. Şu anda hello [Nginx giriş denetleyicisi](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) tooconfigure giriş kuralları ve HTTP ve HTTPS trafiğinin Yük Dengeleme önerilir. 

Daha fazla bilgi için bkz: Merhaba [Nginx giriş denetleyici belgeleri](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).

> [!IMPORTANT]
> Merhaba Nginx giriş denetleyicisi Azure kapsayıcı Hizmeti'nde kullanırken, hello denetleyicisi dağıtımı ile bir hizmet olarak kullanıma `type: LoadBalancer`. Bu, hello Azure yük dengeleyici tooroute trafiği toohello denetleyicisi yapılandırır. Daha fazla bilgi için hello önceki bölümüne bakın.


## <a name="next-steps"></a>Sonraki adımlar

* Merhaba bkz [Kubernetes LoadBalancer belgeleri](https://kubernetes.io/docs/user-guide/load-balancer/)
* Daha fazla bilgi edinmek [Kubernetes giriş ve giriş denetleyicileri](https://kubernetes.io/docs/user-guide/ingress/)
* Bkz: [Kubernetes örnekleri](https://github.com/kubernetes/kubernetes/tree/master/examples)

