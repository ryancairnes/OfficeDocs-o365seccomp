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

Advanced eDiscovery supports many file types in many different ways, which are described in the following tables. This list isn't finalized, and we'll add new file types as we continue our validation testing. These tables indicate if a file type is supported for text extraction (OCR for images), viewable in the Native viewer, available in the Annotate viewer, and the possible extensions for each file type. For container file types (such as PST files and ZIP files), the tables indicate if data in the contain file can be extracted.

## Archive / Container

| Mime type | Container extraction | Possible extensions |
| :- |  :- |  :- | 
| application/x-7z-compressed | Yes | .7z |
| application/x-rar-compressed | Yes | .rar |
| application/x-tar | Yes | .tar |
| application/zip | Yes | .zip |
||||||

## Database

| Mime type | Text extraction | Native viewer | Annotate viewer | Possible extensions |
| :- |  :- |  :- |  :- |  :- | 
| application/x-msaccess | Yes | Yes | Yes | .mdb |
||||||

## Email

| Mime type | Text extraction | Native viewer | Annotate viewer | Possible extensions |
| :- |  :- |  :- |  :- |  :- | 
| application/vnd.ms-outlook | Yes | Yes | Yes | .msg |
| message/rfc822 | Yes | Yes | Yes | .eml |
| text/vcard-contact | Yes | Yes | Yes | .vcf |
||||||

## Email Container

| Mime type | Container extraction | Possible extensions |
| :- |  :- |  :- | 
| application/mbox | Yes | .mbox |
| application/vnd.ms-outlook-pst | Yes | .pst |
||||||

## HTML

| Mime type | Text extraction | Native viewer | Annotate viewer | Possible extensions |
| :- |  :- |  :- |  :- |  :- | 
| application/xhtml+xml | Yes | Yes | Yes | .xhtml |
| application/xml | Yes | Yes | Yes | .xml |
| text/html | Yes | Yes | Yes | .htm; .html; .shtml |
||||||

## Image

| Mime type | OCR Text extraction | Native viewer | Annotate viewer | Possible extensions |
| :- |  :- |  :- |  :- |  :- | 
| image/bmp | Yes | Yes | Yes | .bmp |
| image/emf | Yes | Yes | Yes | .emf |
| image/gif | Yes | Yes | Yes | .gif |
| image/jpeg | Yes | Yes | Yes | .jpeg; .jpg |
| image/png | Yes | Yes | Yes | .png |
| image/tiff | Yes | Yes | Yes | .tif |
| image/vnd.dwg | Yes | Yes | Yes | .dwg; .dxf |
| image/wmf | Yes | Yes | Yes | .wmf |
||||||

## Microsoft Excel

| Mime type | Text extraction | Native viewer | Annotate viewer | Possible extensions |
| :- |  :- |  :- |  :- |  :- | 
| application/vnd.ms-excel | Yes | Yes | Yes | .dat; .xls |
| application/vnd.ms-excel.sheet.binary.macroenabled.12 | Yes | Yes | No | .xlsb |
| application/vnd.ms-excel.sheet.macroenabled.12 | Yes | Yes | Yes | .xlsm |
| application/vnd.ms-excel.template.macroenabled.12 | Yes | No | No | .xltm |
||||||

## Microsoft Powerpoint

| Mime type | Text extraction | Native viewer | Annotate viewer | Possible extensions |
| :- |  :- |  :- |  :- |  :- | 
| application/vnd.ms-powerpoint | Yes | Yes | Yes | .pot; .pps; .ppt |
||||||

## Microsoft Publisher

| Mime type | Text extraction | Native viewer | Annotate viewer | Possible extensions |
| :- |  :- |  :- |  :- |  :- | 
| application/x-mspublisher | Yes | Yes | Yes | .pub |
||||||

## Microsoft Visio

| Mime type | Text extraction | Native viewer | Annotate viewer | Possible extensions |
| :- |  :- |  :- |  :- |  :- | 
| application/vnd.visio | Yes | Yes | Yes | .vsd |
||||||

## Microsoft Word

| Mime type | Text extraction | Native viewer | Annotate viewer | Possible extensions |
| :- |  :- |  :- |  :- |  :- | 
| application/msword | Yes | Yes | Yes | .dat; .doc |
| application/rtf | Yes | Yes | Yes | .doc; .rtf |
| application/vnd.ms-word.document.macroenabled.12 | Yes | Yes | Yes | .docm |
| application/vnd.ms-word.template.macroenabled.12 | Yes | Yes | Yes | .dotm |
| application/vnd.openxmlformats-officedocument.presentationml.presentation | Yes | Yes | Yes | .pptx |
| application/vnd.openxmlformats-officedocument.presentationml.slideshow | Yes | Yes | Yes | .ppsx |
| application/vnd.openxmlformats-officedocument.presentationml.template | Yes | Yes | Yes | .potx |
| application/vnd.openxmlformats-officedocument.spreadsheetml.sheet | Yes | Yes | Yes | .xlsx |
| application/vnd.openxmlformats-officedocument.spreadsheetml.template | Yes | Yes | Yes | .xltx |
| application/vnd.openxmlformats-officedocument.wordprocessingml.document | Yes | Yes | Yes | .docx |
| application/vnd.openxmlformats-officedocument.wordprocessingml.template | Yes | Yes | Yes | .dotx |
||||||

## Open Document Format

| Mime type | Text extraction | Native viewer | Annotate viewer | Possible extensions |
| :- |  :- |  :- |  :- |  :- | 
| application/vnd.oasis.opendocument.text | Yes | Yes | Yes | .odt |
||||||

## Plain Text

| Mime type | Text extraction | Native viewer | Annotate viewer | Possible extensions |
| :- |  :- |  :- |  :- |  :- | 
| text/csv | Yes | Yes | Yes | .csv |
| text/plain | Yes | Yes | Yes | .con; .css; .csv; .dat; .pl; .txt |
||||||

## Portable Document Format

| Mime type | Text extraction | Native viewer | Annotate viewer | Possible extensions |
| :- |  :- |  :- |  :- |  :- | 
| application/pdf | Yes | Yes | Yes | .pdf |
||||||
