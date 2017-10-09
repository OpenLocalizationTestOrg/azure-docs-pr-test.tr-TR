---
title: "Azure remoteapp'te aaaChange hello Azure Active Directory Kiracı | Microsoft Docs"
description: "Nasıl toochange hello Azure Active Directory kiracısı Azure RemoteApp ile ilgili bilgi edinin"
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
ms.openlocfilehash: d0928b099b7fcfb3ab16077e295d7aaf519c3653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-azure-active-directory-tenant-in-azure-remoteapp"></a>Azure remoteapp'te Hello Azure Active Directory kiracısını değiştirme
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Azure RemoteApp Azure Active Directory (Azure AD) tooallow kullanıcı erişimi kullanır. Azure Remoteapp'te kullanabileceğiniz hello yalnızca Azure AD Kiracı hello bir hello Azure aboneliği ile ilişkili ' dir. İlişkili hello abonelik üzerinde hello görüntüleyebilirsiniz **ayarları** hello portalında sayfası. Ara hello **Directory** hello sütunu **abonelikleri** sekmesi.

> [!NOTE]
> Bu değişiklik toosucceed için tüm Azure RemoteApp koleksiyonları hello var olan Azure Active Directory kiracısı önce tüm kullanıcıların kaldırın. toodo Bu, Git toohello Azure Portal, Git toohello **Azure RemoteApp** sekmesinde ve her bir Azure RemoteApp koleksiyonu açın. Toohello Git **kullanıcılar** sekmesinde ve tooyour geçerli Azure Active Directory Kiracı ait olan kullanıcıların kaldırın. Tüm mevcut Azure RemoteApp koleksiyonları için yineleyin. Bunu yapmazsanız, mümkün toocreate ya da düzeltme eki koleksiyonları olmaz.
> 
> 

Toouse farklı bir kiracıya istiyorsanız, bu adımları toochange hello ilişkilendirme aboneliğinizle kullanın:

1. Tüm Azure AD kullanıcıların toowhich Hello Portalı'nda kaldırmak tooAzure RemoteApp koleksiyonları erişim verilir. (Hakkında adımlar için yukarıdaki hello nota bakın toodo bu.)
2. Bir Microsoft hesabı (eski adıyla Live ID) hello Hizmet Yöneticisi olarak ayarlayın. (Hello Hizmet Yöneticisi zaten olup olmadığını bilmiyorsanız? Tıklayarak öğrenebilirsiniz **ayarlar -> Yöneticiler**.) Şimdi, işte, nasıl değiştirin:
   
   1. Merhaba sağ üst köşesindeki Hello kullanıcı tıklayın ve ardından **faturamı görüntüle**.
   2. Merhaba aboneliğe tıklayın. Ardından, hello yeni sayfasında aşağı kaydırın ve tıklatın **abonelik bilgilerini Düzenle** hello doğru olarak. (Merhaba sağ Bu, bir orta alt tür bulmanıza yardımcı olur.)
   3. Hello Hizmet Yöneticisi olmalıdır hello kullanıcının Microsoft hesabını Hello yazın
3. Artık dışında hello portalında oturum ve ardından geri hello hello önceki adımda belirtilen Microsoft hesabı oturum açın.
4. ' I tıklatın **yeni App -> hizmetler -> Active Directory dizin -> özel -> oluşturmak**.
5. Altında **Directory**, seçin **var olan dizini kullan**. Yapacağız toohave toosign hello şimdi portal dışında böylece seçtiğiniz **şimdi oturumu kapattınız hazır toobe ben**.
6. Merhaba tekrar oturum tooadd istediğiniz hello dizininin genel yönetici olarak portal. (Genel yönetici zaten doğru değilse, sonra bir turu olacaktır oturum açın ve sonra oturumu kapatın.)
7. Aboneliğinizde var olan AD kiracınız toouse istiyorsanız, oturum açtığınızda istenir. Tıklatın **devam**ve ardından **şimdi oturumu**.
8. Yeniden yeniden oturum açın ve dön çok**ayarlar -> abonelikler**. Aboneliğinizi seçin ve ardından **dizini Düzenle**. Hello Azure AD Kiracı toouse istediğinizi seçin.

Artık Azure Remoteapp'te hello yeni Azure AD Kiracı toocontrol erişim toohello Azure aboneliği ve tooconfigure kullanıcı erişimini kullanabilirsiniz.

