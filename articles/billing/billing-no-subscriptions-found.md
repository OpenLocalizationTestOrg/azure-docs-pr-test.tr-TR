---
title: "Abonelik bulunamadı hatası Azure portalında veya Azure hesap merkezi oturum açmaya çalıştığınızda | Microsoft Docs"
description: "Hayır abonelik bulunamadı hata oluşur. sorunu için çözüm sağlar Azure portalında veya Azure hesap merkezi ne zaman oturum açın."
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: d1545298-99db-4941-8e97-f24a06bb7cb6
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: genli
ms.openlocfilehash: a4ce9b219c05f8469379c2aac5241fcfffd16033
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a>Abonelik Azure portalında veya Azure hesap merkezi hata bulunamadı
Oturum açmaya çalıştığınızda "abonelik bulunamadı" hata iletisini alabilirsiniz [Azure portal](https://portal.azure.com/) veya [Azure hesap Merkezi](https://account.windowsazure.com/Subscriptions). Bu makalede, bu sorun için bir çözüm sağlar.

## <a name="symptom"></a>Belirti

Oturum açmaya çalıştığınızda [Azure portal](https://portal.azure.com/) veya [Azure hesap Merkezi](https://account.windowsazure.com/Subscriptions), aşağıdaki hata iletisini alıyorsunuz: "abonelik bulunamadı".

## <a name="cause"></a>Nedeni

Hesabınızın yeterli izinleri yoksa, bu sorun oluşur. 

## <a name="solution"></a>Çözüm

Doğru yönetici olarak oturum açtığınızdan emin olun. Bir hesabı yönetici yalnızca hesap merkezi erişebilir. Hizmet yöneticileri (SA) ve ortak Yöneticiler (CA) yalnızca Azure portalından veya Klasik Azure portalı için erişim iznine sahip.

### <a name="scenario-1-error-message-is-received-in-the-azure-portalhttpsportalazurecom"></a>Senaryo 1: Hata iletisi alındığında [Azure portalı](https://portal.azure.com)

Bu sorunu gidermek için:

* Hesabınızı sağ üst köşedeki tıklayarak doğru Azure directory seçildiğinden emin olun.

  ![Üst dizini seçin Azure portalının sağ](./media/billing-no-subscriptions-found/directory-switch.png)

* Sağ Azure directory seçilir, ancak hata iletisini almaya devam [sahibi olarak eklenen hesabınızın](billing-add-change-azure-subscription-administrator.md).

### <a name="scenario-2-error-message-is-received-in-the-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a>Senaryo 2: Hata iletisi alındığında [Azure hesap Merkezi](https://account.windowsazure.com/Subscriptions)

Kullandığınız hesabın hesap yöneticisi olup olmadığını denetleyin. Hesap Yöneticisi olan doğrulamak için aşağıdaki adımları izleyin:

1. [Azure Portal](https://portal.azure.com) oturum açın.
2. Hub menüsünde seçin **abonelik**.
3. Kontrol edin ve ardından istediğiniz aboneliği seçin **ayarları**.
4. Seçin **özellikleri**. Aboneliğin Hesap Yöneticisi görüntülenen **Hesap Yöneticisi** kutusu.

## <a name="need-help-contact-support"></a>Yardım mı gerekiyor? Desteğe başvurun.
Hala yardıma gereksiniminiz varsa [desteğine başvurun](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) hızla çözümlenen sorunu almak için. 
