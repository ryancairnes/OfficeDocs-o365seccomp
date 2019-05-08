---
title: "Supported file types in Advanced eDiscovery"
ms.author: markjjo
author: markjjo
manager: laurawi
ms.date: 
ms.audience: Admin
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
ms.collection: M365-security-compliance
search.appverid: 
- MOE150
- MET150
ms.assetid: 

description: ""
---

# Supported file types in Advanced eDiscovery

Advance eDiscovery (Preview) supports many file types to many different levels, which are described in the following table. This list isn't finalized, and we'll add new file types as we continue our validation testing. The table also indicates if a file type can be viewed in the available viewers in Advance eDiscovery (Preview).

| Mime type | Description | Native viewer | Text viewer | Annotate viewer | Container extraction | Extensions |
| :- | :- | :- | :- | :- | :- | :- |
| application/mbox | Archive / Container |  |  |  | Yes | .mbox |
| application/msword | Productivity | Yes | Yes | Yes |  | .doc; .dat |
| application/pdf | Productivity | Yes | Yes | Yes |  | .pdf |
| application/rtf | Document | Yes | Yes | Yes |  | .rtf;.doc |
| application/vnd.ms-excel | Productivity | Yes | Yes | Yes |  | .xls; .dat |
| application/vnd.ms-excel.sheet.binary.macroenabled.12 | Productivity | Yes | Yes | No |  | .xlsb |
| application/vnd.ms-excel.sheet.macroenabled.12 | Productivity | Yes | Yes | Yes |  | .xlsm |
| application/vnd.ms-excel.template.macroenabled.12 | Productivity | No | Yes | No |  | .xltm |
| application/vnd.ms-outlook | Collaboration | Yes | Yes | Yes |  | .msg |
| application/vnd.ms-outlook-pst | Archive / Container |  |  |  | Yes | .pst |
| application/vnd.ms-powerpoint | Productivity | Yes | Yes | Yes |  | .ppt; .pps;.pot |
| application/vnd.ms-word.document.macroenabled.12 | Productivity | Yes | Yes | Yes |  | .docm |
| application/vnd.ms-word.template.macroenabled.12 | Productivity | Yes | Yes | Yes |  | .dotm |
| application/vnd.oasis.opendocument.text | Productivity | Yes | Yes | Yes |  | .odt;  |
| application/vnd.openxmlformats-officedocument.presentationml.presentation | Productivity | Yes | Yes | Yes |  | .pptx |
| application/vnd.openxmlformats-officedocument.presentationml.slideshow | Productivity | Yes | Yes | Yes |  | .ppsx |
| application/vnd.openxmlformats-officedocument.presentationml.template | Productivity | Yes | Yes | Yes |  | .potx |
| application/vnd.openxmlformats-officedocument.spreadsheetml.sheet | Productivity | Yes | Yes | Yes |  | .xlsx |
| application/vnd.openxmlformats-officedocument.spreadsheetml.template | Productivity | Yes | Yes | Yes |  | .xltx |
| application/vnd.openxmlformats-officedocument.wordprocessingml.document | Productivity | Yes | Yes | Yes |  | .docx |
| application/vnd.openxmlformats-officedocument.wordprocessingml.template | Productivity | Yes | Yes | Yes |  | .dotx |
| application/vnd.visio | Productivity | Yes | Yes | Yes |  | .vsd |
| application/x-7z-compressed | Archive / Container |  |  |  | Yes | .7z |
| application/xhtml+xml | Document | Yes | Yes | Yes |  | .xhtml |
| application/xml | Document | Yes | Yes | Yes |  | .xml |
| application/x-msaccess | Productivity | Yes | Yes | Yes |  | .mdb |
| application/x-mspublisher | Productivity | Yes | Yes | Yes |  | .pub |
| application/x-rar-compressed | Archive / Container |  |  |  | Yes | .rar |
| application/x-tar | Archive / Container |  |  |  | Yes | .tar |
| application/zip | Archive / Container |  |  |  | Yes | .zip |
| image/bmp | Image | Yes | Yes | Yes |  | .bmp |
| image/emf | Image | Yes | Yes | Yes |  | .emf |
| image/gif | Image | Yes | Yes | Yes |  | .gif |
| image/jpeg | Image | Yes | Yes | Yes |  | .jpg; .jpeg; .dat;.jpgt |
| image/png | Image | Yes | Yes | Yes |  | .png |
| image/tiff | Image | Yes | Yes | Yes |  | .tif |
| image/vnd.dwg | Drawings | Yes | Yes | Yes |  | .dwg;.dxf; |
| image/wmf | Document | Yes | Yes | Yes |  | .wmf |
| message/rfc822 | Collaboration | Yes | Yes | Yes |  | .eml |
| text/csv | Document | Yes | Yes | Yes |  | .csv |
| text/html | Document | Yes | Yes | Yes |  | .html;.shtml; .htm |
| text/plain | Document | Yes | Yes | Yes |  | .txt; .css;.con; .pl; .csv; .dat |
| text/vcard-contact | Collaboration | Yes | Yes | Yes |  | .vcf |
||||||||
