---
title: "ATL Typedefs"
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
ms.topic: index-page 
ms.assetid: 7dd05baa-3efb-4e3b-af23-793c610f4560
caps.latest.revision: 15
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
# ATL Typedefs
The Active Template Library includes the following typedefs.  
  
|||  
|-|-|  
|[_ATL_BASE_MODULE](../Topic/_ATL_BASE_MODULE.md)|Defined as a typedef based on                             [_ATL_BASE_MODULE70](../VS_visualcpp/_ATL_BASE_MODULE70-Structure.md).|  
|[_ATL_COM_MODULE](../Topic/_ATL_COM_MODULE.md)|Defined as a typedef based on                             [_ATL_COM_MODULE70](../VS_visualcpp/_ATL_COM_MODULE70-Structure.md).|  
|[_ATL_MODULE](../Topic/_ATL_MODULE.md)|Defined as a typedef based on                             [_ATL_MODULE70](../VS_visualcpp/_ATL_MODULE70-Structure.md).|  
|[_ATL_WIN_MODULE](../Topic/_ATL_WIN_MODULE.md)|Defined as a typedef based on                             [_ATL_WIN_MODULE70](../VS_visualcpp/_ATL_WIN_MODULE70-Structure.md)|  
|[ATL_URL_PORT](../Topic/ATL_URL_PORT.md)|The type used by                             [CUrl](../VS_visualcpp/CUrl-Class.md) for specifying a port number.|  
|[CComDispatchDriver](../Topic/CComDispatchDriver.md)|This class manages COM interface pointers.|  
|[CComGlobalsThreadModel](../Topic/CComGlobalsThreadModel.md)|Calls the appropriate thread model methods, regardless of the threading model being used.|  
|[CComObjectThreadModel](../Topic/CComObjectThreadModel.md)|Calls the appropriate thread model methods, regardless of the threading model being used.|  
|[CContainedWindow](../Topic/CContainedWindow.md)|This class is a specialization of                             **CContainedWindowT.**|  
|[CPath](../Topic/CPath.md)|A specialization of                             [CPathT](../VS_visualcpp/CPathT-Class.md) using                             `CString`.|  
|[CPathA](../Topic/CPathA.md)|A specialization of                             [CPathT](../VS_visualcpp/CPathT-Class.md) using                             `CStringA`.|  
|[CPathW](../Topic/CPathW.md)|A specialization of                             [CPathT](../VS_visualcpp/CPathT-Class.md) using                             `CStringW`.|  
|[CSimpleValArray](../Topic/CSimpleValArray.md)|Represents an array for storing simple types.|  
|[DefaultThreadTraits](../VS_visualcpp/ATL-Typedefs.md)|The default thread traits class.|  
|[LPCURL](../Topic/LPCURL.md)|A pointer to a constant                             [CUrl](../VS_visualcpp/CUrl-Class.md) object.|  
|[LPURL](../Topic/LPURL.md)|A pointer to a                             [CUrl](../VS_visualcpp/CUrl-Class.md) object.|  
  
##  <a name="_atl_base_module"></a>  _ATL_BASE_MODULE  
 Defined as a typedef based on _ATL_BASE_MODULE70.  
  
```  
  
typedef ATL::_ATL_BASE_MODULE70 _ATL_BASE_MODULE;  
  
```  
  
### Remarks  
 Used in every ATL project. Based on                         [_ATL_BASE_MODULE70](../VS_visualcpp/_ATL_BASE_MODULE70-Structure.md).  
  
 Classes that are part of the ATL 7.0 Module Classes derive from the _ATL_BASE_MODULE structure.  For more information on ATL Module Classes, refer to                         [COM Modules Classes](../VS_visualcpp/COM-Modules-Classes.md).  
  
##  <a name="_atl_com_module"></a>  _ATL_COM_MODULE  
 Defined as a typedef based on _ATL_COM_MODULE70.  
  
```  
  
typedef ATL::_ATL_COM_MODULE70 _ATL_COM_MODULE;  
  
```  
  
### Remarks  
 Used by ATL projects which use COM features. Based on                         [_ATL_COM_MODULE70](../VS_visualcpp/_ATL_COM_MODULE70-Structure.md).  
  
##  <a name="_atl_module"></a>  _ATL_MODULE  
 Defined as a typedef based on _ATL_MODULE70.  
  
```  
  
typedef ATL::_ATL_MODULE70 _ATL_MODULE;  
  
```  
  
### Remarks  
 Based on                         [_ATL_MODULE70](../VS_visualcpp/_ATL_MODULE70-Structure.md).  
  
##  <a name="_atl_win_module"></a>  _ATL_WIN_MODULE  
 Defined as a typedef based on _ATL_WIN_MODULE70.  
  
```  
  
typedef ATL::_ATL_WIN_MODULE70 _ATL_WIN_MODULE;  
  
```  
  
### Remarks  
 Used by any ATL projects which use windowing features. Based on                         [_ATL_WIN_MODULE70](../VS_visualcpp/_ATL_WIN_MODULE70-Structure.md).  
  
##  <a name="ccomdispatchdriver"></a>  CComDispatchDriver  
 This class manages COM interface pointers.  
  
```  
  
typedef CComQIPtr<IDispatch, &__uuidof(IDispatch)> CComDispatchDriver;  
  
```  
  
##  <a name="ccomglobalsthreadmodel"></a>  CComGlobalsThreadModel  
 Calls the appropriate thread model methods, regardless of the threading model being used.  
  
```  
  
#if defined( _ATL_SINGLE_THREADED )  
typedef CComSingleThreadModel CComGlobalsThreadModel;  
#elif defined( _ATL_APARTMENT_THREADED )  
typedef CComMultiThreadModel CComGlobalsThreadModel;  
#elif defined( _ATL_FREE_THREADED )  
typedef CComMultiThreadModel CComGlobalsThreadModel;  
#else  
#pragma message ("No global threading model defined")  
#endif  
  
```  
  
### Remarks  
 Depending on the threading model used by your application, the                         `typedef` name                         `CComGlobalsThreadModel` references either                         [CComSingleThreadModel](../VS_visualcpp/CComSingleThreadModel-Class.md) or                         [CComMultiThreadModel](../VS_visualcpp/CComMultiThreadModel-Class.md). These classes provide additional                         `typedef` names to reference a critical section class.  
  
> [!NOTE]
>  `CComGlobalsThreadModel` does not reference class                             [CComMultiThreadModelNoCS](../VS_visualcpp/CComMultiThreadModelNoCS-Class.md).  
  
 Using                         `CComGlobalsThreadModel` frees you from specifying a particular threading model class. Regardless of the threading model being used, the appropriate methods will be called.  
  
 In addition to                         `CComGlobalsThreadModel`, ATL provides the                         `typedef` name                         [CComObjectThreadModel](../Topic/CComObjectThreadModel.md). The class referenced by each                         `typedef` depends on the threading model used, as shown in the following table:  
  
|typedef|Single threading|Apartment threading|Free threading|  
|-------------|----------------------|-------------------------|--------------------|  
|`CComObjectThreadModel`|S|S|M|  
|`CComGlobalsThreadModel`|S|M|M|  
  
 S=                        `CComSingleThreadModel`; M=                        `CComMultiThreadModel`  
  
 Use                         `CComObjectThreadModel` within a single object class. Use                         `CComGlobalsThreadModel` in an object that is globally available to your program, or when you want to protect module resources across multiple threads.  
  
##  <a name="ccomobjectthreadmodel"></a>  CComObjectThreadModel  
 Calls the appropriate thread model methods, regardless of the threading model being used.  
  
```  
  
#if defined( _ATL_SINGLE_THREADED )  
typedef CComSingleThreadModel CComObjectThreadModel;  
#elif defined( _ATL_APARTMENT_THREADED )  
typedef CComSingleThreadModel CComObjectThreadModel;  
#elif defined( _ATL_FREE_THREADED )  
typedef CComMultiThreadModel CComObjectThreadModel;  
#else  
#pragma message ("No global threading model defined")  
#endif  
  
```  
  
### Remarks  
 Depending on the threading model used by your application, the                         `typedef` name                         `CComObjectThreadModel` references either                         [CComSingleThreadModel](../VS_visualcpp/CComSingleThreadModel-Class.md) or                         [CComMultiThreadModel](../VS_visualcpp/CComMultiThreadModel-Class.md). These classes provide additional                         `typedef` names to reference a critical section class.  
  
> [!NOTE]
>  `CComObjectThreadModel` does not reference class                             [CComMultiThreadModelNoCS](../VS_visualcpp/CComMultiThreadModelNoCS-Class.md).  
  
 Using                         `CComObjectThreadModel` frees you from specifying a particular threading model class. Regardless of the threading model being used, the appropriate methods will be called.  
  
 In addition to                         `CComObjectThreadModel`, ATL provides the                         `typedef` name                         [CComGlobalsThreadModel](../Topic/CComGlobalsThreadModel.md). The class referenced by each                         `typedef` depends on the threading model used, as shown in the following table:  
  
|typedef|Single threading|Apartment threading|Free threading|  
|-------------|----------------------|-------------------------|--------------------|  
|`CComObjectThreadModel`|S|S|M|  
|`CComGlobalsThreadModel`|S|M|M|  
  
 S=                        `CComSingleThreadModel`; M=                        `CComMultiThreadModel`  
  
 Use                         `CComObjectThreadModel` within a single object class. Use                         `CComGlobalsThreadModel` in an object that is either globally available to your program, or when you want to protect module resources across multiple threads.  
  
##  <a name="ccontainedwindow"></a>  CContainedWindow  
 This class is a specialization of                 **CContainedWindowT.**  
  
```  
  
typedef CContainedWindowT<CWindow> CContainedWindow;  
  
```  
  
### Remarks  
 `CContainedWindow` is a specialization of                         [CContainedWindowT](../VS_visualcpp/CContainedWindowT-Class.md). If you want to change the base class or traits, use                         `CContainedWindowT` directly.  
  
##  <a name="cpath"></a>  CPath  
 A specialization of                 [CPathT](../VS_visualcpp/CPathT-Class.md) using                 `CString`.  
  
```  
  
typedef CPathT< CString > CPath;  
  
```  
  
##  <a name="cpatha"></a>  CPathA  
 A specialization of                 [CPathT](../VS_visualcpp/CPathT-Class.md) using                 `CStringA`.  
  
```  
  
typedef CPathT< CStringA > CPathA;  
  
```  
  
##  <a name="cpathw"></a>  CPathW  
 A specialization of                 [CPathT](../VS_visualcpp/CPathT-Class.md) using                 `CStringW`.  
  
```  
  
typedef ATL::CPathT< CStringW > CPathW;  
  
```  
  
##  <a name="csimplevalarray"></a>  CSimpleValArray  
 Represents an array for storing simple types.  
  
```  
  
#define CSimpleValArray CSimpleArray  
  
```  
  
### Remarks  
 `CSimpleValArray` is provided for creating and managing arrays containing simple data types. It is a simple #define of                         [CSimpleArray](../VS_visualcpp/CSimpleArray-Class.md).  
  
##  <a name="lpcurl"></a>  LPCURL  
 A pointer to a constant                 [CUrl](../VS_visualcpp/CUrl-Class.md) object.  
  
```  
  
typedef const CUrl * LPCURL;  
  
```  
  
##  <a name="lpurl"></a>  LPURL  
 A pointer to a                 [CUrl](../VS_visualcpp/CUrl-Class.md) object.  
  
```  
  
typedef CUrl* LPURL;  
  
```  
  
## See Also  
 [ATL COM Desktop Components](../VS_visualcpp/ATL-COM-Desktop-Components.md)   
 [Functions](../VS_visualcpp/ATL-Functions.md)   
 [Global Variables](../VS_visualcpp/ATL-Global-Variables.md)   
 [Structures](../VS_visualcpp/ATL-Structures.md)   
 [Macros](../VS_visualcpp/ATL-Macros.md)   
 [Classes](../VS_visualcpp/ATL-Classes.md)