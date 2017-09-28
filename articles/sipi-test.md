---
title: "Sipi test dosyası | Microsoft Docs"
description: "Test dosyası ReadyForTest bağımlılıkları denetle"
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
ms.openlocfilehash: 871d58818dcbaee5f7a5f07c19e2297ec6459a6f
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/28/2017
---
# <a name="sipi-test-file"></a>Sipi test dosyası

Bu Hızlı Başlangıç, bir Microsoft Azure Active Directory (Azure AD) B2C Kiracısında bir uygulamayı birkaç dakika içinde kaydetmenize yardımcı olur. İşiniz bittiğinde, uygulamanız Azure B2C Kiracısında kullanım için kaydedilir.

## <a name="prerequisites"></a>Ön koşullar

Tüketicinin kaydolmasını ve oturum açmasını kabul eden bir uygulama oluşturmak için öncelikle uygulamayı Azure Active Directory B2C kiracısına kaydetmeniz gerekir. [Azure AD B2C kiracısı oluşturma](active-directory-b2c-get-started.md) makalesinde ana hatlarıyla belirtilen adımları izleyerek kendi kiracınızı edinin.

Azure portalında Azure AD B2C dikey penceresinden oluşturulan uygulamaların aynı konumdan yönetilmesi gerekir. B2C uygulamalarını PowerShell veya başka bir portal kullanarak düzenlerseniz bu uygulamalar desteklenmez duruma gelir ve Azure AD B2C ile çalışmaz. [Hatalı uygulamalar](#faulted-apps) bölümünden ayrıntılara bakabilirsiniz. 

## <a name="navigate-to-b2c-settings"></a>B2C ayarlarına gidin

[Azure portalında](https://portal.azure.com/) B2C kiracısının Genel Yöneticisi olarak oturum açın. 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

Sonraki adımları kaydettirmekte olduğunuz uygulama türüne göre seçin:
