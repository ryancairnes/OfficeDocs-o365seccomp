---
title: "Document metadata fields in Advanced eDiscovery"
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

# Document metadata fields in Advanced eDiscovery

The following table lists the metadata fields for documents in a review set in a case in Advanced eDiscovery. The table indicates the name of the metadata field, whether the field can be searched when running a query in a review set, whether the field is present when viewing the file metadata of a selected document in a review set, and whether the field is included when documents are exported.

| Field name | Searchable field name | Export field name | Display field name | Definition |
| :- |  :- |  :- |  :- |  :- |
| Attachment Content Id | AttachmentContentId |  | Attachment Content Id | Attachment content Id of the item |
| Attachment Names | AttachmentNames | Attachment_Names | Attachment Names | List of names of attachments |
| Attorney client privilege score | AttorneyClientPrivilegeScore |  | Attorney client privilege score | Attorney client privilege score  as calculated for analytics |
| Author | Author | Doc_authors | Author | Author from the document metadata |
| BCC | Bcc | Email_bcc | BCC | Bcc field for for message types.  Format is DisplayName <SmtpAddress> |
| CC | Cc | Email_cc | CC | Cc field for for message types.  Format is DisplayName <SmtpAddress> |
| Compliance labels | ComplianceLabels | Compliance_labels | Compliance labels | Compliance labels applied in Office 365 |
| Compound Path | CompoundPath | Compound_path | Compound Path | Human readable path that describes the source of the item. |
| Content | Content |  |  | Extracted text of the item |
| Conversation Body | Conversation Body |  | Conversation Body | Conversation body of the item |
| Conversation Topic | Conversation Topic |  | Conversation Topic | Conversation topic of the item |
| Conversation ID | ConversationId | Conversation_ID | Conversation ID | Conversation Id from the message |
| Conversation Index |  | Conversation_index | Conversation Index | Conversation index from the message |
| Conversation Pdf Time | ConversationPdfTime |  | Conversation Pdf Time | Date when the PDF version of the conversation was created |
| Conversation Redaction Burn Time | ConversationRedactionBurnTime |  | Conversation Redaction Burn Time | Date when the PDF version of the conversation was created for Chat |
| Document date created | CreatedTime | Doc_date_created | Document date created | Create time from document metadata |
| Custodian | Custodian | Custodian | Custodian | Name of the custodian the items were associated with. |
| Date | Date | Date | Date | Date is a computed field which depends on the file type.<br />Email: Sent date<br />Email Attachments: Last modified date of the document, if not available, the parent's Sent date<br />Embedded documents: Last modified date of the document, if not available, the parent's last modified date.<br />SPO Documents (includes modern attachments): SharePoint Last modified date, if not available, the documents last modified date<br />Non Office Documents: Last modified date<br />Meetings: Meeting start date<br />VoiceMail: Sent date<br />IM: Sent date |
| Other paths | Dedupedcompoundpath | Deduped_compound_path | Other paths | List of CompoundPaths of documents where MD5 or SHA1 hash matches. �Separated by semi-colons |
| Other custodians | DedupedCustodians | Deduped_custodians | Other custodians | List of custodians of documents where MD5 or SHA1 hash matches. Separated by semi-colons |
| Other file IDs | DedupedFileIds | Deduped_file_IDs | Other file IDs | List of FileIds of documents where MD5 or SHA1 hash matches. Separated by semi-colons |
| Document comments | DocComments | Doc_comments | Document comments | Comments from the document metadata |
| Document company |  | Doc_company | Document company | Company from the document metadata |
| DocIndex |  |  |  | The index in the family. -1 or 0 means it is the root. |
| Document keywords |  | Doc_keywords | Document keywords | Keywords from the document metadata |
| Document modified by |  | Doc_modified_by | Document modified by | Last modified by from document metadata |
| Document Revision |  | Doc_revision | Document Revision | Revision from the document metadata |
| Document subject |  | Doc_subject | Document subject | subject from the document metadata |
| Document template |  | Doc_template | Document template | Template from the document metadata |
| Dominant theme | DominantTheme | Dominant_theme | Dominant theme | Dominant theme as calculated for analytics |
| Duplicate subset |  | Duplicate_subset | Duplicate subset | Duplicate subset as calculated for analytics |
| EmailAction |  | Email_action |  | None, Reply, Forward based on the action taken on the message |
| Email Delivery Receipt |  | Email_delivery_receipt | Email Delivery Receipt | Email address supplied in Internet Headers for delivery receipt |
| Importance | EmailImportance | Email_importance | Importance | Importance of the message: 0: Low, 1: Normal, 2: High |
| EmailLevel |  | Email_level |  | Email level calculated for analytics |
| Email Message Id |  | Email_message_ID | Email Message Id | Internet message Id from the message |
| EmailReadReceipt |  | Email_read_receipt |  | Email address supplied in Internet Headers for read receipt |
| Email Security | EmailSecurity | Email_security | Email Security | Security setting of the message: 0: None, 1: Signed, 2: Encrypted, 3: Encrypted and Signed |
| Email Sensitivity | EmailSensitivity | email_sensitivity | Email Sensitivity | Sensitivity setting of the message: 0: None, 1: Personal, 2: Private, 3: CompanyConfidential |
| Email set | EmailSet | Email_set | Email set | Email set calculated for analytics |
| EmailThread |  | Email_thread |  | Email thread calculated for analytics |
| Extracted content type |  | Extracted_content_type | Extracted content type | Extracted content type - in the form of mime type, e.g. image/jpeg |
| ExtractedTextLength |  | Extracted_text_length |  | Number of characters in the extracted text |
| Family relevance score Case issue 1 |  | Family_relevance_score_case_issue_1 |  | Family relevance score Case issue 1 from Relevance |
| FamilyDuplicateSet |  | Family_duplicate_set |  | Family duplicate set calculated for analytics |
| Family ID | FamilyId | Family_ID | Family ID | Family Id groups together all items from and email and it's attachments or a document and embedded items. |
| Family Size |  | Family_size | Family Size | Number of documents in the family |
| File relevance score Case issue 1 |  | File_relevance_score_case_issue_1 |  | File relevance score Case issue 1 from Relevance |
| File class | FileClass | File_class | File class | For content from SharePoint and OneDrive, Document.  For content from Exchange, either Email or Attachment |
| File ID | FileId | File_ID | File ID | The SHA256 hash of the Native File Path |
| File system date created |  | File_system_date_created | File system date created | Created date from File System (only applies to Non-Office 365 data) |
| File system date modified |  | File_system_date_modified | File system date modified | Modified date from File System (only applies to Non-Office 365 data) |
| File Type | FileType |  | File Type | File type of the item, based on file extension |
| Has attachment | HasAttachment | Email_has_attachment | Has attachment | Indicates whether or not the message has attachments |
| Has attorney | HasAttorney |  | Has attorney | Has attorney as calculated for analytics |
| HasText |  | Has_text |  | Indicates whether or not the item has text, possible values are True and False |
| Immutable ID | ImmutableId | Immutable_ID | Immutable ID | Immutable Id as stored in Office 365 |
| Inclusive type | InclusiveType | Inclusive_type | Inclusive type | Inclusive type calculated for analytics |
| In Reply To Id |  | In_reply_to_ID | In Reply To Id | In reply to Id from the message |
| Is Representative | IsRepresentative | Is_representative | Is Representative | Is representative as calculated for analytics |
| Item class | ItemClass | Item_class | Item class | Item class supplied by exchange server, e.g. IPM.Note |
| Last modified date | LastModifiedDate | Doc_date_modified | Last modified date | Last modified from document metadata |
| Load ID | LoadId | Load_ID | Load ID | Load Id, in which the item was loaded into a Review set |
| Location | Location | Location | Location | String that indicates the type of location that documents were sourced from.<br />Non-O365 -> Imported Data<br />Teams -> Teams<br />EXO -> Exchange<br />SPO -> SharePoint<br />OD4B -> OneDrive |
| Location name | LocationName | Location_name | Location name | String that identifies the source of the item.  For exchange, this will be the SMTP address of the mailbox.  For SharePoint and OneDrive, the URL to the site collection. |
| Marked as representative | MarkAsRepresentative |  | Marked as representative | Marked as representative  as calculated for analytics |
| Marked as pre tagged Case issue 1 |  | Marked_as_pre_tagged_Case_issue_1 |  | Marked as pre tagged Case issue 1 from Relevance |
| Marked as seed Case issue 1 |  | Marked_as_seed_Case_issue_1 |  | Marked as seed Case issue 1 from Relevance |
| Meeting End Date | MeetingEndDate | Meeting_end_date | Meeting End Date | Meeting end date for meetings |
| Meeting Start Date | MeetingStartDate | Meeting_start_date | Meeting Start Date | Meeting start date for meetings |
| Message kind | MessageKind | Message_kind | Message kind | The type of email message to search for.<br />Possible values: <br />contacts <br />docs <br />email <br />externaldata <br />faxes <br />im <br />journals <br />meetings <br />microsoftteams (returns items from chats, meetings, and calls in Microsoft Teams) <br />notes <br />posts <br />rssfeeds <br />tasks <br />voicemail |
| Native Extension | NativeExtension | Native_extension | Native Extension | Native extension of the item |
| Native file name | NativeFileName | Native_file_name | Native file name | Native file name of the item |
| NativeMD5 |  | Native_MD5 |  | MD5 hash of file stream |
| ND/ET Sort: Excluding attachments | NdEtSortExclAttach | ND_ET_sort_excl_attach | ND/ET Sort: Excluding attachments | ND/ET Sort excluding attachments as calculated for analytics |
| ND/ET Sort: including attachments | NdEtSortInclAttach | ND_ET_sort_incl_attach | ND/ET Sort: including attachments | ND/ET Sort including attachments as calculated for analytics |
| Normalized relevance score Case issue 1 |  | Normalized_relevance_score_case_issue_1 |  | Normalized relevance score Case issue 1 from Relevance |
| O365 authors |  | O365_authors | O365 authors | Author from SharePoint |
| O365 created by |  | O365_created_by | O365 created by | Created by from SharePoint |
| O365 date created |  | O365_date_created | O365 date created | Created date from SharePoint |
| O365 date modified |  | O365_date_modified | O365 date modified | Last modified date from SharePoint |
| O365 modified by |  | O365_modified_by | O365 modified by | Modified by from SharePoint |
| Parent ID | ParentId | Parent_ID | Parent ID | Id of the item's parent |
| ParentNode |  | Parent_node |  | Parent node calculated for analytics |
| Parent path | ParentPath | Parent_path | Parent path | Compound path of the direct parent of the item |
| Participant domains | ParticipantDomains | Email_participant_domains | Participant domains | List of all domains of participants of a message |
| Participants | Participants | Email_participants | Participants | List of all participants of a message (Sender, To, Cc, Bcc) |
| Pivot ID | PivotId | Pivot_ID | Pivot ID | Pivot Id as calculated for analytics |
| Potentially privileged | PotentiallyPrivileged | Potentially_privileged | Potentially privileged | Potentially privileged as calculated for analytics |
| Processing status | ProcessingStatus | Error_code | Processing status | Processing status after the item was ingested into a Review Set |
| Read percent Case issue 1 |  | Read_percent_Case_issue_1 |  | Read percent Case issue 1 from Relevance |
| Read percentile | ReadPercentile |  | Read percentile | Read percentile as calculated for analytics |
| Recipient Count |  | Recipient_count | Recipient Count | Number of recipients in the message |
| Recipient domains | RecipientDomains | Email_recipient_domains | Recipient domains | List of all domains of recipients of a message |
| Recipients | Recipients | Email_recipients | Recipients | List of all recipients of a message (To, Cc, Bcc) |
| Relevance load group Case issue 1 |  | Relevance_load_group_case_issue_1 |  | Relevance load group Case issue 1 from Relevance |
| Relevance status description Case issue 1 |  | Relevance_status_description_Case_issue_1 |  | Relevance status description Case issue 1 from Relevance |
| Relevance tag Case issue 1 |  | Relevance_tag_case_issue_1 |  | Relevance tag Case issue 1 from Relevance |
| Relevance Comment |  | Relevance_comment | Relevance Comment | Comment field from Relevance |
| Relevance score | RelevanceScore |  | Relevance score | Relevance score  as calculated for analytics |
| Relevance tag | RelevanceTag |  | Relevance tag | Relevance tag  as calculated for analytics |
| Representative ID | RepresentativeId |  | Representative ID | Representative Id  as calculated for analytics |
| Sender | Sender | Email_sender | Sender | Sender (From) field for message types.  Format is DisplayName <SmtpAddress> |
| Sender/Author | SenderAuthor |  | Sender/Author | Calculated field comprised of the sender or author of the item |
| Sender domain | SenderDomain | Email_sender_domain | Sender domain | Domain of the sender |
| Sent | Sent | Email_date_sent | Sent | Sent date of the message |
| Set Order: Inclusive First | SetOrderInclusivesFirst | Set_order_inclusives_first | Set Order: Inclusive First | Set order Inclusives calculated for analytics |
| SimilarityPercent |  | Similarity_percent |  | Similarity percent as calculated for analytics |
| Native file size | Size | Native_size | Native file size | Number of bytes of the native item |
| Subject | Subject | Email_subject | Subject | Subject of the message |
| Subject/Title | SubjectTitle |  | Subject/Title | Calculated field comprised of the subject or title of the item |
| Tagged by Case issue 1 |  | Tagged_by_Case_issue_1 |  | Tagged by case issue 1 from Relevance |
| Tags | Tags | Tags | Tags | Tags applied in a Review set |
| Themes list | ThemesList | Themes_list | Themes list | Themes list as calculated for analytics |
| Title | Title | Doc_title | Title | Title from the document metadata |
| To | To | Email_to | To | To field for for message types.  Format is DisplayName <SmtpAddress> |
| Unique in email set | UniqueInEmailSet |  | Unique in email set | Unique in email set as calculated for analytics |
| Was Remediated | WasRemediated | Was_Remediated | Was Remediated | True if the item was remediated, otherwise false |
| Word count | WordCount | Word_count | Word count | Number of words in the item |
||||||

  > [!NOTE]
  > For more information about searchable fields when searching directly against Office 365, refer to [Keyword queries and search conditions for Content Search](https://docs.microsoft.com/en-us/office365/securitycompliance/keyword-queries-and-search-conditions)