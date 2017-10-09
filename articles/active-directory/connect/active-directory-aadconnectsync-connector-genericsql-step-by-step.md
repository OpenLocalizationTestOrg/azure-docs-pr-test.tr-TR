---
title: "aaaGeneric SQL bağlayıcı adım adım | Microsoft Docs"
description: "Bu makalede, taramasını basit bir ik sistemi genel SQL bağlayıcı hello adım adım kullanma."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 28c1cc60-24fd-4d0d-a36d-b4aba6de86e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b1b5f89ab588de6f92f173a7bc00f97180067669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-step-by-step"></a>Adım adım Genel SQL Bağlayıcısı
Bu konu hakkında adım adım bir kılavuzdur. Bir Basit örnek HR veritabanı oluşturur ve bazı kullanıcı ve grup üyeliklerini içeri aktarmak için kullanın.

## <a name="prepare-hello-sample-database"></a>Merhaba örnek veritabanını hazırlama
SQL Server çalıştıran bir sunucuda bulunan hello SQL betiği çalıştırma [ek A](#appendix-a). Bu komut dosyası GSQLDEMO hello adla örnek bir veritabanı oluşturur. Merhaba hello için nesne modeli bu resimdeki veritabanı görülüyor oluşturuldu:  
![Nesne modeli](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)

Ayrıca toouse tooconnect toohello veritabanı istediğiniz bir kullanıcı oluşturun. Bu kılavuzda, hello kullanıcı FABRIKAM\SQLUser çağrılır ve hello etki alanında bulunan.

## <a name="create-hello-odbc-connection-file"></a>Merhaba ODBC bağlantı dosyası oluşturma
Merhaba Genel SQL bağlayıcı ODBC tooconnect toohello uzak sunucu kullanıyor. İlk toocreate hello ODBC bağlantı bilgilerini dosyasıyla gerekir.

1. Merhaba ODBC Yönetimi yardımcı programı, sunucunuzda başlatın:  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. Select hello sekmesini **dosya DSN**. Tıklatın **Ekle...** .  
   ![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)
3. Merhaba out-of-box sürücü works ince, bu nedenle seçin ve **sonraki >**.  
   ![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)
4. Merhaba dosyası gibi bir ad verin **GenericSQL**.  
   ![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)
5. **Son**'a tıklayın.  
   ![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)
6. Zamanı tooconfigure hello bağlantı. Merhaba veri kaynağı iyi bir açıklama girin ve SQL Server çalıştıran hello sunucu hello adını sağlayın.  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. Select nasıl tooauthenticate SQL ile. Bu durumda, Windows kimlik doğrulaması kullanın.  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. Merhaba hello örnek veritabanı adını sağlayın **GSQLDEMO**.  
   ![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)
9. Bu ekranda her şeyi varsayılan devam eder. **Son**'a tıklayın.  
   ![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)
10. her şeyi çalıştığını beklendiği gibi tooverify tıklatın **Test veri kaynağı**.  
    ![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)
11. Merhaba test başarılı olduğundan emin olun.  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. Merhaba ODBC yapılandırma dosyası artık dosya DSN görünür olması gerekir.  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

Şimdi gerekir ve hello bağlayıcı oluşturmaya başlamadan hello dosya sahibiz.

## <a name="create-hello-generic-sql-connector"></a>Merhaba Genel SQL bağlayıcısı oluşturun
1. Hello Eşitleme Hizmeti Yöneticisi kullanıcı Arabirimi, seçin **Bağlayıcılar** ve **oluşturma**. Seçin **Genel SQL (Microsoft)** ve açıklayıcı bir ad verin.  
   ![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)
2. Merhaba önceki bölümde oluşturduğunuz hello DSN dosyası bulunamıyor ve toohello server yükleyin. Merhaba kimlik bilgileri tooconnect toohello veritabanı sağlar.  
   ![Connector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. Bu kılavuzda, biz bize kolaylaşır ve iki nesne türlerini olduğunu söylemek **kullanıcı** ve **grup**.
   ![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)
4. toofind hello öznitelikleri hello tablosuna kendisini bakarak özniteliklerle bağlayıcı toodetect hello istiyoruz. Bu yana **kullanıcılar** ayrılmış bir sözcük içinde köşeli ayraçlar [] tooprovide ihtiyacımız SQL'de.  
   ![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)
5. Zaman toodefine hello bağlantı özniteliği ve hello DN özniteliği. İçin **kullanıcılar**, hello birleşimi hello iki öznitelikleri kullanıcı adı ve EmployeeID kullanırız. İçin **grup**, GroupName kullanıyoruz (değil gerçekçi gerçekçi, ancak bu kılavuz çalışır).
   ![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)
6. Tüm öznitelik türlerini, bir SQL veritabanında algılanabilir. Merhaba başvuru öznitelik türü özellikle yapılamıyor. Merhaba grup nesne türü için toochange hello OwnerId ve Memberıd tooreference gerekir.  
   ![Connector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. başvuru özniteliği hello önceki adımda hello nesne türü bir başvuru bu değerleri gerektiği hello öznitelikleri seçtik. Örneğimizde, kullanıcı nesnesi türü hello.  
   ![Connector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. Merhaba genel parametreleri sayfasında seçin **Filigran** hello delta stratejisi olarak. Ayrıca hello tarih/saat biçiminde yazın **yyyy-aa-gg ss: dd:**.
   ![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)
9. Merhaba üzerinde **yapılandırma bölümleri ve hiyerarşileri** sayfasında, her iki nesne türlerini seçin.
   ![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)
10. Merhaba üzerinde **nesne türlerini Seç** ve **öznitelikleri Seç**, nesne türleri ve tüm öznitelikleri seçin. Merhaba üzerinde **yapılandırma bağlayıcılarını** sayfasında, **son**.

## <a name="create-run-profiles"></a>Çalıştırma profillerini oluşturma
1. Hello Eşitleme Hizmeti Yöneticisi kullanıcı Arabirimi, seçin **Bağlayıcılar**, ve **çalıştırma profillerini Yapılandır**. Tıklatın **yeni bir profil**. Biz başlayın **tam içeri aktarma**.  
   ![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)
2. Merhaba türünü seçin **tam içeri aktarma (yalnızca aşama)**.  
   ![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)
3. Merhaba bölümü seçin **nesne = kullanıcı**.  
   ![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)
4. Seçin **tablo** ve türü **[kullanıcılar]**. Toohello birden çok değerli nesne türü bölümüne kaydırın ve resim aşağıdaki hello olduğu gibi hello veri girin. Seçin **son** toosave hello adım.  
   ![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)  
   ![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)  
5. Seçin **yeni adım**. Bu süre, select **nesne grubu =**. Merhaba son sayfasında, resim aşağıdaki hello olduğu gibi hello yapılandırmasını kullanın. **Son**'a tıklayın.  
   ![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)  
   ![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)  
6. İsteğe bağlı: istiyorsanız, ek çalıştırma profillerini yapılandırabilirsiniz. Bu kılavuzda, yalnızca tam içeri aktarma hello kullanılır.
7. Tıklatın **Tamam** değiştirme toofinish farklı çalıştır profili.

## <a name="add-some-test-data-and-test-hello-import"></a>Bazı test verilerini ve test hello alma ekleme
Örnek veritabanınızdaki bazı test verilerini doldurun. Hazır olduğunuzda seçin **çalıştırmak** ve **tam alma**.

İşte, iki telefon numarası olan bir kullanıcı ve Grup bazı üyeleri ile.  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![CS2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a>Ek A
**SQL komut dosyası toocreate hello örnek veritabanı**

```SQL
---Creating hello Database---------
Create Database GSQLDEMO
Go
-------Using hello Database-----------
Use [GSQLDEMO]
Go
-------------------------------------
USE [GSQLDEMO]
GO
/****** Object:  Table [dbo].[GroupMembers]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GroupMembers](
    [MemberID] [int] NOT NULL,
    [Group_ID] [int] NOT NULL
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[GROUPS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GROUPS](
    [GroupID] [int] NOT NULL,
    [GROUPNAME] [nvarchar](200) NOT NULL,
    [DESCRIPTION] [nvarchar](200) NULL,
    [WATERMARK] [datetime] NULL,
    [OwnerID] [int] NULL,
PRIMARY KEY CLUSTERED
(
    [GroupID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[USERPHONE]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[USERPHONE](
    [USER_ID] [int] NULL,
    [Phone] [varchar](20) NULL
) ON [PRIMARY]

GO
SET ANSI_PADDING OFF
GO
/****** Object:  Table [dbo].[USERS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[USERS](
    [USERID] [int] NOT NULL,
    [USERNAME] [nvarchar](200) NOT NULL,
    [FirstName] [nvarchar](100) NULL,
    [LastName] [nvarchar](100) NULL,
    [DisplayName] [nvarchar](100) NULL,
    [ACCOUNTDISABLED] [bit] NULL,
    [EMPLOYEEID] [int] NOT NULL,
    [WATERMARK] [datetime] NULL,
PRIMARY KEY CLUSTERED
(
    [USERID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_GROUPS] FOREIGN KEY([Group_ID])
REFERENCES [dbo].[GROUPS] ([GroupID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_GROUPS]
GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_USERS] FOREIGN KEY([MemberID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_USERS]
GO
ALTER TABLE [dbo].[GROUPS]  WITH CHECK ADD  CONSTRAINT [FK_GROUPS_USERS] FOREIGN KEY([OwnerID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GROUPS] CHECK CONSTRAINT [FK_GROUPS_USERS]
GO
ALTER TABLE [dbo].[USERPHONE]  WITH CHECK ADD  CONSTRAINT [FK_USERPHONE_USER] FOREIGN KEY([USER_ID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[USERPHONE] CHECK CONSTRAINT [FK_USERPHONE_USER]
GO
```
