---
ms.openlocfilehash: 5e2e8d1ec5d698d1c1649c2a0a1b4b77dbdf4022
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621281"
---
### <a name="wpf-printing-stack-update"></a>Update für WPF-Druckstapel

#### <a name="details"></a>Details

Die Druck-APIs von WPF, die <xref:System.Printing.PrintQueue?displayProperty=fullName> verwenden, rufen nun die Paket-API von Windows zum Drucken von Dokumenten statt der veralteten XPS-Druck-API auf. Diese Änderung wurde für die Wartbarkeit durchgeführt. Weder für Benutzer noch für Entwickler sollten Änderungen im Verhalten oder der API-Nutzung sichtbar werden. Der neue Druckstapel wird bei der Ausführung unter Windows 10 Creators Update standardmäßig aktiviert. Der alte Druckstapel funktioniert in älteren Windows-Versionen weiterhin wie zuvor.

#### <a name="suggestion"></a>Vorschlag

Legen Sie den <code>UseXpsOMPrinting</code>-REG_DWORD-Wert des <code>HKEY_CURRENT_USER\Software\Microsoft\.NETFramework\Windows Presentation Foundation\Printing</code>-Registrierungsschlüssels auf <code>1</code> fest, um den alten Stapel in Windows 10 Creators Update zu verwenden.

| Name    | Wert       |
|:--------|:------------|
| Bereich   |Microsoft Edge|
|Version|4.7|
|Typ|Laufzeit|
