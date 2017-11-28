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
ms.openlocfilehash: 93afa49166c5b31d23237c308b9d34f6d6f3507d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="90360-103">Güvenli LDAP (LDAPS) Azure AD etki alanı Hizmetleri yönetilen etki alanı için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="90360-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="90360-104">Bu makalede, Azure AD etki alanı Hizmetleri yönetilen etki alanınız için Güvenli Basit Dizin Erişim Protokolü (LDAPS) nasıl etkinleştirebilirsiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="90360-104">This article shows how you can enable Secure Lightweight Directory Access Protocol (LDAPS) for your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="90360-105">Güvenli LDAP olduğu olarak da bilinen ' Basit Dizin Erişim Protokolü (LDAP) Güvenli Yuva Katmanı (SSL) üzerinden / Aktarım Katmanı Güvenliği (TLS)'.</span><span class="sxs-lookup"><span data-stu-id="90360-105">Secure LDAP is also known as 'Lightweight Directory Access Protocol (LDAP) over Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="90360-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="90360-106">Before you begin</span></span>
<span data-ttu-id="90360-107">Bu makalede listelenen görevleri gerçekleştirmek için gerekir:</span><span class="sxs-lookup"><span data-stu-id="90360-107">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="90360-108">Geçerli bir **Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="90360-108">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="90360-109">Bir **Azure AD dizini** -ya da bir şirket içi dizin veya bir yalnızca bulut dizini ile eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="90360-109">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="90360-110">**Azure AD etki alanı Hizmetleri** Azure AD dizini için etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="90360-110">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="90360-111">Bunu yapmadıysanız, özetlenen tüm görevleri izleyin [Getting Started guide](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="90360-111">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="90360-112">A **güvenli LDAP etkinleştirmek için kullanılan sertifikayı**.</span><span class="sxs-lookup"><span data-stu-id="90360-112">A **certificate to be used to enable secure LDAP**.</span></span>

   * <span data-ttu-id="90360-113">**Önerilen** -bir güvenilir bir ortak sertifika yetkilisinden bir sertifika edinin.</span><span class="sxs-lookup"><span data-stu-id="90360-113">**Recommended** - Obtain a certificate from a trusted public certification authority.</span></span> <span data-ttu-id="90360-114">Bu yapılandırma seçeneği daha güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="90360-114">This configuration option is more secure.</span></span>
   * <span data-ttu-id="90360-115">Alternatif olarak, siz de seçebilirsiniz [otomatik olarak imzalanan sertifika oluşturma](#task-1---obtain-a-certificate-for-secure-ldap) bu makalenin sonraki bölümlerinde gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="90360-115">Alternately, you may also choose to [create a self-signed certificate](#task-1---obtain-a-certificate-for-secure-ldap) as shown later in this article.</span></span>

<br>

### <a name="requirements-for-the-secure-ldap-certificate"></a><span data-ttu-id="90360-116">Güvenli LDAP sertifika için gereksinimler</span><span class="sxs-lookup"><span data-stu-id="90360-116">Requirements for the secure LDAP certificate</span></span>
<span data-ttu-id="90360-117">Güvenli LDAP etkinleştirmeden önce aşağıdaki yönergeleri başına geçerli bir sertifika edinin.</span><span class="sxs-lookup"><span data-stu-id="90360-117">Acquire a valid certificate per the following guidelines, before you enable secure LDAP.</span></span> <span data-ttu-id="90360-118">Güvenli LDAP geçersiz/hatalı bir sertifika ile yönetilen etki alanınız için etkinleştirmeye çalışırsanız hatalarıyla karşılaşırsanız.</span><span class="sxs-lookup"><span data-stu-id="90360-118">You encounter failures if you try to enable secure LDAP for your managed domain with an invalid/incorrect certificate.</span></span>

1. <span data-ttu-id="90360-119">**Güvenilen veren** -sertifika güvenli LDAP kullanarak yönetilen etki alanına bağlanma bilgisayarlar tarafından güvenilen bir yetkili tarafından verilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="90360-119">**Trusted issuer** - The certificate must be issued by an authority trusted by computers connecting to the managed domain using secure LDAP.</span></span> <span data-ttu-id="90360-120">Bu yetkilisi bu bilgisayarlar tarafından güvenilen bir genel sertifika yetkilisinin olabilir.</span><span class="sxs-lookup"><span data-stu-id="90360-120">This authority may be a public certification authority trusted by these computers.</span></span>
2. <span data-ttu-id="90360-121">**Yaşam süresi** -sertifika en az sonraki 3-6 ay için geçerli olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="90360-121">**Lifetime** - The certificate must be valid for at least the next 3-6 months.</span></span> <span data-ttu-id="90360-122">Sertifikanın süresi dolduğunda, yönetilen etki alanınız güvenli LDAP erişim bozulur.</span><span class="sxs-lookup"><span data-stu-id="90360-122">Secure LDAP access to your managed domain is disrupted when the certificate expires.</span></span>
3. <span data-ttu-id="90360-123">**Konu adı** -yönetilen etki alanınız için joker karakter sertifika üzerindeki konu adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="90360-123">**Subject name** - The subject name on the certificate must be a wildcard for your managed domain.</span></span> <span data-ttu-id="90360-124">Örneğin, etki alanınızın 'contoso100.com' adlı sertifikanın konu adı olması gerekir ' *. contoso100.com'.</span><span class="sxs-lookup"><span data-stu-id="90360-124">For instance, if your domain is named 'contoso100.com', the certificate's subject name must be '*.contoso100.com'.</span></span> <span data-ttu-id="90360-125">DNS adı (konu alternatif adı) Bu joker karakter adına ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="90360-125">Set the DNS name (subject alternate name) to this wildcard name.</span></span>
4. <span data-ttu-id="90360-126">**Anahtar kullanımı** -için aşağıdaki kullanır - dijital imzalar ve anahtar şifreleme sertifikası yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="90360-126">**Key usage** - The certificate must be configured for the following uses - Digital signatures and key encipherment.</span></span>
5. <span data-ttu-id="90360-127">**Sertifika amacı** -sertifikayı SSL sunucu kimlik doğrulaması için geçerli olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="90360-127">**Certificate purpose** - The certificate must be valid for SSL server authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="90360-128">**Kuruluş sertifika yetkilileri:** Azure AD etki alanı Hizmetleri, kuruluşunuzun Kurumsal Sertifika yetkilisi tarafından verilen güvenli LDAP sertifikaları kullanarak desteklemez.</span><span class="sxs-lookup"><span data-stu-id="90360-128">**Enterprise Certification Authorities:** Azure AD Domain Services does not support using secure LDAP certificates issued by your organization's enterprise certification authority.</span></span> <span data-ttu-id="90360-129">Bu kısıtlama, hizmet kuruluş kök sertifika yetkilisi olarak CA'nız güvenmezse olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="90360-129">This restriction is because the service does not trust your enterprise CA as a root certification authority.</span></span> 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a><span data-ttu-id="90360-130">Görev 1 - güvenli LDAP için bir sertifika edinin</span><span class="sxs-lookup"><span data-stu-id="90360-130">Task 1 - obtain a certificate for secure LDAP</span></span>
<span data-ttu-id="90360-131">İlk görev, yönetilen etki alanına güvenli LDAP erişim için kullanılan bir sertifika edinme içerir.</span><span class="sxs-lookup"><span data-stu-id="90360-131">The first task involves obtaining a certificate used for secure LDAP access to the managed domain.</span></span> <span data-ttu-id="90360-132">İki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="90360-132">You have two options:</span></span>

* <span data-ttu-id="90360-133">Bir sertifika yetkilisinden bir sertifika edinin.</span><span class="sxs-lookup"><span data-stu-id="90360-133">Obtain a certificate from a certification authority.</span></span> <span data-ttu-id="90360-134">Yetkili bir ortak sertifika yetkilisi olabilir.</span><span class="sxs-lookup"><span data-stu-id="90360-134">The authority may be a public certification authority.</span></span>
* <span data-ttu-id="90360-135">Kendinden imzalı bir sertifika oluşturun.</span><span class="sxs-lookup"><span data-stu-id="90360-135">Create a self-signed certificate.</span></span>

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a><span data-ttu-id="90360-136">(Önerilen). seçenek - bir sertifika yetkilisinden bir güvenli LDAP sertifikası alın</span><span class="sxs-lookup"><span data-stu-id="90360-136">Option A (Recommended) - Obtain a secure LDAP certificate from a certification authority</span></span>
<span data-ttu-id="90360-137">Kuruluşunuz bir ortak sertifika yetkilisi sertifikalarını alırsa, bu ortak sertifika yetkilisinden güvenli LDAP sertifika edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="90360-137">If your organization obtains its certificates from a public certification authority, you need to obtain the secure LDAP certificate from that public certification authority.</span></span>

<span data-ttu-id="90360-138">Anlatılan tüm gereksinimleri karşılayan bir sertifika isterken olun [güvenli LDAP sertifika için gereksinimler](#requirements-for-the-secure-ldap-certificate).</span><span class="sxs-lookup"><span data-stu-id="90360-138">When requesting a certificate, ensure that you satisfy all the requirements outlined in [Requirements for the secure LDAP certificate](#requirements-for-the-secure-ldap-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="90360-139">Güvenli LDAP kullanarak yönetilen etki alanına bağlanmak için gereken istemci bilgisayarlar güvenli LDAP sertifikayı veren güvenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="90360-139">Client computers that need to connect to the managed domain using secure LDAP must trust the issuer of the secure LDAP certificate.</span></span>
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a><span data-ttu-id="90360-140">Seçeneği B - güvenli LDAP için otomatik olarak imzalanan sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="90360-140">Option B - Create a self-signed certificate for secure LDAP</span></span>
<span data-ttu-id="90360-141">Bir ortak sertifika yetkilisinden bir sertifika kullanmayı düşünmüyorsanız güvenli LDAP için otomatik olarak imzalanan bir sertifika oluşturmak tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90360-141">If you do not expect to use a certificate from a public certification authority, you may choose to create a self-signed certificate for secure LDAP.</span></span>

<span data-ttu-id="90360-142">**PowerShell kullanarak otomatik olarak imzalanan bir sertifika oluşturun**</span><span class="sxs-lookup"><span data-stu-id="90360-142">**Create a self-signed certificate using PowerShell**</span></span>

<span data-ttu-id="90360-143">Windows bilgisayarınızda olarak yeni bir PowerShell penceresi açın **yönetici** ve yeni bir otomatik olarak imzalanan sertifika oluşturmak için aşağıdaki komutları yazın.</span><span class="sxs-lookup"><span data-stu-id="90360-143">On your Windows computer, open a new PowerShell window as **Administrator** and type the following commands, to create a new self-signed certificate.</span></span>

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

<span data-ttu-id="90360-144">Önceki örnekte, Değiştir '*. contoso100.com', yönetilen etki alanınızın DNS etki alanı adına sahip. 'Contoso100.onmicrosoft.com' adında yönetilen bir etki alanı oluşturduysanız, for example, Değiştir '*. contoso100.com' ile yukarıdaki komut dosyasındaki ' *. contoso100.onmicrosoft.com').</span><span class="sxs-lookup"><span data-stu-id="90360-144">In the preceding sample, replace '*.contoso100.com' with the DNS domain name of your managed domain. For example, if you created a managed domain called 'contoso100.onmicrosoft.com', replace '*.contoso100.com' in the above script with '*.contoso100.onmicrosoft.com').</span></span>

![Azure AD Dizini Seçme](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

<span data-ttu-id="90360-146">Yeni oluşturulan otomatik olarak imzalanan sertifika, yerel makinenin sertifika deposuna yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="90360-146">The newly created self-signed certificate is placed in the local machine's certificate store.</span></span>


## <a name="next-step"></a><span data-ttu-id="90360-147">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="90360-147">Next step</span></span>
[<span data-ttu-id="90360-148">Görev 2 - güvenli LDAP sertifika verme bir. PFX dosyası</span><span class="sxs-lookup"><span data-stu-id="90360-148">Task 2 - export the secure LDAP certificate to a .PFX file</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
