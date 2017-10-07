---
title: "Güvenli LDAP (LDAPS) Azure AD Etki Alanı Hizmetleri'nde aaaConfigure | Microsoft Docs"
description: "Güvenli LDAP (LDAPS) bir Azure AD etki alanı Hizmetleri yönetilen etki alanını yapılandırın"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9d563c45-9578-410d-96c8-355af64feae8
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: a0d6e2faf474b1f0cbe157fb4ae2754b1d521ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="39329-103">Güvenli LDAP (LDAPS) Azure AD etki alanı Hizmetleri yönetilen etki alanı için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="39329-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="39329-104">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="39329-104">Before you begin</span></span>
<span data-ttu-id="39329-105">Tamamlandı olun [görev 2 - verme hello güvenli LDAP sertifika tooa. PFX dosyası](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="39329-105">Ensure you've completed [Task 2 - export hello secure LDAP certificate tooa .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="39329-106">Toouse Önizleme Azure portal deneyimi hello veya bu görevi Azure Klasik portalı toocomplete hello seçin.</span><span class="sxs-lookup"><span data-stu-id="39329-106">Choose whether toouse hello preview Azure portal experience or hello Azure classic portal toocomplete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="39329-107">**Azure portal (Önizleme)**: [etkinleştir LDAP hello Azure portal kullanarak güvenli](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="39329-107">**Azure portal (Preview)**: [Enable secure LDAP using hello Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="39329-108">**Klasik Azure portalı**: [etkinleştir güvenli LDAP hello Klasik Azure portalını kullanarak](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="39329-108">**Azure classic portal**: [Enable secure LDAP using hello classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-classic-azure-portal"></a><span data-ttu-id="39329-109">Görev 3 - güvenli LDAP hello Klasik Azure portalını kullanarak hello yönetilen etki alanı için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="39329-109">Task 3 - enable secure LDAP for hello managed domain using hello classic Azure portal</span></span>
<span data-ttu-id="39329-110">tooenable LDAP güvenli, hello aşağıdaki yapılandırma adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="39329-110">tooenable secure LDAP, perform hello following configuration steps:</span></span>

1. <span data-ttu-id="39329-111">Toohello gidin  **[Klasik Azure portalı](https://manage.windowsazure.com)**.</span><span class="sxs-lookup"><span data-stu-id="39329-111">Navigate toohello **[Azure classic portal](https://manage.windowsazure.com)**.</span></span>
2. <span data-ttu-id="39329-112">Select hello **Active Directory** hello sol bölmedeki düğüm.</span><span class="sxs-lookup"><span data-stu-id="39329-112">Select hello **Active Directory** node on hello left pane.</span></span>
3. <span data-ttu-id="39329-113">Azure AD Etki Alanı Hizmetleri'ni etkinleştirdiğiniz hello Azure AD dizini (Ayrıca başvurulan tooas 'Kiracı'), seçin.</span><span class="sxs-lookup"><span data-stu-id="39329-113">Select hello Azure AD directory (also referred tooas 'tenant'), for which you have enabled Azure AD Domain Services.</span></span>

    ![Azure AD Dizini Seçme](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="39329-115">Merhaba tıklatın **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="39329-115">Click hello **Configure** tab.</span></span>

    ![Dizinin yapılandır sekmesi](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="39329-117">Başlıklı toohello bölümüne aşağı kaydırın **etki alanı Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="39329-117">Scroll down toohello section titled **domain services**.</span></span> <span data-ttu-id="39329-118">Başlıklı bir seçenek görmelisiniz **güvenli LDAP (LDAPS)** hello ekran aşağıdaki gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="39329-118">You should see an option titled **Secure LDAP (LDAPS)** as shown in hello following screenshot:</span></span>

    ![Etki Alanı Hizmetleri yapılandırma bölümü](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. <span data-ttu-id="39329-120">Merhaba tıklatın **yapılandırma sertifika...**  hello yukarı düğmesi toobring **güvenli LDAP için sertifika Yapılandır** iletişim.</span><span class="sxs-lookup"><span data-stu-id="39329-120">Click hello **Configure certificate ...** button toobring up hello **Configure Certificate for Secure LDAP** dialog.</span></span>

    ![Güvenli LDAP için sertifika yapılandırma](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. <span data-ttu-id="39329-122">Başlangıç klasörü simgesi aşağıdaki **ile PFX dosyasını sertifika** güvenli LDAP erişim toohello toouse istediğiniz hello sertifikasını içeren toospecify hello PFX dosyası yönetilen etki alanı.</span><span class="sxs-lookup"><span data-stu-id="39329-122">Click hello folder icon following **PFX FILE WITH CERTIFICATE** toospecify hello PFX file, which contains hello certificate you wish toouse for secure LDAP access toohello managed domain.</span></span> <span data-ttu-id="39329-123">Ayrıca hello toohello sertifika.pfx dosyası dışarı aktarılırken belirtilir hello parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="39329-123">Also enter hello password you specified when exporting hello certificate toohello PFX file.</span></span> <span data-ttu-id="39329-124">Merhaba alt düğmesinde bitti hello'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="39329-124">Then, click hello done button on hello bottom.</span></span>

    ![Güvenli LDAP PFX dosyası ve parola belirtin](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. <span data-ttu-id="39329-126">Merhaba **etki alanı Hizmetleri** hello bölümünü **yapılandırma** sekmesi gri ve hello olduğu **bekleyen...**  birkaç dakika için durum.</span><span class="sxs-lookup"><span data-stu-id="39329-126">hello **domain services** section of hello **Configure** tab should get grayed out and is in hello **Pending...** state for a few minutes.</span></span> <span data-ttu-id="39329-127">Bu süre boyunca hello LDAPS sertifika doğruluğu için doğrulanır ve güvenli LDAP yönetilen etki alanınız için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="39329-127">During this period, hello LDAPS certificate is verified for accuracy and secure LDAP is configured for your managed domain.</span></span>

    ![LDAP - bekleme durumunda güvenli](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="39329-129">Tooenable güvenli LDAP yönetilen etki alanınız için yaklaşık 10 too15 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="39329-129">It takes about 10 too15 minutes tooenable secure LDAP for your managed domain.</span></span> <span data-ttu-id="39329-130">Merhaba güvenli LDAP sertifika eşleşmiyor sağladıysanız hello ölçütleri gerekli, güvenli LDAP dizin için etkin değil ve bir hata görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="39329-130">If hello provided secure LDAP certificate does not match hello required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="39329-131">Örneğin, hello etki alanı adı hatalı olduğu, hello sertifikanın süresi dolmuş veya süresi yakında doluyor.</span><span class="sxs-lookup"><span data-stu-id="39329-131">For example, hello domain name is incorrect, hello certificate has already expired or expires soon.</span></span>
   >
   >

9. <span data-ttu-id="39329-132">Güvenli LDAP başarıyla yönetilen etki alanınız için etkinleştirildiğinde, hello **bekleniyor...**  ileti görünmemelidir.</span><span class="sxs-lookup"><span data-stu-id="39329-132">When secure LDAP is successfully enabled for your managed domain, hello **Pending...** message should disappear.</span></span> <span data-ttu-id="39329-133">Merhaba sertifikanın parmak izini görüntülenen hello görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="39329-133">You should see hello thumbprint of hello certificate displayed.</span></span>

    ![Güvenli LDAP Etkin](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-hello-internet"></a><span data-ttu-id="39329-135">Görev 4 - hello güvenli LDAP erişimi etkinleştirmek Internet</span><span class="sxs-lookup"><span data-stu-id="39329-135">Task 4 - enable secure LDAP access over hello internet</span></span>
<span data-ttu-id="39329-136">**İsteğe bağlı görev** - LDAPS kullanarak tooaccess hello yönetilen etki alanı düşünmüyorsanız üzerinde Internet Merhaba, bu yapılandırma görevi atlayın.</span><span class="sxs-lookup"><span data-stu-id="39329-136">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>

<span data-ttu-id="39329-137">Bu görev başlamadan önce özetlenen hello adımlarını tamamladığınızdan emin olun [görev 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="39329-137">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span></span>

1. <span data-ttu-id="39329-138">Bir seçenek çok görmeniz gerekir**etkinleştirmek güvenli LDAP erişim üzerinden INTERNET hello** hello içinde **etki alanı Hizmetleri** hello bölümünü **yapılandırma** sayfası.</span><span class="sxs-lookup"><span data-stu-id="39329-138">You should see an option too**ENABLE SECURE LDAP ACCESS OVER hello INTERNET** in hello **domain services** section of hello **Configure** page.</span></span> <span data-ttu-id="39329-139">Bu seçenek çok ayarlanır**Hayır** Internet erişimi toohello yönetilen beri varsayılan etki alanı güvenli LDAP üzerinde varsayılan olarak devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="39329-139">This option is set too**NO** by default since internet access toohello managed domain over secure LDAP is disabled by default.</span></span>

    ![Güvenli LDAP Etkin](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. <span data-ttu-id="39329-141">İki durumlu **etkinleştirmek güvenli LDAP erişim üzerinden INTERNET hello** çok**Evet**.</span><span class="sxs-lookup"><span data-stu-id="39329-141">Toggle **ENABLE SECURE LDAP ACCESS OVER hello INTERNET** too**YES**.</span></span> <span data-ttu-id="39329-142">Merhaba tıklatın **KAYDETMEK** hello alt paneli düğmesinde.</span><span class="sxs-lookup"><span data-stu-id="39329-142">Click hello **SAVE** button on hello bottom panel.</span></span>
    <span data-ttu-id="39329-143">![Güvenli LDAP Etkin](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span><span class="sxs-lookup"><span data-stu-id="39329-143">![Secure LDAP enabled](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span></span>
3. <span data-ttu-id="39329-144">Merhaba **etki alanı Hizmetleri** hello bölümünü **yapılandırma** sekmesi gri ve hello olduğu **bekleyen...**  birkaç dakika için durum.</span><span class="sxs-lookup"><span data-stu-id="39329-144">hello **domain services** section of hello **Configure** tab should get grayed out and is in hello **Pending...** state for a few minutes.</span></span> <span data-ttu-id="39329-145">Bir süre sonra Internet erişim tooyour yönetilen etki alanı güvenli LDAP üzerinden etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="39329-145">After some time, internet access tooyour managed domain over secure LDAP is enabled.</span></span>

    ![LDAP - bekleme durumunda güvenli](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="39329-147">Yaklaşık 10 dakika sürer yönetilen etki alanınız için güvenli LDAP üzerinden tooenable internet erişimi.</span><span class="sxs-lookup"><span data-stu-id="39329-147">It takes about 10 minutes tooenable internet access over secure LDAP for your managed domain.</span></span>
   >
   >
4. <span data-ttu-id="39329-148">Güvenli LDAP erişim tooyour Internet başarıyla etkinleştirildi hello etki alanı yönetildiğinde hello **bekleniyor...**  ileti görünmemelidir.</span><span class="sxs-lookup"><span data-stu-id="39329-148">When secure LDAP access tooyour managed domain over hello internet is successfully enabled, hello **Pending...** message should disappear.</span></span> <span data-ttu-id="39329-149">Merhaba dış IP adresini görmelisiniz kullanılan tooaccess hello alanında LDAPS üzerinden dizininize olabilir **dış IP adresi için LDAPS erişim**.</span><span class="sxs-lookup"><span data-stu-id="39329-149">You should see hello external IP address that can be used tooaccess your directory over LDAPS in hello field **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

    ![Güvenli LDAP Etkin](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a><span data-ttu-id="39329-151">Görev 5 - DNS tooaccess hello yönetilen etki alanından hello yapılandırma Internet</span><span class="sxs-lookup"><span data-stu-id="39329-151">Task 5 - configure DNS tooaccess hello managed domain from hello internet</span></span>
<span data-ttu-id="39329-152">**İsteğe bağlı görev** - LDAPS kullanarak tooaccess hello yönetilen etki alanı düşünmüyorsanız üzerinde Internet Merhaba, bu yapılandırma görevi atlayın.</span><span class="sxs-lookup"><span data-stu-id="39329-152">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>

<span data-ttu-id="39329-153">Bu görev başlamadan önce özetlenen hello adımlarını tamamladığınızdan emin olun [görev 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="39329-153">Before you begin this task, ensure you have completed hello steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="39329-154">Internet üzerinden güvenli LDAP erişim etkinleştirdikten sonra Merhaba, yönetilen etki alanı için istemci bilgisayarlar bu yönetilen etki alanı bulabilmesi için tooupdate DNS gerekir.</span><span class="sxs-lookup"><span data-stu-id="39329-154">Once you have enabled secure LDAP access over hello internet for your managed domain, you need tooupdate DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="39329-155">Görev 4 Hello sonunda, dış IP adresi üzerinde hello görüntülenir **yapılandırma** sekmesinde **dış IP adresi için LDAPS erişim**.</span><span class="sxs-lookup"><span data-stu-id="39329-155">At hello end of task 4, an external IP address is displayed on hello **Configure** tab in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="39329-156">Dış DNS sağlayıcınız bu hello hello DNS adını (örneğin, ' ldaps.contoso100.com') etki alanı noktaları toothis dış IP adresi yönetilen şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="39329-156">Configure your external DNS provider so that hello DNS name of hello managed domain (for example, 'ldaps.contoso100.com') points toothis external IP address.</span></span> <span data-ttu-id="39329-157">Bizim örneğimizde, DNS girişi aşağıdaki toocreate hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="39329-157">In our example, we need toocreate hello following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="39329-158">İşte bu kadar - yönetilen hazır tooconnect toohello sunulmuştur hello Internet üzerinden güvenli LDAP kullanarak etki alanı.</span><span class="sxs-lookup"><span data-stu-id="39329-158">That's it - you are now ready tooconnect toohello managed domain using secure LDAP over hello internet.</span></span>

> [!WARNING]
> <span data-ttu-id="39329-159">İstemci bilgisayarları hello LDAPS sertifika toobe mümkün tooconnect hello verenin başarıyla güvenmelidir unutmayın toohello yönetilen LDAPS kullanarak etki alanı.</span><span class="sxs-lookup"><span data-stu-id="39329-159">Remember that client computers must trust hello issuer of hello LDAPS certificate toobe able tooconnect successfully toohello managed domain using LDAPS.</span></span> <span data-ttu-id="39329-160">Bir kuruluş sertifika yetkilisi veya genel olarak güvenilir bir sertifika yetkilisi kullanıyorsanız, istemci bilgisayarlar bu sertifikayı verenler güven olduğundan, toodo herhangi bir şey gerekmez.</span><span class="sxs-lookup"><span data-stu-id="39329-160">If you are using an enterprise certification authority or a publicly trusted certification authority, you do not need toodo anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="39329-161">Kendinden imzalı bir sertifika kullanıyorsanız, hello istemci bilgisayarda hello güvenilen sertifika deposuna tooinstall hello ortak parçasını hello kendinden imzalı bir sertifika gerekir.</span><span class="sxs-lookup"><span data-stu-id="39329-161">If you are using a self-signed certificate, you need tooinstall hello public part of hello self-signed certificate into hello trusted certificate store on hello client computer.</span></span>
>
>


## <a name="lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a><span data-ttu-id="39329-162">Kilitleme LDAPS erişim tooyour yönetilen etki alanı hello internet</span><span class="sxs-lookup"><span data-stu-id="39329-162">Lock-down LDAPS access tooyour managed domain over hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="39329-163">**İsteğe bağlı görev** - LDAPS etkinleştirmediyseniz erişim toohello yönetilen etki alanı üzerinde Internet Merhaba, bu yapılandırma görevi atlayın.</span><span class="sxs-lookup"><span data-stu-id="39329-163">**Optional task** - If you have not enabled LDAPS access toohello managed domain over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="39329-164">Bu görev başlamadan önce özetlenen hello adımlarını tamamladığınızdan emin olun [görev 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="39329-164">Before you begin this task, ensure you have completed hello steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="39329-165">Internet hello yönetilen etki alanınız LDAPS erişim için gösterme bir güvenlik tehdidi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="39329-165">Exposing your managed domain for LDAPS access over hello internet represents a security threat.</span></span> <span data-ttu-id="39329-166">Merhaba yönetilen etki hello erişilebildiğinden güvenli LDAP için kullanılan hello noktasındaki Internet (diğer bir deyişle, bağlantı noktası 636).</span><span class="sxs-lookup"><span data-stu-id="39329-166">hello managed domain is reachable from hello internet at hello port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="39329-167">Bu nedenle, IP adreslerini bilinen toorestrict erişim toohello yönetilen etki alanı toospecific seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="39329-167">Therefore, you can choose toorestrict access toohello managed domain toospecific known IP addresses.</span></span> <span data-ttu-id="39329-168">Gelişmiş güvenlik için bir ağ güvenlik grubu (NSG) oluşturun ve Azure AD Etki Alanı Hizmetleri'ni etkinleştirdiğiniz hello alt ağı ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="39329-168">For improved security, create a network security group (NSG) and associate it with hello subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="39329-169">Merhaba aşağıdaki tabloda gösterilmektedir örnek yapılandırabilirsiniz, NSG toolock hello üzerinden güvenli LDAP erişim tuşunu Internet.</span><span class="sxs-lookup"><span data-stu-id="39329-169">hello following table illustrates a sample NSG you can configure, toolock down secure LDAP access over hello internet.</span></span> <span data-ttu-id="39329-170">Merhaba NSG gelen LDAPS erişim TCP bağlantı noktası IP adreslerinin üzerinden 636 belirtilen kümesinden yalnızca izin veren kurallar kümesini içerir.</span><span class="sxs-lookup"><span data-stu-id="39329-170">hello NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="39329-171">Merhaba varsayılan 'DenyAll' Kural tooall diğer gelen trafiği hello geçerlidir Internet.</span><span class="sxs-lookup"><span data-stu-id="39329-171">hello default 'DenyAll' rule applies tooall other inbound traffic from hello internet.</span></span> <span data-ttu-id="39329-172">Merhaba NSG kuralı tooallow LDAPS erişimi hello üzerinden internet'ten belirtilen IP adreslerini hello DenyAll NSG kural daha yüksek önceliğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="39329-172">hello NSG rule tooallow LDAPS access over hello internet from specified IP addresses has a higher priority than hello DenyAll NSG rule.</span></span>

![Merhaba Internet üzerinden örnek NSG toosecure LDAPS erişim](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="39329-174">**Daha fazla bilgi** - [ağ güvenlik grupları](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="39329-174">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="39329-175">İlgili içerik</span><span class="sxs-lookup"><span data-stu-id="39329-175">Related content</span></span>
* [<span data-ttu-id="39329-176">Azure AD etki alanı Hizmetleri - başlangıç kılavuzu</span><span class="sxs-lookup"><span data-stu-id="39329-176">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="39329-177">Azure AD Domain Services tarafından yönetilen etki alanını yönetme</span><span class="sxs-lookup"><span data-stu-id="39329-177">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="39329-178">Grup İlkesi, bir Azure AD etki alanı Hizmetleri yönetilen etki alanını yönetme</span><span class="sxs-lookup"><span data-stu-id="39329-178">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="39329-179">Ağ güvenlik grupları</span><span class="sxs-lookup"><span data-stu-id="39329-179">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="39329-180">Bir ağ güvenlik grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="39329-180">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
