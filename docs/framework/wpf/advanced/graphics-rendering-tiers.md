---
title: Renderingebenen für Grafiken
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [WPF], performance
- rendering graphics [WPF]
- rendering tiers [WPF]
- graphics rendering tiers [WPF]
- graphics [WPF], rendering tiers
ms.assetid: 08dd1606-02a2-4122-9351-c0afd2ec3a70
ms.openlocfilehash: 05847271cf82739a6a0b609771043c02a7ffc0e9
ms.sourcegitcommit: e48a54ebe62e874500a7043f6ee0b77a744d55b4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80291591"
---
# <a name="graphics-rendering-tiers"></a>Renderingebenen für Grafiken
Eine Renderingebene definiert eine Ebene der Grafikleistung eines Geräts, auf dem eine [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-Anwendung ausgeführt wird.  

<a name="graphics_hardware"></a>
## <a name="graphics-hardware"></a>Grafikhardware  
 Die Funktionen der Grafikhardware, die sich am stärksten auf die Renderingebenen auswirken, sind:  
  
- **Video-RAM**: Die Videospeichermenge der Grafikhardware bestimmt die Größe und Anzahl der Puffer, die für die Zusammensetzung von Grafiken verwendet werden kann.  
  
- **Pixel-Shader**: Ein Pixel-Shader ist eine Grafikprozessorfunktion, die Auswirkungen auf eine Pro-Pixel-Basis berechnet. Abhängig von der Auflösung der angezeigten Grafiken kann es mehrere Millionen Pixel geben, die für jeden Frame des Displays verarbeitet werden müssen.  
  
- **Vertex-Shader**: Ein Vertex-Shader ist eine Grafikprozessorfunktion, die mathematische Operationen für die Vertexdaten des Objekts ausführt.  
  
- **Multitexturunterstützung**: Bei Multitexturunterstützung handelt es sich um die Möglichkeit, zwei oder mehr unterschiedliche Texturen während eines Mischvorgangs für ein 3D-Grafikobjekt anzuwenden. Der Grad der Multitexturunterstützung wird durch die Anzahl der Multitextureinheiten in der Grafikhardware bestimmt.  
  
<a name="rendering_tier_definitions"></a>
## <a name="rendering-tier-definitions"></a>Definitionen von Renderingebenen  
 Die Funktionen der Grafikhardware bestimmen die Renderingfunktion einer [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-Anwendung. Das [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-System definiert drei Renderingebenen:  
  
- **Renderingebene 0**: Keine Beschleunigung der Grafikhardware. Alle Grafikfunktionen verwenden Softwarebeschleunigung. Die DirectX-Versionsstufe ist kleiner als Version 9.0.  
  
- **Renderingebene 1**: Einige Grafikfunktionen verwenden die Beschleunigung der Grafikhardware. Die DirectX-Versionsstufe ist größer oder gleich Version 9.0.  
  
- **Renderingebene 2**: Die meisten Grafikfunktionen verwenden die Beschleunigung der Grafikhardware. Die DirectX-Versionsstufe ist größer oder gleich Version 9.0.  
  
 Mit <xref:System.Windows.Media.RenderCapability.Tier%2A?displayProperty=nameWithType> der Eigenschaft können Sie die Renderingebene zur Anwendungslaufzeit abrufen. Sie verwenden die Renderingebene für die Bestimmung, ob das Gerät bestimmte hardwarebeschleunigte Grafikfunktionen unterstützt. Ihre Anwendung kann dann unterschiedliche Codepfade zur Laufzeit verwenden, je nach der vom Gerät unterstützten Renderingebene.  
  
### <a name="rendering-tier-0"></a>Renderingebene 0  
 Der Wert 0 der Renderingebene bedeutet, dass keine Beschleunigung der Grafikhardware vorhanden ist, die für die Anwendung auf dem Gerät verfügbar ist. Auf dieser Ebene sollten Sie davon ausgehen, dass alle Grafiken von Software ohne Hardwarebeschleunigung gerendert werden. Die Funktionalität dieser Ebene entspricht einer DirectX-Version, die kleiner als 9.0 ist.  
  
### <a name="rendering-tier-1-and-rendering-tier-2"></a>Renderingebene 1 und Renderingebene 2
  
> [!NOTE]
> Ab .NET Framework 4 wurde das Rendern von Ebene 1 neu definiert, um nur Grafikhardware einzuschließen, die DirectX 9.0 oder höher unterstützt. Grafikhardware, die DirectX 7 oder 8 unterstützt, ist jetzt als Rendering-Stufe 0 definiert.  
  
 Renderingebene 1 oder 2 bedeutet, dass die meisten der Grafikfunktionen von [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] Hardwarebeschleunigung verwenden, wenn die erforderlichen Systemressourcen verfügbar sind und nicht ausgeschöpft wurden. Dies entspricht einer DirectX-Version, die größer oder gleich 9.0 ist.  
  
 Die folgende Tabelle zeigt die Unterschiede in den Anforderungen der Grafikhardware für die Renderingebene 1 und 2:  
  
|Funktion|Ebene 1|Ebene 2|  
|-------------|------------|------------|  
|DirectX-Version|Muss größer als oder gleich 9.0 sein.|Muss größer als oder gleich 9.0 sein.|  
|Video-RAM|Muss größer oder gleich 60 MB sein.|Muss größer oder gleich 120 MB sein.|  
|Pixel-Shader|Die Versionsebene muss größer als oder gleich 2.0 sein.|Die Versionsebene muss größer als oder gleich 2.0 sein.|  
|Vertex-Shader|Keine Anforderung.|Die Versionsebene muss größer als oder gleich 2.0 sein.|  
|Multitextur-Einheiten|Keine Anforderung.|Die Anzahl der Einheiten muss größer als oder gleich 4 sein.|  
  
 Die folgenden Features und Funktionen sind für die Renderingebene 1 und 2 hardwarebeschleunigt:  
  
|Funktion|Notizen|  
|-------------|-----------|  
|2D-Rendering|Das meiste 2D-Rendering wird unterstützt.|  
|3D-Rasterung|Die meisten 3D-Rasterungen werden unterstützt.|  
|Anisotrope 3D-Filterung|[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] versucht beim Rendering von 3D-Inhalten anisotrope Filterung zu verwenden. Anisotrope Filterung bezieht sich auf die verbesserte Bildqualität von Texturen auf Oberflächen, die in Bezug auf die Kamera weit entfernt und stark angewinkelt sind.|  
|3D-MIP-Zuordnung|[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] versucht beim Rendering von 3D-Inhalten MIP-Zuordnung zu verwenden. Die MIP-Zuordnung verbessert die Qualität des Texturrenderings, wenn <xref:System.Windows.Controls.Viewport3D>eine Textur ein kleineres Sichtfeld in einem einnimmt.|  
|Radiale Farbverläufe|Vermeiden Sie während der <xref:System.Windows.Media.RadialGradientBrush> Unterstützung die Verwendung für große Objekte.|  
|3D-Beleuchtungsberechnungen|[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] führt die Pro-Vertex-Beleuchtung aus, was bedeutet, dass eine Lichtstärke bei jedem Vertex für jedes auf ein Mesh angewendetes Material berechnet werden muss.|  
|Rendering von Text|Das Subpixel-Schriftart-Rendering verwendet verfügbare Pixel-Shader auf der Grafikhardware.|  
  
 Die folgenden Features und Funktionen sind nur für die Renderingebene 2 hardwarebeschleunigt:  
  
|Funktion|Notizen|  
|-------------|-----------|  
|3D-Antialiasing|3D-Antialiasing wird nur auf Betriebssystemen unterstützt, die Windows Display Driver Model (WDDM) unterstützen, z. B. Windows Vista und Windows 7.|  
  
 Die folgenden Features und Funktionen sind **nicht** hardwarebeschleunigt:  
  
|Funktion|Notizen|  
|-------------|-----------|  
|Gedruckter Inhalt|Jeder gedruckte Inhalt wird mithilfe der [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-Softwarepipeline gerendert.|  
|Gerasterte Inhalte, die<xref:System.Windows.Media.Imaging.RenderTargetBitmap>|Alle Inhalte, die <xref:System.Windows.Media.Imaging.RenderTargetBitmap.Render%2A> mithilfe <xref:System.Windows.Media.Imaging.RenderTargetBitmap>der Methode von gerendert werden.|  
|Gekachelte Inhalte, die<xref:System.Windows.Media.TileBrush>|Alle gekachelten Inhalte, in denen die <xref:System.Windows.Media.TileBrush.TileMode%2A> Eigenschaft des auf <xref:System.Windows.Media.TileBrush> <xref:System.Windows.Media.TileMode.Tile>festgelegt ist.|  
|Flächen, die die maximale Texturgröße der Grafikhardware überschreiten|Bei der meisten Grafikhardware sind große Flächen 2048 x 2048 oder 4096 x 4096 Pixel groß.|  
|Jeder Vorgang, dessen Video-RAM-Anforderung den Arbeitsspeicher der Grafikhardware überschreitet|Sie können den Video-RAM-Verbrauch der Anwendung mithilfe des Perforatortools überwachen, das Bestandteil der [WPF Performance Suite](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/aa969767(v=vs.100)) im Windows SDK ist.|  
|Überlappende Fenster|Überlappende Fenster ermöglichen den [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-Anwendungen das Rendering von Inhalt auf dem Bildschirm in einem nicht rechteckigen Fenster. Auf Betriebssystemen, die Windows Display Driver Model (WDDM) unterstützen, wie Windows Vista und Windows 7, werden layered Windows hardwarebeschleunigt. Auf anderen Systemen, z. B. Windows XP, werden mehrschichtige Fenster von Software ohne Hardwarebeschleunigung gerendert.<br /><br /> Sie können layered [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] windows in <xref:System.Windows.Window> aktivieren, indem Sie die folgenden Eigenschaften festlegen:<br /><br /> -   <xref:System.Windows.Window.WindowStyle%2A> = <xref:System.Windows.WindowStyle.None><br />-   <xref:System.Windows.Window.AllowsTransparency%2A> = `true`<br />-   <xref:System.Windows.Controls.Control.Background%2A> = <xref:System.Windows.Media.Brushes.Transparent%2A>|  
  
<a name="other_resources"></a>
## <a name="other-resources"></a>Weitere Ressourcen  
 Die folgenden Ressourcen können Ihnen bei der Analyse der Leistungsmerkmale Ihrer [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-Anwendung helfen.  
  
### <a name="graphics-rendering-registry-settings"></a>Registrierungseinstellungen für das Rendern von Grafiken  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] bietet vier Registrierungseinstellungen zum Steuern des [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-Renderings:  
  
|Einstellung|Beschreibung|  
|-------------|-----------------|  
|**Option zum Deaktivieren der Hardwarebeschleunigung**|Gibt an, ob die Hardwarebeschleunigung aktiviert werden soll|  
|**Maximaler Wert für Multisampling**|Gibt den Grad des Multisamplings für das Antialiasing von 3D-Inhalten an.|  
|**Einstellung für das erforderliche Videotreiberdatum**|Gibt an, ob das System die Hardwarebeschleunigung für Treiber deaktiviert, die vor November 2004 veröffentlicht wurden|  
|**Option zum Verwenden des Referenzrasters**|Gibt an, ob [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] das Referenzraster verwendet werden soll|  
  
 Diese Einstellungen stehen für alle externen Konfigurationshilfsprogramme zur Verfügung, die auf die [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-Registrierungseinstellungen verweisen können. Diese Einstellungen können auch erstellt oder geändert werden, indem Sie direkt über den Windows-Registrierungs-Editor auf die Werte zugreifen. Weitere Informationen finden Sie unter [Registrierungseinstellungen für das Rendern von Grafiken](../graphics-multimedia/graphics-rendering-registry-settings.md).  
  
### <a name="wpf-performance-profiling-tools"></a>WPF-Leistungsprofilerstellungstools  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] stellt eine Suite von Leistungsprofilerstellungstools bereit, mit deren Hilfe Sie das Laufzeitverhalten der Anwendung analysieren und die Typen der anwendbaren Leistungsoptimierungen bestimmen können. In der folgenden Tabelle sind die Leistungsprofilerstellungstools aufgeführt, die im Windows SDK-Tool WPF Performance Suite enthalten sind:  
  
|Tool|Beschreibung|  
|----------|-----------------|  
|Perforator|Wird für die Analyse von Renderingverhalten verwendet.|  
|Visual Profiler|Wird zum Erstellen eines Profils der Verwendung von [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-Diensten durch Elemente in der visuellen Struktur verwendet, z.B. Layout- und Ereignisbehandlung.|  
  
 WPF Performance Suite bietet eine umfassende grafische Ansicht von Leistungsdaten. Weitere Informationen zu WPF-Leistungstools finden Sie unter [WPF Performance Suite](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/aa969767(v=vs.100)).  
  
### <a name="directx-diagnostic-tool"></a>DirectX-Diagnosetool  
 Das DirectX-Diagnosetool Dxdiag.exe wurde entwickelt, um Ihnen bei der Fehlerbehebung im Zusammenhang mit DirectX-Problemen zu helfen. Der Standardinstallationsordner für das DirectX-Diagnosetool lautet:  
  
 `~\Windows\System32`  
  
 Wenn Sie das DirectX-Diagnosetool ausführen, enthält das Hauptfenster eine Reihe von Registerkarten, mit denen Sie DirectX-bezogene Informationen anzeigen und diagnostizieren können. Die Registerkarte **System** enthält beispielsweise Systeminformationen zu Ihrem Computer und gibt die Version von DirectX an, die auf Ihrem Computer installiert ist.  
  
 ![Screenshot: DirectX Diagnostic Tool](./media/directxdiagnostictool-01.png "DirectXDiagnosticTool_01")  
Hauptfenster des DirectX-Diagnosetools  
  
## <a name="see-also"></a>Siehe auch

- <xref:System.Windows.Media.RenderCapability>
- <xref:System.Windows.Media.RenderOptions>
- [Optimieren der WPF-Anwendungsleistung](optimizing-wpf-application-performance.md)
- [WPF Performance Suite](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/aa969767(v=vs.100))
- [Registrierungseinstellungen für das Rendern von Grafiken](../graphics-multimedia/graphics-rendering-registry-settings.md)
- [Tipps und Tricks zu Animationen](../graphics-multimedia/animation-tips-and-tricks.md)
