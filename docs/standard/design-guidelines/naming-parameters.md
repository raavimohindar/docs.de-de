---
title: Benennen von Parametern
description: Hier finden Sie Richtlinien für die Benennung von Parametern. Verwenden Sie beispielsweise beschreibende Parameternamen & Camel-Schreibweise, & Sie die Benennung basierend auf der Bedeutung anstelle des Typs in Erwägung gezogen.
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- parameters, names
- names [.NET Framework], parameters
ms.assetid: ca3c956e-725a-441b-b4e3-eab5d472f41c
ms.openlocfilehash: 54f37c4d6a0f9a6931fa69d612bf0e45bf1f2ce7
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/09/2020
ms.locfileid: "84583517"
---
# <a name="naming-parameters"></a>Benennen von Parametern
Neben dem offensichtlichen Grund für die Lesbarkeit ist es wichtig, den Richtlinien für Parameternamen zu folgen, da Parameter in der-Dokumentation und im-Designer angezeigt werden, wenn visuelle Entwurfs Tools IntelliSense-und Klassen Suchfunktionen bereitstellen.

 ✔️ Verwenden Sie "CamelCase" in Parameternamen.

 ✔️ beschreibende Parameternamen verwenden.

 ✔️ sollten Sie die Verwendung von Namen basierend auf der Bedeutung eines Parameters anstelle des Parameter Typs in Erwägung gezogen.

### <a name="naming-operator-overload-parameters"></a>Überladungs Parameter für Benennungs Operator
 ✔️ Verwenden Sie `left` und `right` für binäre Operator Überladungs Parameternamen, wenn es keine Bedeutung für die Parameter gibt.

 ✔️ `value` für Überladungs Parameternamen von unären Operatoren verwenden, wenn es keine Bedeutung für die Parameter gibt.

 Wenn Sie einen signifikanten Wert hinzufügen, ✔️ aussagekräftige Namen für Operator Überladungs Parameter in Erwägung gezogen.

 ❌Verwenden Sie keine Abkürzungen oder numerischen Indizes für Parameternamen der Operator Überladung.

 *Teile © 2005, 2009 Microsoft Corporation. Alle Rechte vorbehalten.*

 *Nachdruck mit Genehmigung von Pearson Education, Inc aus [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) von Krzysztof Cwalina und Brad Abrams, veröffentlicht am 22. Oktober 2008 durch Addison-Wesley Professional als Teil der Microsoft Windows Development Series.*

## <a name="see-also"></a>Weitere Informationen

- [Framework-Entwurfs Richtlinien](index.md)
- [Benennungs Richtlinien](naming-guidelines.md)
