---
title: "Boyutlandırma bilgileri için bir VNET Azure remoteapp'te | Microsoft Docs"
description: "Bir VNET ile birlikte çalışan Azure RemoteApp için IP adresi gereksinimleri hakkında bilgi edinin"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b6e1c4ba-0236-42b2-bced-69353bf211be
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 9375981db64ec4a1ae523e958423b5f5787cec33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a>Boyutlandırma bilgileri Azure remoteapp'te bir VNET için
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Bir sanal ağ (VNET) ile Azure RemoteApp kullandığınızda, RemoteApp alt ağ içindeki IP adreslerini kullanır. RemoteApp hizmetinizi ölçekte alt ağınızı RemoteApp sanal makineler için kullanılabilir yeterli IP adresine sahip olduğundan emin olun gerekir. Bu boyutlandırma kılavuzluğu nasıl RemoteApp dinamik olarak yukarı döner ve sanal makineleri bir koleksiyon içinde aşağı döner verilen kusursuz olmasa da, alt ağ aralığınızı tahmin etmenize yardımcı olur. Sanal ağ içinde bir RemoteApp hizmete sonra RemoteApp kaldırmadan alt ağ boyutunu artırılamıyor gibi bu özellikle önemlidir.

Maksimum kapasitede çalıştırmak istediğiniz her RemoteApp koleksiyonu için kullanılabilir 100 IP adresleri olmalıdır. Örneğin, standart plana bir RemoteApp koleksiyonu vardır ve en fazla 500 kullanıcıya olmasını istiyorsanız, bu koleksiyon için 100 IP adresi olmalıdır. Benzer şekilde, 100 IP adreslerini 800 kullanıcılara temel planda bir RemoteApp koleksiyonu için gerekir. Az sayıda kullanıcıyla (en büyük değerinden) oluşturmayı planlıyorsanız, koleksiyon gerekli IP adreslerini azaltabilir. En düşük alt ağ boyutu gereksinimdir 30 IP adresleri (/ 27).

Yapılandırılmış ve çalışıyor propertly VNET'İNİZİ emin olmak için aşağıdaki bilgileri kullanıma:

* [Kişisel Sanal ağdan bir Azure sanal ağına geçiş](remoteapp-migratevnet.md)
* [Azure RemoteApp ile kullanmak için Azure VNET doğrula](remoteapp-vnet.md)

