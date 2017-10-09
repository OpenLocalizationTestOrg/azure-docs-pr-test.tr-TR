---
title: "hello Azure Marketi için bir sanal makine görüntüsü oluşturmak için aaaTechnical önkoşulları | Microsoft Docs"
description: "Oluşturma ve başkaları için bir sanal makine görüntü toohello Azure Marketi dağıtma hello gereksinimleri anlamak toopurchase."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 63c16966-0304-4b17-a715-368a0a5ccb2c
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: fcae4d9e052581e3c1dfe7962e6d50ec31040419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="technical-prerequisites-for-creating-a-virtual-machine-image-for-hello-azure-marketplace"></a><span data-ttu-id="985fe-103">Hello Azure Marketi için bir sanal makine görüntüsü oluşturmak için teknik önkoşulları</span><span class="sxs-lookup"><span data-stu-id="985fe-103">Technical prerequisites for creating a virtual machine image for hello Azure Marketplace</span></span>
<span data-ttu-id="985fe-104">Merhaba işlemi başlamadan önce baştan sona okuyun ve nerede ve neden her adım gerçekleştirilir anlayın.</span><span class="sxs-lookup"><span data-stu-id="985fe-104">Read hello process thoroughly before beginning and understand where and why each step is performed.</span></span> <span data-ttu-id="985fe-105">Mümkün olduğunca, şirket bilgilerinizi ve diğer verileri hazırlama, gerekli Araçları'nı indirmek ve/veya teknik bileşenleri hello teklif oluşturma işlemi başlamadan önce oluşturun.</span><span class="sxs-lookup"><span data-stu-id="985fe-105">As much as possible, you should prepare your company information and other data, download necessary tools, and/or create technical components before beginning hello offer creation process.</span></span> <span data-ttu-id="985fe-106">Bu öğeler bu makaleyi gözden açık olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="985fe-106">These items should be clear from reviewing this article.</span></span>  

## <a name="download-needed-tools--applications"></a><span data-ttu-id="985fe-107">Gerekli Araçlar & uygulamaları yükle</span><span class="sxs-lookup"><span data-stu-id="985fe-107">Download needed tools & applications</span></span>
<span data-ttu-id="985fe-108">Merhaba aşağıdaki öğelerindeki hello işlemine başlamadan önce hazır olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="985fe-108">You should have hello following items ready before beginning hello process:</span></span>

* <span data-ttu-id="985fe-109">Hangi işletim sistemine bağlı olarak, hedeflediğiniz, yükleme hello [Azure PowerShell cmdlet'lerini](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) veya [Linux komut satırı arabirimi aracı](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) hello gelen [Azure indirmeleri](https://azure.microsoft.com/downloads/) Sayfa.</span><span class="sxs-lookup"><span data-stu-id="985fe-109">Depending on which operating system you are targeting, install hello [Azure PowerShell cmdlets](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) or [Linux command-line interface tool](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) from hello [Azure Downloads](https://azure.microsoft.com/downloads/) page.</span></span>
* <span data-ttu-id="985fe-110">Azure Storage Gezgini Codeplex'ten yükleyin.</span><span class="sxs-lookup"><span data-stu-id="985fe-110">Install Azure Storage Explorer from CodePlex.</span></span>
* <span data-ttu-id="985fe-111">Karşıdan yükleyip hello sertifika Test aracı Azure sertifikalı için:</span><span class="sxs-lookup"><span data-stu-id="985fe-111">Download and install hello Certification Test Tool for Azure Certified:</span></span>
  * <span data-ttu-id="985fe-112">[http://go.microsoft.com/fwlink/?LinkId=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span><span class="sxs-lookup"><span data-stu-id="985fe-112">[http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span></span> <span data-ttu-id="985fe-113">Bir Windows tabanlı bilgisayar toorun hello sertifika Aracı gerekir.</span><span class="sxs-lookup"><span data-stu-id="985fe-113">You need a Windows-based computer toorun hello certification tool.</span></span> <span data-ttu-id="985fe-114">Windows tabanlı bir bilgisayarda kullanılabilir yoksa, Windows tabanlı bir VM azure'da hello aracını çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="985fe-114">If you do not have a Windows-based computer available, you can run hello tool using a Windows-based VM in Azure.</span></span>

## <a name="platforms-supported"></a><span data-ttu-id="985fe-115">Desteklenen platformlar</span><span class="sxs-lookup"><span data-stu-id="985fe-115">Platforms supported</span></span>
<span data-ttu-id="985fe-116">Windows veya Linux Azure tabanlı VM'ler geliştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="985fe-116">You can develop Azure-based VMs on Windows or Linux.</span></span> <span data-ttu-id="985fe-117">Bir Azure ile uyumlu sanal sabit disk (VHD)--farklı araçlarını kullanın ve hangi işletim sistemine bağlı olarak, kullandığınız adımları oluşturma gibi işlem--yayımlama hello bazı öğeleri:</span><span class="sxs-lookup"><span data-stu-id="985fe-117">Some elements of hello publishing process--such as creating an Azure-compatible virtual hard disk (VHD)--use different tools and steps depending on which operating system you are using:</span></span>  

* <span data-ttu-id="985fe-118">Linux kullanıyorsanız, hello toohello "(Linux tabanlı) bir Azure uyumlu VHD oluşturma" bölümüne bakın [sanal makine görüntüsü yayımlama Kılavuzu](marketplace-publishing-vm-image-creation.md).</span><span class="sxs-lookup"><span data-stu-id="985fe-118">If you are using Linux, refer toohello “Create an Azure-compatible VHD (Linux-based)” section of hello [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>
* <span data-ttu-id="985fe-119">Windows kullanıyorsanız, hello toohello "(Windows tabanlı) bir Azure uyumlu VHD oluşturma" bölümüne bakın [sanal makine görüntüsü yayımlama Kılavuzu](marketplace-publishing-vm-image-creation.md).</span><span class="sxs-lookup"><span data-stu-id="985fe-119">If you are using Windows, refer toohello “Create an Azure-compatible VHD (Windows-based)” section of hello [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>

> [!NOTE]
> <span data-ttu-id="985fe-120">Windows tabanlı tooa makineye erişim:</span><span class="sxs-lookup"><span data-stu-id="985fe-120">You need access tooa Windows-based machine to:</span></span>
> 
> * <span data-ttu-id="985fe-121">Merhaba sertifika doğrulama aracını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="985fe-121">Run hello certification validation tool.</span></span>
> * <span data-ttu-id="985fe-122">Hello VHD paylaşılan erişim imzası hello VHD sertifika gönderme URL'sini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="985fe-122">Create hello VHD shared access signature URL for hello VHD certification submission.</span></span>
> 
> 

## <a name="develop-your-vhd"></a><span data-ttu-id="985fe-123">VHD geliştirin</span><span class="sxs-lookup"><span data-stu-id="985fe-123">Develop your VHD</span></span>
<span data-ttu-id="985fe-124">Merhaba Bulut veya şirket içinde Azure VHD'leri geliştirme yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="985fe-124">You can develop Azure VHDs in hello cloud or on-premises:</span></span>

* <span data-ttu-id="985fe-125">Bulut tabanlı geliştirme tüm geliştirme adımları uzaktan Azure'da yerleşik bir VHD üzerinde gerçekleştirilen anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="985fe-125">Cloud-based development means all development steps are performed remotely on a VHD resident on Azure.</span></span>
* <span data-ttu-id="985fe-126">Şirket içi geliştirme VHD indiriliyor ve şirket içi altyapıyı kullanarak geliştirme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="985fe-126">On-premises development requires downloading a VHD and developing it using on-premises infrastructure.</span></span> <span data-ttu-id="985fe-127">Bu mümkün olsa da, bunu önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="985fe-127">Although this is possible, we do not recommend it.</span></span> <span data-ttu-id="985fe-128">Windows veya SQL için geliştirme şirket içi, toohave hello içi ilgili lisans anahtarları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="985fe-128">Note that developing for Windows or SQL on-premises requires you toohave hello relevant on-premises license keys.</span></span> <span data-ttu-id="985fe-129">Dahil etmek veya VM oluşturduktan sonra SQL Server yükleyin.</span><span class="sxs-lookup"><span data-stu-id="985fe-129">You cannot include or install SQL Server after creating a VM.</span></span> <span data-ttu-id="985fe-130">Ayrıca, onaylanan SQL görüntüden hello Azure portalı üzerinde teklifiniz temel almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="985fe-130">You must also base your offer on an approved SQL image from hello Azure portal.</span></span> <span data-ttu-id="985fe-131">Toodevelop şirket içi karar verirseniz, bazı adımlar hello bulutta geliştirme, farklı bir biçimde gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="985fe-131">If you decide toodevelop on-premises, you must perform some steps differently than if you were developing in hello cloud.</span></span> <span data-ttu-id="985fe-132">İlgili bilgiler bulabilirsiniz [şirket içi VM görüntü oluşturma](marketplace-publishing-vm-image-creation-on-premise.md).</span><span class="sxs-lookup"><span data-stu-id="985fe-132">You can find relevant information in [Create an on-premises VM image](marketplace-publishing-vm-image-creation-on-premise.md).</span></span>

[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
