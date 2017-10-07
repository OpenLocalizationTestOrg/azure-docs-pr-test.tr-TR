---
title: "aaaAzure CLI komut dosyası örneği - bağ özel bir SSL sertifikası tooa web uygulaması | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - BIND özel bir SSL sertifikası tooa web uygulaması"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2fec2db84a2007fa6b005776c84d4f8cba392b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a>Özel SSL sertifika tooa web uygulama bağlama

Bu örnek komut dosyası ile ilgili kaynaklarını App Service'te bir web uygulaması oluşturur, ardından özel etki alanı adı tooit hello SSL sertifikasını bağlar. Bu örnek için şunları yapmanız gerekir:

* Tooyour etki alanı kayıt şirketinizin DNS yapılandırma sayfasına erişin.
* Geçerli. PFX dosyası ve kendi parolasını hello SSL sertifikası, tooupload istediğiniz ve bağlayın.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 


## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az uygulama hizmeti planı oluşturma](https://docs.microsoft.com/cli/azure/appservice/plan#create) | App Service planı oluşturur. |
| [az webapp oluşturma](https://docs.microsoft.com/cli/azure/webapp#create) | Azure web uygulaması oluşturur. |
| [az webapp config ana bilgisayar adı ekleyin](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | Bir özel etki alanı tooa web uygulaması eşler. |
| [az webapp config ssl karşıya yükleme](https://docs.microsoft.com/cli/azure/webapp/config/ssl#upload) | Bir SSL sertifikası tooa web uygulamasını yükler. |
| [az webapp config ssl bağlama](https://docs.microsoft.com/cli/azure/webapp/config/ssl#bind) | Karşıya yüklenen bir SSL sertifikası tooa web uygulaması bağlar. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek uygulama hizmeti CLI kod örnekleri hello bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).
