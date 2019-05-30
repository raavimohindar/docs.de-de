---
title: 'Operatoren im Zusammenhang mit Zeigern: C#-Referenz'
description: Enthält Informationen zu C#-Operatoren, die Sie bei der Arbeit mit Zeigern verwenden können.
ms.date: 05/20/2019
author: pkulikov
f1_keywords:
- ->_CSharpKeyword
helpviewer_keywords:
- pointer related operators [C#]
- address-of operator [C#]
- '& operator [C#]'
- pointer indirection operator [C#]
- dereference operator [C#]
- '* operator [C#]'
- pointer member access operator [C#]
- -> operator [C#]
- pointer element access [C#]
- '[] operator [C#]'
- pointer arithmetic [C#]
- pointer increment [C#]
- pointer decrement [C#]
- pointer comparison [C#]
ms.openlocfilehash: 012e4fe9b8ee49f3b6b7240ac4ccb21dba70a8a9
ms.sourcegitcommit: c4e9d05644c9cb89de5ce6002723de107ea2e2c4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/19/2019
ms.locfileid: "65882778"
---
# <a name="pointer-related-operators-c-reference"></a><span data-ttu-id="21e78-103">Operatoren im Zusammenhang mit Zeigern (C#-Referenz)</span><span class="sxs-lookup"><span data-stu-id="21e78-103">Pointer related operators (C# Reference)</span></span>

<span data-ttu-id="21e78-104">Sie können die folgenden Operatoren für Zeiger verwenden:</span><span class="sxs-lookup"><span data-stu-id="21e78-104">You can use the following operators to work with pointers:</span></span>

- <span data-ttu-id="21e78-105">Unärer Operator [`&` (Adresse von)](#address-of-operator-): Abrufen der Adresse einer Variablen</span><span class="sxs-lookup"><span data-stu-id="21e78-105">Unary [`&` (address-of)](#address-of-operator-) operator: to get the address of a variable</span></span>
- <span data-ttu-id="21e78-106">Unärer Operator [`*` (Zeigerdereferenzierung)](#pointer-indirection-operator-): Abrufen der Variablen, auf die per Zeiger verwiesen wird</span><span class="sxs-lookup"><span data-stu-id="21e78-106">Unary [`*` (pointer indirection)](#pointer-indirection-operator-) operator: to obtain the variable pointed by a pointer</span></span>
- <span data-ttu-id="21e78-107">Operatoren [`->` (Memberzugriff)](#pointer-member-access-operator--) und [`[]` (Elementzugriff)](#pointer-element-access-operator-)</span><span class="sxs-lookup"><span data-stu-id="21e78-107">The [`->` (member access)](#pointer-member-access-operator--) and [`[]` (element access)](#pointer-element-access-operator-) operators</span></span>
- <span data-ttu-id="21e78-108">Arithmetische Operatoren [`+`, `-`, `++` und `--`](#pointer-arithmetic-operators)</span><span class="sxs-lookup"><span data-stu-id="21e78-108">Arithmetic operators [`+`, `-`, `++`, and `--`](#pointer-arithmetic-operators)</span></span>
- <span data-ttu-id="21e78-109">Vergleichsoperatoren [`==`, `!=`, `<`, `>`, `<=` und `>=`](#pointer-comparison-operators)</span><span class="sxs-lookup"><span data-stu-id="21e78-109">Comparison operators [`==`, `!=`, `<`, `>`, `<=`, and `>=`](#pointer-comparison-operators)</span></span>

<span data-ttu-id="21e78-110">Informationen zu Zeigertypen finden Sie unter [Zeigertypen](../../programming-guide/unsafe-code-pointers/pointer-types.md).</span><span class="sxs-lookup"><span data-stu-id="21e78-110">For information about pointer types, see [Pointer types](../../programming-guide/unsafe-code-pointers/pointer-types.md).</span></span>

> [!NOTE]
> <span data-ttu-id="21e78-111">Für alle Operationen mit Zeigern ist der Kontext [unsafe](../keywords/unsafe.md) erforderlich.</span><span class="sxs-lookup"><span data-stu-id="21e78-111">Any operation with pointers requires [unsafe](../keywords/unsafe.md) context.</span></span> <span data-ttu-id="21e78-112">Code, in dem unsafe-Blöcke enthalten sind, muss mit der Compileroption [`-unsafe`](../compiler-options/unsafe-compiler-option.md) kompiliert werden.</span><span class="sxs-lookup"><span data-stu-id="21e78-112">The code that contains unsafe blocks must be compiled with the [`-unsafe`](../compiler-options/unsafe-compiler-option.md) compiler option.</span></span>

## <a name="address-of-operator-amp"></a><span data-ttu-id="21e78-113">„Adresse von“-Operator &amp;</span><span class="sxs-lookup"><span data-stu-id="21e78-113">Address-of operator &amp;</span></span>

<span data-ttu-id="21e78-114">Der unäre Operator `&` gibt die Adresse seines Operanden zurück:</span><span class="sxs-lookup"><span data-stu-id="21e78-114">The unary `&` operator returns the address of its operand:</span></span>

[!code-csharp[address of local](~/samples/snippets/csharp/language-reference/operators/PointerOperators.cs#AddressOf)]

<span data-ttu-id="21e78-115">Der Operand des Operators `&` muss eine feste Variable sein.</span><span class="sxs-lookup"><span data-stu-id="21e78-115">The operand of the `&` operator must be a fixed variable.</span></span> <span data-ttu-id="21e78-116">*Feste* Variablen befinden sich an Speicherorten, auf die sich [Garbage Collector](../../../standard/garbage-collection/index.md)-Operationen nicht auswirken.</span><span class="sxs-lookup"><span data-stu-id="21e78-116">*Fixed* variables are variables that reside in storage locations that are unaffected by operation of the [garbage collector](../../../standard/garbage-collection/index.md).</span></span> <span data-ttu-id="21e78-117">Im vorherigen Beispiel ist die lokale Variable `number` eine feste Variable, da sie im Stapel angeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="21e78-117">In the preceding example, the local variable `number` is a fixed variable, because it resides on the stack.</span></span> <span data-ttu-id="21e78-118">Variablen an Speicherorten, auf die sich der Garbage Collector auswirken kann (z. B. durch eine Verschiebung), werden als *bewegliche* Variablen bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="21e78-118">Variables that reside in storage locations that can be affected by the garbage collector (for example, relocated) are called *movable* variables.</span></span> <span data-ttu-id="21e78-119">Objektfelder und Arrayelemente sind Beispiele für bewegliche Variablen.</span><span class="sxs-lookup"><span data-stu-id="21e78-119">Object fields and array elements are examples of movable variables.</span></span> <span data-ttu-id="21e78-120">Sie können die Adresse einer beweglichen Variablen erhalten, wenn Sie sie mit der Anweisung [fixed](../keywords/fixed-statement.md) „fixieren“ bzw. „anheften“.</span><span class="sxs-lookup"><span data-stu-id="21e78-120">You can get the address of a movable variable if you "fix", or "pin", it with the [fixed](../keywords/fixed-statement.md) statement.</span></span> <span data-ttu-id="21e78-121">Die abgerufene Adresse ist nur für die Dauer des `fixed`-Anweisungsblocks gültig.</span><span class="sxs-lookup"><span data-stu-id="21e78-121">The obtained address is valid only for the duration of the `fixed` statement block.</span></span> <span data-ttu-id="21e78-122">Im folgenden Beispiel wird veranschaulicht, wie Sie die Anweisung `fixed` und den Operator `&` verwenden:</span><span class="sxs-lookup"><span data-stu-id="21e78-122">The following example shows how to use the `fixed` statement and the `&` operator:</span></span>

[!code-csharp[address of fixed](~/samples/snippets/csharp/language-reference/operators/PointerOperators.cs#AddressOfFixed)]

<span data-ttu-id="21e78-123">Sie können nicht die Adresse einer Konstanten oder eines Werts abrufen.</span><span class="sxs-lookup"><span data-stu-id="21e78-123">You can't get the address of a constant or a value.</span></span>

<span data-ttu-id="21e78-124">Weitere Informationen zu festen und beweglichen Variablen finden Sie im Abschnitt [Feste und verschiebbare Variablen](~/_csharplang/spec/unsafe-code.md#fixed-and-moveable-variables) der [Spezifikation für die Sprache C#](~/_csharplang/spec/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="21e78-124">For more information about fixed and movable variables, see the [Fixed and moveable variables](~/_csharplang/spec/unsafe-code.md#fixed-and-moveable-variables) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

<span data-ttu-id="21e78-125">Mit dem binären Operator `&` wird der Wert für [logisches UND](boolean-logical-operators.md#logical-and-operator-) der booleschen Operanden oder der Wert für [bitweise logisches UND](bitwise-and-shift-operators.md#logical-and-operator-) für die integralen Operanden berechnet.</span><span class="sxs-lookup"><span data-stu-id="21e78-125">The binary `&` operator computes the [logical AND](boolean-logical-operators.md#logical-and-operator-) of its Boolean operands or the [bitwise logical AND](bitwise-and-shift-operators.md#logical-and-operator-) of its integral operands.</span></span>

## <a name="pointer-indirection-operator-"></a><span data-ttu-id="21e78-126">Zeigerdereferenzierungsoperator \*</span><span class="sxs-lookup"><span data-stu-id="21e78-126">Pointer indirection operator \*</span></span>

<span data-ttu-id="21e78-127">Mit dem unären Zeigerdereferenzierungsoperator `*` wird die Variable abgerufen, auf die der Operand verweist.</span><span class="sxs-lookup"><span data-stu-id="21e78-127">The unary pointer indirection operator `*` obtains the variable to which its operand points.</span></span> <span data-ttu-id="21e78-128">Er wird auch kurz als Dereferenzierungsoperator bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="21e78-128">It's also known as the dereference operator.</span></span> <span data-ttu-id="21e78-129">Der Operand des Operators `*` muss einen Zeigertyp aufweisen.</span><span class="sxs-lookup"><span data-stu-id="21e78-129">The operand of the `*` operator must be of a pointer type.</span></span>

[!code-csharp[pointer indirection](~/samples/snippets/csharp/language-reference/operators/PointerOperators.cs#PointerIndirection)]

<span data-ttu-id="21e78-130">Sie können den Operator `*` nicht auf einen Ausdruck vom Typ `void*` anwenden.</span><span class="sxs-lookup"><span data-stu-id="21e78-130">You cannot apply the `*` operator to an expression of type `void*`.</span></span>

<span data-ttu-id="21e78-131">Mit dem binären Operator `*` wird das [Produkt](arithmetic-operators.md#multiplication-operator-) seiner numerischen Operanden berechnet.</span><span class="sxs-lookup"><span data-stu-id="21e78-131">The binary `*` operator computes the [product](arithmetic-operators.md#multiplication-operator-) of its numeric operands.</span></span>

## <a name="pointer-member-access-operator--"></a><span data-ttu-id="21e78-132">Zeigermember-Zugriffsoperator -></span><span class="sxs-lookup"><span data-stu-id="21e78-132">Pointer member access operator -></span></span>

<span data-ttu-id="21e78-133">Mit dem Operator `->` werden die [Zeigerdereferenzierung](#pointer-indirection-operator-) und der [Memberzugriff](member-access-operators.md#member-access-operator-) kombiniert.</span><span class="sxs-lookup"><span data-stu-id="21e78-133">The `->` operator combines [pointer indirection](#pointer-indirection-operator-) and [member access](member-access-operators.md#member-access-operator-).</span></span> <span data-ttu-id="21e78-134">Wenn `x` ein Zeiger des Typs `T*` und `y` ein Member von `T` ist, auf den zugegriffen werden kann, ist ein Ausdruck der Form</span><span class="sxs-lookup"><span data-stu-id="21e78-134">That is, if `x` is a pointer of type `T*` and `y` is an accessible member of `T`, an expression of the form</span></span>

```csharp
x->y
```

<span data-ttu-id="21e78-135">eine Entsprechung von</span><span class="sxs-lookup"><span data-stu-id="21e78-135">is equivalent to</span></span>

```csharp
(*x).y
```

<span data-ttu-id="21e78-136">Im folgenden Beispiel wird die Verwendung des `->`-Operators veranschaulicht:</span><span class="sxs-lookup"><span data-stu-id="21e78-136">The following example demonstrates the usage of the `->` operator:</span></span>

[!code-csharp[pointer member access](~/samples/snippets/csharp/language-reference/operators/PointerOperators.cs#MemberAccess)]

<span data-ttu-id="21e78-137">Sie können den Operator `->` nicht auf einen Ausdruck vom Typ `void*` anwenden.</span><span class="sxs-lookup"><span data-stu-id="21e78-137">You cannot apply the `->` operator to an expression of type `void*`.</span></span>

## <a name="pointer-element-access-operator-"></a><span data-ttu-id="21e78-138">Zeigerelementzugriff-Operator []</span><span class="sxs-lookup"><span data-stu-id="21e78-138">Pointer element access operator []</span></span>

<span data-ttu-id="21e78-139">Für einen Ausdruck `p` mit einem Zeigertyp wird ein Zeigerelementzugriff der Form `p[n]` als `*(p + n)` ausgewertet. Hierbei muss `n` einen Typ aufweisen, der implizit in `int`, `uint`, `long` oder `ulong` konvertiert werden kann.</span><span class="sxs-lookup"><span data-stu-id="21e78-139">For an expression `p` of a pointer type, a pointer element access of the form `p[n]` is evaluated as `*(p + n)`, where `n` must be of a type implicitly convertible to `int`, `uint`, `long`, or `ulong`.</span></span> <span data-ttu-id="21e78-140">Informationen zum Verhalten des Operators `+` mit Zeigern finden Sie im Abschnitt [Addieren oder Subtrahieren eines Integralwerts zu bzw. von einem Zeiger](#addition-or-subtraction-of-an-integral-value-to-or-from-a-pointer).</span><span class="sxs-lookup"><span data-stu-id="21e78-140">For information about the behavior of the `+` operator with pointers, see the [Addition or subtraction of an integral value to or from a pointer](#addition-or-subtraction-of-an-integral-value-to-or-from-a-pointer) section.</span></span>

<span data-ttu-id="21e78-141">Im folgenden Beispiel wird veranschaulicht, wie Sie mit einem Zeiger und dem Operator `[]` auf Arrayelemente zugreifen:</span><span class="sxs-lookup"><span data-stu-id="21e78-141">The following example demonstrates how to access array elements with a pointer and the `[]` operator:</span></span>

[!code-csharp[pointer element access](~/samples/snippets/csharp/language-reference/operators/PointerOperators.cs#ElementAccess)]

<span data-ttu-id="21e78-142">Im Beispiel wird der Operator [`stackalloc`](../keywords/stackalloc.md) verwendet, um im Stapel einen Block mit Speicher zuzuordnen.</span><span class="sxs-lookup"><span data-stu-id="21e78-142">The example uses the [`stackalloc` operator](../keywords/stackalloc.md) to allocate a block of memory on the stack.</span></span>

> [!NOTE]
> <span data-ttu-id="21e78-143">Der Zeigerelementzugriff-Operator führt keine Überprüfung auf Fehler vom Typ „Außerhalb des gültigen Bereichs“ durch.</span><span class="sxs-lookup"><span data-stu-id="21e78-143">The pointer element access operator doesn't check for out-of-bounds errors.</span></span>

<span data-ttu-id="21e78-144">Sie können `[]` nicht für den Zeigerelementzugriff mit einem Ausdruck vom Typ `void*` verwenden.</span><span class="sxs-lookup"><span data-stu-id="21e78-144">You cannot use `[]` for pointer element access with an expression of type `void*`.</span></span>

<span data-ttu-id="21e78-145">Sie können auch den Operator `[]` für den [Arrayelement- oder Indexerzugriff](member-access-operators.md#indexer-operator-) nutzen.</span><span class="sxs-lookup"><span data-stu-id="21e78-145">You also can use the `[]` operator for [array element or indexer access](member-access-operators.md#indexer-operator-).</span></span>

## <a name="pointer-arithmetic-operators"></a><span data-ttu-id="21e78-146">Arithmetische Zeigeroperatoren</span><span class="sxs-lookup"><span data-stu-id="21e78-146">Pointer arithmetic operators</span></span>

<span data-ttu-id="21e78-147">Sie können mit Zeigern die folgenden arithmetischen Operationen durchführen:</span><span class="sxs-lookup"><span data-stu-id="21e78-147">You can perform the following arithmetic operations with pointers:</span></span>

- <span data-ttu-id="21e78-148">Addieren oder Subtrahieren eines Integralwerts zu bzw. von einem Zeiger</span><span class="sxs-lookup"><span data-stu-id="21e78-148">Add or subtract an integral value to or from a pointer</span></span>
- <span data-ttu-id="21e78-149">Subtrahieren von zwei Zeigern</span><span class="sxs-lookup"><span data-stu-id="21e78-149">Subtract two pointers</span></span>
- <span data-ttu-id="21e78-150">Inkrementieren oder Dekrementieren eines Zeigers</span><span class="sxs-lookup"><span data-stu-id="21e78-150">Increment or decrement a pointer</span></span>

<span data-ttu-id="21e78-151">Sie können diese Operationen nicht mit Zeigern vom Typ `void*` durchführen.</span><span class="sxs-lookup"><span data-stu-id="21e78-151">You cannot perform those operations with pointers of type `void*`.</span></span>

<span data-ttu-id="21e78-152">Weitere Informationen zu unterstützten arithmetischen Operationen mit numerischen Typen finden Sie unter [Arithmetische Operatoren](arithmetic-operators.md).</span><span class="sxs-lookup"><span data-stu-id="21e78-152">For information about supported arithmetic operations with numeric types, see [Arithmetic operators](arithmetic-operators.md).</span></span>

### <a name="addition-or-subtraction-of-an-integral-value-to-or-from-a-pointer"></a><span data-ttu-id="21e78-153">Addieren oder Subtrahieren eines Integralwerts zu bzw. von einem Zeiger</span><span class="sxs-lookup"><span data-stu-id="21e78-153">Addition or subtraction of an integral value to or from a pointer</span></span>

<span data-ttu-id="21e78-154">Für einen Zeiger `p` vom Typ `T*` und einen Ausdruck `n` eines Typs, der implizit in `int`, `uint`, `long` oder `ulong` konvertiert werden kann, sind die Addition und die Subtraktion wie folgt definiert:</span><span class="sxs-lookup"><span data-stu-id="21e78-154">For a pointer `p` of type `T*` and an expression `n` of a type implicitly convertible to `int`, `uint`, `long`, or `ulong`, addition and subtraction are defined as follows:</span></span>

- <span data-ttu-id="21e78-155">Für die Ausdrücke `p + n` und `n + p` wird jeweils ein Zeiger vom Typ `T*` erzeugt, der sich aus dem Addieren von `n * sizeof(T)` zur Adresse von `p` ergibt.</span><span class="sxs-lookup"><span data-stu-id="21e78-155">Both `p + n` and `n + p` expressions produce a pointer of type `T*` that results from adding `n * sizeof(T)` to the address given by `p`.</span></span>
- <span data-ttu-id="21e78-156">Für den Ausdruck `p - n` wird ein Zeiger vom Typ `T*` erzeugt, der sich ergibt, indem `n * sizeof(T)` von der Adresse von `p` subtrahiert wird.</span><span class="sxs-lookup"><span data-stu-id="21e78-156">The `p - n` expression produces a pointer of type `T*` that results from subtracting `n * sizeof(T)` from the address given by `p`.</span></span>

<span data-ttu-id="21e78-157">Mit dem Operator [`sizeof`](../keywords/sizeof.md) wird die Größe eines Typs in Byte abgerufen.</span><span class="sxs-lookup"><span data-stu-id="21e78-157">The [`sizeof` operator](../keywords/sizeof.md) obtains the size of a type in bytes.</span></span>

<span data-ttu-id="21e78-158">Im folgenden Beispiel wird die Verwendung des Operators `+` mit einem Zeiger veranschaulicht:</span><span class="sxs-lookup"><span data-stu-id="21e78-158">The following example demonstrates the usage of the `+` operator with a pointer:</span></span>

[!code-csharp[pointer addition](~/samples/snippets/csharp/language-reference/operators/PointerOperators.cs#AddNumber)]

### <a name="pointer-subtraction"></a><span data-ttu-id="21e78-159">Zeigersubtraktion</span><span class="sxs-lookup"><span data-stu-id="21e78-159">Pointer subtraction</span></span>

<span data-ttu-id="21e78-160">Für die beiden Zeiger `p1` und `p2` vom Typ `T*` ergibt der Ausdruck `p1 - p2` den Unterschied zwischen den Adressen von `p1` und `p2` dividiert durch `sizeof(T)`.</span><span class="sxs-lookup"><span data-stu-id="21e78-160">For two pointers `p1` and `p2` of type `T*`, the expression `p1 - p2` produces the difference between the addresses given by `p1` and `p2` divided by `sizeof(T)`.</span></span> <span data-ttu-id="21e78-161">Das Ergebnis hat den Typ `long`.</span><span class="sxs-lookup"><span data-stu-id="21e78-161">The type of the result is `long`.</span></span> <span data-ttu-id="21e78-162">`p1 - p2` wird also als `((long)(p1) - (long)(p2)) / sizeof(T)` berechnet.</span><span class="sxs-lookup"><span data-stu-id="21e78-162">That is, `p1 - p2` is computed as `((long)(p1) - (long)(p2)) / sizeof(T)`.</span></span>

<span data-ttu-id="21e78-163">Im folgenden Beispiel ist die Zeigersubtraktion dargestellt:</span><span class="sxs-lookup"><span data-stu-id="21e78-163">The following example demonstrates the pointer subtraction:</span></span>

[!code-csharp[pointer subtraction](~/samples/snippets/csharp/language-reference/operators/PointerOperators.cs#SubtractPointers)]

### <a name="pointer-increment-and-decrement"></a><span data-ttu-id="21e78-164">Inkrementieren und Dekrementieren von Zeigern</span><span class="sxs-lookup"><span data-stu-id="21e78-164">Pointer increment and decrement</span></span>

<span data-ttu-id="21e78-165">Mit dem Inkrementoperator `++` wird 1 zum Zeigeroperanden [addiert](#addition-or-subtraction-of-an-integral-value-to-or-from-a-pointer).</span><span class="sxs-lookup"><span data-stu-id="21e78-165">The `++` increment operator [adds](#addition-or-subtraction-of-an-integral-value-to-or-from-a-pointer) 1 to its pointer operand.</span></span> <span data-ttu-id="21e78-166">Mit dem Dekrementoperator `--` wird 1 vom Zeigeroperanden [subtrahiert](#addition-or-subtraction-of-an-integral-value-to-or-from-a-pointer).</span><span class="sxs-lookup"><span data-stu-id="21e78-166">The `--` decrement operator [subtracts](#addition-or-subtraction-of-an-integral-value-to-or-from-a-pointer) 1 from its pointer operand.</span></span>

<span data-ttu-id="21e78-167">Für beide Operatoren werden zwei Formen unterstützt: Postfix (`p++` und `p--`) und Präfix (`++p` und `--p`).</span><span class="sxs-lookup"><span data-stu-id="21e78-167">Both operators are supported in two forms: postfix (`p++` and `p--`) and prefix (`++p` and `--p`).</span></span> <span data-ttu-id="21e78-168">Das Ergebnis von `p++` und `p--` ist der Wert von `p` *vor* der Operation.</span><span class="sxs-lookup"><span data-stu-id="21e78-168">The result of `p++` and `p--` is the value of `p` *before* the operation.</span></span> <span data-ttu-id="21e78-169">Das Ergebnis von `++p` und `--p` ist der Wert von `p` *nach* der Operation.</span><span class="sxs-lookup"><span data-stu-id="21e78-169">The result of `++p` and `--p` is the value of `p` *after* the operation.</span></span>

<span data-ttu-id="21e78-170">Im folgenden Beispiel wird das Verhalten von Postfix- und Präfix-Inkrementoperatoren veranschaulicht:</span><span class="sxs-lookup"><span data-stu-id="21e78-170">The following example demonstrates the behavior of both postfix and prefix increment operators:</span></span>

[!code-csharp[pointer increment](~/samples/snippets/csharp/language-reference/operators/PointerOperators.cs#Increment)]

## <a name="pointer-comparison-operators"></a><span data-ttu-id="21e78-171">Vergleichsoperatoren für Zeiger</span><span class="sxs-lookup"><span data-stu-id="21e78-171">Pointer comparison operators</span></span>

<span data-ttu-id="21e78-172">Sie können die Operatoren `==`, `!=`, `<`, `>`, `<=` und `>=` verwenden, um Operanden jedes Zeigertyps zu vergleichen, z. B. `void*`.</span><span class="sxs-lookup"><span data-stu-id="21e78-172">You can use the `==`, `!=`, `<`, `>`, `<=`, and `>=` operators to compare operands of any pointer type, including `void*`.</span></span> <span data-ttu-id="21e78-173">Mit diesen Operatoren werden die Adressen der zwei Operanden so verglichen, als ob es sich um ganze Zahlen ohne Vorzeichen handeln würde.</span><span class="sxs-lookup"><span data-stu-id="21e78-173">Those operators compare the addresses given by the two operands as if they were unsigned integers.</span></span>

<span data-ttu-id="21e78-174">Informationen zum Verhalten dieser Operatoren für Operanden anderer Typen finden Sie in den Artikeln zu [Gleichheitsoperatoren](equality-operators.md) und [Vergleichsoperatoren](comparison-operators.md).</span><span class="sxs-lookup"><span data-stu-id="21e78-174">For information about the behavior of those operators for operands of other types, see the [Equality operators](equality-operators.md) and [Comparison operators](comparison-operators.md) articles.</span></span>

## <a name="operator-precedence"></a><span data-ttu-id="21e78-175">Operatorrangfolge</span><span class="sxs-lookup"><span data-stu-id="21e78-175">Operator precedence</span></span>

<span data-ttu-id="21e78-176">In der folgenden Liste sind die Zeigeroperatoren absteigend nach der Rangfolge sortiert:</span><span class="sxs-lookup"><span data-stu-id="21e78-176">The following list orders pointer related operators starting from the highest precedence to the lowest:</span></span>

- <span data-ttu-id="21e78-177">Inkrementierungs- und Dekrementierungsoperatoren in Postfixnotation (`x++` und `x--`) und die Operatoren `->` und `[]`</span><span class="sxs-lookup"><span data-stu-id="21e78-177">Postfix increment `x++` and decrement `x--` operators and the `->` and `[]` operators</span></span>
- <span data-ttu-id="21e78-178">Inkrementierungs- und Dekrementierungsoperatoren in Präfixnotation (`++x` und `--x`) und die Operatoren `&` und `*`</span><span class="sxs-lookup"><span data-stu-id="21e78-178">Prefix increment `++x` and decrement `--x` operators and the `&` and `*` operators</span></span>
- <span data-ttu-id="21e78-179">Additive Operatoren `+` und `-`</span><span class="sxs-lookup"><span data-stu-id="21e78-179">Additive `+` and `-` operators</span></span>
- <span data-ttu-id="21e78-180">Vergleichsoperatoren `<`, `>`, `<=` und `>=`</span><span class="sxs-lookup"><span data-stu-id="21e78-180">Comparison `<`, `>`, `<=`, and `>=` operators</span></span>
- <span data-ttu-id="21e78-181">Gleichheitsoperatoren `==` und `!=`</span><span class="sxs-lookup"><span data-stu-id="21e78-181">Equality `==` and `!=` operators</span></span>

<span data-ttu-id="21e78-182">Verwenden Sie Klammern `()`, wenn Sie die Reihenfolge der Auswertung ändern möchten, die durch die Operatorrangfolge festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="21e78-182">Use parentheses, `()`, to change the order of evaluation imposed by operator precedence.</span></span>

<span data-ttu-id="21e78-183">Die vollständige Liste der nach Rangfolgenebene sortierten C#-Operatoren finden Sie unter [C#-Operatoren](index.md).</span><span class="sxs-lookup"><span data-stu-id="21e78-183">For the complete list of C# operators ordered by precedence level, see [C# operators](index.md).</span></span>

## <a name="operator-overloadability"></a><span data-ttu-id="21e78-184">Operatorüberladbarkeit</span><span class="sxs-lookup"><span data-stu-id="21e78-184">Operator overloadability</span></span>

<span data-ttu-id="21e78-185">Mit einem benutzerdefinierten Typ können die Zeigeroperatoren `&`, `*`, `->` und `[]` nicht überladen werden.</span><span class="sxs-lookup"><span data-stu-id="21e78-185">A user-defined type cannot overload the pointer related operators `&`, `*`, `->`, and `[]`.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="21e78-186">C#-Sprachspezifikation</span><span class="sxs-lookup"><span data-stu-id="21e78-186">C# language specification</span></span>

<span data-ttu-id="21e78-187">Weitere Informationen finden Sie in den folgenden Abschnitten der [C#-Sprachspezifikation](~/_csharplang/spec/introduction.md):</span><span class="sxs-lookup"><span data-stu-id="21e78-187">For more information, see the following sections of the [C# language specification](~/_csharplang/spec/introduction.md):</span></span>

- [<span data-ttu-id="21e78-188">Fixed and moveable variables (Feste und verschiebbare Variablen)</span><span class="sxs-lookup"><span data-stu-id="21e78-188">Fixed and moveable variables</span></span>](~/_csharplang/spec/unsafe-code.md#fixed-and-moveable-variables)
- [<span data-ttu-id="21e78-189">Adresse-von-Operator</span><span class="sxs-lookup"><span data-stu-id="21e78-189">The address-of operator</span></span>](~/_csharplang/spec/unsafe-code.md#the-address-of-operator)
- [<span data-ttu-id="21e78-190">Zeigerdereferenzierung</span><span class="sxs-lookup"><span data-stu-id="21e78-190">Pointer indirection</span></span>](~/_csharplang/spec/unsafe-code.md#pointer-indirection)
- [<span data-ttu-id="21e78-191">Zeigermemberzugriff</span><span class="sxs-lookup"><span data-stu-id="21e78-191">Pointer member access</span></span>](~/_csharplang/spec/unsafe-code.md#pointer-member-access)
- [<span data-ttu-id="21e78-192">Zeigerelementzugriff</span><span class="sxs-lookup"><span data-stu-id="21e78-192">Pointer element access</span></span>](~/_csharplang/spec/unsafe-code.md#pointer-element-access)
- [<span data-ttu-id="21e78-193">Zeigerarithmetik</span><span class="sxs-lookup"><span data-stu-id="21e78-193">Pointer arithmetic</span></span>](~/_csharplang/spec/unsafe-code.md#pointer-arithmetic)
- [<span data-ttu-id="21e78-194">Inkrementieren und Dekrementieren von Zeigern</span><span class="sxs-lookup"><span data-stu-id="21e78-194">Pointer increment and decrement</span></span>](~/_csharplang/spec/unsafe-code.md#pointer-increment-and-decrement)
- [<span data-ttu-id="21e78-195">Zeigervergleich</span><span class="sxs-lookup"><span data-stu-id="21e78-195">Pointer comparison</span></span>](~/_csharplang/spec/unsafe-code.md#pointer-comparison)

## <a name="see-also"></a><span data-ttu-id="21e78-196">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="21e78-196">See also</span></span>

- [<span data-ttu-id="21e78-197">C#-Referenz</span><span class="sxs-lookup"><span data-stu-id="21e78-197">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="21e78-198">C#-Programmierhandbuch</span><span class="sxs-lookup"><span data-stu-id="21e78-198">C# Programming Guide</span></span>](../../programming-guide/index.md)
- [<span data-ttu-id="21e78-199">C#-Operatoren</span><span class="sxs-lookup"><span data-stu-id="21e78-199">C# Operators</span></span>](index.md)
- [<span data-ttu-id="21e78-200">Zeigertypen</span><span class="sxs-lookup"><span data-stu-id="21e78-200">Pointer types</span></span>](../../programming-guide/unsafe-code-pointers/pointer-types.md)
- [<span data-ttu-id="21e78-201">`unsafe`Schlüsselwort</span><span class="sxs-lookup"><span data-stu-id="21e78-201">`unsafe` keyword</span></span>](../keywords/unsafe.md)
- [<span data-ttu-id="21e78-202">`fixed`Schlüsselwort</span><span class="sxs-lookup"><span data-stu-id="21e78-202">`fixed` keyword</span></span>](../keywords/fixed-statement.md)
- [<span data-ttu-id="21e78-203">`stackalloc`-Operator</span><span class="sxs-lookup"><span data-stu-id="21e78-203">`stackalloc` operator</span></span>](../keywords/stackalloc.md)
- [<span data-ttu-id="21e78-204">`sizeof`-Operator</span><span class="sxs-lookup"><span data-stu-id="21e78-204">`sizeof` operator</span></span>](../keywords/sizeof.md)