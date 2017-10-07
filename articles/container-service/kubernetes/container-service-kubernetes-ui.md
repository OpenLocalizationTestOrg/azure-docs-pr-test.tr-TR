---
title: "aaaManage Azure Kubernetes web kullanıcı Arabirimi ile küme | Microsoft Docs"
description: "Hello kullanarak Azure kapsayıcı hizmeti kullanıcı Arabiriminde Kubernetes web"
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
ms.date: 02/21/2017
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: e24ea0b82c94d2fd4610e4442699ef756590e6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-kubernetes-web-ui-with-azure-container-service"></a>Kubernetes web kullanıcı Arabirimi Azure kapsayıcı hizmeti ile Merhaba kullanma

## <a name="prerequisites"></a>Ön koşullar
Bu kılavuz, sahibi olduğunuzu varsayar [Azure kapsayıcı hizmeti kullanarak Kubernetes küme oluşturulan](container-service-kubernetes-walkthrough.md).


Ayrıca, hello Azure CLI 2.0 sahibi olduğunuzu varsayar ve `kubectl` araçları yüklü.

Merhaba varsa test edebilirsiniz `az` çalıştırarak yüklü aracı:

```console
$ az --version
```

Merhaba yoksa `az` yüklü, aracı yönergeler vardır [burada](https://github.com/azure/azure-cli#installation).

Merhaba varsa test edebilirsiniz `kubectl` çalıştırarak yüklü aracı:

```console
$ kubectl version
```

Sahip değilseniz `kubectl` yüklü çalıştırabilirsiniz:

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a>Genel Bakış

### <a name="connect-toohello-web-ui"></a>Toohello web kullanıcı Arabirimi Bağlan
Merhaba Kubernetes web kullanıcı arabirimini çalıştırarak başlatabilirsiniz:

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

Bu, yerel makine toohello Kubernetes web kullanıcı Arabirimi bağlanan bir web tarayıcı yapılandırılmış tootalk tooa güvenli proxy açmanız gerekir.

### <a name="create-and-expose-a-service"></a>Oluşturma ve bir hizmet kullanıma sunma
1. Merhaba Kubernetes web kullanıcı Arabirimi,'ı **oluşturma** hello üst sağ penceresinde düğmesini.

    ![Kubernetes kullanıcı Arabirimi oluşturma](./media/container-service-kubernetes-ui/create.png)

    Uygulamanızı oluşturma başlayabileceğiniz bir iletişim kutusu açılır.

2. Merhaba ad verin `hello-nginx`. Kullanım hello [ `nginx` Docker kapsayıcıdan](https://hub.docker.com/_/nginx/) ve bu web Hizmeti'nin, üç çoğaltmaları dağıtın.

    ![Kubernetes Pod Oluştur iletişim kutusu](./media/container-service-kubernetes-ui/nginx.png)

3. Altında **hizmet**seçin **dış** ve 80 numaralı bağlantı noktasını girin.

    Bu ayar yük-trafik toohello üç çoğaltmaları dengeler.

    ![Kubernetes hizmeti oluşturma iletişim kutusu](./media/container-service-kubernetes-ui/service.png)

4. Tıklatın **dağıtma** toodeploy Bu kapsayıcılar ve Hizmetleri.

    ![Kubernetes dağıtma](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a>Kapsayıcılarınızı görüntüleyin
Tıklattıktan sonra **dağıtma**, hello UI dağıttığı gibi hizmetiniz bir görünümünü gösterir:

![Kubernetes durumu](./media/container-service-kubernetes-ui/status.png)

Merhaba sol tarafında, UI altında her hello daire Kubernetes nesnesinde hello durumunu görebilirsiniz **pod'ları**. Kısmen dolu daire ise, ardından hello nesne hala dağıtıyor. Bir nesne tam olarak dağıtıldığında, yeşil bir onay işareti görüntüler:

![Dağıtılan Kubernetes](./media/container-service-kubernetes-ui/deployed.png)

Her şeyi çalışmaya başladıktan sonra web hizmeti çalıştıran hello pod'ları toosee ayrıntılarını birini tıklatın.

![Kubernetes pod'ları](./media/container-service-kubernetes-ui/pods.png)

Merhaba, **pod'ları** görünümü Merhaba kapsayıcılara hello pod yanı sıra bu kapsayıcıları tarafından kullanılan hello CPU ve bellek kaynakları hakkında bilgileri görebilirsiniz:

![Kubernetes kaynakları](./media/container-service-kubernetes-ui/resources.png)

Merhaba kaynakları görmüyorsanız, toowait veri toopropagate izleme hello için birkaç dakika gerekebilir.

toosee hello günlükleri, kapsayıcı için tıklatın **görüntülemek günlükleri**.

![Kubernetes günlükleri](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a>Hizmetinizi görüntüleme
Bir dış toplama toorunning, kapsayıcıları hello Kubernetes UI oluşturdu `Service` bir yük dengeleyici toobring trafiği toohello kapsayıcıları kümenizdeki sağlar.

Merhaba sol gezinti bölmesinde **Hizmetleri** tooview tüm hizmetleri (olması gerektiğini tek).

![Kubernetes Hizmetleri](./media/container-service-kubernetes-ui/service-deployed.png)

Bu görünümde tooyour hizmet ayrılmış bir dış uç noktası (IP adresi) görmeniz gerekir.
Bu IP adresi tıklarsanız, yük dengeleyicinin ardında çalışan, Nginx kapsayıcısı görmeniz gerekir.

![nginx görünümü](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a>Hizmetinizi yeniden boyutlandırma
Toplama tooviewing, nesnelerinizi UI Merhaba, düzenleme ve hello Kubernetes API nesneleri güncelleştirme.

Önce tıklatın **dağıtımları** sol gezinti bölmesinde toosee hello dağıtım hizmetiniz için hello içinde.

Bu görünümde olduktan sonra hello çoğaltma kümesinde tıklayın ve ardından **Düzenle** hello üst gezinti çubuğunda:

![Kubernetes Düzenle](./media/container-service-kubernetes-ui/edit.png)

Merhaba Düzenle `spec.replicas` alan toobe `2`, tıklatıp **güncelleştirme**.

Bu, çoğaltmaları toodrop tootwo hello sayısı, pod'ları birini silerek neden olur.

 

