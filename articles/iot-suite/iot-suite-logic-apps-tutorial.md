---
title: aaaAzure IOT paketi ve Logic Apps | Microsoft Docs
description: "Bir öğretici nasıl toohook Logic Apps tooAzure IOT paketi iş sürecini için ayarlama."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4629a7af-56ca-4b21-a769-5fa18bc3ab07
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: corywink
ms.openlocfilehash: 6ef7311ac38f4e2ddb032cff0fb73591da5f76c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-connect-logic-app-tooyour-azure-iot-suite-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="cb811-103">Öğretici: Mantıksal uygulama tooyour Azure IOT paketi uzaktan önceden yapılandırılmış izleme çözümü bağlantı</span><span class="sxs-lookup"><span data-stu-id="cb811-103">Tutorial: Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution</span></span>
<span data-ttu-id="cb811-104">Merhaba [Microsoft Azure IOT paketi] [ lnk-internetofthings] Uzaktan izleme çözümü mükemmel şekilde tooget hızlı bir şekilde bir IOT çözüm exemplifies bir uçtan uca özellik kümesi ile başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="cb811-104">hello [Microsoft Azure IoT Suite][lnk-internetofthings] remote monitoring preconfigured solution is a great way tooget started quickly with an end-to-end feature set that exemplifies an IoT solution.</span></span> <span data-ttu-id="cb811-105">Bu öğreticide nasıl tooadd mantıksal uygulama tooyour Microsoft Azure IOT paketi çözümünün önceden yapılandırılmış Uzaktan izleme aracılığıyla açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cb811-105">This tutorial walks you through how tooadd Logic App tooyour Microsoft Azure IoT Suite remote monitoring preconfigured solution.</span></span> <span data-ttu-id="cb811-106">Bu adımları tooa iş sürecini bağlanarak daha IOT çözümünüzü nasıl yararlanabileceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="cb811-106">These steps demonstrate how you can take your IoT solution even further by connecting it tooa business process.</span></span>

<span data-ttu-id="cb811-107">*Tooprovision Uzaktan izleme çözümü nasıl önceden yapılandırılmış üzerinde bir kılavuz arıyorsanız bkz [Öğreticisi: Merhaba IOT önceden yapılandırılmış çözümleri kullanmaya başlama][lnk-getstarted].*</span><span class="sxs-lookup"><span data-stu-id="cb811-107">*If you’re looking for a walkthrough on how tooprovision a remote monitoring preconfigured solution, see [Tutorial: Get started with hello IoT preconfigured solutions][lnk-getstarted].*</span></span>

<span data-ttu-id="cb811-108">Bu öğretici başlamadan önce aşağıdakileri yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="cb811-108">Before you start this tutorial, you should:</span></span>

* <span data-ttu-id="cb811-109">Sağlama hello Uzaktan izleme çözümü Azure aboneliğinizde.</span><span class="sxs-lookup"><span data-stu-id="cb811-109">Provision hello remote monitoring preconfigured solution in your Azure subscription.</span></span>
* <span data-ttu-id="cb811-110">SendGrid hesap tooenable oluşturmak, iş sürecini tetikleyen bir e-posta toosend.</span><span class="sxs-lookup"><span data-stu-id="cb811-110">Create a SendGrid account tooenable you toosend an email that triggers your business process.</span></span> <span data-ttu-id="cb811-111">Ücretsiz bir deneme hesabı için kaydolabilirsiniz [SendGrid](https://sendgrid.com/) tıklayarak **ücretsiz deneyin**.</span><span class="sxs-lookup"><span data-stu-id="cb811-111">You can sign up for a free trial account at [SendGrid](https://sendgrid.com/) by clicking **Try for Free**.</span></span> <span data-ttu-id="cb811-112">Ücretsiz deneme hesabınız için kaydettikten sonra toocreate gereken bir [API anahtarı](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) toosend posta izinler veren SendGrid içinde.</span><span class="sxs-lookup"><span data-stu-id="cb811-112">After you have registered for your free trial account, you need toocreate an [API key](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid that grants permissions toosend mail.</span></span> <span data-ttu-id="cb811-113">Daha sonra hello Öğreticide bu API anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb811-113">You need this API key later in hello tutorial.</span></span>

<span data-ttu-id="cb811-114">toocomplete Bu öğreticide, Visual Studio 2015 veya Visual Studio 2017 toomodify hello eylemlerinde hello önceden yapılandırılmış çözüm arka ucu gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb811-114">toocomplete this tutorial, you need Visual Studio 2015 or Visual Studio 2017 toomodify hello actions in hello preconfigured solution back end.</span></span>

<span data-ttu-id="cb811-115">Önceden yapılandırılmış Çözüm zaten sağladığınız Uzaktan izleme varsayıldığında, bu çözümde hello toohello kaynak grubunun gidin [Azure portal][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="cb811-115">Assuming you’ve already provisioned your remote monitoring preconfigured solution, navigate toohello resource group for that solution in hello [Azure portal][lnk-azureportal].</span></span> <span data-ttu-id="cb811-116">Merhaba kaynak grubuna sahip aynı adı hello çözüm adı gibi hello Uzaktan izleme çözümünüz ne zaman sağladığınız seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="cb811-116">hello resource group has hello same name as hello solution name you chose when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="cb811-117">Merhaba kaynak grubunda Azure kaynaklarını hello hello Klasik Azure portalı bulabilirsiniz Azure Active Directory Uygulama dışında çözümünüz için tüm hello sağlanan görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb811-117">In hello resource group, you can see all hello provisioned Azure resources for your solution except for hello Azure Active Directory application that you can find in hello Azure Classic Portal.</span></span> <span data-ttu-id="cb811-118">Merhaba aşağıdaki ekran görüntüsünde gösteren bir örnek **kaynak grubu** Uzaktan izleme için dikey önceden yapılandırılmış çözüm:</span><span class="sxs-lookup"><span data-stu-id="cb811-118">hello following screenshot shows an example **Resource group** blade for a remote monitoring preconfigured solution:</span></span>

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

<span data-ttu-id="cb811-119">toobegin, çözüm hello mantığı uygulama toouse hello ile ayarlama önceden yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="cb811-119">toobegin, set up hello logic app toouse with hello preconfigured solution.</span></span>

## <a name="set-up-hello-logic-app"></a><span data-ttu-id="cb811-120">Mantıksal uygulama Hello ayarlayın</span><span class="sxs-lookup"><span data-stu-id="cb811-120">Set up hello Logic App</span></span>
1. <span data-ttu-id="cb811-121">Tıklatın **Ekle** , kaynak grubu dikey penceresinde hello Azure Portalı'ndaki hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="cb811-121">Click **Add** at hello top of your resource group blade in hello Azure portal.</span></span>
2. <span data-ttu-id="cb811-122">Arama **mantıksal uygulama**, onu seçin ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="cb811-122">Search for **Logic App**, select it and then click **Create**.</span></span>
3. <span data-ttu-id="cb811-123">Merhaba dolgu **adı** ve kullanım hello aynı **abonelik** ve **kaynak grubu** Uzaktan izleme çözümünüzü sağlarken kullanılan.</span><span class="sxs-lookup"><span data-stu-id="cb811-123">Fill out hello **Name** and use hello same **Subscription** and **Resource group** that you used when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="cb811-124">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cb811-124">Click **Create**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. <span data-ttu-id="cb811-125">Dağıtımınız tamamlandığında, bir kaynak olarak mantıksal uygulama listelenen hello kaynak grubunuzdaki görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb811-125">When your deployment completes, you can see hello Logic App is listed as a resource in your resource group.</span></span>
5. <span data-ttu-id="cb811-126">Tıklatın hello mantıksal uygulama toonavigate toohello mantıksal uygulama dikey penceresinde, select hello **boş mantıksal uygulama** şablonu tooopen hello **Logic Apps Tasarımcısı**.</span><span class="sxs-lookup"><span data-stu-id="cb811-126">Click hello Logic App toonavigate toohello Logic App blade, select hello **Blank Logic App** template tooopen hello **Logic Apps Designer**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. <span data-ttu-id="cb811-127">Seçin **isteği**.</span><span class="sxs-lookup"><span data-stu-id="cb811-127">Select **Request**.</span></span> <span data-ttu-id="cb811-128">Bu eylem, gelen HTTP isteğiyle belirli bir JSON yükü davranır tetikleyici olarak biçimlendirilmiş belirtir.</span><span class="sxs-lookup"><span data-stu-id="cb811-128">This action specifies that an incoming HTTP request with a specific JSON formatted payload acts as a trigger.</span></span>
7. <span data-ttu-id="cb811-129">İstek gövdesi JSON şeması hello koddan hello yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="cb811-129">Paste hello following code into hello Request Body JSON Schema:</span></span>
   
    ```json
    {
      "$schema": "http://json-schema.org/draft-04/schema#",
      "id": "/",
      "properties": {
        "DeviceId": {
          "id": "DeviceId",
          "type": "string"
        },
        "measuredValue": {
          "id": "measuredValue",
          "type": "integer"
        },
        "measurementName": {
          "id": "measurementName",
          "type": "string"
        }
      },
      "required": [
        "DeviceId",
        "measurementName",
        "measuredValue"
      ],
      "type": "object"
    }
    ```
   
   > [!NOTE]
   > <span data-ttu-id="cb811-130">Merhaba mantıksal uygulama kaydedebilir, ancak öncelikle bir eylem eklemeniz gerekir sonra hello HTTP post hello URL'sini kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb811-130">You can copy hello URL for hello HTTP post after you save hello logic app, but first you must add an action.</span></span>
   > 
   > 
8. <span data-ttu-id="cb811-131">Tıklatın **+ yeni adım** el ile tetikleyici altında.</span><span class="sxs-lookup"><span data-stu-id="cb811-131">Click **+ New step** under your manual trigger.</span></span> <span data-ttu-id="cb811-132">Ardından **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="cb811-132">Then click **Add an action**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. <span data-ttu-id="cb811-133">Arama **SendGrid - e-postası gönderme** ve tıklatın.</span><span class="sxs-lookup"><span data-stu-id="cb811-133">Search for **SendGrid - Send email** and click it.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. <span data-ttu-id="cb811-134">Merhaba bağlantı için bir ad girin **SendGridConnection**, hello girin **SendGrid API anahtarı** SendGrid hesabınızı ayarlama'ı tıklattığınızda, oluşturduğunuz **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="cb811-134">Enter a name for hello connection, such as **SendGridConnection**, enter hello **SendGrid API Key** you created when you set up your SendGrid account, and click **Create**.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. <span data-ttu-id="cb811-135">E-posta adresleri, kendi tooboth hello eklemek **gelen** ve **için** alanları.</span><span class="sxs-lookup"><span data-stu-id="cb811-135">Add email addresses you own tooboth hello **From** and **To** fields.</span></span> <span data-ttu-id="cb811-136">Ekleme **Uzaktan izleme uyarı [DeviceID]** toohello **konu** alan.</span><span class="sxs-lookup"><span data-stu-id="cb811-136">Add **Remote monitoring alert [DeviceId]** toohello **Subject** field.</span></span> <span data-ttu-id="cb811-137">Merhaba, **e-posta gövdesi** alanında, eklemek **aygıt [DeviceID], [measurementName] [measuredValue] değerle bildirdi.**</span><span class="sxs-lookup"><span data-stu-id="cb811-137">In hello **Email Body** field, add **Device [DeviceId] has reported [measurementName] with value [measuredValue].**</span></span> <span data-ttu-id="cb811-138">Ekleyebileceğiniz **[DeviceID]**, **[measurementName]**, ve **[measuredValue]** hello tıklayarak **önceki adımlarıveriekleyebilirsiniz**bölümü.</span><span class="sxs-lookup"><span data-stu-id="cb811-138">You can add **[DeviceId]**, **[measurementName]**, and **[measuredValue]** by clicking in hello **You can insert data from previous steps** section.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. <span data-ttu-id="cb811-139">Tıklatın **kaydetmek** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="cb811-139">Click **Save** in hello top menu.</span></span>
13. <span data-ttu-id="cb811-140">Merhaba tıklatın **isteği** tetikleyici ve kopyalama hello **Http Post toothis URL** değeri.</span><span class="sxs-lookup"><span data-stu-id="cb811-140">Click hello **Request** trigger and copy hello **Http Post toothis URL** value.</span></span> <span data-ttu-id="cb811-141">Bu URL'yi daha sonra Bu öğreticide gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb811-141">You need this URL later in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="cb811-142">Logic Apps etkinleştirmek, toorun [farklı türlerde eylem] [ lnk-logic-apps-actions] Office 365'te Eylemler dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="cb811-142">Logic Apps enable you toorun [many different types of action][lnk-logic-apps-actions] including actions in Office 365.</span></span> 
> 
> 

## <a name="set-up-hello-eventprocessor-web-job"></a><span data-ttu-id="cb811-143">EventProcessor Web işi Hello ayarlayın</span><span class="sxs-lookup"><span data-stu-id="cb811-143">Set up hello EventProcessor Web Job</span></span>
<span data-ttu-id="cb811-144">Bu bölümde, önceden yapılandırılmış çözüm toohello mantıksal oluşturduğunuz uygulama bağlayın.</span><span class="sxs-lookup"><span data-stu-id="cb811-144">In this section, you connect your preconfigured solution toohello Logic App you created.</span></span> <span data-ttu-id="cb811-145">toocomplete bu görev, bir cihaz algılayıcı değeri bir eşiği aştığında harekete hello URL tootrigger hello mantıksal uygulama toohello eylem ekleme.</span><span class="sxs-lookup"><span data-stu-id="cb811-145">toocomplete this task, you add hello URL tootrigger hello Logic App toohello action that fires when a device sensor value exceeds a threshold.</span></span>

1. <span data-ttu-id="cb811-146">Git istemci tooclone hello en son sürümüne hello kullan [azure-iot-remote-monitoring github deposunu][lnk-rmgithub].</span><span class="sxs-lookup"><span data-stu-id="cb811-146">Use your git client tooclone hello latest version of hello [azure-iot-remote-monitoring github repository][lnk-rmgithub].</span></span> <span data-ttu-id="cb811-147">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="cb811-147">For example:</span></span>
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. <span data-ttu-id="cb811-148">Visual Studio'da hello açın **RemoteMonitoring.sln** kopyasından hello yerel hello deposu.</span><span class="sxs-lookup"><span data-stu-id="cb811-148">In Visual Studio, open hello **RemoteMonitoring.sln** from hello local copy of hello repository.</span></span>
3. <span data-ttu-id="cb811-149">Açık hello **ActionRepository.cs** hello dosyasında **altyapı\\depo** klasör.</span><span class="sxs-lookup"><span data-stu-id="cb811-149">Open hello **ActionRepository.cs** file in hello **Infrastructure\\Repository** folder.</span></span>
4. <span data-ttu-id="cb811-150">Güncelleştirme hello **actionIds** hello sözlüğüyle **Http Post toothis URL** mantığı uygulamanızdan gibi Not:</span><span class="sxs-lookup"><span data-stu-id="cb811-150">Update hello **actionIds** dictionary with hello **Http Post toothis URL** you noted from your Logic App as follows:</span></span>
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post toothis URL>" },
        { "Raise Alarm", "<Http Post toothis URL>" }
    };
    ```
5. <span data-ttu-id="cb811-151">Çözümde Hello değişiklikleri kaydedin ve Visual Studio çıkın.</span><span class="sxs-lookup"><span data-stu-id="cb811-151">Save hello changes in solution and exit Visual Studio.</span></span>

## <a name="deploy-from-hello-command-line"></a><span data-ttu-id="cb811-152">Merhaba komut satırından dağıtma</span><span class="sxs-lookup"><span data-stu-id="cb811-152">Deploy from hello command line</span></span>
<span data-ttu-id="cb811-153">Bu bölümde, güncelleştirilmiş sürümü şu anda Azure'da çalışan hello Uzaktan izleme çözümü tooreplace hello dağıtın.</span><span class="sxs-lookup"><span data-stu-id="cb811-153">In this section, you deploy your updated version of hello remote monitoring solution tooreplace hello version currently running in Azure.</span></span>

1. <span data-ttu-id="cb811-154">Merhaba aşağıdaki [geliştirme Kurulum] [ lnk-devsetup] ortamınızı dağıtımı için yönergeler tooset.</span><span class="sxs-lookup"><span data-stu-id="cb811-154">Following hello [dev set-up][lnk-devsetup] instructions tooset up your environment for deployment.</span></span>
2. <span data-ttu-id="cb811-155">yerel olarak toodeploy izleyin hello [yerel dağıtım] [ lnk-localdeploy] yönergeler.</span><span class="sxs-lookup"><span data-stu-id="cb811-155">toodeploy locally, follow hello [local deployment][lnk-localdeploy] instructions.</span></span>
3. <span data-ttu-id="cb811-156">toodeploy toohello Bulut ve var olan bulut dağıtımınızı güncelleştirmek, hello izleyin [bulut dağıtımı] [ lnk-clouddeploy] yönergeler.</span><span class="sxs-lookup"><span data-stu-id="cb811-156">toodeploy toohello cloud and update your existing cloud deployment, follow hello [cloud deployment][lnk-clouddeploy] instructions.</span></span> <span data-ttu-id="cb811-157">Merhaba dağıtım adı olarak özgün dağıtımınızın Hello adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="cb811-157">Use hello name of your original deployment as hello deployment name.</span></span> <span data-ttu-id="cb811-158">Merhaba özgün dağıtım çağrıldı örneğin **demologicapp**, komutu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="cb811-158">For example if hello original deployment was called **demologicapp**, use hello following command:</span></span>
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   <span data-ttu-id="cb811-159">Merhaba komut dosyasını çalıştırır derlerken toouse aynı hello emin olun Azure hesabınız, abonelik, bölgeye ve hello çözüm sağladığında kullanılan Active Directory örneğini.</span><span class="sxs-lookup"><span data-stu-id="cb811-159">When hello build script runs, be sure toouse hello same Azure account, subscription, region, and Active Directory instance you used when you provisioned hello solution.</span></span>

## <a name="see-your-logic-app-in-action"></a><span data-ttu-id="cb811-160">Mantıksal uygulamanızı eylem bakın</span><span class="sxs-lookup"><span data-stu-id="cb811-160">See your Logic App in action</span></span>
<span data-ttu-id="cb811-161">Merhaba Uzaktan izleme çözümü bir çözüm sağladığınızda, varsayılan olarak ayarlanan iki kuralları vardır.</span><span class="sxs-lookup"><span data-stu-id="cb811-161">hello remote monitoring preconfigured solution has two rules set up by default when you provision a solution.</span></span> <span data-ttu-id="cb811-162">Merhaba üzerinde hem kurallardır **SampleDevice001** aygıt:</span><span class="sxs-lookup"><span data-stu-id="cb811-162">Both rules are on hello **SampleDevice001** device:</span></span>

* <span data-ttu-id="cb811-163">Sıcaklık > 38.00</span><span class="sxs-lookup"><span data-stu-id="cb811-163">Temperature > 38.00</span></span>
* <span data-ttu-id="cb811-164">Nem > 48.00</span><span class="sxs-lookup"><span data-stu-id="cb811-164">Humidity > 48.00</span></span>

<span data-ttu-id="cb811-165">Merhaba sıcaklık kuralını tetikler hello **yükseltmek Alarm** eylem ve hello nem kuralını tetikler hello **SendMessage** eylem.</span><span class="sxs-lookup"><span data-stu-id="cb811-165">hello temperature rule triggers hello **Raise Alarm** action and hello Humidity rule triggers hello **SendMessage** action.</span></span> <span data-ttu-id="cb811-166">Kullandığınız varsayılarak hello aynı URL için her iki Eylemler hello **ActionRepository** sınıfı, her iki kural için logic app Tetikleyicileri.</span><span class="sxs-lookup"><span data-stu-id="cb811-166">Assuming you used hello same URL for both actions hello **ActionRepository** class, your logic app triggers for either rule.</span></span> <span data-ttu-id="cb811-167">SendGrid toosend bir e-posta toohello hem kurallarıyla **için** hello uyarı ayrıntılarını adresiyle.</span><span class="sxs-lookup"><span data-stu-id="cb811-167">Both rules use SendGrid toosend an email toohello **To** address with details of hello alert.</span></span>

> [!NOTE]
> <span data-ttu-id="cb811-168">Merhaba eşiğine her zaman hello mantıksal uygulama tootrigger devam eder.</span><span class="sxs-lookup"><span data-stu-id="cb811-168">hello Logic App continues tootrigger every time hello threshold is met.</span></span> <span data-ttu-id="cb811-169">tooavoid gereksiz e-postalar, ya da devre dışı bırakabilirsiniz hello kuralları, çözüm portalı veya devre dışı bırakma hello mantıksal uygulama hello içinde [Azure portal][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="cb811-169">tooavoid unnecessary emails, you can either disable hello rules in your solution portal or disable hello Logic App in hello [Azure portal][lnk-azureportal].</span></span>
> 
> 

<span data-ttu-id="cb811-170">Merhaba Portalı'nda Hello mantıksal uygulama çalıştığında, ayrıca tooreceiving e-postalar, de görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cb811-170">In addition tooreceiving emails, you can also see when hello Logic App runs in hello portal:</span></span>

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a><span data-ttu-id="cb811-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cb811-171">Next steps</span></span>
<span data-ttu-id="cb811-172">Bir mantıksal uygulama tooconnect hello önceden yapılandırılmış çözüm tooa iş sürecini kullanmış olduğunuz, hello önceden yapılandırılmış çözümleri özelleştirme hello seçenekleri hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cb811-172">Now that you've used a Logic App tooconnect hello preconfigured solution tooa business process, you can learn more about hello options for customizing hello preconfigured solutions:</span></span>

* <span data-ttu-id="cb811-173">[Dinamik telemetri hello Uzaktan izleme çözümü ile kullanma][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="cb811-173">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="cb811-174">[Cihaz bilgi meta verilerde hello Uzaktan izleme çözümü][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="cb811-174">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo]</span></span>

[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk-internetofthings]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-getstarted]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-azureportal]: https://portal.azure.com
[lnk-logic-apps-actions]: ../connectors/apis-list.md
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-devsetup]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/dev-setup.md
[lnk-localdeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/local-deployment.md
[lnk-clouddeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
