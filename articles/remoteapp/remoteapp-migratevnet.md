---
title: bir RemoteApp Koleksiyonunuzla tooan Azure VNET gelen aaaHow toomigrate | Microsoft Docs
description: "Bilgi nasıl RemoteApp Koleksiyonunuzla tooan Azure VNET gelen toomigrate"
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
ms.openlocfilehash: c0f8617556c6f1e33eca8322febf67ff33937ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-a-hybrid-collection-from-a-remoteapp-vnet-tooan-azure-vnet"></a>Nasıl toomigrate RemoteApp Koleksiyonunuzla tooan Azure VNET karma koleksiyonundan
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

İyi haber! Biz, toodeploy karma RemoteApp RemoteApp özel sanal ağlar oluşturmak yerine doğrudan, mevcut Azure sanal ağlar (Vnet'ler) koleksiyonlara etkinleştirmiş olmanız gerekir. Bu, son VNET özelliklerine (örneğin, ExpressRoute) hello yararlanmak ve Azure Hizmetleri, karma koleksiyonlar doğrudan ağ erişim tooother verin sağlar ve toothat VNET dağıtılan sanal makineler.  (Bu, daha iyi performans ve VNET-VNET yapılandırmaları daha kolay kurulum alır).

Adlı karma RemoteApp koleksiyonu zaten oluşturduğunuzu düşünelim *OriginalCollection* bir RemoteApp sanal ağı ile adlı *RemoteAppVNET*. Merhaba adımları toomigrate İşte bunu yeni Azure VNET adlı tooa *AzureVNET*.

1. Merhaba üzerinde **ağlar** hello sekmesinde [Yönetim Portalı](http://manage.windowsazure.com/), adlı bir VNET oluşturma *AzureVNET*kullanarak hello aynı konumda, DNS yapılandırması ve adres alanı (en az biri için Merhaba, *AzureVNET* alt ağlar) için kullanılan aynı *RemoteAppVNET*.
2. Yapılandırma *AzureVNET* tooeither konak veya ağ bağlantısı toohello Active Directory dağıtımınız varsa, *OriginalCollection* etki alanına katıldı.
3. Merhaba üzerinde **Remoteapps'leri** sekmesinde, adı verilen yeni bir RemoteApp koleksiyonu oluşturun *yeni koleksiyon*. (Kullanım hello **Create VNET ile** seçeneği değil, **hızlı Oluştur**.)
4. Yapılandırma *NewCollection* toobe tooa alt ağda dağıtılan *AzureVNET*.
5. Yapılandırma *NewCollection* toouse hello aynı görüntü ve etki alanına katılım bilgileri için kullanılan aynı *OriginalCollection*.
6. Birkaç saat sonra *NewCollection* koleksiyonu listenize etkin duruma ile gösterilir.

Herhangi bir kullanıcı bilgisi koleksiyonundan hello özgün koleksiyonu toohello yeni toomigrate gerekmiyorsa, artık, ardından bu adımları uygulayın:

1. Silme *OriginalCollection*.
2. Silme *RemoteAppVNET*.

Ve bitirdiniz!

Merhaba özgün koleksiyonu toohello yeni koleksiyon toomigrate kullanıcı bilgilerini gerekiyorsa, alternatif olarak, ardından bu adımları uygulayın:

1. Bir e-posta çok gönderme[ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) Azure abonelik Kimliğinizi ile Merhaba, özgün koleksiyonun adını ve yeni koleksiyonunuzu hello adını ve toomigrate isteyin kullanıcı bilgilerinizi.
2. 2 iş günü içinde hello RemoteApp ekibi hello kullanıcı erişim listesi ve tüm kullanıcı belgeleri ve kullanıcı ayarlarını hello özgün koleksiyonu toohello yeni koleksiyondan taşınır.
3. Silme *OriginalCollection*.
4. Silme *RemoteAppVNET*.

Ve şimdi bitirdiniz!

Sorularınız veya özel Yardım gerekirse, lütfen e-posta [ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).

