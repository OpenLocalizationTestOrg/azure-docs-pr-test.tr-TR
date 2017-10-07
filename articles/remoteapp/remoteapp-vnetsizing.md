---
title: "Azure remoteapp'te bir VNET için aaaSizing bilgi | Microsoft Docs"
description: "Bir VNET ile birlikte çalışan Azure RemoteApp için başlangıç IP adresi gereksinimleri hakkında bilgi edinin"
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
ms.openlocfilehash: f98b831af32c41740b258d122b3e18765be08d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a>Boyutlandırma bilgileri Azure remoteapp'te bir VNET için
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Bir sanal ağ (VNET) ile Azure RemoteApp kullandığınızda, RemoteApp hello alt ağ içindeki IP adreslerini kullanır. RemoteApp hizmetinizi Hello ölçeğini bağlı olarak, alt ağınızı RemoteApp sanal makineler için kullanılabilir yeterli IP adresine sahip tooensure gerekir. Bu boyutlandırma kılavuzluğu nasıl RemoteApp dinamik olarak yukarı döner ve sanal makineleri bir koleksiyon içinde aşağı döner verilen kusursuz olmasa da, alt ağ aralığınızı tahmin etmenize yardımcı olur. Sanal ağ içinde bir RemoteApp hizmete sonra RemoteApp kaldırmadan hello alt ağ boyutunu artırılamıyor gibi bu özellikle önemlidir.

En büyük kapasitesini toorun istediğiniz her RemoteApp koleksiyonu için kullanılabilir 100 IP adresleri olmalıdır. Örneğin, bir RemoteApp koleksiyonu hello standart planda varsa ve toohave hello en fazla 500 kullanıcıya istediğiniz, bu koleksiyon için 100 IP adresi olmalıdır. Benzer şekilde, 100 IP adreslerini 800 kullanıcısı olan hello temel planda bir RemoteApp koleksiyonu için gerekir. (Küçüktür hello maksimum) daha az kullanıcı toohave planlıyorsanız, koleksiyon gerekli hello IP adreslerini azaltabilir. Merhaba en düşük alt ağ boyutu gereksinimdir, 30 IP adresleri (/ 27).

Bilgi toomake ağınızı yapılandırıldığından emin izleyen ve propertly çalışma hello denetleyin:

* [Kişisel VNET tooan Azure VNET geçirme](remoteapp-migratevnet.md)
* [Azure RemoteApp ile Hello Azure VNET toouse doğrula](remoteapp-vnet.md)

