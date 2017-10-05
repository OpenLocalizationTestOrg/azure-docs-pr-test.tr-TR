---
title: "Güvenli LDAP (LDAPS) Azure AD Etki Alanı Hizmetleri'nde yapılandırma | Microsoft Docs"
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
ms.openlocfilehash: 3b19f078b0d6dc3e02d951014056406fd1b099a8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="4d5e3-103">Güvenli LDAP (LDAPS) Azure AD etki alanı Hizmetleri yönetilen etki alanı için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4d5e3-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4d5e3-104">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="4d5e3-104">Before you begin</span></span>
<span data-ttu-id="4d5e3-105">Tamamlandı olun [görev 2 - güvenli LDAP sertifika verme bir. PFX dosyası](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="4d5e3-105">Ensure you've completed [Task 2 - export the secure LDAP certificate to a .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="4d5e3-106">Bu görevi tamamlamak için Azure portal deneyimi Önizleme veya Klasik Azure Portalı'nı kullanıp kullanmayacağınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-106">Choose whether to use the preview Azure portal experience or the Azure classic portal to complete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="4d5e3-107">**Azure portal (Önizleme)**: [etkinleştir güvenli LDAP Azure Portalı'nı kullanarak](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="4d5e3-107">**Azure portal (Preview)**: [Enable secure LDAP using the Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="4d5e3-108">**Klasik Azure portalı**: [etkinleştir güvenli LDAP Klasik Azure Portalı'nı kullanarak](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="4d5e3-108">**Azure classic portal**: [Enable secure LDAP using the classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview"></a><span data-ttu-id="4d5e3-109">Görev 3 - güvenli LDAP (Önizleme) Azure portalını kullanarak yönetilen etki alanı için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="4d5e3-109">Task 3 - enable secure LDAP for the managed domain using the Azure portal (Preview)</span></span>
<span data-ttu-id="4d5e3-110">Güvenli LDAP etkinleştirmek için aşağıdaki yapılandırma adımlarını gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4d5e3-110">To enable secure LDAP, perform the following configuration steps:</span></span>

1. <span data-ttu-id="4d5e3-111">Gidin  **[Azure portal](https://portal.azure.com)**.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-111">Navigate to the **[Azure portal](https://portal.azure.com)**.</span></span>

2. <span data-ttu-id="4d5e3-112">Arama 'etki alanı Hizmetleri'nde' **arama kaynakları** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-112">Search for 'domain services' in the **Search resources** search box.</span></span> <span data-ttu-id="4d5e3-113">Seçin **Azure AD etki alanı Hizmetleri** arama sonuç.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-113">Select **Azure AD Domain Services** from the search result.</span></span> <span data-ttu-id="4d5e3-114">**Azure AD etki alanı Hizmetleri** dikey penceresinde, yönetilen etki alanınız listelenir.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-114">The **Azure AD Domain Services** blade lists your managed domain.</span></span>

    ![Yönetilen etki alanı sağlanacak Bul](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="4d5e3-116">Etki alanı hakkında daha fazla ayrıntı görmek için yönetilen etki alanının adını (örneğin, ' contoso100.com')'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-116">Click the name of the managed domain (for example, 'contoso100.com') to see more details about the domain.</span></span>

    ![Etki alanı hizmetleri - sağlama durumu](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="4d5e3-118">Tıklatın **güvenli LDAP** Gezinti Bölmesi.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-118">Click **Secure LDAP** on the navigation pane.</span></span>

    ![Etki Alanı Hizmetleri - güvenli LDAP dikey penceresi](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. <span data-ttu-id="4d5e3-120">Varsayılan olarak, yönetilen etki alanınız için güvenli LDAP erişim devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-120">By default, secure LDAP access to your managed domain is disabled.</span></span> <span data-ttu-id="4d5e3-121">İki durumlu **güvenli LDAP** için **etkinleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-121">Toggle **Secure LDAP** to **Enable**.</span></span>

    ![Güvenli LDAP etkinleştir](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. <span data-ttu-id="4d5e3-123">Varsayılan olarak, internet üzerinden yönetilen etki alanınız için güvenli LDAP erişim devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-123">By default, secure LDAP access to your managed domain over the internet is disabled.</span></span> <span data-ttu-id="4d5e3-124">İki durumlu **Internet üzerinden güvenli LDAP erişim izni** için **etkinleştirmek**istenirse.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-124">Toggle **Allow secure LDAP access over the internet** to **Enable**, if desired.</span></span> 

6. <span data-ttu-id="4d5e3-125">Klasör simgesine aşağıdaki **. Güvenli LDAP Sertifika PFX dosyası**.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-125">Click the folder icon following **.PFX file with secure LDAP certificate**.</span></span> <span data-ttu-id="4d5e3-126">Güvenli LDAP erişim yönetilen etki alanı için sertifikayla PFX dosyasının yolunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-126">Specify the path to the PFX file with the certificate for secure LDAP access to the managed domain.</span></span>

7. <span data-ttu-id="4d5e3-127">Belirtin **şifresini çözmek için parola. PFX dosyası**.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-127">Specify the **Password to decrypt .PFX file**.</span></span> <span data-ttu-id="4d5e3-128">Sertifika PFX dosyasına dışarı aktarılırken kullanılan aynı parolayı belirtin.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-128">Provide the same password you used when exporting the certificate to the PFX file.</span></span>

8. <span data-ttu-id="4d5e3-129">İşiniz bittiğinde tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-129">When you are done, click the **Save** button.</span></span>

9. <span data-ttu-id="4d5e3-130">Yönetilen etki alanı için yapılandırılan LDAP güvenli bildiren bir bildirim görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-130">You see a notification that informs you secure LDAP is being configured for the managed domain.</span></span> <span data-ttu-id="4d5e3-131">Bu işlem tamamlanana kadar diğer etki alanı ayarlarını değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-131">Until this operation is complete, you cannot modify other settings for the domain.</span></span>

    ![Güvenli LDAP yönetilen etki alanı için yapılandırma](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> <span data-ttu-id="4d5e3-133">Yönetilen etki alanınız için güvenli LDAP etkinleştirmek için yaklaşık 10-15 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-133">It takes about 10 to 15 minutes to enable secure LDAP for your managed domain.</span></span> <span data-ttu-id="4d5e3-134">Sağlanan güvenli LDAP sertifika gereken ölçütleri eşleşmiyorsa, güvenli LDAP dizin için etkin değil ve bir hata görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-134">If the provided secure LDAP certificate does not match the required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="4d5e3-135">Örneğin, etki alanı adı hatalı olduğu, sertifikanın süresi dolmuş veya süresi yakında doluyor.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-135">For example, the domain name is incorrect, the certificate has already expired or expires soon.</span></span> <span data-ttu-id="4d5e3-136">Bu durumda, geçerli bir sertifikayla yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-136">In this case, retry with a valid certificate.</span></span>
>
>

<br>

## <a name="task-4---configure-dns-to-access-the-managed-domain-from-the-internet"></a><span data-ttu-id="4d5e3-137">Görev 4 - internet'ten yönetilen etki alanına erişmek için DNS yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4d5e3-137">Task 4 - configure DNS to access the managed domain from the internet</span></span>
> [!NOTE]
> <span data-ttu-id="4d5e3-138">**İsteğe bağlı görev** -, düşünmüyorsanız LDAPS kullanarak internet yönetilen etki alanına erişmek için bu yapılandırma görevi atlayın.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-138">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="4d5e3-139">Bu görev başlamadan önce özetlenen adımları tamamladığınızdan emin olun [görev 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="4d5e3-139">Before you begin this task, ensure you have completed the steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="4d5e3-140">Güvenli LDAP erişim internet üzerinden yönetilen etki alanınız için etkinleştirdikten sonra DNS istemci bilgisayarları Bu yönetilen etki alanı bulabilmesi için güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-140">Once you have enabled secure LDAP access over the internet for your managed domain, you need to update DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="4d5e3-141">Dış IP adresini gösterilir görev 3 sonunda **özellikleri** dikey penceresinde **dış IP adresi için LDAPS erişim**.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-141">At the end of task 3, an external IP address is displayed on the **Properties** blade in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="4d5e3-142">(Örneğin, ' ldaps.contoso100.com') yönetilen etki alanının DNS adı bu dış IP adresine işaret eden dış DNS sağlayıcınız yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-142">Configure your external DNS provider so that the DNS name of the managed domain (for example, 'ldaps.contoso100.com') points to this external IP address.</span></span> <span data-ttu-id="4d5e3-143">Bizim örneğimizde aşağıdaki DNS girişini oluşturmak üzere ihtiyacımız var:</span><span class="sxs-lookup"><span data-stu-id="4d5e3-143">In our example, we need to create the following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="4d5e3-144">İşte bu kadar - güvenli LDAP internet üzerinden kullanarak yönetilen etki alanına bağlanmak artık hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-144">That's it - you are now ready to connect to the managed domain using secure LDAP over the internet.</span></span>

> [!WARNING]
> <span data-ttu-id="4d5e3-145">İstemci bilgisayarları LDAPS kullanarak yönetilen etki alanı başarıyla bağlanabilmesi için LDAPS sertifikayı veren güvenmelidir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-145">Remember that client computers must trust the issuer of the LDAPS certificate to be able to connect successfully to the managed domain using LDAPS.</span></span> <span data-ttu-id="4d5e3-146">Genel olarak güvenilir bir sertifika yetkilisi kullanıyorsanız, istemci bilgisayarlar bu sertifikayı verenler güven bu yana bir şey yapmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-146">If you are using a publicly trusted certification authority, you do not need to do anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="4d5e3-147">Kendinden imzalı bir sertifika kullanıyorsanız, otomatik olarak imzalanan sertifika ortak parçasını istemci bilgisayarındaki güvenilen sertifika deposuna yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-147">If you are using a self-signed certificate, install the public part of the self-signed certificate into the trusted certificate store on the client computer.</span></span>
>
>


## <a name="task-5---lock-down-ldaps-access-to-your-managed-domain-over-the-internet"></a><span data-ttu-id="4d5e3-148">Görev 5 - internet üzerinden yönetilen etki alanınız için kilitleme LDAPS erişim</span><span class="sxs-lookup"><span data-stu-id="4d5e3-148">Task 5 - lock-down LDAPS access to your managed domain over the internet</span></span>
> [!NOTE]
> <span data-ttu-id="4d5e3-149">**İsteğe bağlı görev** - internet üzerinden yönetilen etki alanına LDAPS erişim etkinleştirmediyseniz, bu yapılandırma görevi atlayın.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-149">**Optional task** - If you have not enabled LDAPS access to the managed domain over the internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="4d5e3-150">Bu görev başlamadan önce özetlenen adımları tamamladığınızdan emin olun [görev 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="4d5e3-150">Before you begin this task, ensure you have completed the steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="4d5e3-151">Yönetilen etki alanınız LDAPS erişim için internet üzerinden kullanıma sunan bir güvenlik tehdidi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-151">Exposing your managed domain for LDAPS access over the internet represents a security threat.</span></span> <span data-ttu-id="4d5e3-152">Yönetilen etki alanı güvenli LDAP için kullanılan bağlantı noktası Internet'ten erişilebilir olduğundan (diğer bir deyişle, bağlantı noktası 636).</span><span class="sxs-lookup"><span data-stu-id="4d5e3-152">The managed domain is reachable from the internet at the port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="4d5e3-153">Bu nedenle, belirli bilinen IP adreslerini yönetilen etki alanına erişimi kısıtlamak seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-153">Therefore, you can choose to restrict access to the managed domain to specific known IP addresses.</span></span> <span data-ttu-id="4d5e3-154">Gelişmiş güvenlik için bir ağ güvenlik grubu (NSG) oluşturun ve Azure AD Etki Alanı Hizmetleri'ni etkinleştirdiğiniz alt ağı ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-154">For improved security, create a network security group (NSG) and associate it with the subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="4d5e3-155">Aşağıdaki tabloda bir örnek, internet üzerinden güvenli LDAP erişim kilitlemek için yapılandırabileceğiniz NSG gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-155">The following table illustrates a sample NSG you can configure, to lock down secure LDAP access over the internet.</span></span> <span data-ttu-id="4d5e3-156">NSG gelen LDAPS erişim TCP bağlantı noktası IP adreslerinin üzerinden 636 belirtilen kümesinden yalnızca izin veren kurallar kümesini içerir.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-156">The NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="4d5e3-157">Varsayılan 'DenyAll' kural, internet'ten diğer gelen trafik için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-157">The default 'DenyAll' rule applies to all other inbound traffic from the internet.</span></span> <span data-ttu-id="4d5e3-158">Belirtilen IP adreslerini Internet üzerinden LDAPS erişime izin verecek şekilde NSG kuralı DenyAll NSG kural daha yüksek önceliğe sahip.</span><span class="sxs-lookup"><span data-stu-id="4d5e3-158">The NSG rule to allow LDAPS access over the internet from specified IP addresses has a higher priority than the DenyAll NSG rule.</span></span>

![Örnek internet üzerinden LDAPS erişimi güvenli hale getirmek için NSG](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="4d5e3-160">**Daha fazla bilgi** - [ağ güvenlik grupları](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="4d5e3-160">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="4d5e3-161">İlgili içerik</span><span class="sxs-lookup"><span data-stu-id="4d5e3-161">Related content</span></span>
* [<span data-ttu-id="4d5e3-162">Azure AD etki alanı Hizmetleri - başlangıç kılavuzu</span><span class="sxs-lookup"><span data-stu-id="4d5e3-162">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="4d5e3-163">Azure AD Domain Services tarafından yönetilen etki alanını yönetme</span><span class="sxs-lookup"><span data-stu-id="4d5e3-163">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="4d5e3-164">Grup İlkesi, bir Azure AD etki alanı Hizmetleri yönetilen etki alanını yönetme</span><span class="sxs-lookup"><span data-stu-id="4d5e3-164">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="4d5e3-165">Ağ güvenlik grupları</span><span class="sxs-lookup"><span data-stu-id="4d5e3-165">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="4d5e3-166">Bir ağ güvenlik grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="4d5e3-166">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
