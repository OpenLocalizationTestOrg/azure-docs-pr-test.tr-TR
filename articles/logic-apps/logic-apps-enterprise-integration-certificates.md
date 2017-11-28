---
title: Enterprise Integration Pack aaaUsing sertifikalarla | Microsoft Docs
description: "Enterprise Integration Pack Merhaba ile nasıl toouse sertifikaları öğrenin | Azure mantıksal uygulamaları"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: cgronlun
ms.assetid: 4cbffd85-fe8d-4dde-aa5b-24108a7caa7d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 7ba9f597a03a852a9ba05d2af08fe4bc2d98aef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a><span data-ttu-id="036a3-103">Sertifikalar ve Enterprise Integration Pack hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="036a3-103">Learn about certificates and Enterprise Integration Pack</span></span>
## <a name="overview"></a><span data-ttu-id="036a3-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="036a3-104">Overview</span></span>
<span data-ttu-id="036a3-105">Enterprise Integration sertifikaları toosecure B2B iletişimleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="036a3-105">Enterprise integration uses certificates toosecure B2B communications.</span></span> <span data-ttu-id="036a3-106">Enterprise Integration uygulamalarınızda iki sertifika türünü kullanarak şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="036a3-106">You can use two types of certificates in your enterprise integration apps:</span></span>

* <span data-ttu-id="036a3-107">Ortak Sertifikalar, sertifika yetkilisinden (CA) satın alınması gerekir.</span><span class="sxs-lookup"><span data-stu-id="036a3-107">Public certificates, which must be purchased from a certification authority (CA).</span></span>
* <span data-ttu-id="036a3-108">Özel sertifikaları kendiniz uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="036a3-108">Private certificates, which you can issue yourself.</span></span> <span data-ttu-id="036a3-109">Bu sertifikalar bazen başvurulan tooas otomatik olarak imzalanan sertifikalar.</span><span class="sxs-lookup"><span data-stu-id="036a3-109">These certificates are sometimes referred tooas self-signed certificates.</span></span>

## <a name="what-are-certificates"></a><span data-ttu-id="036a3-110">Sertifikalar nelerdir?</span><span class="sxs-lookup"><span data-stu-id="036a3-110">What are certificates?</span></span>
<span data-ttu-id="036a3-111">Sertifikalar elektronik iletişimin hello katılımcıları hello kimliğini doğrulamak ve ayrıca elektronik iletişimleri güvenli dijital belgelerdir.</span><span class="sxs-lookup"><span data-stu-id="036a3-111">Certificates are digital documents that verify hello identity of hello participants in electronic communications and that also secure electronic communications.</span></span>

## <a name="why-use-certificates"></a><span data-ttu-id="036a3-112">Sertifikaları neden kullanılır?</span><span class="sxs-lookup"><span data-stu-id="036a3-112">Why use certificates?</span></span>
<span data-ttu-id="036a3-113">Bazen B2B iletişimleri gizli tutulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="036a3-113">Sometimes B2B communications must be kept confidential.</span></span> <span data-ttu-id="036a3-114">Enterprise Integration sertifikaları toosecure bu iletişimler iki yolla kullanır:</span><span class="sxs-lookup"><span data-stu-id="036a3-114">Enterprise integration uses certificates toosecure these communications in two ways:</span></span>

* <span data-ttu-id="036a3-115">İletileri Merhaba içeriğine şifreleyerek</span><span class="sxs-lookup"><span data-stu-id="036a3-115">By encrypting hello contents of messages</span></span>
* <span data-ttu-id="036a3-116">İletileri imzalamak tarafından</span><span class="sxs-lookup"><span data-stu-id="036a3-116">By digitally signing messages</span></span>  

## <a name="upload-a-public-certificate"></a><span data-ttu-id="036a3-117">Ortak sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="036a3-117">Upload a public certificate</span></span>

<span data-ttu-id="036a3-118">toouse bir *ortak sertifika* B2B özellikleriyle logic apps içinde ilk tooupload hello sertifika tümleştirme hesabınızda gerekir.</span><span class="sxs-lookup"><span data-stu-id="036a3-118">toouse a *public certificate* in your logic apps with B2B capabilities, you first need tooupload hello certificate into your integration account.</span></span>  

<span data-ttu-id="036a3-119">Bir sertifika yükledikten sonra güvenli B2B iletilerinizi hello özelliklerini tanımladığınızda kullanılabilir toohelp olan [anlaşmaları](logic-apps-enterprise-integration-agreements.md) oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="036a3-119">After you upload a certificate, it's available toohelp you secure your B2B messages when you define their properties in hello [agreements](logic-apps-enterprise-integration-agreements.md) that you create.</span></span>  

<span data-ttu-id="036a3-120">Merhaba toohello Azure portalında oturum sonra ortak sertifikalarınızı tümleştirme hesabınızda karşıya yükleme için ayrıntılı adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="036a3-120">Here are hello detailed steps for uploading your public certificates into your integration account after you sign in toohello Azure portal:</span></span>

1. <span data-ttu-id="036a3-121">Seçin **daha fazla hizmet** ve girin **tümleştirme** hello filtre arama kutusuna.</span><span class="sxs-lookup"><span data-stu-id="036a3-121">Select **More services** and enter **integration** in hello filter search box.</span></span> <span data-ttu-id="036a3-122">Seçin **tümleştirme hesapları** hello sonuçları listesinden</span><span class="sxs-lookup"><span data-stu-id="036a3-122">Select **Integration Accounts** from hello results list</span></span>     
<span data-ttu-id="036a3-123">![Gözat seçin](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span><span class="sxs-lookup"><span data-stu-id="036a3-123">![Select Browse](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span></span>  
2. <span data-ttu-id="036a3-124">Hello tümleştirme hesabı toowhich tooadd hello sertifika istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="036a3-124">Select hello integration account toowhich you want tooadd hello certificate.</span></span>  
![Merhaba tümleştirme hesabı toowhich tooadd hello sertifika istediğiniz seçin](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. <span data-ttu-id="036a3-126">Select hello **sertifikaları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="036a3-126">Select hello **Certificates** tile.</span></span>  
<span data-ttu-id="036a3-127">![Select hello sertifikaları döşeme](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="036a3-127">![Select hello Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>
4. <span data-ttu-id="036a3-128">Merhaba, **sertifikaları** açar, select hello dikey **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="036a3-128">In hello **Certificates** blade that opens, select hello **Add** button.</span></span>   
<span data-ttu-id="036a3-129">![Merhaba Ekle düğmesini seçin](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="036a3-129">![Select hello Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
5. <span data-ttu-id="036a3-130">Girin bir **adı** sertifika ve ardından hello sertifika türü olarak **ortak** gelen hello açılır.</span><span class="sxs-lookup"><span data-stu-id="036a3-130">Enter a **Name** for your certificate, and then select hello certificate type as **public** from hello dropdown.</span></span>  
6. <span data-ttu-id="036a3-131">Select hello klasör simgesine hello hello sağ tarafındaki **sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="036a3-131">Select hello folder icon on hello right side of hello **Certificate** text box.</span></span> <span data-ttu-id="036a3-132">Merhaba dosya seçiciyi oturum açtığında, bulun ve tooupload tooyour tümleştirme hesabını istediğiniz hello sertifika dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="036a3-132">When hello file picker opens, find and select hello certificate file that you want tooupload tooyour integration account.</span></span>
7. <span data-ttu-id="036a3-133">Merhaba sertifikayı seçin ve ardından **Tamam** hello dosya Seçici.</span><span class="sxs-lookup"><span data-stu-id="036a3-133">Select hello certificate, and then select **OK** in hello file picker.</span></span> <span data-ttu-id="036a3-134">Bu doğrular ve hello sertifika tooyour tümleştirme hesabı yükler.</span><span class="sxs-lookup"><span data-stu-id="036a3-134">This validates and uploads hello certificate tooyour integration account.</span></span>
8. <span data-ttu-id="036a3-135">Son olarak, üzerinde hello geri **sertifika Ekle** dikey penceresinde, select hello **Tamam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="036a3-135">Finally, back on hello **Add certificate** blade, select hello **OK** button.</span></span>  
<span data-ttu-id="036a3-136">![Merhaba Tamam düğmesini seçin](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span><span class="sxs-lookup"><span data-stu-id="036a3-136">![Select hello OK button](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span></span>  
9. <span data-ttu-id="036a3-137">Select hello **sertifikaları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="036a3-137">Select hello **Certificates** tile.</span></span> <span data-ttu-id="036a3-138">Merhaba sertifika yeni eklenen görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="036a3-138">You should see hello newly added certificate.</span></span>  
<span data-ttu-id="036a3-139">![Merhaba yeni sertifika bakın](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span><span class="sxs-lookup"><span data-stu-id="036a3-139">![See hello new certificate](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span></span>  

## <a name="upload-a-private-certificate"></a><span data-ttu-id="036a3-140">Özel bir sertifika karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="036a3-140">Upload a private certificate</span></span>

<span data-ttu-id="036a3-141">toouse bir *özel sertifika* B2B özellikleriyle logic apps içinde aşağıdaki adımları alma hello tarafından özel sertifika tooyour tümleştirme hesabı karşıya yükleyebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="036a3-141">toouse a *private certificate* in your logic apps with B2B capabilities, You can upload a private certificate tooyour integration account by taking hello following steps</span></span>

1. <span data-ttu-id="036a3-142">[Özel anahtar tooKey kasası karşıya](../key-vault/key-vault-get-started.md "anahtar kasası hakkında bilgi edinin") ve sağlayan bir **anahtar adı**</span><span class="sxs-lookup"><span data-stu-id="036a3-142">[Upload your private key tooKey Vault](../key-vault/key-vault-get-started.md "Learn about Key Vault") and provide a **Key Name**</span></span> 
   
   > [!TIP]
   > <span data-ttu-id="036a3-143">Anahtar kasası Logic Apps tooperform işlemleri yetkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="036a3-143">You must authorize Logic Apps tooperform operations on Key Vault.</span></span> <span data-ttu-id="036a3-144">Merhaba aşağıdaki PowerShell komutunu kullanarak erişim toohello Logic Apps hizmet sorumlusu verebilirsiniz:`Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span><span class="sxs-lookup"><span data-stu-id="036a3-144">You can grant access toohello Logic Apps service principal by using hello following PowerShell command: `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span></span>  
   > 
   > 

<span data-ttu-id="036a3-145">Merhaba önceki adımı ayırdıktan sonra bir özel sertifika toointegration hesabı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="036a3-145">After you've taken hello previous step, add a private certificate toointegration account.</span></span>

<span data-ttu-id="036a3-146">Aşağıdaki hello toohello Azure portalında oturum sonra özel sertifikalarınızı tümleştirme hesabınızda karşıya yükleme için ayrıntılı adımlar:</span><span class="sxs-lookup"><span data-stu-id="036a3-146">Following are hello detailed steps for uploading your private certificates into your integration account after you sign in toohello Azure portal:</span></span>  
 
1. <span data-ttu-id="036a3-147">Tooadd hello sertifika istediğiniz ve seçin hello hello tümleştirme hesap toowhich seçin **sertifikaları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="036a3-147">Select hello integration account toowhich you want tooadd hello certificate and select hello **Certificates** tile.</span></span>  
<span data-ttu-id="036a3-148">![Select hello sertifikaları döşeme](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="036a3-148">![Select hello Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>  
2. <span data-ttu-id="036a3-149">Merhaba, **sertifikaları** açar, select hello dikey **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="036a3-149">In hello **Certificates** blade that opens, select hello **Add** button.</span></span>   
<span data-ttu-id="036a3-150">![Merhaba Ekle düğmesini seçin](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="036a3-150">![Select hello Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
3. <span data-ttu-id="036a3-151">Girin bir **adı** sertifika ve select hello sertifika türü olarak **özel** gelen hello açılır.</span><span class="sxs-lookup"><span data-stu-id="036a3-151">Enter a **Name** for your certificate, and select hello certificate type as **private** from hello dropdown.</span></span>   
4. <span data-ttu-id="036a3-152">Merhaba klasör simgesine hello hello sağ tarafındaki seçin **sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="036a3-152">select hello folder icon on hello right side of hello **Certificate** text box.</span></span> <span data-ttu-id="036a3-153">Merhaba dosya seçiciyi oturum açtığında, tooupload tooyour tümleştirme hesabını istediğiniz hello karşılık gelen ortak sertifika bulun.</span><span class="sxs-lookup"><span data-stu-id="036a3-153">When hello file picker opens, find hello corresponding public certificate that you want tooupload tooyour integration account.</span></span>   
   
   > [!Note]
   > <span data-ttu-id="036a3-154">Özel bir sertifika eklenirken karşılık gelen ortak tooadd sertifika tooshow içinde önemlidir [AS2 sözleşmesi](logic-apps-enterprise-integration-as2.md) gönderip ayarları imzalama ve karışılama iletileri şifrelemek için.</span><span class="sxs-lookup"><span data-stu-id="036a3-154">While adding a private certificate it is important tooadd corresponding public certificate tooshow in [AS2 agreement](logic-apps-enterprise-integration-as2.md) receive and send settings for signing and encrypting hello messages.</span></span>
   > 
   >   

5. <span data-ttu-id="036a3-155">Select hello **kaynak grubu**, **anahtar kasası**, **anahtar adı** ve select hello **Tamam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="036a3-155">Select hello **Resource Group**, **Key Vault**, **Key Name** and select hello **OK** button.</span></span>  
<span data-ttu-id="036a3-156">![Sertifika Ekle](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="036a3-156">![Add certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span></span>  
6. <span data-ttu-id="036a3-157">Select hello **sertifikaları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="036a3-157">Select hello **Certificates** tile.</span></span> <span data-ttu-id="036a3-158">Merhaba sertifika yeni eklenen görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="036a3-158">You should see hello newly added certificate.</span></span>
<span data-ttu-id="036a3-159">![Merhaba yeni sertifika bakın](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="036a3-159">![See hello new certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span></span>  



* [<span data-ttu-id="036a3-160">B2B sözleşmesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="036a3-160">Create a B2B agreement</span></span>](logic-apps-enterprise-integration-agreements.md)  
* [<span data-ttu-id="036a3-161">Anahtar kasası hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="036a3-161">Learn more about Key Vault</span></span>](../key-vault/key-vault-get-started.md "anahtar kasası hakkında bilgi edinin")  

