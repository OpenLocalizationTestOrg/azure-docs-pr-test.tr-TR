---
title: "Azure Market teklifi oluşturmak için teknik olmayan önkoşulları | Microsoft Docs"
description: "Oluşturma ve bir teklifi Azure satın almak için Marketinde başkalarının dağıtma gereksinimlerini anlayın."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 3dae463b-8f48-4f52-8fa8-4e3975f09f43
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 08/18/2016
ms.author: hascipio
ms.openlocfilehash: 4f86d444a2f2b97fd8605d480db358813bc39fd3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="general-prerequisites-for-creating-an-offer-for-the-azure-marketplace"></a><span data-ttu-id="27068-103">Azure Market teklifi oluşturmak için genel Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="27068-103">General prerequisites for creating an offer for the Azure Marketplace</span></span>
<span data-ttu-id="27068-104">Teklif oluşturma işlemine ilerlemek için gereken genel, iş işlemi-merkezli Önkoşullar anlayın.</span><span class="sxs-lookup"><span data-stu-id="27068-104">Understand the general, business-process-centric prerequisites that are needed to move forward with the offer creation process.</span></span>

## <a name="ensure-that-you-are-registered-as-a-seller-with-microsoft"></a><span data-ttu-id="27068-105">Microsoft ile bir satıcı olarak kayıtlı olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="27068-105">Ensure that you are registered as a seller with Microsoft</span></span>
<span data-ttu-id="27068-106">Bir satıcı hesabı Microsoft ile kaydetme hakkında ayrıntılı yönergeler için Git [hesap oluşturma ve kayıt](marketplace-publishing-accounts-creation-registration.md).</span><span class="sxs-lookup"><span data-stu-id="27068-106">For detailed instructions on registering a seller account with Microsoft, go to [Account creation and registration](marketplace-publishing-accounts-creation-registration.md).</span></span>

* <span data-ttu-id="27068-107">**Bir satıcı geliştirme Merkezi'ndeki olarak, şirketinizin zaten kayıtlı ve yeni bir teklif oluşturmak istiyorsanız** sonra oturum açma yayımlama için portal ile hangi Geliştirme Merkezi kayıt yapılır aynı e-posta kimliği.</span><span class="sxs-lookup"><span data-stu-id="27068-107">**If your company is already registered as a seller in the Dev Center and you want to create a new offer,** then login to the Publishing portal with the same email id with which Dev Center registration is done.</span></span> <span data-ttu-id="27068-108">Geliştirici Merkezi ve yayımlama portal bağlı böylece birbirleri ile bu adım gereklidir.</span><span class="sxs-lookup"><span data-stu-id="27068-108">This step is required so that the Dev Center and Publishing portal are linked with each other.</span></span>
* <span data-ttu-id="27068-109">**Şirketiniz zaten bir satıcı geliştirme Merkezi'ndeki olarak kayıtlıysa ve mevcut bir teklif düzenlemek istediğiniz** sonra ya da oturum açma yayımlama yönetici hesabıyla veya yayımlama ortak yönetici olarak eklenen bir hesap portalı portal.</span><span class="sxs-lookup"><span data-stu-id="27068-109">**If your company is already registered as a seller in the Dev Center and you want to edit an existing offer,** then either login to the Publishing portal with the admin account or with an account which is added as a co-admin in the Publishing portal.</span></span> <span data-ttu-id="27068-110">Bir ortak yönetici hesabı eklemek için adımları aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="27068-110">Steps to add a co-admin account is given below.</span></span>

## <a name="steps-to-add-a-co-admin-in-the-publishing-portal"></a><span data-ttu-id="27068-111">Yayımlama portalında ortak yönetici ekleme adımları</span><span class="sxs-lookup"><span data-stu-id="27068-111">Steps to add a co-admin in the Publishing Portal</span></span>
<span data-ttu-id="27068-112">Yöneticileri yayımlanmasıyla, yayımlama ortak yönetici olarak, uygulama üzerinde çalışan, diğer üyeleriyle Şirket portalı ekleyebilirsiniz portal.</span><span class="sxs-lookup"><span data-stu-id="27068-112">Admins of the Publishing portal can add the other members of the company, who are working on the application, as a co-admin in the Publishing portal.</span></span> <span data-ttu-id="27068-113">**Yönetici olduğu varsayımıyla** aşağıda verilen olan bir ortak yönetici ekleme adımları</span><span class="sxs-lookup"><span data-stu-id="27068-113">**Assuming that you are the admin,** given below are the steps to add a co-admin.</span></span>

> [!NOTE]
> <span data-ttu-id="27068-114">Yeni kullanıcılar için önce eklediğiniz bir ortak yönetici yayımlama portal, en az bir uygulama yayımlama oluşturduğunuz olun portal.</span><span class="sxs-lookup"><span data-stu-id="27068-114">For new users, before you add a co-admin in the Publishing portal, ensure that you have created at least one application in the Publishing portal.</span></span> <span data-ttu-id="27068-115">Bu olarak gereklidir **YAYIMCILAR** sekmesi görünür en az bir uygulama Yayımlama özelliği yalnızca oluşturduktan sonra portal.</span><span class="sxs-lookup"><span data-stu-id="27068-115">This is required as the **PUBLISHERS** tab appear only after creating at least one application in the Publishing portal.</span></span>
> 
> 

1. <span data-ttu-id="27068-116">Ortak yönetici e-posta kimliği Microsoft account(MSA) olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="27068-116">Ensure that the co-admin email id is a Microsoft account(MSA).</span></span> <span data-ttu-id="27068-117">Değilse, bunu kullanarak MSA kaydetmek [bağlantı](https://signup.live.com/signup?uaid=0089f09ccae94043a0f07c2aaf928831&lic=1).</span><span class="sxs-lookup"><span data-stu-id="27068-117">If not, register it as a MSA using this [link](https://signup.live.com/signup?uaid=0089f09ccae94043a0f07c2aaf928831&lic=1).</span></span>
2. <span data-ttu-id="27068-118">Ortak yönetici eklemek denemeden önce en az bir uygulama yönetici hesabı altında olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="27068-118">Ensure that there is at least one application under the admin account before trying to add a co-admin.</span></span>
3. <span data-ttu-id="27068-119">Yukarıdaki adımları yapılır sonra oturum açma yayımlama için portal ortak yönetici e-posta kimliği ve sonra oturumu kapatın.</span><span class="sxs-lookup"><span data-stu-id="27068-119">After the above steps are done, login to the Publishing portal with the co-admin email id and then log out.</span></span>
4. <span data-ttu-id="27068-120">Şimdi oturum açma yayımlama için portal yönetici e-posta kimliği.</span><span class="sxs-lookup"><span data-stu-id="27068-120">Now login to the Publishing portal with the admin email id.</span></span>
5. <span data-ttu-id="27068-121">Gidin yayımcılar -> hesabınıza -> seçin Yöneticiler -> Ekle ortak yönetici (ekran görüntüsü aşağıda verilen)</span><span class="sxs-lookup"><span data-stu-id="27068-121">Navigate to Publishers->select your account->Administrators->Add the co-admin (screenshot given below)</span></span>
   
    ![Çizim](media/marketplace-publishing-pre-requisites/imgAddAdmin_05.png)
6. <span data-ttu-id="27068-123">Yayımlama işlemi (örneğin Geliştirici portalını yayımlama Merkezi,) çeşitli aşamalarında sağlanan e-posta kimlikleri Microsoft tüm iletişimi için izlenir emin olun.</span><span class="sxs-lookup"><span data-stu-id="27068-123">Ensure that email ids provided at the various stages of the publishing process (e.g. Dev Center, Publishing portal) are monitored for any communication from Microsoft.</span></span>
7. <span data-ttu-id="27068-124">Geliştirici Merkezi kayıt için tek bir kişi ile ilişkili bir hesabı kullanmaktan kaçının.</span><span class="sxs-lookup"><span data-stu-id="27068-124">For Dev Center registration, avoid using an account associated with a single person.</span></span> <span data-ttu-id="27068-125">Bu, bağımlılık bir kişinin kaldırmak için önerilir.</span><span class="sxs-lookup"><span data-stu-id="27068-125">This is suggested for removing dependency from one individual.</span></span>
8. <span data-ttu-id="27068-126">Geliştirici Merkezi kayıt sorunlarla karşılaşırken, bunu kullanarak bir bilet Lütfen Yükselt [bağlantı](https://developer.microsoft.com/en-us/windows/support).</span><span class="sxs-lookup"><span data-stu-id="27068-126">If you face any issues with Dev Center registration, then please raise a ticket using this [link](https://developer.microsoft.com/en-us/windows/support).</span></span>

## <a name="steps-to-delete-a-co-admin-in-the-publishing-portal"></a><span data-ttu-id="27068-127">Ortak yönetici yayımlama silmek için adımları portalı</span><span class="sxs-lookup"><span data-stu-id="27068-127">Steps to delete a co-admin in the Publishing portal</span></span>
<span data-ttu-id="27068-128">**Yönetici olduğu varsayımıyla** aşağıda verilen bir ortak yönetici silmek için adımlardır</span><span class="sxs-lookup"><span data-stu-id="27068-128">**Assuming that you are the admin,** given below are the steps to delete a co-admin.</span></span>

1. <span data-ttu-id="27068-129">Yayımlama için oturum açma portal yönetici e-posta kimliği.</span><span class="sxs-lookup"><span data-stu-id="27068-129">Login to the Publishing portal with the admin email id.</span></span>
2. <span data-ttu-id="27068-130">Gidin **yayımcılar** hesabınızı -> Seç -> **Yöneticiler** -> **ortak yöneticileri**.</span><span class="sxs-lookup"><span data-stu-id="27068-130">Navigate to **Publishers** -> select your account -> **Administrators** -> **Co-Admins**.</span></span>
3. <span data-ttu-id="27068-131">Tıklayın **X** Sigortalanan Top Sil (ekran görüntüsü aşağıda verilen) istediğiniz ortak yönetici yanındaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="27068-131">Click on the **X** button next to the co-admin you want tot delete (screenshot given below).</span></span>
   
    ![Çizim](media/marketplace-publishing-pre-requisites/imgDeleteAdmin_03.png)

> [!IMPORTANT]
> <span data-ttu-id="27068-133">Yalnızca ücretsiz tekliflerini yayınlama (veya kendi lisansını Getir) planlıyorsanız, Şirket vergi ve banka bilgileri tamamlamak zorunda değildir.</span><span class="sxs-lookup"><span data-stu-id="27068-133">You do not have to complete company tax and bank information if you are planning to publish only free offers (or bring your own license).</span></span>
> 
> <span data-ttu-id="27068-134">Başlamak için şirket kayıt tamamlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="27068-134">The company registration must be completed to get started.</span></span> <span data-ttu-id="27068-135">Şirketiniz Microsoft Developer hesabı vergi ve banka bilgileri çalışırken, ancak, geliştiriciler, sanal makine görüntüsü oluşturma çalışmaya başlamadan [yayımlama portalında](https://publish.windowsazure.com), onu sertifikalı alma ve test etme Bunu Azure hazırlama ortamında.</span><span class="sxs-lookup"><span data-stu-id="27068-135">However, while your company works on the tax and bank information in the Microsoft Developer account, the developers can start working on creating the virtual machine image in the [Publishing Portal](https://publish.windowsazure.com), getting it certified, and testing it in the Azure staging environment.</span></span> <span data-ttu-id="27068-136">Teklifiniz Azure Marketinde yayımlama, yalnızca son adım için tam satıcı hesap onayı gerekir.</span><span class="sxs-lookup"><span data-stu-id="27068-136">You will need the complete seller account approval only for the final step of publishing your offer to the Azure Marketplace.</span></span>
> 
> 

## <a name="acquire-an-azure-pay-as-you-go-subscription"></a><span data-ttu-id="27068-137">"Kullandıkça Öde" Azure aboneliği edinin</span><span class="sxs-lookup"><span data-stu-id="27068-137">Acquire an Azure "pay-as-you-go" subscription</span></span>
<span data-ttu-id="27068-138">Bu VM görüntülerinizi oluşturmak ve görüntüleri üzerinden el için kullanacağınız aboneliğin olduğu [Azure Marketi](https://azure.microsoft.com/marketplace/).</span><span class="sxs-lookup"><span data-stu-id="27068-138">This is the subscription that you will use to create your VM images and hand over the images to the [Azure Marketplace](https://azure.microsoft.com/marketplace/).</span></span> <span data-ttu-id="27068-139">Mevcut bir aboneliğiniz yoksa, sonra lütfen https://account.windowsazure.com/signup?offer=ms-azr-0003p kaydolun.</span><span class="sxs-lookup"><span data-stu-id="27068-139">If you do not have an existing subscription, then please sign up at https://account.windowsazure.com/signup?offer=ms-azr-0003p.</span></span>

## <a name="sell-from-countries"></a><span data-ttu-id="27068-140">"Satış Yeri" ülkelerde</span><span class="sxs-lookup"><span data-stu-id="27068-140">"Sell-from" countries</span></span>
> [!WARNING]
> <span data-ttu-id="27068-141">Hizmetlerinizi Azure Market'te satmak için kayıtlı varlığınız onaylanan "Satış Yeri" ülkelerde birinden olduğundan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="27068-141">In order to sell your services on the Azure Marketplace, you must make sure that your registered entity is from one of the approved “sell-from” countries.</span></span> <span data-ttu-id="27068-142">Ödeme ve vergi nedeniyle kısıtlamadır.</span><span class="sxs-lookup"><span data-stu-id="27068-142">This restriction is for payout and taxation reasons.</span></span> <span data-ttu-id="27068-143">Etkin olarak arıyoruz ülkelerin listesi yakın gelecekte genişletin, bu nedenle bizi izlemeye devam edin.</span><span class="sxs-lookup"><span data-stu-id="27068-143">We are actively looking to expand this list of countries in the near future, so stay tuned.</span></span> <span data-ttu-id="27068-144">Bölüm 1b, tam listesi için bkz: [Azure Marketi katılım ilkeleri](http://go.microsoft.com/fwlink/?LinkID=526833).</span><span class="sxs-lookup"><span data-stu-id="27068-144">For the complete list, see section 1b of the [Azure Marketplace participation policies](http://go.microsoft.com/fwlink/?LinkID=526833).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="27068-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="27068-145">Next steps</span></span>
<span data-ttu-id="27068-146">Sonraki teknik olmayan ön koşullar karşılandıktan sonra teklif belirli teknik ön koşullar verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="27068-146">Once the non-technical pre-requisites are fulfilled, next are the offer specific technical prerequisites.</span></span> <span data-ttu-id="27068-147">Makale için Azure Marketi oluşturmak istediğinizi ilgili Teklif türü için bağlantısını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="27068-147">Click the link to the article for the respective offer type that you would like to create for the Azure Marketplace.</span></span>

* [<span data-ttu-id="27068-148">VM teknik ön koşullar</span><span class="sxs-lookup"><span data-stu-id="27068-148">VM technical pre-requisites</span></span>](marketplace-publishing-vm-image-creation-prerequisites.md)
* [<span data-ttu-id="27068-149">Çözüm şablonu teknik ön koşullar</span><span class="sxs-lookup"><span data-stu-id="27068-149">Solution Template technical pre-requisites</span></span>](marketplace-publishing-solution-template-creation-prerequisites.md)

## <a name="see-also"></a><span data-ttu-id="27068-150">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="27068-150">See also</span></span>
* [<span data-ttu-id="27068-151">Başlarken: bir teklifi Azure Marketinde yayımlama</span><span class="sxs-lookup"><span data-stu-id="27068-151">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

