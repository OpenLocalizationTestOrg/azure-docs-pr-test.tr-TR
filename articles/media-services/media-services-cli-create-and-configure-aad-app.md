---
title: "aaaUse CLI 2.0 toocreate bir Azure AD uygulaması ve Azure Media Services API tooaccess yapılandırma | Microsoft Docs"
description: "Bu konuda gösterilmektedir nasıl toouse CLI 2.0 toocreate bir Azure AD uygulaması ve Azure Media Services API tooaccess yapılandırın."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: c865e2701722374b5dd17b0e20fa848c07065006
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-20-toocreate-an-aad-app-and-configure-it-tooaccess-azure-media-services-api"></a><span data-ttu-id="83330-103">CLI 2.0 toocreate bir AAD uygulaması kullanın ve tooaccess Azure Media Services API yapılandırın</span><span class="sxs-lookup"><span data-stu-id="83330-103">Use CLI 2.0 toocreate an AAD app and configure it tooaccess Azure Media Services API</span></span>

<span data-ttu-id="83330-104">Bu konuda nasıl toouse CLI 2.0 toocreate bir Azure Active Directory (Azure AD) uygulama ve hizmet asıl tooaccess Azure Media Services gösterilmektedir kaynakları.</span><span class="sxs-lookup"><span data-stu-id="83330-104">This topic shows you how toouse CLI 2.0 toocreate an Azure Active Directory (Azure AD) application and service principal tooaccess Azure Media Services resources.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="83330-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="83330-105">Prerequisites</span></span>

- <span data-ttu-id="83330-106">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="83330-106">An Azure account.</span></span> <span data-ttu-id="83330-107">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="83330-107">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="83330-108">Bir Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="83330-108">A Media Services account.</span></span> <span data-ttu-id="83330-109">Daha fazla bilgi için bkz: [hello Azure portal kullanarak bir Azure Media Services hesabı oluşturma](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="83330-109">For more information, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>

## <a name="use-hello-azure-cloud-shell"></a><span data-ttu-id="83330-110">Hello Azure bulut Kabuğu'nu kullanın</span><span class="sxs-lookup"><span data-stu-id="83330-110">Use hello Azure Cloud Shell</span></span>

1. <span data-ttu-id="83330-111">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="83330-111">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="83330-112">Merhaba bulut Kabuk hello portalı hello üst gezinti bölmesinden başlatın.</span><span class="sxs-lookup"><span data-stu-id="83330-112">Launch hello Cloud Shell from hello upper navigation pane of hello portal.</span></span>

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

<span data-ttu-id="83330-114">Daha fazla bilgi için bkz: [Azure bulut Kabuk genel bakış](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="83330-114">For more information, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md).</span></span>

## <a name="create-an-azure-ad-app-and-configure-access-toohello-media-account-with-cli-20"></a><span data-ttu-id="83330-115">Bir Azure AD uygulaması oluştur ve erişim toohello medya hesabı CLI 2.0 ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="83330-115">Create an Azure AD app and configure access toohello media account with CLI 2.0</span></span>
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create -- assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

<span data-ttu-id="83330-116">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="83330-116">For example:</span></span>

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

<span data-ttu-id="83330-117">Bu örnekte, hello **kapsam** hello tam kaynak hello media services hesabı yoludur.</span><span class="sxs-lookup"><span data-stu-id="83330-117">In this example, hello **scope** is hello full resource path for hello media services account.</span></span> <span data-ttu-id="83330-118">Ancak, hello **kapsam** herhangi bir düzeyde olabilir.</span><span class="sxs-lookup"><span data-stu-id="83330-118">However, hello **scope** can be at any level.</span></span>

<span data-ttu-id="83330-119">Örneğin, düzeyleri aşağıdaki hello biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="83330-119">For example, it could be one of hello following levels:</span></span>
 
* <span data-ttu-id="83330-120">Merhaba **abonelik** düzeyi.</span><span class="sxs-lookup"><span data-stu-id="83330-120">hello **subscription** level.</span></span>
* <span data-ttu-id="83330-121">Merhaba **kaynak grubu** düzeyi.</span><span class="sxs-lookup"><span data-stu-id="83330-121">hello **resource group** level.</span></span>
* <span data-ttu-id="83330-122">Merhaba **kaynak** düzeyi (örneğin, bir ortam hesabı).</span><span class="sxs-lookup"><span data-stu-id="83330-122">hello **resource** level (for example, a Media account).</span></span>

<span data-ttu-id="83330-123">Daha fazla bilgi için bkz: [bir Azure hizmet sorumlusu Azure CLI 2.0 ile oluşturun.](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="83330-123">For more information, see [Create an Azure service principal with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

<span data-ttu-id="83330-124">Ayrıca bkz. [Manage Role-Based erişim denetimi hello Azure komut satırı arabirimi ile](../active-directory/role-based-access-control-manage-access-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="83330-124">Also see [Manage Role-Based Access Control with hello Azure command-line interface](../active-directory/role-based-access-control-manage-access-azure-cli.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="83330-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="83330-125">Next steps</span></span>

<span data-ttu-id="83330-126">Kullanmaya başlama [tooyour hesabı dosyaları karşıya yükleme](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="83330-126">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
