---
title: 'Gewusst wie: Bestimmen der installierten .NET Framework-Versionen | Microsoft-Dokumentation'
ms.custom: 
ms.date: 04/07/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- versions, determining for .NET Framework
- .NET Framework, determining version
ms.assetid: 40a67826-e4df-4f59-a651-d9eb0fdc755d
caps.latest.revision: 62
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 3f2aca8f5f977d278fd326dfb20267d9bf1a8262
ms.contentlocale: de-de
ms.lasthandoff: 04/18/2017

---
# <a name="how-to-determine-which-net-framework-versions-are-installed"></a>Gewusst wie: Bestimmen der installierten .NET Framework-Versionen
Benutzer können mehrere Versionen von .NET Framework auf einem Computer installieren und ausführen. Wenn Sie eine App entwickeln oder bereitstellen, müssen Sie möglicherweise herausfinden, welche Versionen von .NET Framework auf dem Computer des Benutzers installiert sind. Beachten Sie, dass .NET Framework aus zwei Hauptkomponenten besteht, deren Versionen separat voneinander sind:  
  
-   Ein Satz von Assemblys, bei denen es sich um Sammlungen von Typen und Ressourcen handelt, die die Funktionalität Ihre Apps bereitstellen. .NET Framework und Assemblys verwenden die gleiche Versionsnummer.  
  
-   Die CLR (Common Language Runtime, CLR), die den Code Ihrer App verwaltet und ausführt. Die CLR wird durch ihre eigene Versionsnummer identifiziert (siehe [Versionen und Abhängigkeiten](~/docs/framework/migration-guide/versions-and-dependencies.md)).  
  
 Sie können die Registrierung öffnen oder in Ihrem Code abfragen, um eine exakte Liste der auf einem Computer installierten Versionen von .NET Framework zu erhalten:  
  
 [Anzeigen der Registrierung (Versionen 1-4)](#net_a)  
 [Anzeigen der Registrierung ( Version 4.5 und neuer)](#net_b)  
 [Codegesteuertes Anzeigen der Registrierung (Versionen 1-4)](#net_c)  
 [Codegesteuertes Anzeigen der Registrierung (Version 4.5 und neuer)](#net_d)  
  
 Sie können ein Tool oder Code verwenden, um die CLR-Version zu ermitteln:  
  
 [Verwenden des Clrver-Tools](#clr_a)  
 [Codegesteuertes Abfragen der System.Environment-Klasse](#clr_b)  
  
 Informationen zum Ermitteln der installierten Updates für jede Version von .NET Framework finden Sie unter [Gewusst wie: Bestimmen der installierten .NET Framework-Updates](~/docs/framework/migration-guide/how-to-determine-which-net-framework-updates-are-installed.md). Informationen zum Installieren von .NET Framework finden Sie im [Installationshandbuch](../../../docs/framework/install/guide-for-developers.md).  
  
<a name="net_a"></a>   
#### <a name="to-find-net-framework-versions-by-viewing-the-registry-net-framework-1-4"></a>Ermitteln der .NET Framework-Versionen durch Anzeigen der Registrierung (.NET Framework 1-4)  
  
1.  Klicken Sie im Menü **Start** auf **Ausführen**.  
  
2.  Im Feld **Öffnen** geben Sie **regedit.exe** ein.  
  
     Sie müssen über Administratorrechte verfügen, um regedit.exe ausführen zu können.  
  
3.  Öffnen Sie im Registrierungs-Editor den folgenden Unterschlüssel:  
  
     `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP`  
  
     Die installierten Versionen werden unter dem NDP-Unterschlüssel aufgeführt. Die Versionsnummer ist unter dem Eintrag **Version** gespeichert. In der [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)]-Version oder höher befindet sich der Eintrag **Version** unter dem Client- oder Full-Unterschlüssel (unter NDP) oder unter beiden Unterschlüsseln.  
  
    > [!NOTE]
    >  Der Ordner "NET Framework Setup" in der Registrierung beginnt nicht mit einem Punkt.  
  
<a name="net_b"></a>   
#### <a name="to-find-net-framework-versions-by-viewing-the-registry-net-framework-45-and-later"></a>Ermitteln der .NET Framework-Versionen durch Anzeigen der Registrierung (.NET Framework 4.5 und neuer)  
  
1.  Klicken Sie im Menü **Start** auf **Ausführen**.  
  
2.  Im Feld **Öffnen** geben Sie **regedit.exe** ein.  
  
     Sie müssen über Administratorrechte verfügen, um regedit.exe ausführen zu können.  
  
3.  Öffnen Sie im Registrierungs-Editor den folgenden Unterschlüssel:  
  
     `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full`  
  
     Beachten Sie, dass der Pfad zum `Full`-Unterschlüssel den Unterschlüssel `Net Framework` anstelle von `.NET Framework` enthält.  
  
    > [!NOTE]
    >  Wenn der `Full`-Unterschlüssel nicht vorhanden ist, ist .NET Framework 4.5 oder höher nicht installiert.  
  
     Suchen Sie nach einem DWORD-Wert mit dem Namen `Release`. Wenn das `Release`-DWORD vorhanden ist, können Sie von der Installation von [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] oder höher auf dem Computer ausgehen.  
  
     ![Registrierungseintrag für .NET Framework 4.5](../../../docs/framework/migration-guide/media/clr-installdir.png "CLR_InstallDir")  
  
     Der Wert von `Release` gibt an, welche Version von .NET Framework installiert ist.  
  
    |Wert des Versions-DWORD|Version|  
    |--------------------------------|-------------|  
    |378389|.NET Framework 4.5|  
    |378675|.NET Framework 4.5.1 installiert mit Windows 8.1 oder Windows Server 2012 R2|  
    |378758|.NET Framework 4.5.1 installiert unter Windows 8, Windows 7 SP1 oder Windows Vista SP2|  
    |379893|.NET Framework 4.5.2|  
    |Auf Systemen unter Windows 10: 393295<br /><br /> Auf allen anderen Betriebssystemversionen: 393297|[!INCLUDE[net_v46](../../../includes/net-v46-md.md)]|  
    |Auf Systemen mit Windows 10, November-Update: 394254<br /><br /> Auf allen anderen Betriebssystemversionen: 394271|[!INCLUDE[net_v461](../../../includes/net-v461-md.md)]|  
    |Auf Systemen unter Windows 10 Anniversary Update: 394802<br /><br /> Auf allen anderen Betriebssystemversionen: 394806|[!INCLUDE[net_v462](../../../includes/net-v462-md.md)]| 
    |Auf Systemen unter Windows 10 Creators Update: 460798 | .NET Framework 4.7 |  
  
<a name="net_c"></a>   
#### <a name="to-find-net-framework-versions-by-querying-the-registry-in-code-net-framework-1-4"></a>Ermitteln der .NET Framework-Versionen durch codegesteuertes Abfragen der Registrierung (.NET Framework 1-4)  
  
-   Verwenden Sie die <xref:Microsoft.Win32.RegistryKey?displayProperty=fullName>-Klasse, um auf den Unterschlüssel „Software\Microsoft\NET Framework Setup\NDP\“ unter „HKEY_LOCAL_MACHINE“ in der Windows-Registrierung zuzugreifen.  
  
     Der folgende Code veranschaulicht diese Abfrage beispielhaft.  
  
    > [!NOTE]
    >  In diesem Code wird nicht veranschaulicht, wie [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] oder später zu erkennen ist. Zum Erkennen dieser Versionen überprüfen Sie das `Release`-DWORD, wie im vorherigen Abschnitt beschrieben. Informationen zu Code, der [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] oder höhere Versionen nicht erkennt, finden Sie im nächsten Abschnitt dieses Artikels.  
  
     [!code-csharp[ListVersions#0](../../../samples/snippets/csharp/VS_Snippets_CLR/listversions/cs/program.cs#0)]
     [!code-vb[ListVersions#0](../../../samples/snippets/visualbasic/VS_Snippets_CLR/listversions/vb/program.vb#0)]  
    [!code-csharp[ListVersions#1](../../../samples/snippets/csharp/VS_Snippets_CLR/listversions/cs/program.cs#1)]
    [!code-vb[ListVersions#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/listversions/vb/program.vb#1)]  
  
     Das Beispiel führt zu einer Ausgabe, die der folgenden Ausgabe ähnelt:  
  
    ```  
  
    v2.0.50727  2.0.50727.4016  SP2  
    v3.0  3.0.30729.4037  SP2  
    v3.5  3.5.30729.01  SP1  
    v4  
      Client  4.0.30319  
      Full  4.0.30319  
  
    ```  
  
<a name="net_d"></a>   
#### <a name="to-find-net-framework-versions-by-querying-the-registry-in-code-net-framework-45-and-later"></a>Ermitteln der .NET Framework-Versionen durch codegesteuertes Abfragen der Registrierung (.NET Framework 4.5 und neuer)  
  
1.  Wenn das `Release`-DWORD vorhanden ist, können Sie davon ausgehen, dass .NET Framework 4.5 oder neuer auf dem Computer installiert ist. Der Wert des Schlüsselworts gibt die installierte Version an. Verwenden Sie zur Überprüfung dieses Schlüsselwort die Methoden <xref:Microsoft.Win32.RegistryKey.OpenBaseKey%2A> und <xref:Microsoft.Win32.RegistryKey.OpenSubKey%2A> der Klasse <xref:Microsoft.Win32.RegistryKey?displayProperty=fullName>, um auf den Unterschlüssel „Software\Microsoft\NET Framework Setup\NDP\v4\Full“ unter „HKEY_LOCAL_MACHINE“ in der Windows-Registrierung zugreifen.  
  
2.  Überprüfen Sie den Wert des `Release`-Schlüsselworts, um die installierte Version zu bestimmen. Um aufwärtskompatibel zu sein, können Sie einen Wert größer als oder gleich den Werten suchen, die in der Tabelle aufgelistet sind. Dies sind die .NET Framework-Versionen und die jeweiligen `Release`-Schlüsselwörter.  
  
    |Version|Wert des Versions-DWORD|  
    |-------------|--------------------------------|  
    |.NET Framework 4.5|378389|  
    |.NET Framework 4.5.1 installiert mit Windows 8.1|378675|  
    |.NET Framework 4.5.1 installiert unter Windows 8, Windows 7 SP1 oder Windows Vista SP2|378758|  
    |.NET Framework 4.5.2|379893|  
    |[!INCLUDE[net_v46](../../../includes/net-v46-md.md)] installiert mit Windows 10|393295|  
    |[!INCLUDE[net_v46](../../../includes/net-v46-md.md)] installiert auf allen anderen Windows-Betriebssystemversionen|393297|  
    |[!INCLUDE[net_v461](../../../includes/net-v461-md.md)] installiert unter Windows 10|394254|  
    |[!INCLUDE[net_v461](../../../includes/net-v461-md.md)] installiert auf allen anderen Windows-Betriebssystemversionen|394271|  
    |[!INCLUDE[net_v462](../../../includes/net-v462-md.md)] installiert unter Windows 10 Anniversary Update|394802|  
    |[!INCLUDE[net_v462](../../../includes/net-v462-md.md)] installiert auf allen anderen Windows-Betriebssystemversionen|394806|
    |.NET Framework 4.7 installiert unter Windows 10 Creators Update|460798|  
  
     Das folgende Beispiel überprüft den `Release`-Wert in der Registrierung, um zu ermitteln, ob [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] oder eine höhere Version von .NET Framework installiert ist.  
  
     [!code-csharp[ListVersions#5](../../../samples/snippets/csharp/VS_Snippets_CLR/listversions/cs/Versions45Plus.cs#5)]
     [!code-vb[ListVersions#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/listversions/vb/Versions45Plus.vb#5)]  
  
     In diesem Beispiel wird der empfohlenen Vorgehensweise zur Versionsprüfung gefolgt:  
  
    -   Es überprüft, ob der Wert des `Release`-Eintrags *größer als oder gleich* dem Wert der bekannten Versionsschlüssel ist.  
  
    -   Es wird beginnend mit der neuesten Version bis hin zur ältesten Version geprüft.  
  
<a name="clr_a"></a>   
#### <a name="to-find-the-current-runtime-version-by-using-the-clrver-tool"></a>Ermitteln der aktuellen Laufzeitversion mithilfe des Clrver-Tools  
  
-   Verwenden Sie das CLR-Versions-Tool (Clrver.exe), um zu bestimmen, welche Versionen der Common Language Runtime auf einem Computer installiert sind.  
  
     Geben Sie an der Visual Studio-Eingabeaufforderung `clrver` ein. Dieser Befehl erzeugt eine Ausgabe ähnlich der folgenden:  
  
    ```  
    Versions installed on the machine:  
    v2.0.50727  
    v4.0.30319  
    ```  
  
     Weitere Informationen über die Verwendung dieses Tools finden Sie unter [Clrver.exe (CLR-Versionstool)](~/docs/framework/tools/clrver-exe-clr-version-tool.md).  
  
<a name="clr_b"></a>   
#### <a name="to-find-the-current-runtime-version-by-querying-the-environment-class-in-code"></a>Ermitteln der aktuellen Laufzeitversion durch programmgesteuerte Abfragen der "Environment"-Klasse  
  
-   Fragen Sie die Eigenschaft <xref:System.Environment.Version%2A?displayProperty=fullName> ab, um ein <xref:System.Version>-Objekt abzurufen, das die Version der Runtime ermittelt, die aktuell für die Ausführung des Codes zuständig ist. Sie können die Eigenschaft <xref:System.Version.Major%2A?displayProperty=fullName> verwenden, um den Bezeichner für die Hauptversion abzurufen (Beispiel: „4“ für Version 4.0). Mithilfe der Eigenschaft <xref:System.Version.Minor%2A?displayProperty=fullName> können Sie den Bezeichner der Nebenversion abrufen (Beispiel: „0“ für Version 4.0). Die Methode <xref:System.Object.ToString%2A?displayProperty=fullName> gibt die gesamte Zeichenfolge der Version zurück (Beispiel: „4.0.30319.18010“, wie im folgenden Code veranschaulicht). Diese Eigenschaft gibt einen einzelnen Wert zurück, der die Version der Laufzeit angibt, die gerade den Code ausführt; sie gibt keine Assemblyversionen oder andere Versionen der Laufzeit zurück, die möglicherweise auf dem Computer installiert sind.  
  
     Für die .NET Framework-Versionen 4, 4.5, 4.5.1 und 4.5.2 gibt die Eigenschaft <xref:System.Environment.Version%2A?displayProperty=fullName> ein <xref:System.Version>-Objekt zurück, dessen Zeichenfolgendarstellung die Form `4.0.30319.xxxxx` aufweist. Für .NET Framework 4.6 und höher weist sie die Form `4.0.30319.42000` auf.  
  
    > [!IMPORTANT]
    >  Für [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] und höher wird nicht empfohlen, die Version der Runtime mithilfe der Eigenschaft <xref:System.Environment.Version%2A?displayProperty=fullName> zu ermitteln. Stattdessen empfehlen wir, dass Sie die Registrierung abfragen, wie im Abschnitt [Ermitteln der .NET Framework-Versionen durch codegesteuertes Abfragen der Registrierung (.NET Framework 4.5 und neuer)](#net_d) weiter oben in diesem Artikel beschrieben.  
  
     Hier folgt ein Beispiel zum Abfragen der Eigenschaft <xref:System.Environment.Version%2A?displayProperty=fullName> hinsichtlich der Informationen zur Runtimeversion:  
  
     [!code-csharp[ListVersions#0](../../../samples/snippets/csharp/VS_Snippets_CLR/listversions/cs/program.cs#0)]
     [!code-vb[ListVersions#0](../../../samples/snippets/visualbasic/VS_Snippets_CLR/listversions/vb/program.vb#0)]  
    [!code-csharp[ListVersions#2](../../../samples/snippets/csharp/VS_Snippets_CLR/listversions/cs/program.cs#2)]
    [!code-vb[ListVersions#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/listversions/vb/program.vb#2)]  
  
     Das Beispiel führt zu einer Ausgabe, die der folgenden Ausgabe ähnelt:  
  
    ```  
    Version: 4.0.30319.18010  
    ```  
  
## <a name="see-also"></a>Siehe auch  
 [Gewusst wie: Bestimmen der installierten .NET Framework-Updates](~/docs/framework/migration-guide/how-to-determine-which-net-framework-updates-are-installed.md)   
 [Installationshandbuch](../../../docs/framework/install/guide-for-developers.md)   
 [Versionen und Abhängigkeiten](~/docs/framework/migration-guide/versions-and-dependencies.md)
