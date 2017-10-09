---
title: "aaaAzure CLI komut dosyası örneği - bağ özel SSL sertifika tooa işlevi uygulama | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - BIND özel SSL sertifika tooa işlevi uygulama azure'da"
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 04/10/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 692dbc03583f2978131823083f1bfd257882664c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-function-app"></a>Özel SSL sertifika tooa işlevi uygulama bağlama

Bu örnek betik bir işlev uygulaması App Service'te ile ilgili kaynaklarını oluşturur, ardından özel etki alanı adı tooit hello SSL sertifikasını bağlar. Bu örnek için şunlar gerekir:

* Tooyour etki alanı kayıt şirketinizin DNS yapılandırma sayfasına erişin.
* Geçerli. PFX dosyası ve kendi parolasını hello SSL sertifikası, tooupload istediğiniz ve bağlayın.

bir SSL sertifikası toobind, işlevi uygulamanızı tüketim planı içinde değil, bir uygulama hizmeti planındaki oluşturulması gerekir.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az uygulama hizmeti planı oluşturma](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Bir uygulama hizmeti planı gerekli toobind SSL sertifikaları oluşturur. |
| [az functionapp oluşturma]() | Bir işlev uygulaması oluşturur. |
| [az appservice web yapılandırma ana bilgisayar adı ekleyin](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | Özel etki alanı toohello işlev uygulaması eşler. |
| [az appservice web yapılandırma ssl karşıya yükleme](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | Bir SSL sertifikası tooa işlevi uygulamayı yükler. |
| [az appservice web yapılandırma ssl bağlama](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | Karşıya yüklenen bir SSL sertifikası tooa işlev uygulaması bağlar. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek uygulama hizmeti CLI kod örnekleri hello bulunabilir [Azure App Service belgeleri]().
