---
title: "aaaManage Azure DC/OS kümesi Marathon kullanıcı Arabirimi ile | Microsoft Docs"
description: "Kapsayıcıları tooan Azure kapsayıcı hizmeti Küme hizmetine hello Marathon web kullanıcı arabirimini kullanarak dağıtın."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Kapsayıcılar, Mikro hizmetler, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: a90180e1b4763e6d2ddfa699ed4b7269f209f728
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-hello-marathon-web-ui"></a>Azure kapsayıcı hizmeti DC/OS kümesi hello Marathon web kullanıcı Arabirimi üzerinden yönetmek
DC/OS dağıtma ve hello temel donanımı özetlerken, kümelenmiş iş yükleri ölçekleme için bir ortam sağlar. DC/OS’nin en üstünde, hesaplama iş yüklerini zamanlamayı ve yürütmeyi yöneten bir çerçeve vardır.

Çerçeveler çok sayıda yaygın iş yükü için kullanılabilir, ancak bu belgede Marathon ile kapsayıcı dağıtma tooget nasıl başlatılacağını açıklar. 


## <a name="prerequisites"></a>Ön koşullar
Bu örneklerin üzerinden geçmeden önce, Azure Kapsayıcı Hizmeti’nde yapılandırılan bir DC/OS kümeniz olması gerekir. Ayrıca toohave uzak bağlantı toothis küme gerekir. Bu öğeler hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:

* [Azure Container Service kümesi dağıtma](container-service-deployment.md)
* [Tooan Azure kapsayıcı hizmeti kümesine bağlanma](../container-service-connect.md)

> [!NOTE]
> Bu makalede, yerel bağlantı noktası 80 üzerinden toohello DC/OS kümesine tünel varsayar.
>

## <a name="explore-hello-dcos-ui"></a>Merhaba DC/OS kullanıcı arabirimini keşfetme
Secure Shell (SSH) tüneli ile [kurulan](../container-service-connect.md), toohttp://localhost/ göz atın. Bu hello DC/OS web kullanıcı arabirimini yükler ve kullanılan kaynaklar, etkin aracılar ve çalışan hizmetler gibi hello küme hakkında bilgileri gösterir.

![DC/OS Kullanıcı Arabirimi](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-hello-marathon-ui"></a>Merhaba Marathon kullanıcı arabirimini keşfetme
toosee hello Marathon kullanıcı Arabirimi, toohttp://localhost/marathon göz atın. Bu ekranda hello Azure kapsayıcı hizmeti DC/OS kümesinde yeni bir kapsayıcı veya başka bir uygulama başlatabilirsiniz. Kapsayıcıları ve uygulamaları çalıştırma hakkında bilgileri de görebilirsiniz.  

![Marathon kullanıcı arabirimi](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a>Docker biçimli kapsayıcı dağıtma
toodeploy Marathon, kullanarak yeni bir kapsayıcı tıklatın **uygulama oluştur**ve hello form sekmelere bilgisinden hello girin:

| Alan | Değer |
| --- | --- |
| Kimlik |nginx |
| Bellek | 32 |
| Görüntü |nginx |
| Ağ |Bağlantı |
| Ana Bilgisayar Bağlantı Noktası |80 |
| Protokol |TCP |

![Yeni Uygulama Kullanıcı Arabirimi --Genel](./media/container-service-mesos-marathon-ui/dcos4.png)

![Yeni Uygulama Kullanıcı Arabirimi--Docker Kapsayıcısı](./media/container-service-mesos-marathon-ui/dcos5.png)

![Yeni Uygulama Kullanıcı Arabirimi--Bağlantı Noktaları ve Hizmet Bulma](./media/container-service-mesos-marathon-ui/dcos6.png)

Toostatically harita hello kapsayıcı bağlantı noktası tooa bağlantı noktası üzerinde hello Aracısı istiyorsanız toouse JSON modu gerekir. toodo bu nedenle, geçiş hello yeni uygulama Sihirbazı'nı çok**JSON modu** hello geçiş kullanarak. Ayarı hello altında aşağıdaki hello enter `portMappings` hello uygulama tanımının bölümü. Bu örnek hello DC/OS aracının 80 hello kapsayıcı tooport bağlantı noktası 80 bağlar. Bu değişikliği yaptıktan sonra bu sihirbazı JSON modundan çıkarabilirsiniz.

```none
"hostPort": 80,
```

![Yeni Uygulama Kullanıcı Arabirimi--bağlantı noktası 80 örneği](./media/container-service-mesos-marathon-ui/dcos13.png)

Tooenable durumu denetimleri istiyorsanız, bir yol hello ayarlayın **sistem durumu denetler** sekmesi.

![Yeni Uygulama UI--durum denetimleri](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

Merhaba DC/OS kümesi özel ve ortak aracıyla kümesiyle dağıtılır. Merhaba küme toobe mümkün tooaccess uygulamalardan için hello Internet toodeploy hello uygulamaları tooa ortak Aracı gerekir. toodo, bu nedenle, hello seçin **isteğe bağlı** sekmesini hello yeni uygulama Sihirbazı'nın ve girin **slave_public** hello için **kabul edilen kaynak rolleri**.

Ardından **Uygulama Oluştur**'a tıklayın.

![Yeni Uygulama Kullanıcı Arabirimi--ortak aracı ayarı](./media/container-service-mesos-marathon-ui/dcos14.png)

Geri hello Marathon ana sayfasına hello kapsayıcı hello dağıtım durumunu görebilirsiniz. Başlangıçta **Dağıtılıyor** durumu görüntülenir. Başarılı dağıtım sonrasında, durum değişikliklerini çok hello**çalıştıran**.

![Marathon ana sayfası kullanıcı arabirimi--kapsayıcı dağıtım durumu](./media/container-service-mesos-marathon-ui/dcos7.png)

Geri toohello DC/OS web kullanıcı Arabirimine (http://localhost/) geçiş yaptığınızda, bir görevin (örneğimizde, Docker biçimli kapsayıcının) hello DC/OS kümesinde çalıştığını görürsünüz.

![DC/OS web kullanıcı Arabirimi--hello kümede çalışan görev](./media/container-service-mesos-marathon-ui/dcos8.png)

Görev hello toosee hello küme düğümü üzerinde çalıştığından, hello tıklatın **düğümleri** sekmesi.

![DC/OS web kullanıcı arabirimi--görev küme düğümü](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-hello-container"></a>Merhaba kapsayıcı ulaşmak

Bu örnekte, bir ortak aracı düğümünde Merhaba uygulaması çalışıyor. Merhaba hello uygulamadan ulaşmak toohello Aracısı hello küme FQDN'si giderek Internet: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, burada:

* **DNSPREFIX** hello kümeyi dağıttığınızda sağladığınız hello DNS önekidir.
* **Bölge** kaynak grubunuzun bulunduğu hello bölgedir.

    ![Internet'ten Nginx](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a>Sonraki adımlar
* [Marathon API'si hello ve DC/OS ile çalışma](container-service-mesos-marathon-rest.md)

* Azure kapsayıcı hizmeti Mesos ile Merhaba üzerinde derin Dalış

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
