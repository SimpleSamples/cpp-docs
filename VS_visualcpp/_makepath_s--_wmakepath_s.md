---
title: "_makepath_s, _wmakepath_s"
ms.custom: na
ms.date: 10/03/2016
ms.devlang: 
  - C++
  - C
ms.prod: visual-studio-dev14
ms.reviewer: na
ms.suite: na
ms.technology: 
  - devlang-cpp
ms.tgt_pltfrm: na
ms.topic: article
apiname: 
  - _wmakepath_s
  - _makepath_s
apilocation: 
  - msvcrt.dll
  - msvcr80.dll
  - msvcr90.dll
  - msvcr100.dll
  - msvcr100_clr0400.dll
  - msvcr110.dll
  - msvcr110_clr0400.dll
  - msvcr120.dll
  - msvcr120_clr0400.dll
  - ucrtbase.dll
  - api-ms-win-crt-filesystem-l1-1-0.dll
apitype: DLLExport
ms.assetid: 4405e43c-3d63-4697-bb80-9b8dcd21d027
caps.latest.revision: 29
manager: ghogen
translation.priority.ht: 
  - de-de
  - es-es
  - fr-fr
  - it-it
  - ja-jp
  - ko-kr
  - ru-ru
  - zh-cn
  - zh-tw
translation.priority.mt: 
  - cs-cz
  - pl-pl
  - pt-br
  - tr-tr
---
# _makepath_s, _wmakepath_s
Creates a path name from components. These are versions of [_makepath, _wmakepath](../VS_visualcpp/_makepath--_wmakepath.md) with security enhancements as described in [Security Features in the CRT](../VS_visualcpp/Security-Features-in-the-CRT.md).  
  
## Syntax  
  
```  
errno_t _makepath_s(  
   char *path,  
   size_t sizeInBytes,  
   const char *drive,  
   const char *dir,  
   const char *fname,  
   const char *ext   
);  
errno_t _wmakepath_s(  
   wchar_t *path,  
   size_t sizeInWords,  
   const wchar_t *drive,  
   const wchar_t *dir,  
   const wchar_t *fname,  
   const wchar_t *ext   
);  
template <size_t size>  
errno_t _makepath_s(  
   char (&path)[size],  
   const char *drive,  
   const char *dir,  
   const char *fname,  
   const char *ext   
); // C++ only  
template <size_t size>  
errno_t _wmakepath_s(  
   wchar_t (&path)[size],  
   const wchar_t *drive,  
   const wchar_t *dir,  
   const wchar_t *fname,  
   const wchar_t *ext   
); // C++ only  
```  
  
#### Parameters  
 [out] `path`  
 Full path buffer.  
  
 [in] `sizeInWords`  
 Size of the buffer in words.  
  
 [in] `sizeInBytes`  
 Size of the buffer in bytes.  
  
 [in] `drive`  
 Contains a letter (A, B, and so on) corresponding to the desired drive and an optional trailing colon. `_makepath_s` inserts the colon automatically in the composite path if it is missing. If `drive` is `NULL` or points to an empty string, no drive letter appears in the composite `path` string.  
  
 [in] `dir`  
 Contains the path of directories, not including the drive designator or the actual file name. The trailing slash is optional, and either a forward slash (/) or a backslash (\\) or both might be used in a single `dir` argument. If no trailing slash (/ or \\) is specified, it is inserted automatically. If `dir` is `NULL` or points to an empty string, no directory path is inserted in the composite `path` string.  
  
 [in] `fname`  
 Contains the base file name without any file name extensions. If `fname` is `NULL` or points to an empty string, no filename is inserted in the composite `path` string.  
  
 [in] `ext`  
 Contains the actual file name extension, with or without a leading period (.). `_makepath_s` inserts the period automatically if it does not appear in `ext`. If `ext` is `NULL` or points to an empty string, no extension is inserted in the composite `path` string.  
  
## Return Value  
 Zero if successful; an error code on failure.  
  
### Error Conditions  
  
|`path`|`sizeInWords` / `sizeInBytes`|Return|Contents of `path`|  
|------------|------------------------------------|------------|------------------------|  
|`NULL`|any|`EINVAL`|not modified|  
|any|<= 0|`EINVAL`|not modified|  
  
 If any of the above error conditions occurs, these functions invoke the invalid parameter handler, as described in [Parameter Validation](../VS_visualcpp/Parameter-Validation.md). If execution is allowed to continue, `errno` is set to`EINVAL` and the functions returns`EINVAL`**.** `NULL` is allowed for the parameters `drive`, `fname`, and `ext`. For information about the behavior when these parameters are null pointers or empty strings, see the Remarks section.  
  
## Remarks  
 The `_makepath_s` function creates a composite path string from individual components, storing the result in `path`. The `path` might include a drive letter, directory path, file name, and file name extension. `_wmakepath_s` is a wide-character version of `_makepath_s`; the arguments to `_wmakepath_s` are wide-character strings. `_wmakepath_s` and `_makepath_s` behave identically otherwise.  
  
### Generic-Text Routine Mappings  
  
|Tchar.h routine|_UNICODE and _MBCS not defined|_MBCS defined|_UNICODE defined|  
|---------------------|--------------------------------------|--------------------|-----------------------|  
|`_tmakepath_s`|`_makepath_s`|`_makepath_s`|`_wmakepath_s`|  
  
 The `path` argument must point to an empty buffer large enough to hold the complete path. The composite `path` must be no larger than the `_MAX_PATH` constant, defined in Stdlib.h.  
  
 If path is `NULL`, the invalid parameter handler is invoked, as described in [Parameter Validation](../VS_visualcpp/Parameter-Validation.md). In addition, `errno` is set to `EINVAL`. `NULL` values are allowed for all other parameters.  
  
 In C++, using these functions is simplified by template overloads; the overloads can infer buffer length automatically (eliminating the need to specify a size argument) and they can automatically replace older, non-secure functions with their newer, secure counterparts. For more information, see [Secure Template Overloads](../VS_visualcpp/Secure-Template-Overloads.md).  
  
 The debug versions of these functions first fill the buffer with 0xFD. To disable this behavior, use [_CrtSetDebugFillThreshold](../VS_visualcpp/_CrtSetDebugFillThreshold.md).  
  
## Requirements  
  
|Routine|Required header|  
|-------------|---------------------|  
|`_makepath_s`|<stdlib.h>|  
|`_wmakepath_s`|<stdlib.h> or <wchar.h>|  
  
 For more compatibility information, see [Compatibility](../VS_visualcpp/Compatibility.md) in the Introduction.  
  
## Example  
  
```  
// crt_makepath_s.c  
  
#include <stdlib.h>  
#include <stdio.h>  
  
int main( void )  
{  
   char path_buffer[_MAX_PATH];  
   char drive[_MAX_DRIVE];  
   char dir[_MAX_DIR];  
   char fname[_MAX_FNAME];  
   char ext[_MAX_EXT];  
   errno_t err;  
  
   err = _makepath_s( path_buffer, _MAX_PATH, "c", "\\sample\\crt\\",  
                      "crt_makepath_s", "c" );  
   if (err != 0)  
   {  
      printf("Error creating path. Error code %d.\n", err);  
      exit(1);  
   }  
   printf( "Path created with _makepath_s: %s\n\n", path_buffer );  
   err = _splitpath_s( path_buffer, drive, _MAX_DRIVE, dir, _MAX_DIR, fname,  
                       _MAX_FNAME, ext, _MAX_EXT );  
   if (err != 0)  
   {  
      printf("Error splitting the path. Error code %d.\n", err);  
      exit(1);  
   }  
   printf( "Path extracted with _splitpath_s:\n" );  
   printf( "  Drive: %s\n", drive );  
   printf( "  Dir: %s\n", dir );  
   printf( "  Filename: %s\n", fname );  
   printf( "  Ext: %s\n", ext );  
}  
```  
  
## Output  
  
```  
Path created with _makepath_s: c:\sample\crt\crt_makepath_s.c  
  
Path extracted with _splitpath_s:  
  Drive: c:  
  Dir: \sample\crt\  
  Filename: crt_makepath_s  
  Ext: .c  
```  
  
## .NET Framework Equivalent  
 [System::IO::File::Create](https://msdn.microsoft.com/en-us/library/system.io.file.create.aspx)  
  
## See Also  
 [File Handling](../VS_visualcpp/File-Handling.md)   
 [_fullpath, _wfullpath](../VS_visualcpp/_fullpath--_wfullpath.md)   
 [_splitpath_s, _wsplitpath_s](../VS_visualcpp/_splitpath_s--_wsplitpath_s.md)   
 [_makepath, _wmakepath](../VS_visualcpp/_makepath--_wmakepath.md)