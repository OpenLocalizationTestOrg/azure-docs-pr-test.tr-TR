---
title: "azure'da aaaPrivate Docker kapsayıcısı kayıt defterleri | Microsoft Docs"
description: "Giriş toohello Azure kapsayıcı kayıt defteri hizmeti, bulut tabanlı, yönetilen, özel Docker kayıt defterleri sağlama."
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: ee2b652b-fb7c-455b-8275-b8d4d08ffeb3
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f6edcf0bf947b7770ee0a4e4a5cfbf4ef8b7392a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooprivate-docker-container-registries"></a>Giriş tooprivate Docker kapsayıcısı kayıt defterleri


Azure kapsayıcı kayıt defteri olan yönetilen [Docker kayıt defteri](https://docs.docker.com/registry/) göre hizmet hello açık kaynak Docker kayıt defteri 2.0. Oluşturma ve Azure kapsayıcı kayıt defterleri toostore korumak ve, özel yönetme [Docker kapsayıcısı](https://www.docker.com/what-docker) görüntüler. Azure kapsayıcı kayıt defterleri varolan kapsayıcı geliştirme ve dağıtım ardışık düzen ile kullanın ve Docker topluluk uzmanlık hello gövdesi çizin.

Docker ve kapsayıcılarla ilgili arka plan bilgileri için bkz.

* [Docker kullanıcı kılavuzu](https://docs.docker.com/engine/userguide/)




## <a name="use-cases"></a>Uygulama alanları
Görüntüleri Azure kapsayıcıdan kayıt defteri toovarious dağıtım hedefleri çekme:

* [DC/OS](https://docs.mesosphere.com/), [Docker Swarm](https://docs.docker.com/swarm/) ve [Kubernetes](http://kubernetes.io/docs/) dahil olmak üzere konak kümeleri arasında kapsayıcı haline getirilmiş uygulamaları yöneten **ölçeklenebilir düzenleme sistemleri** .
* [Container Service](../container-service/index.yml), [App Service](/app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/) ve diğerleri gibi uygun ölçekte uygulama oluşturulmasını ve çalıştırılmasını destekleyen **Azure hizmetleri**.

Geliştiriciler ayrıca tooa kapsayıcı kayıt kapsayıcı geliştirme iş akışının parçası olarak gönderebilir. Örneğin, [Visual Studio Team Services](https://www.visualstudio.com/docs/overview) veya [Jenkins](https://jenkins.io/) gibi bir sürekli tümleştirme ve dağıtım aracından bir kapsayıcı kayıt defteri hedeflenebilir.





## <a name="key-concepts"></a>Önemli kavramlar
* **Kayıt Defteri** - Azure aboneliğinizde bir veya daha fazla kapsayıcı kayıt defteri oluşturun. Her kayıt defteri standart Azure tarafından desteklenen [depolama hesabı](../storage/common/storage-introduction.md) hello içinde aynı konumu. Bir kayıt defteri hello oluşturarak yerel, ağ Kapat depolama kapsayıcısı görüntülerinizin yararlanmak dağıtımlarınızı aynı Azure konumunda. Tam kayıt adını hello form sahip `myregistry.azurecr.io`.

  [Erişimi denetlemenize](container-registry-authentication.md) tooa kapsayıcı kayıt defteri Azure Active Directory destekli kullanarak [hizmet sorumlusu](../active-directory/active-directory-application-objects.md) veya sağlanan yönetici hesabı. Standart çalışma hello `docker login` komutu tooauthenticate bir kayıt defteri ile.

* **Yönetilen Kayıt Defteri** - Üç SKU’da (Temel, Standart ve Premium) kayıt defterleri için ek özellikler sunan bir katmandır. Bu SKU'ları Hello görüntülerinde hello güvenilirliğini artırır ve yeni özellikleri etkinleştirir Azure kapsayıcı kayıt defterleri hizmet tarafından yönetilen depolama hesaplarındaki depolanır. Yeni özellikler; web kancası tümleştirme, Azure Active Directory ile depo kimlik doğrulaması ve silme işlemi için desteği içerir. Kullanıcılar yönetilen kayıt defterleri veya toocreate arasında hello seçeneği toochoose kayıt defterleri oluştururken kendi depolama hesapları tarafından yedeklenen bir kayıt defteri sahiptir.

* **Depo** -Bir kayıt defteri, kapsayıcı görüntüleri grubu olan bir veya daha çok depo içerir. Azure Container Kayıt Defteri, çok düzeyli depo ad alanlarını destekler. Bu özellik, görüntüleri ilgili tooa belirli uygulama toogroup koleksiyonları veya uygulamaları toospecific geliştirme veya işletimsel takımlar koleksiyonunu sağlar. Örneğin:

  * `myregistry.azurecr.io/aspnetcore:1.0.1`, kurum çapında bir görüntüyü temsil eder
  * `myregistry.azurecr.io/warrantydept/dotnet-build`temsil görüntüyü hello garanti departman genelinde paylaşılan toobuild .NET uygulamalarını kullanılır.
  * `myregistry.azrecr.io/warrantydept/customersubmissions/web`uygulamasındaki hello garanti bölümünüzün ait hello müşteri gönderimlerini gruplandırılmış bir web resmi temsil eder

* **Görüntü** - Bir depoda depolanan görüntülerin her biri, bir Docker kapsayıcısının salt okunur anlık görüntüsüdür. Azure kapsayıcısı kayıt defterleri hem Windows hem de Linux görüntüleri içerebilir. Tüm kapsayıcı dağıtımlarınız için görüntü adlarını siz denetlersiniz. Kullanım standart [Docker komutları](https://docs.docker.com/engine/reference/commandline/) toopush görüntülere bir havuz veya çekme bir depodan bir görüntü.

* **Kapsayıcı** - Kapsayıcı, bir yazılım uygulamasını ve uygulamanın bağımlılıklarını kod, çalışma zamanı, sistem araçları ve kitaplıkları içeren eksiksiz bir dosya sistemi şeklinde sarmalanmış bir halde tanımlar. Docker kapsayıcılarını bir kapsayıcı kayıt defterinden çektiğiniz Windows veya Linux görüntülerine bağlı olarak çalıştırın. Tek bir makinede çalışan kapsayıcılar hello işletim sisteminin çekirdek paylaşır. Docker tümüyle taşınabilir tooall ana Linux distro'lar, Mac ve Windows kapsayıcılardır.




## <a name="next-steps"></a>Sonraki adımlar
* [Hello Azure portal kullanarak bir kapsayıcı kayıt defteri oluşturma](container-registry-get-started-portal.md)
* [Hello Azure CLI kullanarak bir kapsayıcı kayıt defteri oluşturma](container-registry-get-started-azure-cli.md)
* [Merhaba Docker CLI kullanarak ilk görüntünüzü bildirme](container-registry-get-started-docker-cli.md)
* bkz: toobuild sürekli tümleştirme ve Visual Studio Team Services, Azure kapsayıcı hizmeti ve Azure kapsayıcı kayıt defterini kullanarak dağıtım iş akışı [Bu öğretici](../container-service/dcos-swarm/container-service-docker-swarm-setup-ci-cd.md).
* Tooset kendi Docker özel kayıt defterinde Azure (olmadan genel bir uç nokta) yedeklemek istiyorsanız, bkz: [dağıtma bilgisayarınızı kendi özel Docker kayıt defteri Azure üzerinde](../virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md).
