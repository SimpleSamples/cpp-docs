---
title: "Command Macros and Options Macros"
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
ms.topic: article
ms.assetid: 50dff03c-0dc3-4a8a-9a17-57e0e4ea9bac
caps.latest.revision: 7
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
# Command Macros and Options Macros
Command macros are predefined for Microsoft products. Options macros represent options to these products and are undefined by default. Both are used in predefined inference rules and can be used in description blocks or user-defined inference rules. Command macros can be redefined to represent part or all of a command line, including options. Options macros generate a null string if left undefined.  
  
|Microsoft product|Command macro|Defined as|Options macro|  
|-----------------------|-------------------|----------------|-------------------|  
|Macro Assembler|**AS**|ml|**AFLAGS**|  
|Basic Compiler|**BC**|bc|**BFLAGS**|  
|C Compiler|**CC**|cl|**CFLAGS**|  
|C++ Compiler|**CPP**|cl|**CPPFLAGS**|  
|C++ Compiler|**CXX**|cl|**CXXFLAGS**|  
|Resource Compiler|**RC**|rc|**RFLAGS**|  
  
## See Also  
 [Special NMAKE Macros](../VS_visualcpp/Special-NMAKE-Macros.md)