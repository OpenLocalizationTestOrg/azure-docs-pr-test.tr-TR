---
title: "aaaPython betik tooretrieve verileri Azure günlük analizi | Microsoft Docs"
description: "Merhaba günlük analizi günlük arama API herhangi bir REST API istemcisi günlük analizi çalışma alanı tooretrieve verileri sağlar.  Bu makalede hello günlük arama API kullanarak bir örnek Python komut dosyası sağlar."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: bwren
ms.openlocfilehash: a45693b04cd388301b859e7186ca671786d0229e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="retrieve-data-from-log-analytics-with-a-python-script"></a>Bir Python betiği ile günlük Analytics'ten verileri
Merhaba [günlük analizi günlük arama API](log-analytics-log-search-api.md) herhangi bir REST API istemcisi günlük analizi çalışma alanı tooretrieve verileri sağlar.  Bu makalede hello günlük analizi günlük arama API'si kullanan bir örnek Python komut dosyası gösterir.  

## <a name="authentication"></a>Kimlik Doğrulaması
Bu komut dosyası Azure Active Directory tooauthenticate toohello çalışma alanında bir hizmet sorumlusu kullanır.  Hizmet sorumluları bir istemci izin hizmet hello uygulama toorequest hello istemci hello hesap adı yok olsa bile bir hesabın kimlik doğrulaması. Bu komut dosyasını çalıştırmadan önce hello işleme kullanan bir hizmet sorumlusu oluşturmalısınız [bir Azure Active Directory Uygulama ve kaynaklarına erişebilir hizmet sorumlusu portal toocreate kullanmak](../azure-resource-manager/resource-group-create-service-principal-portal.md).  Tooprovide hello uygulama kimliği, Kiracı kimliği ve kimlik doğrulama anahtarı toohello betik gerekir. 

> [!NOTE]
> Olduğunda, [Azure Automation hesabı oluşturma](../automation/automation-create-standalone-account.md), bir hizmet sorumlusu, diğer bir deyişle uygun toouse ile bu komut dosyası oluşturulur.  Azure Automation tarafından oluşturulan bir hizmet sorumlusu zaten sonra mümkün toouse olmalıdır, çok kullanmanız gerekebilir, ancak yeni bir tane oluşturmak yerine[bir kimlik doğrulama anahtarı oluşturma](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) , zaten yoksa.

## <a name="script"></a>Betik
``` python
import adal
import requests
import json
import datetime
from pprint import pprint

# Details of workspace.  Fill in details for your workspace.
resource_group = 'xxxxxxxx'
workspace = 'xxxxxxxx'

# Details of query.  Modify these tooyour requirements.
query = "Type=Event"
end_time = datetime.datetime.utcnow()
start_time = end_time - datetime.timedelta(hours=24)
num_results = 100  # If not provided, a default of 10 results will be used.

# IDs for authentication.  Fill in values for your service principal.
subscription_id = 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'
tenant_id = 'xxxxxxxx-xxxx-xxxx-xxx-xxxxxxxxxxxx'
application_id = 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx'
application_key = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'

# URLs for authentication
authentication_endpoint = 'https://login.microsoftonline.com/'
resource  = 'https://management.core.windows.net/'

# Get access token
context = adal.AuthenticationContext('https://login.microsoftonline.com/' + tenant_id)
token_response = context.acquire_token_with_client_credentials('https://management.core.windows.net/', application_id, application_key)
access_token = token_response.get('accessToken')

# Add token tooheader
headers = {
    "Authorization": 'Bearer ' + access_token,
    "Content-Type":'application/json'
}

# URLs for retrieving data
uri_base = 'https://management.azure.com'
uri_api = 'api-version=2015-11-01-preview'
uri_subscription = 'https://management.azure.com/subscriptions/' + subscription_id
uri_resourcegroup = uri_subscription + '/resourcegroups/'+ resource_group
uri_workspace = uri_resourcegroup + '/providers/Microsoft.OperationalInsights/workspaces/' + workspace
uri_search = uri_workspace + '/search'

# Build search parameters from query details
search_params = {
        "query": query,
        "top": num_results,
        "start": start_time.strftime('%Y-%m-%dT%H:%M:%S'),
        "end": end_time.strftime('%Y-%m-%dT%H:%M:%S')
        }

# Build URL and send post request
uri = uri_search + '?' + uri_api
response = requests.post(uri,json=search_params,headers=headers)

# Response of 200 if successful
if response.status_code == 200:

    # Parse hello response tooget hello ID and status
    data = response.json()
    search_id = data["id"].split("/")
    id = search_id[len(search_id)-1]
    status = data["__metadata"]["Status"]

    # If status is pending, then keep checking until complete
    while status == "Pending":

        # Build URL tooget search from ID and send request
        uri_search = uri_search + '/' + id
        uri = uri_search + '?' + uri_api
        response = requests.get(uri,headers=headers)

        # Parse hello response tooget hello status
        data = response.json()
        status = data["__metadata"]["Status"]

else:

    # Request failed
    print (response.status_code)
    response.raise_for_status()

print ("Total records:" + str(data["__metadata"]["total"]))
print ("Returned top:" + str(data["__metadata"]["top"]))
pprint (data["value"])
```
## <a name="next-steps"></a>Sonraki adımlar
- Merhaba hakkında daha fazla bilgi [günlük analizi günlük arama API](log-analytics-log-search-api.md).
