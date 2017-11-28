---
title: "Azure AD Connect eşitleme: hello AD DS hesap parolası değiştiriliyor | Microsoft Docs"
description: "Bu konuda belge tooupdate hello AD DS hesabı hello parola sonra Azure AD Connect nasıl değiştirilir açıklar."
services: active-directory
keywords: "AD DS hesabı, Active Directory hesap parolası"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2707c9246446612f8d083ecde876b3b4fb2435ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-ad-ds-account-password"></a><span data-ttu-id="30f6b-104">Merhaba AD DS hesap parolasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="30f6b-104">Changing hello AD DS account password</span></span>
<span data-ttu-id="30f6b-105">Merhaba AD DS hesap şirket içi Active Directory ile Azure AD Connect toocommunicate tarafından kullanılan toohello kullanıcı hesabına başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="30f6b-105">hello AD DS account refers toohello user account used by Azure AD Connect toocommunicate with on-premises Active Directory.</span></span> <span data-ttu-id="30f6b-106">Merhaba AD DS hesabı hello parolasını değiştirirseniz, Azure AD Connect eşitleme hizmeti hello yeni parolayla güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="30f6b-106">If you change hello password of hello AD DS account, you must update Azure AD Connect Synchronization Service with hello new password.</span></span> <span data-ttu-id="30f6b-107">Aksi takdirde eşitleme artık doğru şekilde hello ile eşitleyebilirsiniz hello içi Active Directory ve aşağıdaki hatalar hello karşılaşırsınız:</span><span class="sxs-lookup"><span data-stu-id="30f6b-107">Otherwise, hello Synchronization can no longer synchronize correctly with hello on-premises Active Directory and you will encounter hello following errors:</span></span>

* <span data-ttu-id="30f6b-108">Hello Eşitleme Hizmeti Yöneticisi, içeri aktarma veya dışarı aktarma işlemi AD başarısız ile şirket içi **Hayır başlangıç kimlik** hata.</span><span class="sxs-lookup"><span data-stu-id="30f6b-108">In hello Synchronization Service Manager, any import or export operation with on-premises AD fails with **no-start-credentials** error.</span></span>

* <span data-ttu-id="30f6b-109">Windows Olay Görüntüleyicisi'ni altında hello uygulama olay günlüğüne bir hata ile içeren **olay kimliği 6000** ve ileti **'hello yönetim Aracısı "contoso.com" başarısız toorun hello kimlik bilgileri geçersiz olduğundan'** .</span><span class="sxs-lookup"><span data-stu-id="30f6b-109">Under Windows Event Viewer, hello application event log contains an error with **Event ID 6000** and message **'hello management agent "contoso.com" failed toorun because hello credentials were invalid'**.</span></span>


## <a name="how-tooupdate-hello-synchronization-service-with-new-password-for-ad-ds-account"></a><span data-ttu-id="30f6b-110">Nasıl tooupdate hello eşitleme hizmeti ile AD DS hesabı için yeni parola</span><span class="sxs-lookup"><span data-stu-id="30f6b-110">How tooupdate hello Synchronization Service with new password for AD DS account</span></span>
<span data-ttu-id="30f6b-111">Merhaba yeni parolayla tooupdate hello eşitleme hizmeti:</span><span class="sxs-lookup"><span data-stu-id="30f6b-111">tooupdate hello Synchronization Service with hello new password:</span></span>

1. <span data-ttu-id="30f6b-112">Merhaba Eşitleme Hizmeti Yöneticisi'ni (Başlangıç → eşitleme hizmeti) başlatın.</span><span class="sxs-lookup"><span data-stu-id="30f6b-112">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="30f6b-113">![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="30f6b-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  

2. <span data-ttu-id="30f6b-114">Toohello Git **Bağlayıcılar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="30f6b-114">Go toohello **Connectors** tab.</span></span>

3. <span data-ttu-id="30f6b-115">Select hello **AD Bağlayıcısı** toohello AD DS hesap parolası değiştirildi karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="30f6b-115">Select hello **AD Connector** that corresponds toohello AD DS account for which its password was changed.</span></span>

4. <span data-ttu-id="30f6b-116">Altında **Eylemler**seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="30f6b-116">Under **Actions**, select **Properties**.</span></span>

5. <span data-ttu-id="30f6b-117">Merhaba açılan iletişim kutusunda seçin **tooActive Directory ormanına Bağlan**:</span><span class="sxs-lookup"><span data-stu-id="30f6b-117">In hello pop-up dialog, select **Connect tooActive Directory Forest**:</span></span>

6. <span data-ttu-id="30f6b-118">Yeni bir parola Hello hello AD DS hesabının hello girin **parola** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="30f6b-118">Enter hello new password of hello AD DS account in hello **Password** textbox.</span></span>

7. <span data-ttu-id="30f6b-119">Tıklatın **Tamam** toosave hello yeni parola ve Kapat hello açılan iletişim.</span><span class="sxs-lookup"><span data-stu-id="30f6b-119">Click **OK** toosave hello new password and close hello pop-up dialog.</span></span>

8. <span data-ttu-id="30f6b-120">Hello Azure AD Connect eşitleme hizmeti altında Windows Hizmet Denetimi Yöneticisi'ni yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="30f6b-120">Restart hello Azure AD Connect Synchronization Service under Windows Service Control Manager.</span></span> <span data-ttu-id="30f6b-121">Tooensure budur, başvuru toohello eski parola hello bellek önbellekten kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="30f6b-121">This is tooensure that any reference toohello old password is removed from hello memory cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30f6b-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="30f6b-122">Next steps</span></span>
<span data-ttu-id="30f6b-123">**Genel bakış konuları**</span><span class="sxs-lookup"><span data-stu-id="30f6b-123">**Overview topics**</span></span>

* [<span data-ttu-id="30f6b-124">Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme</span><span class="sxs-lookup"><span data-stu-id="30f6b-124">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="30f6b-125">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="30f6b-125">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
