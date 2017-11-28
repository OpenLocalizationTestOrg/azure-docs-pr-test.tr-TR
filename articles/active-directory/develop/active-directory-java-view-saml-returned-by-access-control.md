---
title: "aaaView SAML döndürülen hello erişim denetimi hizmeti (Java) tarafından"
description: "Nasıl tooview SAML Java uygulamalarını hello erişim denetimi hizmeti tarafından döndürülen Azure üzerinde barındırılan öğrenin."
services: active-directory
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6cd216f9-eb43-46b4-b30d-f194d0ae2d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.custom: aaddev
ms.openlocfilehash: b6733bc98b505cfa89a4ce456f368ee15da11427
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-saml-returned-by-hello-azure-access-control-service"></a><span data-ttu-id="e2e04-103">Nasıl tooview SAML hello Azure erişim denetimi hizmeti tarafından döndürülen</span><span class="sxs-lookup"><span data-stu-id="e2e04-103">How tooview SAML returned by hello Azure Access Control Service</span></span>
<span data-ttu-id="e2e04-104">Bu kılavuz size nasıl güvenlik onaylama işlemi biçimlendirme dili (SAML) temel tooview hello tooyour hello Azure erişim denetimi Hizmeti'nden (ACS) tarafından döndürülen gösterir.</span><span class="sxs-lookup"><span data-stu-id="e2e04-104">This guide will show you how tooview hello underlying Security Assertion Markup Language (SAML) returned tooyour application by hello Azure Access Control Service (ACS).</span></span> <span data-ttu-id="e2e04-105">Merhaba Kılavuzu derlemeler üzerinde hello [nasıl tooAuthenticate Azure erişim denetimi hizmeti kullanılarak Eclipse Web kullanıcılarla](active-directory-java-authenticate-users-access-control-eclipse.md) hello SAML bilgilerini görüntüler kod sağlayarak konu.</span><span class="sxs-lookup"><span data-stu-id="e2e04-105">hello guide builds on hello [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) topic, by providing code that displays hello SAML information.</span></span> <span data-ttu-id="e2e04-106">Tamamlanan Merhaba uygulaması benzer toohello aşağıdaki arar.</span><span class="sxs-lookup"><span data-stu-id="e2e04-106">hello completed application will look similar toohello following.</span></span>

![Örnek SAML çıktı][saml_output]

<span data-ttu-id="e2e04-108">Merhaba ACS hakkında daha fazla bilgi için bkz: [sonraki adımlar](#next_steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="e2e04-108">For more information on ACS, see hello [Next steps](#next_steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="e2e04-109">Hello Azure Erişim Hizmetleri Denetim filtresi topluluk teknoloji önizlemesidir.</span><span class="sxs-lookup"><span data-stu-id="e2e04-109">hello Azure Access Services Control Filter is a community technology preview.</span></span> <span data-ttu-id="e2e04-110">Yayın öncesi yazılım olarak bunu resmi olarak Microsoft tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="e2e04-110">As pre-release software, it is not formally supported by Microsoft.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="e2e04-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e2e04-111">Prerequisites</span></span>
<span data-ttu-id="e2e04-112">toocomplete hello görevler bu kılavuzda, tam örnek: Merhaba [nasıl tooAuthenticate Azure erişim denetimi hizmeti kullanılarak Eclipse Web kullanıcılarla](active-directory-java-authenticate-users-access-control-eclipse.md) ve hello Bu öğretici için başlangıç noktası olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="e2e04-112">toocomplete hello tasks in this guide, complete hello sample at [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) and use it as hello starting point for this tutorial.</span></span>

## <a name="add-hello-jspwriter-library-tooyour-build-path-and-deployment-assembly"></a><span data-ttu-id="e2e04-113">Yol ve dağıtım Hello JspWriter kitaplığı tooyour yapı derleme ekleyin</span><span class="sxs-lookup"><span data-stu-id="e2e04-113">Add hello JspWriter library tooyour build path and deployment assembly</span></span>
<span data-ttu-id="e2e04-114">Merhaba içeren hello Kitaplığı eklemek **javax.servlet.jsp.JspWriter** sınıfı tooyour derleme yolu ve dağıtım derleme.</span><span class="sxs-lookup"><span data-stu-id="e2e04-114">Add hello library that contains hello **javax.servlet.jsp.JspWriter** class tooyour build path and deployment assembly.</span></span> <span data-ttu-id="e2e04-115">Tomcat kullanıyorsanız, hello kitaplığıdır **jsp api.jar**, hello Apache bulunan **lib** klasör.</span><span class="sxs-lookup"><span data-stu-id="e2e04-115">If you are using Tomcat, hello library is **jsp-api.jar**, which is located in hello Apache **lib** folder.</span></span>

1. <span data-ttu-id="e2e04-116">Eclipse'nın Proje Gezgini'nde sağ **MyACSHelloWorld**,'ı tıklatın **yapı yolu**,'ı tıklatın **oluşturma yolunu Yapılandır**, hello tıklatın **kitaplıkları** sekmesini ve ardından **dış Jar'lar Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e2e04-116">In Eclipse's Project Explorer, right-click **MyACSHelloWorld**, click **Build Path**, click **Configure Build Path**, click hello **Libraries** tab, and then click **Add External JARs**.</span></span>
2. <span data-ttu-id="e2e04-117">Merhaba, **JAR seçimi** iletişim kutusunda, toohello gidin gerekli JAR seçin ve ardından **açık**.</span><span class="sxs-lookup"><span data-stu-id="e2e04-117">In hello **JAR Selection** dialog, navigate toohello necessary JAR, select it, and then click **Open**.</span></span>
3. <span data-ttu-id="e2e04-118">Merhaba ile **MyACSHelloWorld özelliklerini** iletişim hala açık tıklatın **dağıtım derleme**.</span><span class="sxs-lookup"><span data-stu-id="e2e04-118">With hello **Properties for MyACSHelloWorld** dialog still open, click **Deployment Assembly**.</span></span>
4. <span data-ttu-id="e2e04-119">Merhaba, **Web dağıtımı derleme** iletişim kutusunda, tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e2e04-119">In hello **Web Deployment Assembly** dialog, click **Add**.</span></span>
5. <span data-ttu-id="e2e04-120">Merhaba, **yeni derleme yönergesi** iletişim kutusunda, tıklatın **Java derleme yolu girişleri** ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="e2e04-120">In hello **New Assembly Directive** dialog, click **Java Build Path Entries** and then click **Next**.</span></span>
6. <span data-ttu-id="e2e04-121">Merhaba uygun kitaplığı seçin ve tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="e2e04-121">Select hello appropriate library and click **Finish**.</span></span>
7. <span data-ttu-id="e2e04-122">Tıklatın **Tamam** tooclose hello **MyACSHelloWorld özelliklerini** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e2e04-122">Click **OK** tooclose hello **Properties for MyACSHelloWorld** dialog.</span></span>

## <a name="modify-hello-jsp-file-toodisplay-saml"></a><span data-ttu-id="e2e04-123">Merhaba JSP dosyası toodisplay SAML değiştirme</span><span class="sxs-lookup"><span data-stu-id="e2e04-123">Modify hello JSP file toodisplay SAML</span></span>
<span data-ttu-id="e2e04-124">Değiştirme **index.jsp** toouse hello koddan.</span><span class="sxs-lookup"><span data-stu-id="e2e04-124">Modify **index.jsp** toouse hello following code.</span></span>

    <%@ page language="java" contentType="text/html; charset=UTF-8"
        pageEncoding="UTF-8"%>
        <%@ page import="javax.xml.parsers.*"
                 import="javax.xml.transform.*"
                 import="org.w3c.dom.*"
                 import="java.io.*"
                 import="javax.xml.transform.stream.*"
                 import="javax.xml.transform.dom.*"
                 import="javax.xml.xpath.*"
                 import="javax.servlet.jsp.JspWriter" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Sample ACS Filter</title>
    </head>
    <body>
        <h3>SAML information from sample ACS program</h3>
        <%!
        void displaySAMLInfo(Node node, String parent, JspWriter out)
        {

            try
            {
                String nodeName;
                int nChild, i;

                nodeName = node.getNodeName();
                out.println("<br>");
                out.println("<u>Examining <b>" + parent + nodeName + "</b></u><br>");

                   // Attributes.
                   NamedNodeMap attribsMap = node.getAttributes();
                   if (null != attribsMap)
                   {
                         for (i=0; i < attribsMap.getLength(); i++)
                         {
                                Node attrib = attribsMap.item(i);
                                out.println("Attribute: <b>" + attrib.getNodeName() + "</b>: " + attrib.getNodeValue()  + "<br>");
                         }
                   }

                   // Child nodes.
                   NodeList list = node.getChildNodes();
                   if (null != list)
                    {
                          nChild = list.getLength();
                          if (nChild > 0)
                          {                    

                                 // If it is a text node, just print hello text.
                                 if (list.item(0).getNodeName() == "#text")
                                 {
                                     out.println("Text value: <b>" + list.item(0).getTextContent() + "</b><br>");
                                 }
                                 else
                                 {
                                     // Print out hello child node names.
                                     out.print("Contains " + nChild + " child node(s): ");   
                                        for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);

                                        out.print("<b>" + temp.getNodeName() + "</b>");
                                        if (i < nChild - 1)
                                        {
                                            // Separate hello names.
                                            out.print(", ");
                                        }
                                        else
                                        {
                                            // Finish hello sentence.
                                            out.print(".");
                                        }

                                     }
                                     out.println("<br>");

                                     // Process hello child nodes.
                                     for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);
                                        displaySAMLInfo(temp, parent + nodeName + "\\", out);
                                     }
                               }
                          }
                      }
                  }
                catch (Exception e)
                {
                    System.out.println("Exception encountered.");
                    e.printStackTrace();            
                }
            }
        %>

        <%
        try
        {
            String data  = (String) request.getAttribute("ACSSAML");

            DocumentBuilder docBuilder;
            Document doc = null;
            DocumentBuilderFactory docBuilderFactory = DocumentBuilderFactory.newInstance();
            docBuilderFactory.setIgnoringElementContentWhitespace(true);
            docBuilder = docBuilderFactory.newDocumentBuilder();
            byte[] xmlDATA = data.getBytes();

            ByteArrayInputStream in = new ByteArrayInputStream(xmlDATA);
            doc = docBuilder.parse(in);
            doc.getDocumentElement().normalize();

            // Iterate hello child nodes of hello doc.
            NodeList list = doc.getChildNodes();

            for (int i=0; i < list.getLength(); i++)
            {
                displaySAMLInfo(list.item(i), "", out);
            }
        }
        catch (Exception e)
        {
            out.println("Exception encountered.");
            e.printStackTrace();
        }

        %>
    </body>
    </html>

## <a name="run-hello-application"></a><span data-ttu-id="e2e04-125">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="e2e04-125">Run hello application</span></span>
1. <span data-ttu-id="e2e04-126">Uygulamanızı hello bilgisayar öykünücüsünde çalıştırın veya adresinde belgelenen hello adımları kullanarak tooAzure dağıtmak [nasıl tooAuthenticate Azure erişim denetimi hizmeti kullanılarak Eclipse Web kullanıcılarla](active-directory-java-authenticate-users-access-control-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="e2e04-126">Run your application in hello computer emulator or deploy tooAzure, using hello steps documented at [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span></span>
2. <span data-ttu-id="e2e04-127">Bir tarayıcıyı başlatın ve web uygulamasını açın.</span><span class="sxs-lookup"><span data-stu-id="e2e04-127">Launch a browser and open your web application.</span></span> <span data-ttu-id="e2e04-128">Tooyour uygulama açtıktan sonra hello güvenlik onaylama işlemi hello kimlik sağlayıcısı tarafından sağlanan SAML bilgilerini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="e2e04-128">After you log on tooyour application, you'll see SAML information, including hello security assertion provided by hello identity provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2e04-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e2e04-129">Next steps</span></span>
<span data-ttu-id="e2e04-130">toofurther ACS'ın işlevselliği ve daha karmaşık senaryolar ile tooexperiment keşfetmek için bkz: [erişim denetimi hizmeti 2.0][Access Control Service 2.0].</span><span class="sxs-lookup"><span data-stu-id="e2e04-130">toofurther explore ACS's functionality and tooexperiment with more sophisticated scenarios, see [Access Control Service 2.0][Access Control Service 2.0].</span></span>

[Prerequisites]: #pre
[Modify hello JSP file toodisplay SAML]: #modify_jsp
[Add hello JspWriter library tooyour build path and deployment assembly]: #add_library
[Run hello application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
