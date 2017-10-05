---
title: "Bir sanal makine görüntüsü için Azure Marketi oluşturma teknik önkoşulları | Microsoft Docs"
description: "Oluşturma ve bir sanal makine görüntüsü Azure satın almak için Marketinde başkalarının dağıtma gereksinimlerini anlayın."
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
ms.openlocfilehash: af3e2ad623d8d7bfafe676411f9ae3fbee78aab8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="technical-prerequisites-for-creating-a-virtual-machine-image-for-the-azure-marketplace"></a><span data-ttu-id="ed358-103">Bir sanal makine görüntüsü için Azure Marketi oluşturma teknik önkoşulları</span><span class="sxs-lookup"><span data-stu-id="ed358-103">Technical prerequisites for creating a virtual machine image for the Azure Marketplace</span></span>
<span data-ttu-id="ed358-104">İşlemi başlamadan önce baştan sona okuyun ve nerede ve neden her adım gerçekleştirilir anlayın.</span><span class="sxs-lookup"><span data-stu-id="ed358-104">Read the process thoroughly before beginning and understand where and why each step is performed.</span></span> <span data-ttu-id="ed358-105">Mümkün olduğunca, şirket bilgilerinizi ve diğer verileri hazırlama, gerekli Araçları'nı indirmek ve/veya teknik bileşenleri teklifi oluşturma işlemi başlamadan önce oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ed358-105">As much as possible, you should prepare your company information and other data, download necessary tools, and/or create technical components before beginning the offer creation process.</span></span> <span data-ttu-id="ed358-106">Bu öğeler bu makaleyi gözden açık olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ed358-106">These items should be clear from reviewing this article.</span></span>  

## <a name="download-needed-tools--applications"></a><span data-ttu-id="ed358-107">Gerekli Araçlar & uygulamaları yükle</span><span class="sxs-lookup"><span data-stu-id="ed358-107">Download needed tools & applications</span></span>
<span data-ttu-id="ed358-108">Aşağıdaki öğeler işlemine başlamadan önce hazır olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="ed358-108">You should have the following items ready before beginning the process:</span></span>

* <span data-ttu-id="ed358-109">Hangi işletim sistemine bağlı olarak, hedeflediğiniz, yükleme [Azure PowerShell cmdlet'lerini](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) veya [Linux komut satırı arabirimi aracı](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) gelen [Azure indirmeleri](https://azure.microsoft.com/downloads/) sayfası.</span><span class="sxs-lookup"><span data-stu-id="ed358-109">Depending on which operating system you are targeting, install the [Azure PowerShell cmdlets](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) or [Linux command-line interface tool](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) from the [Azure Downloads](https://azure.microsoft.com/downloads/) page.</span></span>
* <span data-ttu-id="ed358-110">Azure Storage Gezgini Codeplex'ten yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ed358-110">Install Azure Storage Explorer from CodePlex.</span></span>
* <span data-ttu-id="ed358-111">Karşıdan yükle ve Azure sertifikalı için sertifika Test aracı yükleyin:</span><span class="sxs-lookup"><span data-stu-id="ed358-111">Download and install the Certification Test Tool for Azure Certified:</span></span>
  * <span data-ttu-id="ed358-112">[http://go.microsoft.com/fwlink/?LinkId=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span><span class="sxs-lookup"><span data-stu-id="ed358-112">[http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span></span> <span data-ttu-id="ed358-113">Sertifika aracını çalıştırmak için Windows tabanlı bir bilgisayar gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed358-113">You need a Windows-based computer to run the certification tool.</span></span> <span data-ttu-id="ed358-114">Windows tabanlı bir bilgisayarda kullanılabilir değilse, aracı Windows tabanlı bir VM ile Azure kullanarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ed358-114">If you do not have a Windows-based computer available, you can run the tool using a Windows-based VM in Azure.</span></span>

## <a name="platforms-supported"></a><span data-ttu-id="ed358-115">Desteklenen platformlar</span><span class="sxs-lookup"><span data-stu-id="ed358-115">Platforms supported</span></span>
<span data-ttu-id="ed358-116">Windows veya Linux Azure tabanlı VM'ler geliştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ed358-116">You can develop Azure-based VMs on Windows or Linux.</span></span> <span data-ttu-id="ed358-117">Bir Azure ile uyumlu sanal sabit disk (VHD)--farklı araçlarını kullanın ve hangi işletim sistemine bağlı olarak, kullandığınız adımları oluşturma gibi yayımlama işlemi--bazı öğeleri:</span><span class="sxs-lookup"><span data-stu-id="ed358-117">Some elements of the publishing process--such as creating an Azure-compatible virtual hard disk (VHD)--use different tools and steps depending on which operating system you are using:</span></span>  

* <span data-ttu-id="ed358-118">Linux kullanıyorsanız, "(Linux tabanlı) bir Azure uyumlu VHD oluşturma" bölümüne bakın [sanal makine görüntüsü yayımlama Kılavuzu](marketplace-publishing-vm-image-creation.md).</span><span class="sxs-lookup"><span data-stu-id="ed358-118">If you are using Linux, refer to the “Create an Azure-compatible VHD (Linux-based)” section of the [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>
* <span data-ttu-id="ed358-119">Windows kullanıyorsanız, "(Windows tabanlı) bir Azure uyumlu VHD oluşturma" bölümüne bakın [sanal makine görüntüsü yayımlama Kılavuzu](marketplace-publishing-vm-image-creation.md).</span><span class="sxs-lookup"><span data-stu-id="ed358-119">If you are using Windows, refer to the “Create an Azure-compatible VHD (Windows-based)” section of the [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ed358-120">Windows tabanlı bir makineye erişmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="ed358-120">You need access to a Windows-based machine to:</span></span>
> 
> * <span data-ttu-id="ed358-121">Sertifika doğrulama aracını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ed358-121">Run the certification validation tool.</span></span>
> * <span data-ttu-id="ed358-122">VHD sertifika göndermelerini VHD paylaşılan erişim imzası URL'SİNİN oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ed358-122">Create the VHD shared access signature URL for the VHD certification submission.</span></span>
> 
> 

## <a name="develop-your-vhd"></a><span data-ttu-id="ed358-123">VHD geliştirin</span><span class="sxs-lookup"><span data-stu-id="ed358-123">Develop your VHD</span></span>
<span data-ttu-id="ed358-124">Bulutta veya şirket içi Azure VHD'ler geliştirme yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ed358-124">You can develop Azure VHDs in the cloud or on-premises:</span></span>

* <span data-ttu-id="ed358-125">Bulut tabanlı geliştirme tüm geliştirme adımları uzaktan Azure'da yerleşik bir VHD üzerinde gerçekleştirilen anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="ed358-125">Cloud-based development means all development steps are performed remotely on a VHD resident on Azure.</span></span>
* <span data-ttu-id="ed358-126">Şirket içi geliştirme VHD indiriliyor ve şirket içi altyapıyı kullanarak geliştirme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ed358-126">On-premises development requires downloading a VHD and developing it using on-premises infrastructure.</span></span> <span data-ttu-id="ed358-127">Bu mümkün olsa da, bunu önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="ed358-127">Although this is possible, we do not recommend it.</span></span> <span data-ttu-id="ed358-128">Windows veya SQL için geliştirme şirket içi ilgili lisans anahtarları olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ed358-128">Note that developing for Windows or SQL on-premises requires you to have the relevant on-premises license keys.</span></span> <span data-ttu-id="ed358-129">Dahil etmek veya VM oluşturduktan sonra SQL Server yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ed358-129">You cannot include or install SQL Server after creating a VM.</span></span> <span data-ttu-id="ed358-130">Ayrıca, görüntüdeki onaylanmış SQL Azure portalından teklifiniz temel almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed358-130">You must also base your offer on an approved SQL image from the Azure portal.</span></span> <span data-ttu-id="ed358-131">Şirket içi geliştirmek karar verirseniz, farklı bir şekilde bulutta geliştirme varsa bazı adımları uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed358-131">If you decide to develop on-premises, you must perform some steps differently than if you were developing in the cloud.</span></span> <span data-ttu-id="ed358-132">İlgili bilgiler bulabilirsiniz [şirket içi VM görüntü oluşturma](marketplace-publishing-vm-image-creation-on-premise.md).</span><span class="sxs-lookup"><span data-stu-id="ed358-132">You can find relevant information in [Create an on-premises VM image](marketplace-publishing-vm-image-creation-on-premise.md).</span></span>

[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
