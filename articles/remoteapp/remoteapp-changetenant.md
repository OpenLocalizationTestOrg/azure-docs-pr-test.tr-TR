---
title: "Azure remoteapp'te Azure Active Directory kiracısını değiştirme | Microsoft Docs"
description: "Azure RemoteApp ile ilişkili Azure Active Directory kiracısını değiştirme öğrenin"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 20faf169-6e48-428a-8bdd-f231daff19fa
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 7c6c4ded8a11d8399968b2c32aff055d7f3ae5f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-azure-active-directory-tenant-in-azure-remoteapp"></a>Azure remoteapp'te Azure Active Directory kiracısını değiştirme
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Azure RemoteApp kullanıcı erişimine izin vermek için Azure Active Directory (Azure AD) kullanır. Azure Remoteapp'te kullanabileceğiniz yalnızca Azure AD kiracısı Azure aboneliği ile ilişkili adrestir. İlişkili abonelik görüntüleyebilirsiniz **ayarları** portalında sayfası. Bakmak **Directory** sütunu **abonelikleri** sekmesi.

> [!NOTE]
> Bu değişiklik başarılı olması, var olan tüm Azure RemoteApp koleksiyonları Azure Active Directory kiracısı önce tüm kullanıcıların kaldırın. Bunu yapmak için Azure Portalı'na gidin, Git **Azure RemoteApp** sekmesinde ve her bir Azure RemoteApp koleksiyonu açın. Git **kullanıcılar** sekmesinde ve geçerli Azure Active Directory kiracınıza ait olan kullanıcıların kaldırın. Tüm mevcut Azure RemoteApp koleksiyonları için yineleyin. Bunu yapmazsanız, oluşturmak veya koleksiyonlar düzeltme eki mümkün olmaz.
> 
> 

Farklı bir kiracı kullanmak istiyorsanız, aboneliğinizi ilişkilendirmesini değiştirmek için aşağıdaki adımları kullanın:

1. Portalda, Azure AD kullanıcısı için erişim Azure RemoteApp koleksiyonları için verdiniz kaldırın. (Yukarıdaki adımları için Not bunu nasıl bakın.)
2. Bir Microsoft hesabı (eski adıyla Live ID) Hizmet Yöneticisi olarak ayarlayın. (Hizmet Yöneticisi zaten olup olmadığını bilmiyorsanız? Tıklayarak öğrenebilirsiniz **ayarlar -> Yöneticiler**.) Şimdi, işte, nasıl değiştirin:
   
   1. Sağ üst köşesinde kullanıcı tıklayın ve ardından **faturamı görüntüle**.
   2. Abonelik'ı tıklatın. Ardından, yeni sayfasında aşağı kaydırın ve tıklatın **Düzenle abonelik ayrıntıları** sağ. (Bu varsa sağ Orta alt tür bulmanıza yardımcı olur.)
   3. Hizmet Yöneticisi olmalıdır kullanıcının Microsoft hesabını girin
3. Şimdi portal dışında oturum ve ardından önceki adımda belirtilen Microsoft hesabıyla oturum açın.
4. ' I tıklatın **yeni App -> hizmetler -> Active Directory dizin -> özel -> oluşturmak**.
5. Altında **Directory**, seçin **var olan dizini kullan**. Şimdi portal dışında oturum, bu nedenle seçin olmasını yapacağız **şimdi oturumunuz için hazır ben**.
6. Oturum Portalı'na eklemek istediğiniz dizinin genel Yöneticisi olarak yedekleyin. (Genel yönetici zaten doğru değilse, sonra bir turu olacaktır oturum açın ve sonra oturumu kapatın.)
7. Oturum açtığınızda aboneliğinizde var olan AD kiracınıza kullanmak isteyip istemediğinizi istenir. Tıklatın **devam**ve ardından **şimdi oturumu**.
8. Yeniden yeniden oturum açın ve geri dönüp **ayarlar -> abonelikler**. Aboneliğinizi seçin ve ardından **dizini Düzenle**. Kullanmak istediğiniz Azure AD kiracısı seçin.

Şimdi kullanım yeni Azure AD Kiracı Azure aboneliği erişimi denetlemek ve Azure RemoteApp kullanıcı erişimi yapılandırmak için kullanabilirsiniz.

