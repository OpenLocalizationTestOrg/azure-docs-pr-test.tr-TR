---
title: "Web App için TLS Karşılıklı Kimlik Doğrulamayı Yapılandırma"
description: "Web uygulamanız TLS istemci sertifikası kimlik doğrulamasını kullanmak için yapılandırmayı öğrenin."
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: cd1d15d3-2d9e-4502-9f11-a306dac4453a
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2016
ms.author: naziml
ms.openlocfilehash: db69852cffd1ff331ac4a640b04ea4360d00bf75
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-tls-mutual-authentication-for-web-app"></a><span data-ttu-id="aa15c-103">Web App için TLS Karşılıklı Kimlik Doğrulamayı Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="aa15c-103">How To Configure TLS Mutual Authentication for Web App</span></span>
## <a name="overview"></a><span data-ttu-id="aa15c-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="aa15c-104">Overview</span></span>
<span data-ttu-id="aa15c-105">Kimlik doğrulaması için farklı türlerde etkinleştirerek Azure web uygulamanıza erişimi kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa15c-105">You can restrict access to your Azure web app by enabling different types of authentication for it.</span></span> <span data-ttu-id="aa15c-106">Bunu yapmak için bir istek TLS/SSL üzerinden olduğunda istemci sertifikası kullanılarak kimlik doğrulaması için yoludur.</span><span class="sxs-lookup"><span data-stu-id="aa15c-106">One way to do so is to authenticate using a client certificate when the request is over TLS/SSL.</span></span> <span data-ttu-id="aa15c-107">Bu mekanizma TLS karşılıklı kimlik doğrulaması veya istemci sertifikası kimlik doğrulaması ve bu makalede istemci sertifikası kimlik doğrulamasını kullanmak için web uygulamanızı nasıl ayrıntılarıyla açıklar çağrılır.</span><span class="sxs-lookup"><span data-stu-id="aa15c-107">This mechanism is called TLS mutual authentication or client certificate authentication and this article will detail how to setup your web app to use client certificate authentication.</span></span>

> <span data-ttu-id="aa15c-108">**Not:** sitenizi HTTP ve HTTPS değil üzerinden erişirseniz, herhangi bir istemci sertifikası almaz.</span><span class="sxs-lookup"><span data-stu-id="aa15c-108">**Note:** If you access your site over HTTP and not HTTPS, you will not receive any client certificate.</span></span> <span data-ttu-id="aa15c-109">Uygulamanızın istemci sertifikası gerektiriyorsa, bu nedenle, istekleri uygulamanıza HTTP üzerinden izin vermemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="aa15c-109">So if your application requires client certificates you should not allow requests to your application over HTTP.</span></span>
> 
> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="configure-web-app-for-client-certificate-authentication"></a><span data-ttu-id="aa15c-110">Web uygulaması için istemci sertifikası kimlik doğrulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="aa15c-110">Configure Web App for Client Certificate Authentication</span></span>
<span data-ttu-id="aa15c-111">İstemci sertifikaları gerektirmek için web uygulamanızı için web uygulamanız için clientCertEnabled site ayarı ekleyin ve true olarak ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="aa15c-111">To setup your web app to require client certificates you need to add the clientCertEnabled site setting for your web app and set it to true.</span></span> <span data-ttu-id="aa15c-112">Bu ayar Portalı'nda yönetim deneyimi aracılığıyla şu anda kullanılabilir değil ve REST API bunu gerçekleştirmek için kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="aa15c-112">This setting is not currently available through the management experience in the Portal, and the REST API will need to be used to accomplish this.</span></span>

<span data-ttu-id="aa15c-113">Kullanabileceğiniz [ARMClient aracı](https://github.com/projectkudu/ARMClient) REST API çağrısı oluşturabilir kolaylaştırmak için.</span><span class="sxs-lookup"><span data-stu-id="aa15c-113">You can use the [ARMClient tool](https://github.com/projectkudu/ARMClient) to make it easy to craft the REST API call.</span></span> <span data-ttu-id="aa15c-114">Aracın oturum oturum sonra aşağıdaki komutu yürütün gerekir:</span><span class="sxs-lookup"><span data-stu-id="aa15c-114">After you log in with the tool you will need to issue the following command:</span></span>

    ARMClient PUT subscriptions/{Subscription Id}/resourcegroups/{Resource Group Name}/providers/Microsoft.Web/sites/{Website Name}?api-version=2015-04-01 @enableclientcert.json -verbose

<span data-ttu-id="aa15c-115">{} her şeyi web uygulamanız için bilgi ile değiştirerek ve bir dosya oluşturulurken aşağıdaki JSON ile enableclientcert.json içerik çağrılır:</span><span class="sxs-lookup"><span data-stu-id="aa15c-115">replacing everything in {} with information for your web app and creating a file called enableclientcert.json with the following JSON content:</span></span>

    {
        "location": "My Web App Location",
        "properties": {
            "clientCertEnabled": true
        }
    }

<span data-ttu-id="aa15c-116">Yerlerde, web uygulamanızın bulunduğu için "Konum" değerini değiştirdiğinizden emin olun ör Kuzey Orta ABD veya Batı ABD vs.</span><span class="sxs-lookup"><span data-stu-id="aa15c-116">Make sure to change the value of "location" to wherever your web app is located e.g. North Central US or West US etc.</span></span>

<span data-ttu-id="aa15c-117">Çevrilecek https://resources.azure.com kullanabilirsiniz `clientCertEnabled` özelliğine `true`.</span><span class="sxs-lookup"><span data-stu-id="aa15c-117">You can also use https://resources.azure.com to flip the `clientCertEnabled` property to `true`.</span></span>

> <span data-ttu-id="aa15c-118">**Not:** Powershell'den ARMClient çalıştırırsanız, kaçış gerekir @ simgesinden geri değer çizgisi olan JSON dosyası için '.</span><span class="sxs-lookup"><span data-stu-id="aa15c-118">**Note:** If you run ARMClient from Powershell, you will need to escape the @ symbol for the JSON file with a back tick \`.</span></span>
> 
> 

## <a name="accessing-the-client-certificate-from-your-web-app"></a><span data-ttu-id="aa15c-119">Web uygulamanızdan istemci sertifikasına erişme</span><span class="sxs-lookup"><span data-stu-id="aa15c-119">Accessing the Client Certificate From Your Web App</span></span>
<span data-ttu-id="aa15c-120">ASP.NET kullanıyorsanız ve istemci sertifikası kimlik doğrulamasını kullanmak için uygulamanızı yapılandırmak için sertifika ile de kullanılabilir olması **HttpRequest.ClientCertificate** özelliği.</span><span class="sxs-lookup"><span data-stu-id="aa15c-120">If you are using ASP.NET and configure your app to use client certificate authentication, the certificate will be available through the **HttpRequest.ClientCertificate** property.</span></span> <span data-ttu-id="aa15c-121">Diğer uygulama yığınları için istemci sertifikası uygulamanızda "X-ARR-ClientCert" istek üst bilgisinde base64 ile kodlanmış değeri ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="aa15c-121">For other application stacks, the client cert will be available in your app through a base64 encoded value in the "X-ARR-ClientCert" request header.</span></span> <span data-ttu-id="aa15c-122">Uygulamanız bu değerinden bir sertifika oluşturur ve uygulamanızda herhangi bir kimlik doğrulama ve yetkilendirme amacıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="aa15c-122">Your application can create a certificate from this value and then use it for authentication and authorization purposes in your application.</span></span>

## <a name="special-considerations-for-certificate-validation"></a><span data-ttu-id="aa15c-123">Sertifika doğrulama için özel hususlar</span><span class="sxs-lookup"><span data-stu-id="aa15c-123">Special Considerations for Certificate Validation</span></span>
<span data-ttu-id="aa15c-124">Uygulamaya gönderilen istemci sertifikası Azure Web Apps platformu tarafından herhangi bir doğrulama geçmez.</span><span class="sxs-lookup"><span data-stu-id="aa15c-124">The client certificate that is sent to the application does not go through any validation by the Azure Web Apps platform.</span></span> <span data-ttu-id="aa15c-125">Bu sertifika doğrulama web uygulaması sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="aa15c-125">Validating this certificate is the responsibility of the web app.</span></span> <span data-ttu-id="aa15c-126">Burada, kimlik doğrulama amacıyla sertifika özellikleri doğrular örnek ASP.NET kodu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="aa15c-126">Here is sample ASP.NET code that validates certificate properties for authentication purposes.</span></span>

    using System;
    using System.Collections.Specialized;
    using System.Security.Cryptography.X509Certificates;
    using System.Web;

    namespace ClientCertificateUsageSample
    {
        public partial class cert : System.Web.UI.Page
        {
            public string certHeader = "";
            public string errorString = "";
            private X509Certificate2 certificate = null;
            public string certThumbprint = "";
            public string certSubject = "";
            public string certIssuer = "";
            public string certSignatureAlg = "";
            public string certIssueDate = "";
            public string certExpiryDate = "";
            public bool isValidCert = false;

            //
            // Read the certificate from the header into an X509Certificate2 object
            // Display properties of the certificate on the page
            //
            protected void Page_Load(object sender, EventArgs e)
            {
                NameValueCollection headers = base.Request.Headers;
                certHeader = headers["X-ARR-ClientCert"];
                if (!String.IsNullOrEmpty(certHeader))
                {
                    try
                    {
                        byte[] clientCertBytes = Convert.FromBase64String(certHeader);
                        certificate = new X509Certificate2(clientCertBytes);
                        certSubject = certificate.Subject;
                        certIssuer = certificate.Issuer;
                        certThumbprint = certificate.Thumbprint;
                        certSignatureAlg = certificate.SignatureAlgorithm.FriendlyName;
                        certIssueDate = certificate.NotBefore.ToShortDateString() + " " + certificate.NotBefore.ToShortTimeString();
                        certExpiryDate = certificate.NotAfter.ToShortDateString() + " " + certificate.NotAfter.ToShortTimeString();
                    }
                    catch (Exception ex)
                    {
                        errorString = ex.ToString();
                    }
                    finally 
                    {
                        isValidCert = IsValidClientCertificate();
                        if (!isValidCert) Response.StatusCode = 403;
                        else Response.StatusCode = 200;
                    }
                }
                else
                {
                    certHeader = "";
                }
            }

            //
            // This is a SAMPLE verification routine. Depending on your application logic and security requirements, 
            // you should modify this method
            //
            private bool IsValidClientCertificate()
            {
                // In this example we will only accept the certificate as a valid certificate if all the conditions below are met:
                // 1. The certificate is not expired and is active for the current time on server.
                // 2. The subject name of the certificate has the common name nildevecc
                // 3. The issuer name of the certificate has the common name nildevecc and organization name Microsoft Corp
                // 4. The thumbprint of the certificate is 30757A2E831977D8BD9C8496E4C99AB26CB9622B
                //
                // This example does NOT test that this certificate is chained to a Trusted Root Authority (or revoked) on the server 
                // and it allows for self signed certificates
                //

                if (certificate == null || !String.IsNullOrEmpty(errorString)) return false;

                // 1. Check time validity of certificate
                if (DateTime.Compare(DateTime.Now, certificate.NotBefore) < 0 || DateTime.Compare(DateTime.Now, certificate.NotAfter) > 0) return false;

                // 2. Check subject name of certificate
                bool foundSubject = false;
                string[] certSubjectData = certificate.Subject.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
                foreach (string s in certSubjectData)
                {
                    if (String.Compare(s.Trim(), "CN=nildevecc") == 0)
                    {
                        foundSubject = true;
                        break;
                    }
                }
                if (!foundSubject) return false;

                // 3. Check issuer name of certificate
                bool foundIssuerCN = false, foundIssuerO = false;
                string[] certIssuerData = certificate.Issuer.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
                foreach (string s in certIssuerData)
                {
                    if (String.Compare(s.Trim(), "CN=nildevecc") == 0)
                    {
                        foundIssuerCN = true;
                        if (foundIssuerO) break;
                    }

                    if (String.Compare(s.Trim(), "O=Microsoft Corp") == 0)
                    {
                        foundIssuerO = true;
                        if (foundIssuerCN) break;
                    }
                }

                if (!foundIssuerCN || !foundIssuerO) return false;

                // 4. Check thumprint of certificate
                if (String.Compare(certificate.Thumbprint.Trim().ToUpper(), "30757A2E831977D8BD9C8496E4C99AB26CB9622B") != 0) return false;

                // If you also want to test if the certificate chains to a Trusted Root Authority you can uncomment the code below
                //
                //X509Chain certChain = new X509Chain();
                //certChain.Build(certificate);
                //bool isValidCertChain = true;
                //foreach (X509ChainElement chElement in certChain.ChainElements)
                //{
                //    if (!chElement.Certificate.Verify())
                //    {
                //        isValidCertChain = false;
                //        break;
                //    }
                //}
                //if (!isValidCertChain) return false;

                return true;
            }
        }
    }
