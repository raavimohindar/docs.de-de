---
title: 'Vorgehensweise: Entwickeln eines mit IIS ausgeführten WCF-Datendiensts'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, developing
- WCF Data Services, deploying
- WCF Data Services, hosting
ms.assetid: f6f768c5-4989-49e3-a36f-896ab4ded86e
ms.openlocfilehash: 8a1a0c2c55267940463e2c9ab82bb52345269260
ms.sourcegitcommit: 43cbde34970f5f38f30c43cd63b9c7e2e83717ae
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/11/2020
ms.locfileid: "81121616"
---
# <a name="how-to-develop-a-wcf-data-service-running-on-iis"></a>Gewusst wie: Entwickeln eines WCF-Datendienstes, der auf IIS ausgeführt wird

Dieser Artikel zeigt, wie Sie WCF Data Services verwenden, um einen Datendienst zu erstellen, der auf der Northwind-Beispieldatenbank basiert, die von einer ASP.NET Web-App gehostet wird, die auf InternetInformationsdiensten (Internet Information Services, IIS) ausgeführt wird. Ein Beispiel für das Erstellen desselben Northwind-Datendienstes wie eine ASP.NET Web-App, die auf dem ASP.NET Development Server ausgeführt wird, finden Sie im [WCF Data Services-Schnellstart](quickstart-wcf-data-services.md).

> [!NOTE]
> Um den Northwind-Datendienst zu erstellen, installieren Sie zunächst die Northwind-Beispieldatenbank auf dem lokalen Computer. Um die Datenbank zu installieren, führen Sie das Transact-SQL-Skript von [Northwind und pubs Beispieldatenbanken für Microsoft SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/northwind-pubs)aus.

In diesem Artikel wird gezeigt, wie Sie einen Datendienst mithilfe des Entity Framework-Anbieters erstellen. Weitere Datendiensteanbieter sind verfügbar. Weitere Informationen finden Sie unter [Data Services Providers](data-services-providers-wcf-data-services.md).

Nach dem Erstellen des Diensts, müssen Sie explizit den Zugriff auf Datendienstressourcen bereitstellen. Weitere Informationen finden Sie unter [Gewusst wie: Aktivieren des Zugriffs auf den Datendienst](how-to-enable-access-to-the-data-service-wcf-data-services.md).

## <a name="create-the-aspnet-web-application-that-runs-on-iis"></a>Erstellen der ASP.NET Webanwendung, die auf IIS ausgeführt wird

1. Wählen Sie in Visual Studio im Menü **Datei** die Optionen **Neu** > **Projekt** aus.

2. Wählen Sie im Dialogfeld **Neues Projekt** die > **Webkategorie** **Installierte** > [**Visual C"** oder **Visual Basic**] aus.

3. Wählen Sie die Vorlage **ASP.NET-Webanwendung** .

4. Geben `NorthwindService` Sie den Namen des Projekts ein.

5. Klicken Sie auf **OK**.

6. Wählen Sie im Menü **Projekt** **NorthwindService-Eigenschaften**aus.

7. Wählen Sie die **Registerkarte Web** aus, und wählen Sie dann **Lokale IIS-Webserver verwenden**aus.

8. Klicken Sie auf **Virtuelles Verzeichnis erstellen,** und klicken Sie dann auf **OK**.

9. Führen Sie an der Eingabeaufforderung mit Administratorrechten einen der folgenden Befehle aus (je nach Betriebssystem):

    - 32-Bit-Systeme:

        ```console
        "%windir%\Microsoft.NET\Framework\v3.0\Windows Communication Foundation\ServiceModelReg.exe" -i
        ```

    - 64-Bit-Systeme:

        ```console
        "%windir%\Microsoft.NET\Framework64\v3.0\Windows Communication Foundation\ServiceModelReg.exe" -i
        ```

     Hierdurch wird sichergestellt, dass Windows Communication Foundation (WCF) auf dem Computer registriert wird.

10. Führen Sie an der Eingabeaufforderung mit Administratorrechten einen der folgenden Befehle aus (je nach Betriebssystem):

    - 32-Bit-Systeme:

        ```console
        "%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet_regiis.exe" -i -enable
        ```

    - 64-Bit-Systeme:

        ```console
        "%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe" -i -enable
        ```

     Dadurch wird sichergestellt, dass ISS ordnungsgemäß ausgeführt wird, nachdem WCF auf dem Computer installiert wurde. Möglicherweise müssen Sie außerdem einen Neustart von IIS ausführen.

11. Wenn die ASP.NET-Anwendung in IIS7 ausgeführt wird, müssen Sie außerdem die folgenden Schritte ausführen:

    1. Öffnen Sie IIS Manager, und navigieren Sie zur PhotoService-Anwendung unter **Standardwebsite**.

    2. Doppelklicken Sie in **Ansicht "Features"** auf **Authentifizierung**.

    3. Wählen Sie auf der Seite **Authentifizierung****Anonyme Authentifizierung**.

    4. Klicken Sie im Bereich **Aktionen** auf **Bearbeiten,** um den Sicherheitsprinzipal festzulegen, unter dem anonyme Benutzer eine Verbindung mit der Website herstellen.

    5. Wählen Sie im Dialogfeld **Anonyme Authentifizierungsanmeldeinformationen** bearbeiten **die Anwendungspoolidentität**aus.

    > [!IMPORTANT]
    > Wenn Sie das Netzwerkdienstkonto verwenden, gewähren Sie anonymen Benutzern alle Zugriffsrechte dieses Kontos für das interne Netzwerk.

12. Führen Sie mit SQL Server Management Studio, dem SQLCMD-Hilfsprogramm oder dem Transact-SQL-Editor in Visual Studio den folgenden Transact-SQL-Befehl für die Instanz von SQL Server aus, der die Northwind-Datenbank angefügt ist:

    ```sql
    CREATE LOGIN [NT AUTHORITY\NETWORK SERVICE] FROM WINDOWS;
    GO
    ```

    Dadurch wird in der SQL Server-Instanz eine Anmeldung für das Windows-Konto erstellt, das verwendet wurde, um IIS auszuführen. Dies ermöglicht es IIS, eine Verbindung mit der SQL Server-Instanz herzustellen.

13. Führen Sie mit der angefügten Northwind-Datenbank, die folgenden Transact-SQL-Befehle aus:

    ```sql
    USE Northwind
    GO
    CREATE USER [NT AUTHORITY\NETWORK SERVICE]
    FOR LOGIN [NT AUTHORITY\NETWORK SERVICE] WITH DEFAULT_SCHEMA=[dbo];
    GO
    ALTER LOGIN [NT AUTHORITY\NETWORK SERVICE]
    WITH DEFAULT_DATABASE=[Northwind];
    GO
    EXEC sp_addrolemember 'db_datareader', 'NT AUTHORITY\NETWORK SERVICE'
    GO
    EXEC sp_addrolemember 'db_datawriter', 'NT AUTHORITY\NETWORK SERVICE'
    GO
    ```

    Hierdurch werden der neuen Anmeldung Rechte erteilt, die IIS den Lese- und Schreibzugriff für Daten der Northwind-Datenbank zu gewähren.

## <a name="define-the-data-model"></a>Definieren des Datenmodells

1. Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf den Namen des ASP.NET-Projekts, und klicken Sie dann auf**Neues Element** **hinzufügen** > .

2. Wählen Sie im Dialogfeld **Neues Element hinzufügen** ADO.NET **Entitätsdatenmodell**aus.

3. Geben Sie für den Namen `Northwind.edmx`des Datenmodells ein.

4. Wählen Sie im Entitätsdatenmodell-Assistenten die Option **Aus Datenbank generieren**aus, und klicken Sie dann auf **Weiter**.

5. Verbinden Sie das Datenmodell mit der Datenbank, indem Sie einen der folgenden Schritte ausführen, und klicken Sie dann auf **Weiter:**

    - Wenn Sie noch keine Datenbankverbindung konfiguriert haben, klicken Sie auf **Neue Verbindung,** und erstellen Sie eine neue Verbindung. Weitere Informationen finden Sie unter [How to: Create Connections to SQL Server Databases](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/s4yys16a(v=vs.90)). Dieser SQL Server-Instanz muss die Northwind-Beispieldatenbank angefügt sein.

         \- oder -

    - Wenn bereits eine Datenbankverbindung für die Northwind-Datenbank konfiguriert wurde, wählen Sie diese Verbindung in der Liste der Verbindungen aus.

6. Aktivieren Sie auf der letzten Seite des Assistenten die Kontrollkästchen für alle Tabellen in der Datenbank, und deaktivieren Sie die Kontrollkästchen für Sichten und gespeicherte Prozeduren.

7. Klicken Sie auf **Fertig stellen**, und beenden Sie den Assistenten.

## <a name="create-the-data-service"></a>Erstellen des Datendiensts

1. Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf den Namen Ihres ASP.NET-Projekts, und klicken Sie dann auf**Neues Element** **hinzufügen** > .

2. Wählen Sie im Dialogfeld **Neues Element hinzufügen** **wCF Data Service**aus.

   ![WCF-Datendienstelementvorlage in Visual Studio 2015](./media/wcf-data-service-item-template.png)

   > [!NOTE]
   > Die **WCF-Datendienstvorlage** ist in Visual Studio 2015 verfügbar, jedoch nicht in Visual Studio 2017 oder höher.

3. Geben Sie `Northwind`für den Namen des Dienstes .

     Visual Studio erstellt das XML-Markup und die Codedateien für den neuen Dienst. In der Standardeinstellung wird das Fenster des Code-Editors geöffnet. Im **Projektmappen-Explorer**hat der Dienst den Namen Northwind und die Erweiterung .svc.cs oder .svc.vb.

4. Ersetzen Sie im Code für den Datendienst in der Definition der Klasse, die den Datendienst definiert, den Kommentar `/* TODO: put your data source class name here */` durch den Typ des Entitätscontainers des Datenmodells, in diesem Fall `NorthwindEntities`. Die Klassendefinition sollte wie folgt aussehen:

     [!code-csharp[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_quickstart_service/cs/northwind.svc.cs#servicedefinition)]
     [!code-vb[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_service/vb/northwind.svc.vb#servicedefinition)]

## <a name="see-also"></a>Siehe auch

- [Verfügbarmachen Ihrer Daten als Dienst](exposing-your-data-as-a-service-wcf-data-services.md)
