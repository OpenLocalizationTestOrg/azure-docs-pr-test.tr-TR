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
# <a name="use-cli-20-toocreate-an-aad-app-and-configure-it-tooaccess-azure-media-services-api"></a>CLI 2.0 toocreate bir AAD uygulaması kullanın ve tooaccess Azure Media Services API yapılandırın

Bu konuda nasıl toouse CLI 2.0 toocreate bir Azure Active Directory (Azure AD) uygulama ve hizmet asıl tooaccess Azure Media Services gösterilmektedir kaynakları. 

## <a name="prerequisites"></a>Ön koşullar

- Bir Azure hesabı. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/). 
- Bir Media Services hesabı. Daha fazla bilgi için bkz: [hello Azure portal kullanarak bir Azure Media Services hesabı oluşturma](media-services-portal-create-account.md).

## <a name="use-hello-azure-cloud-shell"></a>Hello Azure bulut Kabuğu'nu kullanın

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Merhaba bulut Kabuk hello portalı hello üst gezinti bölmesinden başlatın.

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

Daha fazla bilgi için bkz: [Azure bulut Kabuk genel bakış](../cloud-shell/overview.md).

## <a name="create-an-azure-ad-app-and-configure-access-toohello-media-account-with-cli-20"></a>Bir Azure AD uygulaması oluştur ve erişim toohello medya hesabı CLI 2.0 ile yapılandırma
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create -- assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

Örneğin:

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

Bu örnekte, hello **kapsam** hello tam kaynak hello media services hesabı yoludur. Ancak, hello **kapsam** herhangi bir düzeyde olabilir.

Örneğin, düzeyleri aşağıdaki hello biri olabilir:
 
* Merhaba **abonelik** düzeyi.
* Merhaba **kaynak grubu** düzeyi.
* Merhaba **kaynak** düzeyi (örneğin, bir ortam hesabı).

Daha fazla bilgi için bkz: [bir Azure hizmet sorumlusu Azure CLI 2.0 ile oluşturun.](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)

Ayrıca bkz. [Manage Role-Based erişim denetimi hello Azure komut satırı arabirimi ile](../active-directory/role-based-access-control-manage-access-azure-cli.md). 

## <a name="next-steps"></a>Sonraki adımlar

Kullanmaya başlama [tooyour hesabı dosyaları karşıya yükleme](media-services-portal-upload-files.md).
