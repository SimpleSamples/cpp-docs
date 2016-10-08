---
title: "CObject Class"
ms.custom: na
ms.date: 10/03/2016
ms.devlang: 
  - C++
ms.prod: visual-studio-dev14
ms.reviewer: na
ms.suite: na
ms.technology: 
  - devlang-cpp
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 95e9acd3-d9eb-4ac0-b52b-ca4a501a7a3a
caps.latest.revision: 18
manager: ghogen
translation.priority.ht: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - it-it
  - ja-jp
  - ko-kr
  - pl-pl
  - pt-br
  - ru-ru
  - tr-tr
  - zh-cn
  - zh-tw
---
# CObject Class
The principal base class for the Microsoft Foundation Class Library.  
  
## Syntax  
  
```  
class AFX_NOVTABLE CObject  
```  
  
## Members  
  
### Protected Constructors  
  
|Name|Description|  
|----------|-----------------|  
|[CObject::CObject](#cobject__cobject)|Default constructor.|  
  
### Public Methods  
  
|Name|Description|  
|----------|-----------------|  
|[CObject::AssertValid](#cobject__assertvalid)|Validates this object's integrity.|  
|[CObject::Dump](#cobject__dump)|Produces a diagnostic dump of this object.|  
|[CObject::GetRuntimeClass](#cobject__getruntimeclass)|Returns the `CRuntimeClass` structure corresponding to this object's class.|  
|[CObject::IsKindOf](#cobject__iskindof)|Tests this object's relationship to a given class.|  
|[CObject::IsSerializable](#cobject__isserializable)|Tests to see whether this object can be serialized.|  
|[CObject::Serialize](#cobject__serialize)|Loads or stores an object from/to an archive.|  
  
### Public Operators  
  
|Name|Description|  
|----------|-----------------|  
|[CObject::operator delete](#cobject__operator_delete)|Special **delete** operator.|  
|[CObject::operator new](#cobject__operator_new)|Special **new** operator.|  
  
## Remarks  
 It serves as the root not only for library classes such as `CFile` and `CObList`, but also for the classes that you write. `CObject` provides basic services, including  
  
-   Serialization support  
  
-   Run-time class information  
  
-   Object diagnostic output  
  
-   Compatibility with collection classes  
  
 Note that `CObject` does not support multiple inheritance. Your derived classes can have only one `CObject` base class, and that `CObject` must be leftmost in the hierarchy. It is permissible, however, to have structures and non- `CObject`-derived classes in right-hand multiple-inheritance branches.  
  
 You will realize major benefits from `CObject` derivation if you use some of the optional macros in your class implementation and declarations.  
  
 The first-level macros, [DECLARE_DYNAMIC](../Topic/DECLARE_DYNAMIC.md) and [IMPLEMENT_DYNAMIC](../Topic/IMPLEMENT_DYNAMIC.md), permit run-time access to the class name and its position in the hierarchy. This, in turn, allows meaningful diagnostic dumping.  
  
 The second-level macros, [DECLARE_SERIAL](../Topic/DECLARE_SERIAL.md) and [IMPLEMENT_SERIAL](../Topic/IMPLEMENT_SERIAL.md), include all the functionality of the first-level macros, and they enable an object to be "serialized" to and from an "archive."  
  
 For information about deriving Microsoft Foundation classes and C++ classes in general and using `CObject`, see [Using CObject](../VS_visualcpp/Using-CObject.md) and [Serialization](../VS_visualcpp/Serialization-in-MFC.md).  
  
## Inheritance Hierarchy  
 `CObject`  
  
## Requirements  
 **Header:** afx.h  
  
##  <a name="cobject__assertvalid"></a>  CObject::AssertValid  
 Validates this object's integrity.  
  
```  
virtual void AssertValid() const;  
```  
  
### Remarks  
 `AssertValid` performs a validity check on this object by checking its internal state. In the Debug version of the library, `AssertValid` may assert and thus terminate the program with a message that lists the line number and filename where the assertion failed.  
  
 When you write your own class, you should override the `AssertValid` function to provide diagnostic services for yourself and other users of your class. The overridden `AssertValid` usually calls the `AssertValid` function of its base class before checking data members unique to the derived class.  
  
 Because `AssertValid` is a **const** function, you are not permitted to change the object state during the test. Your own derived class `AssertValid` functions should not throw exceptions but rather should assert whether they detect invalid object data.  
  
 The definition of "validity" depends on the object's class. As a rule, the function should perform a "shallow check." That is, if an object contains pointers to other objects, it should check to see whether the pointers are not null, but it should not perform validity testing on the objects referred to by the pointers.  
  
### Example  
 See [CObList::CObList](../VS_visualcpp/CObList-Class.md#coblist__coblist) for a listing of the `CAge` class used in all `CObject` examples.  
  
 [!CODE [NVC_MFCCObjectSample#7](../CodeSnippet/VS_Snippets_Cpp/NVC_MFCCObjectSample#7)]  
  
 For another example, see [AfxDoForAllObjects](../Topic/AfxDoForAllObjects.md).  
  
##  <a name="cobject__cobject"></a>  CObject::CObject  
 These functions are the standard `CObject` constructors.  
  
```  
CObject();  
  
CObject( const CObject& objectSrc );  
```  
  
### Parameters  
 *objectSrc*  
 A reference to another `CObject`  
  
### Remarks  
 The default version is automatically called by the constructor of your derived class.  
  
 If your class is serializable (it incorporates the `IMPLEMENT_SERIAL` macro), then you must have a default constructor (a constructor with no arguments) in your class declaration. If you do not need a default constructor, declare a private or protected "empty" constructor. For more information, see [Using CObject](../VS_visualcpp/Using-CObject.md).  
  
 The standard C++ default class copy constructor does a member-by-member copy. The presence of the private `CObject` copy constructor guarantees a compiler error message if the copy constructor of your class is needed but not available. You must therefore provide a copy constructor if your class requires this capability.  
  
### Example  
 See [CObList::CObList](../VS_visualcpp/CObList-Class.md#coblist__coblist) for a listing of the `CAge` class used in the `CObject` examples.  
  
 [!CODE [NVC_MFCCObjectSample#8](../CodeSnippet/VS_Snippets_Cpp/NVC_MFCCObjectSample#8)]  
  
##  <a name="cobject__dump"></a>  CObject::Dump  
 Dumps the contents of your object to a [CDumpContext](../VS_visualcpp/CDumpContext-Class.md) object.  
  
```  
virtual void Dump( CDumpContext& dc ) const;  
```  
  
### Parameters  
 `dc`  
 The diagnostic dump context for dumping, usually `afxDump`.  
  
### Remarks  
 When you write your own class, you should override the `Dump` function to provide diagnostic services for yourself and other users of your class. The overridden `Dump` usually calls the `Dump` function of its base class before printing data members unique to the derived class. `CObject::Dump` prints the class name if your class uses the `IMPLEMENT_DYNAMIC` or `IMPLEMENT_SERIAL` macro.  
  
> [!NOTE]
>  Your `Dump` function should not print a newline character at the end of its output.  
  
 `Dump` calls make sense only in the Debug version of the Microsoft Foundation Class Library. You should bracket calls, function declarations, and function implementations with **#ifdef _DEBUG**/ `#endif` statements for conditional compilation.  
  
 Since `Dump` is a **const** function, you are not permitted to change the object state during the dump.  
  
 The [CDumpContext insertion (<<) operator](../VS_visualcpp/CDumpContext-Class.md#cdumpcontext__operator__lt__lt_) calls `Dump` when a `CObject` pointer is inserted.  
  
 `Dump` permits only "acyclic" dumping of objects. You can dump a list of objects, for example, but if one of the objects is the list itself, you will eventually overflow the stack.  
  
### Example  
 See [CObList::CObList](../VS_visualcpp/CObList-Class.md#coblist__coblist) for a listing of the `CAge` class used in all `CObject` examples.  
  
 [!CODE [NVC_MFCCObjectSample#9](../CodeSnippet/VS_Snippets_Cpp/NVC_MFCCObjectSample#9)]  
  
##  <a name="cobject__getruntimeclass"></a>  CObject::GetRuntimeClass  
 Returns the `CRuntimeClass` structure corresponding to this object's class.  
  
```  
virtual CRuntimeClass* GetRuntimeClass() const;  
```  
  
### Return Value  
 A pointer to the [CRuntimeClass](../VS_visualcpp/CRuntimeClass-Structure.md) structure corresponding to this object's class; never **NULL**.  
  
### Remarks  
 There is one `CRuntimeClass` structure for each `CObject`-derived class. The structure members are as follows:  
  
-   **LPCSTR m_lpszClassName** A null-terminated string containing the ASCII class name.  
  
-   **int m_nObjectSize** The size of the object, in bytes. If the object has data members that point to allocated memory, the size of that memory is not included.  
  
-   **UINT m_wSchema** The schema number ( – 1 for nonserializable classes). See the [IMPLEMENT_SERIAL](../Topic/IMPLEMENT_SERIAL.md) macro for a description of schema number.  
  
-   **CObject\* ( PASCAL\* m_pfnCreateObject )( )** A function pointer to the default constructor that creates an object of your class (valid only if the class supports dynamic creation; otherwise, returns **NULL**).  
  
-   **CRuntimeClass\* ( PASCAL\* m_pfn_GetBaseClass )( )** If your application is dynamically linked to the AFXDLL version of MFC, a pointer to a function that returns the `CRuntimeClass` structure of the base class.  
  
-   **CRuntimeClass\* m_pBaseClass** If your application is statically linked to MFC, a pointer to the `CRuntimeClass` structure of the base class.  
  
 This function requires use of the [IMPLEMENT_DYNAMIC](../Topic/IMPLEMENT_DYNAMIC.md), [IMPLEMENT_DYNCREATE](../Topic/IMPLEMENT_DYNCREATE.md), or [IMPLEMENT_SERIAL](../Topic/IMPLEMENT_SERIAL.md) macro in the class implementation. You will get incorrect results otherwise.  
  
### Example  
 See [CObList::CObList](../VS_visualcpp/CObList-Class.md#coblist__coblist) for a listing of the `CAge` class used in all `CObject` examples.  
  
 [!CODE [NVC_MFCCObjectSample#10](../CodeSnippet/VS_Snippets_Cpp/NVC_MFCCObjectSample#10)]  
  
##  <a name="cobject__iskindof"></a>  CObject::IsKindOf  
 Tests this object's relationship to a given class.  
  
```  
BOOL IsKindOf( const CRuntimeClass* pClass ) const;  
```  
  
### Parameters  
 `pClass`  
 A pointer to a [CRuntimeClass](../VS_visualcpp/CRuntimeClass-Structure.md) structure associated with your `CObject`-derived class.  
  
### Return Value  
 Nonzero if the object corresponds to the class; otherwise 0.  
  
### Remarks  
 This function tests `pClass` to see if (1) it is an object of the specified class or (2) it is an object of a class derived from the specified class. This function works only for classes declared with the [DECLARE_DYNAMIC](../Topic/DECLARE_DYNAMIC.md), [DECLARE_DYNCREATE](../Topic/DECLARE_DYNCREATE.md), or [DECLARE_SERIAL](../Topic/DECLARE_SERIAL.md) macro.  
  
 Do not use this function extensively because it defeats the C++ polymorphism feature. Use virtual functions instead.  
  
### Example  
 See [CObList::CObList](../VS_visualcpp/CObList-Class.md#coblist__coblist) for a listing of the `CAge` class used in all `CObject` examples.  
  
 [!CODE [NVC_MFCCObjectSample#11](../CodeSnippet/VS_Snippets_Cpp/NVC_MFCCObjectSample#11)]  
  
##  <a name="cobject__isserializable"></a>  CObject::IsSerializable  
 Tests whether this object is eligible for serialization.  
  
```  
BOOL IsSerializable() const;  
```  
  
### Return Value  
 Nonzero if this object can be serialized; otherwise 0.  
  
### Remarks  
 For a class to be serializable, its declaration must contain the [DECLARE_SERIAL](../Topic/DECLARE_SERIAL.md) macro, and the implementation must contain the [IMPLEMENT_SERIAL](../Topic/IMPLEMENT_SERIAL.md) macro.  
  
> [!NOTE]
>  Do not override this function.  
  
### Example  
 See [CObList::CObList](../VS_visualcpp/CObList-Class.md#coblist__coblist) for a listing of the `CAge` class used in all `CObject` examples.  
  
 [!CODE [NVC_MFCCObjectSample#12](../CodeSnippet/VS_Snippets_Cpp/NVC_MFCCObjectSample#12)]  
  
##  <a name="cobject__operator_delete"></a>  CObject::operator delete  
 For the Release version of the library, operator **delete** frees the memory allocated by operator **new**.  
  
```  
void PASCAL operator delete(  
    void* p );  
  
void PASCAL operator delete(  
    void* p, void* pPlace );  
  
void PASCAL operator delete(  
    void* p,  
    LPCSTR lpszFileName,  
    int nLine );  
```  
  
### Remarks  
 In the Debug version, operator **delete** participates in an allocation-monitoring scheme designed to detect memory leaks.  
  
 If you use the code line  
  
 [!CODE [NVC_MFCCObjectSample#14](../CodeSnippet/VS_Snippets_Cpp/NVC_MFCCObjectSample#14)]  
  
 before any of your implementations in a .CPP file, then the third version of **delete** will be used, storing the filename and line number in the allocated block for later reporting. You do not have to worry about supplying the extra parameters; a macro takes care of that for you.  
  
 Even if you do not use `DEBUG_NEW` in Debug mode, you still get leak detection, but without the source-file line-number reporting described above.  
  
 If you override operators **new** and **delete**, you forfeit this diagnostic capability.  
  
### Example  
 See [CObList::CObList](../VS_visualcpp/CObList-Class.md#coblist__coblist) for a listing of the `CAge` class used in the `CObject` examples.  
  
 [!CODE [NVC_MFCCObjectSample#15](../CodeSnippet/VS_Snippets_Cpp/NVC_MFCCObjectSample#15)]  
  
##  <a name="cobject__operator_new"></a>  CObject::operator new  
 For the Release version of the library, operator **new** performs an optimal memory allocation in a manner similar to `malloc`.  
  
```  
void* PASCAL operator new(  
    size_t nSize );  
  
void* PASCAL operator new(  
    size_t,  
    void* p );  
  
void* PASCAL operator new(  
    size_t nSize,  
    LPCSTR lpszFileName,  
    int nLine );  
```  
  
### Remarks  
 In the Debug version, operator **new** participates in an allocation-monitoring scheme designed to detect memory leaks.  
  
 If you use the code line  
  
 [!CODE [NVC_MFCCObjectSample#14](../CodeSnippet/VS_Snippets_Cpp/NVC_MFCCObjectSample#14)]  
  
 before any of your implementations in a .CPP file, then the second version of **new** will be used, storing the filename and line number in the allocated block for later reporting. You do not have to worry about supplying the extra parameters; a macro takes care of that for you.  
  
 Even if you do not use `DEBUG_NEW` in Debug mode, you still get leak detection, but without the source-file line-number reporting described above.  
  
> [!NOTE]
>  If you override this operator, you must also override **delete**. Do not use the standard library **_new_handler** function.  
  
### Example  
 See [CObList::CObList](../VS_visualcpp/CObList-Class.md#coblist__coblist) for a listing of the `CAge` class used in the `CObject` examples.  
  
 [!CODE [NVC_MFCCObjectSample#16](../CodeSnippet/VS_Snippets_Cpp/NVC_MFCCObjectSample#16)]  
  
##  <a name="cobject__serialize"></a>  CObject::Serialize  
 Reads or writes this object from or to an archive.  
  
```  
virtual void Serialize( CArchive& ar );  
```  
  
### Parameters  
 `ar`  
 A `CArchive` object to serialize to or from.  
  
### Remarks  
 You must override `Serialize` for each class that you intend to serialize. The overridden `Serialize` must first call the `Serialize` function of its base class.  
  
 You must also use the [DECLARE_SERIAL](../Topic/DECLARE_SERIAL.md) macro in your class declaration, and you must use the [IMPLEMENT_SERIAL](../Topic/IMPLEMENT_SERIAL.md) macro in the implementation.  
  
 Use [CArchive::IsLoading](../VS_visualcpp/CArchive-Class.md#carchive__isloading) or [CArchive::IsStoring](../VS_visualcpp/CArchive-Class.md#carchive__isstoring) to determine whether the archive is loading or storing.  
  
 `Serialize` is called by [CArchive::ReadObject](../VS_visualcpp/CArchive-Class.md#carchive__readobject) and [CArchive::WriteObject](../VS_visualcpp/CArchive-Class.md#carchive__writeobject). These functions are associated with the `CArchive` insertion operator ( **<<**) and extraction operator ( **>>**).  
  
 For serialization examples, see the article [Serialization: Serializing an Object](../VS_visualcpp/Serialization--Serializing-an-Object.md).  
  
### Example  
 See [CObList::CObList](../VS_visualcpp/CObList-Class.md#coblist__coblist) for a listing of the `CAge` class used in all `CObject` examples.  
  
 [!CODE [NVC_MFCCObjectSample#13](../CodeSnippet/VS_Snippets_Cpp/NVC_MFCCObjectSample#13)]  
  
## See Also  
 [Hierarchy Chart](../VS_visualcpp/Hierarchy-Chart.md)