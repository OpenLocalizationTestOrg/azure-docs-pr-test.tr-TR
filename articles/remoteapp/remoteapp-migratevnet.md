---
title: "Bir RemoteApp sanal ağdan bir Azure sanal ağına geçiş yapma | Microsoft Docs"
description: "Bir RemoteApp sanal ağdan bir Azure sanal ağına geçiş hakkında bilgi edinin"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: baea5d29-353b-48f8-b47f-806f2163e067
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 10b5f4844a38fe97852dee8634e8cf54f1a23a1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-migrate-a-hybrid-collection-from-a-remoteapp-vnet-to-an-azure-vnet"></a>Karma koleksiyon için bir Azure sanal bir RemoteApp sanal ağdan geçirme
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

İyi haber! Karma RemoteApp koleksiyonları RemoteApp özel sanal ağlar oluşturmak yerine doğrudan, mevcut Azure sanal ağlar (Vnet'ler) halinde dağıtmak etkin. Bu, (örneğin, ExpressRoute) en son VNET özelliklerden yararlanmak ve karma koleksiyonlarınızı doğrudan ağ diğer Azure Hizmetleri ve bu VNET'e dağıtılan sanal makineleri erişmenizi sağlar.  (Bu, daha iyi performans ve VNET-VNET yapılandırmaları daha kolay kurulum alır).

Adlı karma RemoteApp koleksiyonu zaten oluşturduğunuzu düşünelim *OriginalCollection* bir RemoteApp sanal ağı ile adlı *RemoteAppVNET*. Adlı yeni Azure VNET için geçirmek için adımlar şunlardır *AzureVNET*.

1. Üzerinde **ağlar** sekmesinde [Yönetim Portalı](http://manage.windowsazure.com/), adlı bir VNET oluşturma *AzureVNET*kullanarak aynı konum, DNS yapılandırması ve adres alanı (en az biri için *AzureVNET* alt ağlar) için kullanılan aynı *RemoteAppVNET*.
2. Yapılandırma *AzureVNET* ana bilgisayar veya Active Directory dağıtımı için bir ağ bağlantınız için *OriginalCollection* etki alanına katıldı.
3. Üzerinde **Remoteapps'leri** sekmesinde, adı verilen yeni bir RemoteApp koleksiyonu oluşturun *yeni koleksiyon*. (Kullanım **Create VNET ile** seçeneği değil, **hızlı Oluştur**.)
4. Yapılandırma *NewCollection* bir alt ağda dağıtmak üzere *AzureVNET*.
5. Yapılandırma *NewCollection* için kullanılan aynı etki alanına katılım bilgileri ve aynı görüntü kullanılacak *OriginalCollection*.
6. Birkaç saat sonra *NewCollection* koleksiyonu listenize etkin duruma ile gösterilir.

Herhangi bir kullanıcı bilgisi özgün koleksiyondan yeni koleksiyon geçişi gerekmiyorsa, artık, ardından bu adımları uygulayın:

1. Silme *OriginalCollection*.
2. Silme *RemoteAppVNET*.

Ve bitirdiniz!

Kullanıcı bilgilerini özgün koleksiyondan yeni koleksiyon geçişi gerekiyorsa, alternatif olarak, ardından bu adımları uygulayın:

1. E-posta Gönder [ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) Azure abonelik Kimliğinizi, özgün koleksiyonun adını ve yeni koleksiyonunuzu adını ve kullanıcı bilgilerinizi geçirmek isteyin.
2. 2 iş günü içinde yeni koleksiyon, özgün koleksiyondan RemoteApp ekibi kullanıcı erişim listesi ve tüm kullanıcı belgeleri ve kullanıcı ayarlarını taşınır.
3. Silme *OriginalCollection*.
4. Silme *RemoteAppVNET*.

Ve şimdi bitirdiniz!

Sorularınız veya özel Yardım gerekirse, lütfen e-posta [ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).

