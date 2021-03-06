---
title: Die "<propertyname1>"-Standardeigenschaft verursacht einen Konflikt mit der "<propertyname2>"-Standardeigenschaft in "<classname>" und sollte daher als "Shadows" deklariert werden.
ms.date: 07/20/2015
f1_keywords:
- vbc40007
- bc40007
helpviewer_keywords:
- BC40007
ms.assetid: 692ccf76-5715-4f11-a972-84cf9de30bc1
ms.openlocfilehash: 37f98ce8120d5861552819690f9d5f22c9959a0e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409724"
---
# <a name="default-property-propertyname1-conflicts-with-default-property-propertyname2-in-classname-and-so-should-be-declared-shadows"></a>Die "\<propertyname1>"-Standardeigenschaft verursacht einen Konflikt mit der "\<propertyname2>"-Standardeigenschaft in "\<classname>" und sollte daher als "Shadows" deklariert werden.
Eine Eigenschaft wird mit dem gleichen Namen wie eine Eigenschaft deklariert, die in der Basisklasse definiert ist. In dieser Situation sollte die-Eigenschaft in dieser Klasse den Schatten der Basisklassen Eigenschaft überschatten.  
  
 Diese Meldung ist eine Warnung. `Shadows` wird standardmäßig angenommen. Weitere Informationen zum Ausblenden von Warnungen oder zum Behandeln von Warnungen als Fehler finden Sie unter [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **Fehler-ID:** BC40007  
  
## <a name="to-correct-this-error"></a>So beheben Sie diesen Fehler  
  
- Fügen Sie das- `Shadows` Schlüsselwort zur Deklaration hinzu, oder ändern Sie den Namen der Eigenschaft, die deklariert wird.  
  
## <a name="see-also"></a>Weitere Informationen

- [Shadows](../modifiers/shadows.md)
- [Shadowing in Visual Basic](../../programming-guide/language-features/declared-elements/shadowing.md)
