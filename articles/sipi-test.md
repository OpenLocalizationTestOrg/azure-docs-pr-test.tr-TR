---
title: "Sipi test dosyası | Microsoft Docs"
description: "Dosya toocheck ReadyForTest bağımlılıkları test"
services: active-directory-b2c
documentationcenter: 
author: Sipi
manager: Sipi
editor: Sipi
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f68
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: Sipi
ms.openlocfilehash: afd3dc94dfb30926b316256fb06a768a391004f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sipi-test-file"></a>Sipi test dosyası

Bu Hızlı Başlangıç, bir Microsoft Azure Active Directory (Azure AD) B2C Kiracısında bir uygulamayı birkaç dakika içinde kaydetmenize yardımcı olur. İşiniz bittiğinde, uygulamanızı hello Azure B2C Kiracı kullanmak için kayıtlı.

## <a name="prerequisites"></a>Ön koşullar

toobuild tüketicinin kaydolmasını ve oturum açma kabul eden bir uygulama, ilk Azure Active Directory B2C kiracısı ile tooregister Merhaba uygulaması gerekir. Kendi Kiracı özetlenen hello adımları kullanarak alma [bir Azure AD B2C kiracısı oluşturma](active-directory-b2c-get-started.md).

Hello hello Azure AD B2C dikey penceresinde hello Azure portalında oluşturulan uygulamaları yönetilen aynı konumu. PowerShell veya başka bir portal kullanarak hello B2C uygulamaları düzenlerseniz, desteklenmeyen haline gelir ve Azure AD B2C ile çalışmaz. Merhaba ayrıntıları görmek [hatalı uygulamaları](#faulted-apps) bölümü. 

## <a name="navigate-toob2c-settings"></a>TooB2C ayarları gidin

İçinde toohello oturum [Azure portal](https://portal.azure.com/) hello B2C kiracısının genel Yöneticisi hello gibi. 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

Sonraki adımlar kaydettirmekte olduğunuz hello uygulama türüne göre seçin:
