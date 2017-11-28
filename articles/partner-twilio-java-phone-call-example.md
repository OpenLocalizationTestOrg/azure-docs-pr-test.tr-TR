---
title: "aaaHow tooMake Twilio (Java) bir telefon çağrısında | Microsoft Docs"
description: "Nasıl toomake bir telefon çağrısı Azure üzerinde bir Java uygulamasında Twilio kullanarak bir web sayfasından öğrenin."
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 0381789e-e775-41a0-a784-294275192b1d
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 04fe5a78d431a79790dee3ca75c2b004aea4345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-java-application-on-azure"></a><span data-ttu-id="34c1a-103">Nasıl tooMake kullanarak bir telefon araması Twilio Azure üzerinde bir Java uygulamasında</span><span class="sxs-lookup"><span data-stu-id="34c1a-103">How tooMake a Phone Call Using Twilio in a Java Application on Azure</span></span>
<span data-ttu-id="34c1a-104">Merhaba aşağıdaki örnek, Azure üzerinde barındırılan bir web sayfasından bir çağrı Twilio toomake nasıl kullanabileceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="34c1a-104">hello following example shows you how you can use Twilio toomake a call from a web page hosted in Azure.</span></span> <span data-ttu-id="34c1a-105">Merhaba sonuç uygulaması hello aşağıdaki ekran görüntüsü gösterildiği gibi hello kullanıcıdan telefon araması değerlerini ister.</span><span class="sxs-lookup"><span data-stu-id="34c1a-105">hello resulting application will prompt hello user for phone call values, as shown in hello following screen shot.</span></span>

![Twilio ve Java kullanarak azure çağrı formu][twilio_java]

<span data-ttu-id="34c1a-107">Toodo hello aşağıdakilere ihtiyacınız olacak toouse hello kod bu konuda:</span><span class="sxs-lookup"><span data-stu-id="34c1a-107">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="34c1a-108">Twilio hesabı ve kimlik doğrulama alma belirteci.</span><span class="sxs-lookup"><span data-stu-id="34c1a-108">Acquire a Twilio account and authentication token.</span></span> <span data-ttu-id="34c1a-109">tooget Twilio ile kullanmaya değerlendirmek, fiyatlandırma [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="34c1a-109">tooget started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="34c1a-110">Konumundaki kaydolabilirsiniz [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="34c1a-110">You can sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="34c1a-111">Merhaba Twilio tarafından sağlanan API hakkında daha fazla bilgi için bkz: [http://www.twilio.com/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="34c1a-111">For information about hello API provided by Twilio, see [http://www.twilio.com/api][twilio_api].</span></span>
2. <span data-ttu-id="34c1a-112">Merhaba Twilio JAR edinin.</span><span class="sxs-lookup"><span data-stu-id="34c1a-112">Obtain hello Twilio JAR.</span></span> <span data-ttu-id="34c1a-113">Konumundaki [https://github.com/twilio/twilio-java][twilio_java_github], hello GitHub kaynakları indirmek ve kendi JAR oluşturabilir veya önceden oluşturulmuş bir JAR (veya ile bağımlılıklar olmadan) yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34c1a-113">At [https://github.com/twilio/twilio-java][twilio_java_github], you can download hello GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
   <span data-ttu-id="34c1a-114">Bu konudaki Hello kod bağımlılıkları ile TwilioJava 3.3.8 JAR önceden oluşturulmuş hello kullanılarak yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="34c1a-114">hello code in this topic was written using hello pre-built TwilioJava-3.3.8-with-dependencies JAR.</span></span>
3. <span data-ttu-id="34c1a-115">Java derleme yolu hello JAR tooyour ekleyin.</span><span class="sxs-lookup"><span data-stu-id="34c1a-115">Add hello JAR tooyour Java build path.</span></span>
4. <span data-ttu-id="34c1a-116">Bu Java uygulaması Eclipse toocreate kullanıyorsanız, hello Twilio JAR Eclipse'nın dağıtım derleme özelliğini kullanarak, uygulama dağıtım dosyanızda (WAR) içerir.</span><span class="sxs-lookup"><span data-stu-id="34c1a-116">If you are using Eclipse toocreate this Java application, include hello Twilio JAR in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="34c1a-117">Bu Java uygulaması Eclipse toocreate kullanmıyorsanız hello Twilio JAR hello içinde dahil olduğundan emin olun, Java uygulama ve eklenen toohello sınıf yolu uygulamanızın olarak aynı Azure rol.</span><span class="sxs-lookup"><span data-stu-id="34c1a-117">If you are not using Eclipse toocreate this Java application, ensure hello Twilio JAR is included within hello same Azure role as your Java application, and added toohello class path of your application.</span></span>
5. <span data-ttu-id="34c1a-118">Cacerts anahtar deposu MD5 parmak izi 67:CB:9 D ile Merhaba Equifax güvenli sertifika yetkilisi sertifikasına sahip olmasını: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (Merhaba numarası 35:DE:F4:CF ve hello SHA1 parmak izi D2:32:09:AD:23:D seri 3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="34c1a-118">Ensure your cacerts keystore contains hello Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello serial number is 35:DE:F4:CF and hello SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="34c1a-119">Merhaba sertifika yetkilisi (CA) sertifikası hello için budur [https://api.twilio.com] [ twilio_api_service] Twilio API'leri kullandığınızda çağrılan hizmet.</span><span class="sxs-lookup"><span data-stu-id="34c1a-119">This is hello certificate authority (CA) certificate for hello [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="34c1a-120">Bu CA sertifikası tooyour JDK'ın cacert depolama ekleme hakkında daha fazla bilgi için bkz: [sertifika toohello Java CA sertifika deposuna ekleme][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="34c1a-120">For information about adding this CA certificate tooyour JDK's cacert store, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="34c1a-121">Merhaba bilgilerine ek olarak, bir aşina [bir Hello World uygulamasını kullanarak hello Eclipse için Azure araç seti oluşturma][azure_java_eclipse_hello_world], ya da Azure IF içinde Java uygulamalarını barındırmak için başka teknikler, Eclipse kullanmıyorsanız, kesinlikle önerilir.</span><span class="sxs-lookup"><span data-stu-id="34c1a-121">Additionally, familiarity with hello information at [Creating a Hello World Application Using hello Azure Toolkit for Eclipse][azure_java_eclipse_hello_world], or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="34c1a-122">Arama yapmak için web formu oluşturma</span><span class="sxs-lookup"><span data-stu-id="34c1a-122">Create a web form for making a call</span></span>
<span data-ttu-id="34c1a-123">koddan hello nasıl toocreate web form arama yapmak için tooretrieve kullanıcı verileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="34c1a-123">hello following code shows how toocreate a web form tooretrieve user data for making a call.</span></span> <span data-ttu-id="34c1a-124">Bu örnekte, yeni bir dinamik web projesi adlı **TwilioCloud**, oluşturulduğu ve **callform.jsp** bir JSP dosyası olarak eklendi.</span><span class="sxs-lookup"><span data-stu-id="34c1a-124">For purposes of this example, a new dynamic web project, named **TwilioCloud**, was created, and **callform.jsp** was added as a JSP file.</span></span>

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Automated call form</title>
    </head>
    <body>
     <p>Fill in all fields and click <b>Make this call</b>.</p>
     <br/>
      <form action="makecall.jsp" method="post">
       <table>
         <tr>
           <td>To:</td>
           <td><input type="text" size=50 name="callTo" value="" />
           </td>
         </tr>
         <tr>
           <td>From:</td>
           <td><input type="text" size=50 name="callFrom" value="" />
           </td>
         </tr>
         <tr>
           <td>Call message:</td>
           <td><input type="text" size=400 name="callText" value="Hello. This is hello call text. Good bye." />
           </td>
         </tr>
         <tr>
           <td colspan=2><input type="submit" value="Make this call" />
           </td>
         </tr>
       </table>
     </form>
     <br/>
    </body>
    </html>

## <a name="create-hello-code-toomake-hello-call"></a><span data-ttu-id="34c1a-125">Merhaba kod toomake hello çağrı oluşturma</span><span class="sxs-lookup"><span data-stu-id="34c1a-125">Create hello code toomake hello call</span></span>
<span data-ttu-id="34c1a-126">Merhaba hello kullanıcı callform.jsp tarafından görüntülenen hello formun tamamlandığında olarak adlandırılır, aşağıdaki kod, hello çağrı iletisi oluşturur ve hello çağrı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="34c1a-126">hello following code, which is called when hello user completes hello form displayed by callform.jsp, creates hello call message and generates hello call.</span></span> <span data-ttu-id="34c1a-127">Bu örneğin amaçları doğrultusunda hello JSP dosyası adlı **makecall.jsp** ve toohello eklendi **TwilioCloud** projesi.</span><span class="sxs-lookup"><span data-stu-id="34c1a-127">For purposes of this example, hello JSP file is named **makecall.jsp** and was added toohello **TwilioCloud** project.</span></span> <span data-ttu-id="34c1a-128">(Twilio hesabı ve kimlik doğrulama belirteci çok atanan hello yer tutucu değerlerini yerine kullanım**accountSID** ve **authToken** aşağıdaki hello kodda.)</span><span class="sxs-lookup"><span data-stu-id="34c1a-128">(Use your Twilio account and authentication token instead of hello placeholder values assigned too**accountSID** and **authToken** in hello code below.)</span></span>

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    import="java.util.*"
    import="com.twilio.*"
    import="com.twilio.sdk.*"
    import="com.twilio.sdk.resource.factory.*"
    import="com.twilio.sdk.resource.instance.*"
    pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Call processing happens here</title>
    </head>
    <body>
        <b>This is my make call page.</b><p/>
     <%
    try 
    {
         // Use your account SID and authentication token instead
         // of hello placeholders shown here.
         String accountSID = "your_twilio_account";
         String authToken = "your_twilio_authentication_token";

         // Instantiate an instance of hello Twilio client.     
         TwilioRestClient client;
         client = new TwilioRestClient(accountSID, authToken);

         // Retrieve hello account, used later tooretrieve hello CallFactory.
         Account account = client.getAccount();

         // Display hello client endpoint. 
         out.println("<p>Using Twilio endpoint " + client.getEndpoint() + ".</p>");

         // Display hello API version.
         String APIVERSION = TwilioRestClient.DEFAULT_VERSION;
         out.println("<p>Twilio client API version is " + APIVERSION + ".</p>");

         // Retrieve hello values entered by hello user.
         String callTo = request.getParameter("callTo");  
         // hello Outgoing Caller ID, used for hello From parameter,
         // must have previously been verified with Twilio.
         String callFrom = request.getParameter("callFrom");
         String userText = request.getParameter("callText");

         // Replace spaces in hello user's text with '%20', 
         // toomake hello text suitable for a URL.
         userText = userText.replace(" ", "%20");

         // Create a URL using hello Twilio message and hello user-entered text.
         String Url="http://twimlets.com/message";
         Url = Url + "?Message%5B0%5D=" + userText;

         // Display hello message URL.
         out.println("<p>");
         out.println("hello URL is " + Url);
         out.println("</p>");

         // Place hello call From, tooand URL values into a hash map. 
         HashMap<String, String> params = new HashMap<String, String>();
         params.put("From", callFrom);
         params.put("To", callTo);
         params.put("Url", Url);

         CallFactory callFactory = account.getCallFactory();
         Call call = callFactory.create(params);
         out.println("<p>Call status: " + call.getStatus()  + "</p>"); 
    } 
    catch (TwilioRestException e) 
    {
        out.println("<p>TwilioRestException encountered: " + e.getMessage() + "</p>");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    catch (Exception e) 
    {
        out.println("<p>Exception encountered: " + e.getMessage() + "");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    %>
    </body>
    </html>

<span data-ttu-id="34c1a-129">Ayrıca toomaking Merhaba çağrısı, makecall.jsp hello Twilio uç noktası, API sürümü ve hello çağrı durumunu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="34c1a-129">In addition toomaking hello call, makecall.jsp displays hello Twilio endpoint, API version, and hello call status.</span></span> <span data-ttu-id="34c1a-130">Aşağıdaki ekran görüntüsü hello buna bir örnektir:</span><span class="sxs-lookup"><span data-stu-id="34c1a-130">An example is hello following screen shot:</span></span>

![Twilio ve Java kullanarak azure çağrı yanıtı][twilio_java_response]

## <a name="run-hello-application"></a><span data-ttu-id="34c1a-132">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="34c1a-132">Run hello application</span></span>
<span data-ttu-id="34c1a-133">Aşağıdaki olan hello üst düzey adımları toorun uygulamanızı; Bu adımları bulunabilir ayrıntıları [bir Hello World uygulamasını kullanarak hello Eclipse için Azure araç seti oluşturma][azure_java_eclipse_hello_world].</span><span class="sxs-lookup"><span data-stu-id="34c1a-133">Following are hello high-level steps toorun your application; details for these steps can be found at [Creating a Hello World Application Using hello Azure Toolkit for Eclipse][azure_java_eclipse_hello_world].</span></span>

1. <span data-ttu-id="34c1a-134">TwilioCloud WAR toohello Azure verme **approot** klasör.</span><span class="sxs-lookup"><span data-stu-id="34c1a-134">Export your TwilioCloud WAR toohello Azure **approot** folder.</span></span> 
2. <span data-ttu-id="34c1a-135">Değiştirme **startup.cmd** toounzip TwilioCloud WAR.</span><span class="sxs-lookup"><span data-stu-id="34c1a-135">Modify **startup.cmd** toounzip your TwilioCloud WAR.</span></span>
3. <span data-ttu-id="34c1a-136">Merhaba işlem öykünücüsü için uygulamanızı derleyin.</span><span class="sxs-lookup"><span data-stu-id="34c1a-136">Compile your application for hello compute emulator.</span></span>
4. <span data-ttu-id="34c1a-137">Dağıtımınızı hello işlem öykünücüsünde başlatın.</span><span class="sxs-lookup"><span data-stu-id="34c1a-137">Start your deployment in hello compute emulator.</span></span>
5. <span data-ttu-id="34c1a-138">Bir tarayıcı açın ve Çalıştır **http://localhost:8080/TwilioCloud/callform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="34c1a-138">Open a browser, and run **http://localhost:8080/TwilioCloud/callform.jsp**.</span></span>
6. <span data-ttu-id="34c1a-139">Değerleri hello girin, tıklatın **bu çağrıyı yapmak**ve ardından makecall.jsp hello sonuçlarında görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34c1a-139">Enter values in hello form, click **Make this call**, and then see hello results in makecall.jsp.</span></span>

<span data-ttu-id="34c1a-140">Hazır toodeploy tooAzure olduğunda, dağıtım toohello bulut için yeniden derleyin, tooAzure dağıtmak ve http:// çalıştırmak*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp hello tarayıcıda ( içindeğeryerine*your_hosted_name*).</span><span class="sxs-lookup"><span data-stu-id="34c1a-140">When you are ready toodeploy tooAzure, recompile for deployment toohello cloud, deploy tooAzure, and run http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp in hello browser (substitute your value for *your_hosted_name*).</span></span>

## <a name="next-steps"></a><span data-ttu-id="34c1a-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="34c1a-141">Next steps</span></span>
<span data-ttu-id="34c1a-142">Bu kod tooshow sağlanan Azure üzerinde Java Twilio kullanarak, temel işlevleri.</span><span class="sxs-lookup"><span data-stu-id="34c1a-142">This code was provided tooshow you basic functionality using Twilio in Java on Azure.</span></span> <span data-ttu-id="34c1a-143">TooAzure üretimde dağıtmadan önce daha fazla hata işleme veya diğer özellikler tooadd isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34c1a-143">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="34c1a-144">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="34c1a-144">For example:</span></span>

* <span data-ttu-id="34c1a-145">Bir web formu kullanmak yerine, Azure storage bloblarında veya SQL veritabanı toostore telefon numaralarını kullanın ve metin arama.</span><span class="sxs-lookup"><span data-stu-id="34c1a-145">Instead of using a web form, you could use Azure storage blobs or SQL Database toostore phone numbers and call text.</span></span> <span data-ttu-id="34c1a-146">Azure storage bloblarında Java kullanma hakkında daha fazla bilgi için bkz: [nasıl tooUse hello Java'dan Blob Depolama hizmetinin][howto_blob_storage_java].</span><span class="sxs-lookup"><span data-stu-id="34c1a-146">For information about using Azure storage blobs in Java, see [How tooUse hello Blob Storage Service from Java][howto_blob_storage_java].</span></span> <span data-ttu-id="34c1a-147">SQL veritabanı Java kullanma hakkında daha fazla bilgi için bkz: [SQL veritabanında kullanarak Java][howto_sql_azure_java].</span><span class="sxs-lookup"><span data-stu-id="34c1a-147">For information about using SQL Database in Java, see [Using SQL Database in Java][howto_sql_azure_java].</span></span>
* <span data-ttu-id="34c1a-148">Kullanabileceğinizi **RoleEnvironment.getConfigurationSettings** tooretrieve hello Twilio hesap Kimliğini ve kimlik doğrulama belirteci makecall.jsp hello değerleri sabit kodlama yerine dağıtımınızın yapılandırma ayarları.</span><span class="sxs-lookup"><span data-stu-id="34c1a-148">You could use **RoleEnvironment.getConfigurationSettings** tooretrieve hello Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding hello values in makecall.jsp.</span></span> <span data-ttu-id="34c1a-149">Merhaba hakkında bilgi için **RoleEnvironment** sınıfı için bkz: [kullanma hello Azure hizmeti Çalışma Zamanı Kitaplığı'nda JSP] [ azure_runtime_jsp] ve hello Azure hizmeti çalışma zamanı paketi belgeleri [http://dl.windowsazure.com/javadoc][azure_javadoc].</span><span class="sxs-lookup"><span data-stu-id="34c1a-149">For information about hello **RoleEnvironment** class, see [Using hello Azure Service Runtime Library in JSP][azure_runtime_jsp] and hello Azure Service Runtime package documentation at [http://dl.windowsazure.com/javadoc][azure_javadoc].</span></span>
* <span data-ttu-id="34c1a-150">Merhaba makecall.jsp kodunu atar Twilio tarafından sağlanan URL [http://twimlets.com/message][twimlet_message_url], toohello **Url** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="34c1a-150">hello makecall.jsp code assigns a Twilio-provided URL, [http://twimlets.com/message][twimlet_message_url], toohello **Url** variable.</span></span> <span data-ttu-id="34c1a-151">Bu URL'yi nasıl tooproceed hello ile çağrı Twilio bildiren bir Twilio biçimlendirme dili (TwiML) yanıt sağlar.</span><span class="sxs-lookup"><span data-stu-id="34c1a-151">This URL provides a Twilio Markup Language (TwiML) response that informs Twilio how tooproceed with hello call.</span></span> <span data-ttu-id="34c1a-152">Örneğin, hello döndürülen TwiML içerebilir bir  **&lt;Say&gt;**  konuşulan toohello çağrı alıcı olan metinde sonuçları fiil.</span><span class="sxs-lookup"><span data-stu-id="34c1a-152">For example, hello TwiML that is returned can contain a **&lt;Say&gt;** verb that results in text being spoken toohello call recipient.</span></span> <span data-ttu-id="34c1a-153">Merhaba Twilio tarafından sağlanan URL kullanmak yerine, kendi hizmet toorespond tooTwilio's isteği oluşturabilirsiniz; Daha fazla bilgi için bkz: [nasıl tooUse ses ve Java SMS yetenekler için Twilio][howto_twilio_voice_sms_java].</span><span class="sxs-lookup"><span data-stu-id="34c1a-153">Instead of using hello Twilio-provided URL, you could build your own service toorespond tooTwilio's request; for more information, see [How tooUse Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java].</span></span> <span data-ttu-id="34c1a-154">TwiML hakkında daha fazla bilgi bulunabilir [http://www.twilio.com/docs/api/twiml][twiml]ve hakkında daha fazla bilgi  **&lt;Say&gt;**  ve diğer Twilio fiiller bulunabilir [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="34c1a-154">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about **&lt;Say&gt;** and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="34c1a-155">Merhaba Twilio güvenlik yönergeleri okuyun [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="34c1a-155">Read hello Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="34c1a-156">Twilio hakkında ek bilgi için bkz: [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="34c1a-156">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="34c1a-157">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34c1a-157">See Also</span></span>
* <span data-ttu-id="34c1a-158">[Nasıl tooUse Twilio ses ve Java SMS özellikleri][howto_twilio_voice_sms_java]</span><span class="sxs-lookup"><span data-stu-id="34c1a-158">[How tooUse Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java]</span></span>
* <span data-ttu-id="34c1a-159">[Sertifika toohello Java CA sertifika deposuna ekleme][add_ca_cert]</span><span class="sxs-lookup"><span data-stu-id="34c1a-159">[Adding a Certificate toohello Java CA Certificate Store][add_ca_cert]</span></span>

[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/api
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_java_github]: http://github.com/twilio/twilio-java
[twimlet_message_url]: http://twimlets.com/message
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api_service]: http://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[azure_java_eclipse_hello_world]: http://msdn.microsoft.com/library/windowsazure/hh690944.aspx
[howto_twilio_voice_sms_java]: partner-twilio-java-how-to-use-voice-sms.md
[howto_blob_storage_java]: http://www.windowsazure.com/develop/java/how-to-guides/blob-storage/
[howto_sql_azure_java]: http://msdn.microsoft.com/library/windowsazure/hh749029.aspx
[azure_runtime_jsp]: http://msdn.microsoft.com/library/windowsazure/hh690948.aspx
[azure_javadoc]: http://dl.windowsazure.com/javadoc
[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say
[twilio_java]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaCallForm.jpg
[twilio_java_response]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaMakeCall.jpg
