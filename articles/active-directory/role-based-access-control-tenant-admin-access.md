---
title: "aaaTenant yönetici yükseltmesine erişim - Azure AD | Microsoft Docs"
description: "Bu konu, rol tabanlı erişim denetimi (RBAC) rollerini yerleşik hello açıklar."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: rqureshi
ms.assetid: b547c5a5-2da2-4372-9938-481cb962d2d6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andredm
ms.openlocfilehash: 7996f2af3277dc40e2a1766cc4a7862a2399cdef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a>Rol tabanlı erişim denetimi ile bir kiracı Yöneticisi olarak erişimini yükseltme

Rol tabanlı erişim denetimi normalden daha yüksek izinleri verebilirsiniz geçici yükseltmeleri erişim elde Kiracı Yöneticiler yardımcı olur. Bir kiracı Yöneticisi kendisini gerektiğinde toohello kullanıcı erişimi yöneticisi rolü yükseltebilirsiniz. Bu rol hello verir yönetici izinleri toogrant kendisini veya başkalarının Kiracı hello rollerini "/" kapsamı.

Bu özellik, tüm kuruluştaki mevcut abonelikleri Merhaba yönetici toosee hello Kiracı izin verdiği için önemlidir. Ayrıca, otomasyon (örneğin, faturalama ve denetimi) uygulamaları tooaccess için tüm hello aboneliklere izin verir ve faturalama veya varlık yönetim hello kuruluş hello durumunu doğru bir görünümünü sağlar.  

## <a name="how-toouse-elevateaccess-toogive-tenant-access"></a>Nasıl toouse elevateAccess toogive Kiracı erişim

Merhaba temel işlem aşağıdaki adımları hello ile çalışır:

1. REST kullanarak, çağrı *elevateAccess*, kullanıcı erişimi yöneticisi rolü hello "/" kapsam hangi verir.

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. Oluşturma bir [rol ataması](/rest/api/authorization/roleassignments) tooassign herhangi kapsamındaki herhangi bir rolü. Aşağıdaki örneğine hello atamak için hello özellikleri, okuyucu rolüne hello "/" kapsam gösterir:

    ```
    { "properties":{
    "roleDefinitionId": "providers/Microsoft.Authorization/roleDefinitions/acdd72a7338548efbd42f606fba81ae7",
    "principalId": "cbc5e050-d7cd-4310-813b-4870be8ef5bb",
    "scope": "/"
    },
    "id": "providers/Microsoft.Authorization/roleAssignments/64736CA0-56D7-4A94-A551-973C2FE7888B",
    "type": "Microsoft.Authorization/roleAssignments",
    "name": "64736CA0-56D7-4A94-A551-973C2FE7888B"
    }
    ```

3. Kullanıcı erişim yönetimi sırasında de rol atamaları olarak sil "/" kapsam.

4. Gerektiğinde kadar kullanıcı erişimi yönetici ayrıcalıkları iptal edin.


## <a name="how-tooundo-hello-elevateaccess-action"></a>Nasıl tooundo hello elevateAccess eylem

Çağırdığınızda *elevateAccess* kendiniz için bir rol ataması oluşturma, toorevoke olanlar ayrıcalıkları şekilde toodelete atama hello.

1.  Çağrı [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) burada roleName = kullanıcı erişimi Yöneticisi toodetermine hello adı hello kullanıcı erişimi yöneticisi rolünün bir GUID. Merhaba yanıt aşağıdaki gibi görünmelidir:

    ```
    {"value":[{"properties":{
    "roleName":"User Access Administrator",
    "type":"BuiltInRole",
    "description":"Lets you manage user access tooAzure resources.",
    "assignableScopes":["/"],
    "permissions":[{"actions":["*/read","Microsoft.Authorization/*","Microsoft.Support/*"],"notActions":[]}],
    "createdOn":"0001-01-01T08:00:00.0000000Z",
    "updatedOn":"2016-05-31T23:14:04.6964687Z",
    "createdBy":null,
    "updatedBy":null},
    "id":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "type":"Microsoft.Authorization/roleDefinitions",
    "name":"18d7d88d-d35e-4fb5-a5c3-7773c20a72d9"}],
    "nextLink":null}
    ```

    Hello Hello GUID Kaydet *adı* parametresi, bu durumda **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.

2. Çağrı [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) burada Principalıd kendi objectID =. Bu, tüm atamalarınızı hello kiracısında listeler. Merhaba kapsam olduğu Hello için bir Ara "/" ve hello Roledefinitionıd biter hello rol adı 1. adımda bulduğunuz GUID. Merhaba rol ataması aşağıdaki gibi görünmelidir:

    ```
    {"value":[{"properties":{
    "roleDefinitionId":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "principalId":"{objectID}",
    "scope":"/",
    "createdOn":"2016-08-17T19:21:16.3422480Z",
    "updatedOn":"2016-08-17T19:21:16.3422480Z",
    "createdBy":"93ce6722-3638-4222-b582-78b75c5c6d65",
    "updatedBy":"93ce6722-3638-4222-b582-78b75c5c6d65"},
    "id":"/providers/Microsoft.Authorization/roleAssignments/e7dd75bc-06f6-4e71-9014-ee96a929d099",
    "type":"Microsoft.Authorization/roleAssignments",
    "name":"e7dd75bc-06f6-4e71-9014-ee96a929d099"}],
    "nextLink":null}
    ```

    Merhaba GUID hello kaydetmeyi yeniden, *adı* parametresi, bu durumda **e7dd75bc-06f6-4e71-9014-ee96a929d099**.

3. Son olarak, arama [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) burada roleAssignmentId = 2. adımda bulduğunuz GUID'i hello adı.

## <a name="next-steps"></a>Sonraki adımlar

- Daha fazla bilgi edinmek [rol tabanlı erişim denetimini REST ile yönetme](role-based-access-control-manage-access-rest.md)

- [Erişim atamalarını yönetmeyi](role-based-access-control-manage-assignments.md) hello Azure portal'ın
