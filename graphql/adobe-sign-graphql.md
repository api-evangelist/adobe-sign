# Adobe Sign (Acrobat Sign) GraphQL Schema

## Overview

This directory contains a conceptual GraphQL schema for the Adobe Acrobat Sign REST API v6. Adobe Acrobat Sign (formerly Adobe Sign and EchoSign) is a cloud-based electronic signature and digital document workflow service that enables organizations to send, sign, track, and manage legally binding agreements.

The schema translates the Adobe Sign REST API v6 resource model into a GraphQL type system covering agreements, participants, signatures, templates, widgets, megaSigns, web forms, workflows, users, groups, accounts, webhooks, and supporting data structures.

## Source API

- **API**: Adobe Acrobat Sign REST API v6
- **REST Reference**: https://secure.na1.adobesign.com/public/docs/restapi/v6
- **Developer Guide**: https://opensource.adobe.com/acrobat-sign/developer_guide/index.html
- **GitHub**: https://github.com/adobe/adobesign-api
- **Authentication**: OAuth 2.0 Bearer tokens; clients must call GET /baseUris first to discover the region-specific apiAccessPoint

## Schema File

- `adobe-sign-schema.graphql` — Full GraphQL SDL with 60+ named types, enums, inputs, queries, mutations, and subscriptions

## Type Coverage

### Enums

| Enum | Description |
|------|-------------|
| `AgreementStatus` | Lifecycle states for an agreement (OUT_FOR_SIGNATURE, SIGNED, CANCELLED, EXPIRED, etc.) |
| `ParticipantRole` | Role of a participant in an agreement (SIGNER, APPROVER, CC, DELEGATE, etc.) |
| `SignerStatus` | Per-participant signing status |
| `SignatureType` | ESIGN or WRITTEN |
| `WidgetStatus` | ACTIVE, INACTIVE, DRAFT, AUTHORING |
| `WidgetView` | AGREEMENT, AUTHORING, PREFILLING |
| `MegaSignStatus` | ACTIVE, CANCELLED, COMPLETED |
| `LibraryType` | DOCUMENT or FORM_FIELD_LAYER |
| `LibraryDocumentAccess` | GLOBAL, USER, GROUP, ACCOUNT |
| `WebFormStatus` | ACTIVE, INACTIVE, DRAFT, AUTHORING |
| `WebhookEvent` | All subscribable agreement, megaSign, and widget events |
| `ResourceType` | AGREEMENT, WIDGET, MEGASIGN, LIBRARY_DOCUMENT |
| `NotificationType` | SIGNED, APPROVED, DECLINED, EXPIRED, CANCELLED, etc. |
| `FormFieldType` | SIGNATURE, INITIALS, DATE, TEXT, CHECKBOX, RADIO, DROPDOWN, etc. |
| `FormFieldAlignment` | LEFT, RIGHT, CENTER |

### Core Agreement Types

| Type | Description |
|------|-------------|
| `Agreement` | Full agreement object with all fields |
| `AgreementInfo` | Summary view used in list responses |
| `AgreementCreation` | Input shape for creating agreements |
| `AgreementDocument` | Document attached to an agreement |
| `AgreementStatus` | Current status with next participant sets and signing URLs |
| `AgreementList` | Paginated list of agreement summaries |

### Participant Types

| Type | Description |
|------|-------------|
| `ParticipantSet` | Ordered group of participants sharing a role |
| `ParticipantInfo` | Individual participant detail |
| `MemberInfo` | Member within a participant set |
| `SigningUrlSetInfo` | Signing URLs scoped to a participant set |
| `SigningUrl` | Per-member signing URL |

### Recipient Types

| Type | Description |
|------|-------------|
| `Recipient` | Generic recipient with email or fax |
| `RecipientEmail` | Email-based recipient |
| `RecipientFax` | Fax-based recipient |
| `RecipientGroup` | Named group of recipients |

### Signature Types

| Type | Description |
|------|-------------|
| `ESignature` | Electronic signature record |
| `Initials` | Initials captured during signing |
| `Handwritten` | Handwritten signature image |
| `MobileSignature` | Mobile-based signature workflow |
| `SigningOrder` | Ordered participant sets for sequential signing |

### Form Field Types

| Type | Description |
|------|-------------|
| `SignerFormField` | Form field definition within an agreement |
| `SignerFormFieldLocation` | Page/position coordinates for a form field |
| `FormFieldCondition` | Conditional show/hide or value rule |
| `HyperlinkField` | Hyperlink form field data |
| `MergeField` | Pre-fill merge field name/value pairs |

### Widget Types

| Type | Description |
|------|-------------|
| `Widget` | Full web form / widget object |
| `WidgetInfo` | Summary widget view for lists |
| `WidgetView` | URL for a specific widget view mode |
| `WidgetCompletionInfo` | Post-completion redirect configuration |
| `WidgetList` | Paginated list of widgets |

### MegaSign Types

| Type | Description |
|------|-------------|
| `MegaSign` | Bulk send agreement object |
| `MegaSignInfo` | Summary view for megaSign lists |
| `MegaSignChild` | Individual child agreement spawned by a megaSign |
| `MegaSignList` | Paginated list of megaSigns |

### Template and Library Document Types

| Type | Description |
|------|-------------|
| `Template` | Agreement template metadata |
| `LibraryDocument` | Reusable library document or form field layer |
| `LibraryDocumentList` | Paginated list of library documents |

### Web Form Types

| Type | Description |
|------|-------------|
| `WebForm` | Embeddable web form (widget) |
| `WebFormCreation` | Input shape for creating a web form |

### User Types

| Type | Description |
|------|-------------|
| `UserAgreement` | Agreements scoped to a user |
| `UserLibraryDocument` | Library documents scoped to a user |
| `UserInfo` | Full user profile |
| `SenderInfo` | Agreement sender summary |
| `Delegate` | Delegation from one participant to another |
| `DisplayUserInfo` | Compact user display info |
| `DisplayUserSetInfo` | Display info for a participant set |
| `UserList` | Paginated list of users |

### Group and Account Types

| Type | Description |
|------|-------------|
| `GroupInfo` | Group name, ID, and metadata |
| `GroupList` | Paginated list of groups |
| `AccountInfo` | Account-level details and settings |
| `OrganizationInfo` | Organization (enterprise) details |

### Webhook and Notification Types

| Type | Description |
|------|-------------|
| `WebhookInfo` | Webhook registration details |
| `WebhookUrlInfo` | Target URL for webhook delivery |
| `WebhookList` | Paginated list of webhooks |
| `Notification` | Notification event triggered by agreement actions |

### Workflow Types

| Type | Description |
|------|-------------|
| `WorkflowDefinition` | Named reusable agreement workflow |
| `WorkflowCcListInfo` | CC configuration in a workflow |
| `WorkflowExpirationInfo` | Expiration settings in a workflow |
| `WorkflowFileInfo` | File info configuration in a workflow |
| `WorkflowMergeFieldInfo` | Merge field configuration in a workflow |
| `WorkflowMessageInfo` | Message field configuration |
| `WorkflowParticipantInfo` | Participant configuration per workflow step |
| `WorkflowPasswordInfo` | Password protection workflow settings |
| `WorkflowReminderInfo` | Reminder configuration in a workflow |
| `WorkflowSecurityOptionInfo` | Security option per workflow |
| `WorkflowList` | Paginated list of workflows |

### Document and Resource Types

| Type | Description |
|------|-------------|
| `ResourceUpload` | Result of uploading a transient document |
| `Document` | Document object returned from the API |
| `DocumentMetadata` | Detailed document metadata including page info |
| `PageInfo` | Page dimensions and rotation |
| `FileInfo` | File reference by transient ID, library ID, or URL |
| `DocumentUrl` | URL-based document descriptor |
| `UrlFileInfo` | URL-based file info |

### Auth Types

| Type | Description |
|------|-------------|
| `APIKey` | API key credential object |
| `Token` | OAuth 2.0 access token response |

### Supporting Types

| Type | Description |
|------|-------------|
| `SecurityOption` | Authentication and access protection settings |
| `ParticipantSecurityOption` | Per-participant security settings |
| `PhoneInfo` | Phone number with country code |
| `PostSignOption` | Post-signing redirect configuration |
| `VaultingInfo` | Document vaulting settings |
| `ExternalId` | External system ID reference |
| `NotarizationInfo` | Notarization configuration |
| `AuthFailureInfo` | Authentication failure redirect |
| `CcInfo` | CC recipient with label and page restrictions |
| `ImageUrl` | Typed image URL |
| `SendThroughWebOption` | Web-based file upload options |
| `FileUploadOptions` | Allowed file upload sources |
| `BaseUri` | Region-specific API and web access points |
| `PageCursor` | Pagination cursor and result count |

## Query Operations

The schema exposes the following top-level queries:

- `baseUris` — discover region-specific API access points
- `agreements` / `agreement` — list and fetch agreements
- `agreementDocuments` — list documents in an agreement
- `agreementSigningUrls` — get signing URLs per participant set
- `agreementAuditTrail` — retrieve audit trail document
- `agreementFormFields` — list form fields for an agreement
- `libraryDocuments` / `libraryDocument` / `libraryDocumentDocuments`
- `widgets` / `widget`
- `megaSigns` / `megaSign` / `megaSignChildAgreements`
- `users` / `user` / `userAgreements` / `userLibraryDocuments` / `me`
- `groups` / `group` / `groupUsers`
- `webhooks` / `webhook`
- `workflows` / `workflow`

## Mutation Operations

- `uploadTransientDocument` — upload a file for use in agreements
- `createAgreement` / `cancelAgreement` / `deleteAgreement`
- `delegateAgreementSigner` — delegate a signing step to another person
- `sendAgreementReminder` — send a reminder to pending participants
- `createLibraryDocument` / `deleteLibraryDocument`
- `createWidget` / `updateWidgetStatus`
- `createMegaSign` / `cancelMegaSign`
- `createUser` / `updateUser`
- `createGroup` / `updateGroup` / `deleteGroup`
- `addUserToGroup` / `removeUserFromGroup`
- `createWebhook` / `updateWebhookState` / `deleteWebhook`

## Subscription Operations

- `agreementStatusChanged` — real-time agreement state changes
- `agreementSigned` — fired when a signature is captured
- `widgetSubmitted` — fired when a widget form is submitted
- `megaSignChildCompleted` — fired when a megaSign child agreement completes

## Design Notes

- The schema uses custom scalars (`DateTime`, `URL`, `EmailAddress`, `JSON`) to preserve semantic types from the REST API.
- All list responses include a `PageCursor` for cursor-based pagination, mirroring the REST API's `nextPageCursor` pattern.
- The `AgreementStatus` enum name collision (also used as a type) is resolved by context in GraphQL — the enum is used as a field value, the type as an object.
- Workflow types decompose the REST API's nested `WorkflowDefaultParams` structure into individual typed objects for each configurable workflow section.
- The `FileInfo` union-like type uses optional fields to represent the three ways a file can be referenced in the REST API: transient document ID, library document ID, or external URL.
