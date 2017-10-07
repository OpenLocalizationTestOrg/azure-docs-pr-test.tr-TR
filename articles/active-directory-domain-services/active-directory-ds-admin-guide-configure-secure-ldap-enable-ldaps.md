---
title: "Güvenli LDAP (LDAPS) Azure AD Etki Alanı Hizmetleri'nde aaaConfigure | Microsoft Docs"
description: "Güvenli LDAP (LDAPS) bir Azure AD etki alanı Hizmetleri yönetilen etki alanını yapılandırın"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 8781285cd02d690788056b985b017efd7e4d6b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="cbde4-103">Güvenli LDAP (LDAPS) Azure AD etki alanı Hizmetleri yönetilen etki alanı için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cbde4-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="cbde4-104">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="cbde4-104">Before you begin</span></span>
<span data-ttu-id="cbde4-105">Tamamlandı olun [görev 2 - verme hello güvenli LDAP sertifika tooa. PFX dosyası](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="cbde4-105">Ensure you've completed [Task 2 - export hello secure LDAP certificate tooa .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="cbde4-106">Toouse Önizleme Azure portal deneyimi hello veya bu görevi Azure Klasik portalı toocomplete hello seçin.</span><span class="sxs-lookup"><span data-stu-id="cbde4-106">Choose whether toouse hello preview Azure portal experience or hello Azure classic portal toocomplete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="cbde4-107">**Azure portal (Önizleme)**: [etkinleştir LDAP hello Azure portal kullanarak güvenli](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="cbde4-107">**Azure portal (Preview)**: [Enable secure LDAP using hello Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="cbde4-108">**Klasik Azure portalı**: [etkinleştir güvenli LDAP hello Klasik Azure portalını kullanarak](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="cbde4-108">**Azure classic portal**: [Enable secure LDAP using hello classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-azure-portal-preview"></a><span data-ttu-id="cbde4-109">Görev 3 - güvenli LDAP hello Azure portal (Önizleme) kullanarak hello yönetilen etki alanı için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="cbde4-109">Task 3 - enable secure LDAP for hello managed domain using hello Azure portal (Preview)</span></span>
<span data-ttu-id="cbde4-110">tooenable LDAP güvenli, hello aşağıdaki yapılandırma adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cbde4-110">tooenable secure LDAP, perform hello following configuration steps:</span></span>

1. <span data-ttu-id="cbde4-111">Toohello gidin  **[Azure portal](https://portal.azure.com)**.</span><span class="sxs-lookup"><span data-stu-id="cbde4-111">Navigate toohello **[Azure portal](https://portal.azure.com)**.</span></span>

2. <span data-ttu-id="cbde4-112">' Etki alanı Hizmetleri'nde' hello Ara **arama kaynakları** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="cbde4-112">Search for 'domain services' in hello **Search resources** search box.</span></span> <span data-ttu-id="cbde4-113">Seçin **Azure AD etki alanı Hizmetleri** hello arama sonuç.</span><span class="sxs-lookup"><span data-stu-id="cbde4-113">Select **Azure AD Domain Services** from hello search result.</span></span> <span data-ttu-id="cbde4-114">Merhaba **Azure AD etki alanı Hizmetleri** dikey penceresinde, yönetilen etki alanınız listelenir.</span><span class="sxs-lookup"><span data-stu-id="cbde4-114">hello **Azure AD Domain Services** blade lists your managed domain.</span></span>

    ![Yönetilen etki alanı sağlanacak Bul](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="cbde4-116">Merhaba etki alanı hakkında daha fazla ayrıntı hello yönetilen etki alanı (örneğin, ' contoso100.com') toosee Hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cbde4-116">Click hello name of hello managed domain (for example, 'contoso100.com') toosee more details about hello domain.</span></span>

    ![Etki alanı hizmetleri - sağlama durumu](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="cbde4-118">Tıklatın **güvenli LDAP** hello Gezinti Bölmesi.</span><span class="sxs-lookup"><span data-stu-id="cbde4-118">Click **Secure LDAP** on hello navigation pane.</span></span>

    ![Etki Alanı Hizmetleri - güvenli LDAP dikey penceresi](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. <span data-ttu-id="cbde4-120">Varsayılan olarak güvenli LDAP erişim tooyour yönetilen etki alanı devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="cbde4-120">By default, secure LDAP access tooyour managed domain is disabled.</span></span> <span data-ttu-id="cbde4-121">İki durumlu **güvenli LDAP** çok**etkinleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="cbde4-121">Toggle **Secure LDAP** too**Enable**.</span></span>

    ![Güvenli LDAP etkinleştir](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. <span data-ttu-id="cbde4-123">Varsayılan olarak, güvenli LDAP erişim tooyour etki alanı Internet devre dışı hello yönetilir.</span><span class="sxs-lookup"><span data-stu-id="cbde4-123">By default, secure LDAP access tooyour managed domain over hello internet is disabled.</span></span> <span data-ttu-id="cbde4-124">İki durumlu **Internet üzerinden güvenli LDAP erişim izni ver hello** çok**etkinleştirmek**istenirse.</span><span class="sxs-lookup"><span data-stu-id="cbde4-124">Toggle **Allow secure LDAP access over hello internet** too**Enable**, if desired.</span></span> 

6. <span data-ttu-id="cbde4-125">Başlangıç klasörü simgesi aşağıdaki **. Güvenli LDAP Sertifika PFX dosyası**.</span><span class="sxs-lookup"><span data-stu-id="cbde4-125">Click hello folder icon following **.PFX file with secure LDAP certificate**.</span></span> <span data-ttu-id="cbde4-126">Güvenli LDAP erişim toohello yönetilen etki alanı için hello sertifikasıyla Hello yol toohello PFX dosyası belirtin.</span><span class="sxs-lookup"><span data-stu-id="cbde4-126">Specify hello path toohello PFX file with hello certificate for secure LDAP access toohello managed domain.</span></span>

7. <span data-ttu-id="cbde4-127">Merhaba belirtin **parola toodecrypt. PFX dosyası**.</span><span class="sxs-lookup"><span data-stu-id="cbde4-127">Specify hello **Password toodecrypt .PFX file**.</span></span> <span data-ttu-id="cbde4-128">Merhaba sağlamak hello toohello sertifika.pfx dosyası dışa aktarırken kullanılan aynı parola.</span><span class="sxs-lookup"><span data-stu-id="cbde4-128">Provide hello same password you used when exporting hello certificate toohello PFX file.</span></span>

8. <span data-ttu-id="cbde4-129">İşiniz bittiğinde, hello tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cbde4-129">When you are done, click hello **Save** button.</span></span>

9. <span data-ttu-id="cbde4-130">Güvenli LDAP hello yönetilen etki alanı için yapılandırılmış bildiren bir bildirim görür.</span><span class="sxs-lookup"><span data-stu-id="cbde4-130">You see a notification that informs you secure LDAP is being configured for hello managed domain.</span></span> <span data-ttu-id="cbde4-131">Bu işlem tamamlanana kadar diğer hello etki alanı ayarlarını değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbde4-131">Until this operation is complete, you cannot modify other settings for hello domain.</span></span>

    ![Güvenli LDAP hello yönetilen etki alanı için yapılandırma](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> <span data-ttu-id="cbde4-133">Tooenable güvenli LDAP yönetilen etki alanınız için yaklaşık 10 too15 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="cbde4-133">It takes about 10 too15 minutes tooenable secure LDAP for your managed domain.</span></span> <span data-ttu-id="cbde4-134">Merhaba güvenli LDAP sertifika eşleşmiyor sağladıysanız hello ölçütleri gerekli, güvenli LDAP dizin için etkin değil ve bir hata görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbde4-134">If hello provided secure LDAP certificate does not match hello required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="cbde4-135">Örneğin, hello etki alanı adı hatalı olduğu, hello sertifikanın süresi dolmuş veya süresi yakında doluyor.</span><span class="sxs-lookup"><span data-stu-id="cbde4-135">For example, hello domain name is incorrect, hello certificate has already expired or expires soon.</span></span> <span data-ttu-id="cbde4-136">Bu durumda, geçerli bir sertifikayla yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="cbde4-136">In this case, retry with a valid certificate.</span></span>
>
>

<br>

## <a name="task-4---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a><span data-ttu-id="cbde4-137">Görev 4 - DNS tooaccess hello yönetilen etki alanından hello yapılandırma Internet</span><span class="sxs-lookup"><span data-stu-id="cbde4-137">Task 4 - configure DNS tooaccess hello managed domain from hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="cbde4-138">**İsteğe bağlı görev** - LDAPS kullanarak tooaccess hello yönetilen etki alanı düşünmüyorsanız üzerinde Internet Merhaba, bu yapılandırma görevi atlayın.</span><span class="sxs-lookup"><span data-stu-id="cbde4-138">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="cbde4-139">Bu görev başlamadan önce özetlenen hello adımlarını tamamladığınızdan emin olun [görev 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="cbde4-139">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="cbde4-140">Internet üzerinden güvenli LDAP erişim etkinleştirdikten sonra Merhaba, yönetilen etki alanı için istemci bilgisayarlar bu yönetilen etki alanı bulabilmesi için tooupdate DNS gerekir.</span><span class="sxs-lookup"><span data-stu-id="cbde4-140">Once you have enabled secure LDAP access over hello internet for your managed domain, you need tooupdate DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="cbde4-141">Görev 3 Hello sonunda, dış IP adresi üzerinde hello görüntülenir **özellikleri** dikey penceresinde **dış IP adresi için LDAPS erişim**.</span><span class="sxs-lookup"><span data-stu-id="cbde4-141">At hello end of task 3, an external IP address is displayed on hello **Properties** blade in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="cbde4-142">Dış DNS sağlayıcınız bu hello hello DNS adını (örneğin, ' ldaps.contoso100.com') etki alanı noktaları toothis dış IP adresi yönetilen şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cbde4-142">Configure your external DNS provider so that hello DNS name of hello managed domain (for example, 'ldaps.contoso100.com') points toothis external IP address.</span></span> <span data-ttu-id="cbde4-143">Bizim örneğimizde, DNS girişi aşağıdaki toocreate hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="cbde4-143">In our example, we need toocreate hello following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="cbde4-144">İşte bu kadar - yönetilen hazır tooconnect toohello sunulmuştur hello Internet üzerinden güvenli LDAP kullanarak etki alanı.</span><span class="sxs-lookup"><span data-stu-id="cbde4-144">That's it - you are now ready tooconnect toohello managed domain using secure LDAP over hello internet.</span></span>

> [!WARNING]
> <span data-ttu-id="cbde4-145">İstemci bilgisayarları hello LDAPS sertifika toobe mümkün tooconnect hello verenin başarıyla güvenmelidir unutmayın toohello yönetilen LDAPS kullanarak etki alanı.</span><span class="sxs-lookup"><span data-stu-id="cbde4-145">Remember that client computers must trust hello issuer of hello LDAPS certificate toobe able tooconnect successfully toohello managed domain using LDAPS.</span></span> <span data-ttu-id="cbde4-146">Genel olarak güvenilir bir sertifika yetkilisi kullanıyorsanız, istemci bilgisayarlar bu sertifikayı verenler güven olduğundan, toodo herhangi bir şey gerekmez.</span><span class="sxs-lookup"><span data-stu-id="cbde4-146">If you are using a publicly trusted certification authority, you do not need toodo anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="cbde4-147">Kendinden imzalı bir sertifika kullanıyorsanız, hello otomatik olarak imzalanan sertifika ortak parçasını hello hello istemci bilgisayarda hello güvenilen sertifika deposuna yükleyin.</span><span class="sxs-lookup"><span data-stu-id="cbde4-147">If you are using a self-signed certificate, install hello public part of hello self-signed certificate into hello trusted certificate store on hello client computer.</span></span>
>
>


## <a name="task-5---lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a><span data-ttu-id="cbde4-148">Görev 5 - kilitleme LDAPS erişim tooyour yönetilen etki alanı üzerinde hello Internet</span><span class="sxs-lookup"><span data-stu-id="cbde4-148">Task 5 - lock-down LDAPS access tooyour managed domain over hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="cbde4-149">**İsteğe bağlı görev** - LDAPS etkinleştirmediyseniz erişim toohello yönetilen etki alanı üzerinde Internet Merhaba, bu yapılandırma görevi atlayın.</span><span class="sxs-lookup"><span data-stu-id="cbde4-149">**Optional task** - If you have not enabled LDAPS access toohello managed domain over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="cbde4-150">Bu görev başlamadan önce özetlenen hello adımlarını tamamladığınızdan emin olun [görev 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="cbde4-150">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="cbde4-151">Internet hello yönetilen etki alanınız LDAPS erişim için gösterme bir güvenlik tehdidi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="cbde4-151">Exposing your managed domain for LDAPS access over hello internet represents a security threat.</span></span> <span data-ttu-id="cbde4-152">Merhaba yönetilen etki hello erişilebildiğinden güvenli LDAP için kullanılan hello noktasındaki Internet (diğer bir deyişle, bağlantı noktası 636).</span><span class="sxs-lookup"><span data-stu-id="cbde4-152">hello managed domain is reachable from hello internet at hello port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="cbde4-153">Bu nedenle, IP adreslerini bilinen toorestrict erişim toohello yönetilen etki alanı toospecific seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbde4-153">Therefore, you can choose toorestrict access toohello managed domain toospecific known IP addresses.</span></span> <span data-ttu-id="cbde4-154">Gelişmiş güvenlik için bir ağ güvenlik grubu (NSG) oluşturun ve Azure AD Etki Alanı Hizmetleri'ni etkinleştirdiğiniz hello alt ağı ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="cbde4-154">For improved security, create a network security group (NSG) and associate it with hello subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="cbde4-155">Merhaba aşağıdaki tabloda gösterilmektedir örnek yapılandırabilirsiniz, NSG toolock hello üzerinden güvenli LDAP erişim tuşunu Internet.</span><span class="sxs-lookup"><span data-stu-id="cbde4-155">hello following table illustrates a sample NSG you can configure, toolock down secure LDAP access over hello internet.</span></span> <span data-ttu-id="cbde4-156">Merhaba NSG gelen LDAPS erişim TCP bağlantı noktası IP adreslerinin üzerinden 636 belirtilen kümesinden yalnızca izin veren kurallar kümesini içerir.</span><span class="sxs-lookup"><span data-stu-id="cbde4-156">hello NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="cbde4-157">Merhaba varsayılan 'DenyAll' Kural tooall diğer gelen trafiği hello geçerlidir Internet.</span><span class="sxs-lookup"><span data-stu-id="cbde4-157">hello default 'DenyAll' rule applies tooall other inbound traffic from hello internet.</span></span> <span data-ttu-id="cbde4-158">Merhaba NSG kuralı tooallow LDAPS erişimi hello üzerinden internet'ten belirtilen IP adreslerini hello DenyAll NSG kural daha yüksek önceliğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="cbde4-158">hello NSG rule tooallow LDAPS access over hello internet from specified IP addresses has a higher priority than hello DenyAll NSG rule.</span></span>

![Merhaba Internet üzerinden örnek NSG toosecure LDAPS erişim](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="cbde4-160">**Daha fazla bilgi** - [ağ güvenlik grupları](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="cbde4-160">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="cbde4-161">İlgili içerik</span><span class="sxs-lookup"><span data-stu-id="cbde4-161">Related content</span></span>
* [<span data-ttu-id="cbde4-162">Azure AD etki alanı Hizmetleri - başlangıç kılavuzu</span><span class="sxs-lookup"><span data-stu-id="cbde4-162">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="cbde4-163">Azure AD Domain Services tarafından yönetilen etki alanını yönetme</span><span class="sxs-lookup"><span data-stu-id="cbde4-163">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="cbde4-164">Grup İlkesi, bir Azure AD etki alanı Hizmetleri yönetilen etki alanını yönetme</span><span class="sxs-lookup"><span data-stu-id="cbde4-164">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="cbde4-165">Ağ güvenlik grupları</span><span class="sxs-lookup"><span data-stu-id="cbde4-165">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="cbde4-166">Bir ağ güvenlik grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="cbde4-166">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
