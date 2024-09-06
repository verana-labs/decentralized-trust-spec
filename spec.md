# Decentralized Trust Service v1.0 Specification

**Specification Status:** [Pre-Draft](https://github.com/decentralized-identity/org/blob/master/work-item-lifecycle.md)

**Latest Draft:** [2060-io/dts-specs](https://github.com/2060-io/dts-specs)

**Editors:**

~ [Fabrice Rochette](https://www.linkedin.com/in/fabricerochette) (2060.io)

<!-- -->

**Participate:**

~ [GitHub repo](https://github.com/2060-io/dts-specs)

~ [File a bug](https://github.com/2060-io/dts-specs/issues)

~ [Commit history](https://github.com/2060-io/dts-specs/commits/main)

---

## Abstract

The Internet is broken. All existing communication channels are insecure, and obsolete. Because all existing communication channels rely on public identifiers, anyone that knows your identifier can reach you.

Furthermore, existing communication channel do not provide a sure-fire way of verifying service provider and end-user Identity. This is an open door to spam, phishing, fraud, identity theft...

Regarding service providers and services, each service has it own registration process, fastidious password rules... And/or they are usually using federated login, that makes you depend on a third party service for accessing your accounts.

If the World Wide Web was initially designed for interoperability, major companies have managed to transform it to a closed, centralized internet, that we all depend on.

Not to talk about privacy, and what's done with our data.

To build a new, trustable internet, we need new, trustable communication channels, where both ends can be clearly identified, and where providing a service, accessing a service, or creating a new account, should be as simple as presenting a credential.

Decentralized Trust Services are services that are using a secure bidirectional persistent communication channel that, combined to trust layers such as [Public Trust Registries](https://github.com/2060-io/public-trust-registry-specs), enable establishing a trustable communication channel between peers.

## About this Document

In order to fully understand the concepts developed in this document, you should have some basic knowledge of [[ref:DID]], [[ref:DIDComm]], [[ref:DTS]], [[ref:trust registry]], ledger-based applications, and more generally, all terms present in the [Terminology](#terminology) section.

## Introduction

### What is a Trustable Communication Channel?

*This section is non-normative.*

A trustable communication channel is a persistent communication channel, where participants have been fully authenticated with a [[ref: verifiable credential]] or equivalent.

Communication channel is considered trustable in the following use cases:

- immediately when establishing the connection for all participants. In this case, all participants must present a [[ref: verifiable credential]] to establish a connection.
- immediately when establishing the connection for some participants. If some of the participants present a [[ref: verifiable credential]] to establish a connection, and some other participants connect without authenticating themselves, only authenticated participants will be trustable in this connection. These unauthenticated participants must later on present a credential through the established connection to authenticate themselves.
- after establishing the connection, by presenting [[ref: verifiable credentials]] directly after having established the connection.

### What is a Decentralized Trust Service?

*This section is non-normative.*

A [[ref: decentralized trust service]] is a service that provide a way to identify itself *before* connecting to it. Entities that want to connect to a [[ref: decentralized trust service]] can review its presented [[ref: verifiable credentials]], prove their legitimacy by performing a [[ref: trust resolution]], and based on the result, decide to connect or not.

Additionally, a [[ref: decentralized trust service]] that would like to issue or request verification of credentials must prove it is allowed to do so.

### Conformance

As well as sections marked as non-normative, all authoring guidelines, diagrams, examples, and notes in this specification are non-normative. Everything else in this specification is normative.
The key words MAY, MUST, MUST NOT, OPTIONAL, RECOMMENDED, REQUIRED, SHOULD, and SHOULD NOT in this document are to be interpreted as described in [BCP 14](https://datatracker.ietf.org/doc/html/bcp14) [RFC2119](https://w3c.github.io/vc-data-model/#bib-rfc2119) [RFC8174](https://w3c.github.io/vc-data-model/#bib-rfc8174) when, and only when, they appear in all capitals, as shown here.

## Terminology

[[def: account, accounts]]:
~ A [[ref: public trust registry]] account.

[[def: applicant, applicants]]:
~ A [[ref: controller]] that starts a [[ref: validation process]].

[[def: controller, controllers]]:
~ An [[ref: account]] which is the controller of a specific resource in an [[ref: PTR]].

[[def: credential schema, credential schemas]]:
~ An [[ref: PTR]] resource which represents a verifiable credential definition and the associated permissions and business rules for issuing, verifying or holding a credential linked to this credential schema.

[[def: decentralized identifier, DID, DIDs]]:
~ A decentralized identifier, as specified in [[spec-norm:DID-CORE]].

[[def: decentralized identifier communication, DIDComm]]:
~ [DIDComm](https://identity.foundation/didcomm-messaging/spec/) uses [[ref: DIDs]] to establish confidential, ongoing connections.

[[def: decentralized identifier document, DID Document, DID Documents]]:
~ A DID Document, as specified in [[spec-norm:DID-CORE]].

[[def: decentralized trust service, DTS, DTSs]]:
~ A service, usually provided using [[ref: DIDComm]], that can be deployed anywhere by its owner, and that is using the decentralized trust layer provided by an [[ref: PTR]], and has a resolvable [[ref: proof of trust]].

[[def: decentralized trust service browser, DTS browser, DTS browsers]]:
~ A browser for accessing and using [[ref: DTSs]]. To be considered as a [[ref: DTS browser]], a browser must implement an [[ref: PTR]] trust layer and use a trust resolution using use the [[ref: essential credential schema]] of a given trust registry for providing a [[ref: proof of trust]] to users so that user clearly identifies [[ref: DTS]] provider and decides to connect or not.

[[def: DID Directory, DID directory]]:
~ A repository of DIDs in an PTR.

[[def: essential credential schema, essential credential schemas]]:
~ Default [[ref: credential schema]], owned by a [[ref: trust registry]], that provide the basis for a trust layer to exist in the ecosystem so that [[ref: DTS browser]] can generate a [[ref: proof of trust]].

[[def: holder, holders]]:
~ A role an entity might perform by possessing one or more verifiable credentials and generating verifiable presentations from them. A holder is often, but not always, a [[ref: subject]] of the verifiable credentials they are holding. Holders store their credentials in credential repositories. Example holders include organizations, persons, things.

[[def: issuer, issuers]]:
~ A role an entity can perform by asserting claims about one or more [[ref: subjects]], creating a verifiable credential from these claims, and transmitting the verifiable credential to a [[ref: holder]]. Example issuers include corporations, non-profit organizations, trade associations, governments, and individuals.

[[def: json schema, json schemas]]:
~ A json schema as defined in [JSON-SCHEMA](https://json-schema.org).

[[def: json schema credential, json schema credentials]]:
~ A json schema credential as defined in [[spec-norm:VC-JSON-SCHEMA]].

[[def: linked-vp]]:
~ A presentation of a [[ref: verifiable credential]] as specified in [LINKED-VP](https://identity.foundation/linked-vp/).

[[def: participant, participants]]:
~ An entity that uses an [[ref: PTR]] and its trust layer to provide or use services.

[[def: proof of trust]]:
~ Visual representation using [[ref: essential credential schemas]] of a [[ref: trust resolution]] process of a [[ref: DTS]], for identifying the [[ref: DTS]], its owner, and the [[ref: issuer]] of the verifiable credential of its owner.

[[def: public trust registry, PTR]]:
~ a decentralized, ledger-based network, which provides: trust registry features that can be used by all its [[ref: participants]]; and a tokenized business model allows charging [[ref: participants]] for trust fees that are transferred to other [[ref: participants]], or locked into [[ref: trust deposits]].

[[def: subject, subjects]]:
~ A thing about which claims are made. Example subjects include human beings, animals, things, and organization, a [[ref: DID]]...

[[def: trust deposit, trust deposits]]:
~ A financial deposit that is used as a trust guarantee. For a given [[ref: controller]], its trust deposit is increased when running validation process (either as an [[ref: applicant]] or as a [[ref: validator]]), or when registering [[ref: DID]] in the DID directory.

[[def:trust registry, trust registries]]
~ An approved list of [[ref: issuers]] and [[ref: verifiers]] that are authorized to issue/verify certain credentials in an ecosystem.

[[def: trust resolution]]:
~ Process run by, for example a [[ref: DTS browser]], which purpose is to recursively resolve [[ref: DID]] by digging into [[ref: DID Documents]] and look for [[ref: linked-vp]] entries and their [[ref: issuer]] [[ref: DIDs]], and [trust registry](https://trustoverip.github.io/tswg-trust-registry-protocol/) entries to gather whether the service provided by the [[ref: DID]] is trustable (and legitimate), or not.

[[def: validation process]]:
~ A process run by [[ref: applicants]] that want to, for a specific [[ref: credential schema]], be a [[ref: issuer]], be a [[ref: verifier]], or simply hold a verifiable credential linked to the [[ref: credential schema]].

[[def: validator]]:
~ A role an entity performs by participating in validation processes with [[ref: applicants]] in order to register them as [[ref: issuer]], or [[ref: verifier]] of a [[ref: credential schema]], or to deliver a verifiable credential to them.

[[def: verifier, verifiers]]:
~ A role an entity performs by receiving one or more verifiable credentials, optionally inside a verifiable presentation for processing. Example verifiers include service providers.

[[def: verifiable credential, verifiable credentials]]:
~ A verifiable credential as defined in [[spec-norm:VC-DATA-MODEL]].

## Specification

### [ECS] Essential Credential Schemas

Essential Credential Schemas (ECS) are created in a PTR by a Trust Registry. There are 3 kind of ECS:

- Service;
- Organization;
- Person.

A Trust Registry creates itself in a [[ref: PTR]] by creating a `TrustRegistry` entry `tr`. For this Trust Registry to qualify for being used for trust resolution in DTS and browsers, it MUST provide, associated to the `TrustRegistry` entry `tr`, all 3 `CredentialSchema` entries, with a respective `json_schema` attribute defined as follows in [ECS-SERVICE], [ECS-ORG], and [ECS-PERSON].

#### [ECS-SERVICE] Service Credential Json Schema

Credential subject object of schema MUST contain the following attributes:

- `id` (string) (*mandatory*): the [[ref: DID]] of the service the credential will be issued to.
- `name` (string) (*mandatory*): service name. UTF8 charset, max length: 512 bytes.
- `description` (string) (*mandatory*): service description. UTF8 charset, max length: 4096 bytes.
- `logo` (image) (*mandatory*): the logo of the service, as it will be shown in browsers and search engines.
- `minimumAgeRequired` (integer) (*mandatory*): minimum required age to connect to service. Allowed value: 0 to 255. Used by browsers that provide a simple birth date based parental control.
- `termsAndConditions` (string) (*mandatory*): URL of the terms and conditions of the service. It is recommended to store terms and conditions in a file, in a repository that allows file hash verification (IPFS).
- `termsAndConditionsHash` (string) (*optional*): If terms and conditions of the service are stored in a file, optional hash of the file for data integrity verification.
- `privacyPolicy` (string) (*mandatory*): URL of the terms and conditions of the service. MAY be the same URL that `terms_and_conditions` if file are combined. It is recommended to store privacy policy in a file repository that allows file hash verification (IPFS).
- `privacyPolicyHash` (string) (*optional*): If privacy policy of the service are stored in a file, optional hash of the file for data integrity verification.

the resulting `json_schema` attribute will be the following Json Schema. Replace:

- `{$chain-rest-api}` with [[ref: PTR]] API domain,
- `{$tr.did}` with `tr.did`,
- `{$uuid}` with the `uuid` of the created `CredentialSchema` entry.

```json
{
  "$id": "https://{$chain-rest-api}/{$tr.did}/cs/js/{$uuid}",
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "ServiceCredential",
  "description": "ServiceCredential using JsonSchema",
  "type": "object",
  "properties": {
    "credentialSubject": {
      "type": "object",
      "properties": {
        "id": {
          "type": "string",
          "format": "uri"
        },
        "name": {
          "type": "string",
          "minLength": 0,
          "maxLength": 512
        },
        "description": {
          "type": "string",
          "minLength": 0,
          "maxLength": 4096
        },
        "logo": {
          "type": "string",
          "contentEncoding": "base64",
          "contentMediaType": "image/png"
        },
        "minimumAgeRequired": {
          "type": "number",
          "minimum": 0,
          "exclusiveMaximum": 150
        },
        "termsAndConditions": {
          "type": "string",
          "format": "uri"
        },
        "termsAndConditionsHash": {
          "type": "string"
        },
        "policyPrivacy": {
          "type": "string",
          "format": "uri"
        },
        "policyPrivacyHash": {
          "type": "string"
        }
      },
      "required": [
        "id",
        "name",
        "description",
        "logo",
        "minimumAgeRequired",
        "termsAndConditions",
        "policyPrivacy"
      ]
    }
  }
}
```

#### [ECS-ORG] OrganizationCredential Json Schema

Credential subject object of schema MUST contain the following attributes:

- `id` (string) (*mandatory*): the [[ref: DID]] of the service the credential has been issued to, which is the subject of the [[ref: verifiable credential]].
- `name` (string) (*mandatory*): name of the organization.
- `logo` (image) (*mandatory*): the logo of the organization, as it will be shown in browsers and search engines.
- `registryId` (string) (*mandatory*): registry id of the organization.
- `address` (string) (*mandatory*): address of the organization.
- `type` (enum) (*mandatory*): type of organization. PUBLIC, PRIVATE, FOUNDATION.
- `countryCode` (string) (*mandatory*): country where the company is registered.

the resulting `json_schema` attribute will be the following Json Schema. Replace:

- `{$chain-rest-api}` with [[ref: PTR]] API domain,
- `{$tr.did}` with `tr.did`,
- `{$uuid}` with the `uuid` of the created `CredentialSchema` entry.


```json
{
  "$id": "https://{$chain-rest-api}/{$tr.did}/cs/{$uuid}/jsonschema",
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "OrganizationCredential",
  "description": "OrganizationCredential using JsonSchema",
  "type": "object",
  "properties": {
    "credentialSubject": {
      "type": "object",
      "properties": {
        "id": {
          "type": "string",
          "format": "uri"
        },
        "name": {
          "type": "string",
          "minLength": 0,
          "maxLength": 256
        },
        "logo": {
          "type": "string",
          "contentEncoding": "base64",
          "contentMediaType": "image/png"
        },
        "registryId": {
          "type": "string",
          "minLength": 0,
          "maxLength": 256
        },
        "address": {
          "type": "string",
          "minLength": 0,
          "maxLength": 1024
        },
        "type": {
          "type": "enum",
          "value": ["PUBLIC", "PRIVATE", "FOUNDATION"]
        },
        "countryCode": {
          "type": "string",
          "minLength": 2,
          "maxLength": 2
        }
      },
      "required": [
        "id",
        "name",
        "logo",
        "registryId",
        "address",
        "type",
        "countryCode"
      ]
    }
  }
}
```

#### [ECS-PERSON] Person Credential Json Schema

Credential subject object of schema MUST contain the following attributes:

- `id` (string) (*mandatory*): the [[ref: DID]] of the service the credential has been issued to.
- `firstName` (string) (*optional*): first name of the person.
- `lastName` (string) (*mandatory*): last name of the person.
- `avatar` (image) (*optional*): the avatar of this person, as it will be shown in browsers and search engines.
- `birthDate` (date) (*mandatory*): date of birth.
- `countryOfResidence` (string) (*mandatory*): the country of residence.

the resulting `json_schema` attribute will be the following Json Schema. Replace:

- `{$chain-rest-api}` with [[ref: PTR]] API domain,
- `{$tr.did}` with `tr.did`,
- `{$uuid}` with the `uuid` of the created `CredentialSchema` entry.

```json
{
  "$id": "https://{$chain-rest-api}/{$tr.did}/cs/{$uuid}/jsonschema",
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "PersonCredential",
  "description": "PersonCredential using JsonSchema",
  "type": "object",
  "properties": {
    "credentialSubject": {
      "type": "object",
      "properties": {
        "id": {
          "type": "string",
          "format": "uri"
        },
        "firstName": {
          "type": "string",
          "minLength": 0,
          "maxLength": 256
        },
        "lastName": {
          "type": "string",
          "minLength": 1,
          "maxLength": 256
        },
        "avatar": {
          "type": "string",
          "contentEncoding": "base64",
          "contentMediaType": "image/png"
        },
        "birthDate": {
          "type": "string",
          "format": "date"
        },
        "countryOfResidence": {
          "type": "string",
          "minLength": 2,
          "maxLength": 2
        }
      },
      "required": [
        "id",
        "lastName",
        "birthDate",
        "countryOfResidence"
      ]
    }
  }
}
```

### [DT-JSON-SCHEMA-CRED] Decentralized Trust Json Schema Credential

A DT Json Schema Credential is a [[ref: json schema credential]] self-issued by a Trust Registry DID, that MUST refer to the json schema of a `CredentialSchema` entry created in a `PTR`. Issuer of the DT Json Schema Credential MUST be the same DID that the DID of the `TrustRegistry` entry created in the [[ref: PTR]] than owns the `CredentialSchema` entry in the [[ref: PTR]].

A DT Json Schema Credential MUST have a `credentialSchema` property that contains exactly the following:

```json
  "credentialSchema": {
    "id": "https://www.w3.org/2022/credentials/v2/json-schema-credential-schema.json",
    "type": "JsonSchema",
    "digestSRI": "sha384-S57yQDg1MTzF56Oi9DbSQ14u7jBy0RDdx0YbeV7shwhCS88G8SCXeFq82PafhCrW"
  }
```

Additionally, it MUST have a `credentialSubject` object with:

- a `id` properties that is the URL to access the [[ref: json schema]] in the PTR,
- `type` MUST be set to "JsonSchema",
- an object `jsonSchema` MUST be present with an `$ref` properties that is the URL to access the [[ref: json schema]] in the PTR
- a digestSRI property that MUST match the [[ref: json schema]] file content hash.

Example of a DT Json Schema Credential:

DtJsonSchemaCredential.json:

```json

{
  "@context": [
      "https://www.w3.org/ns/credentials/v2"
  ],
  "id": "https://ecs-trust-registry/dt-credential-schema-credential.json",
  "type": ["VerifiableCredential", "JsonSchemaCredential"],
  "issuer": "did:abc:ecs-trust-registry",
  "issuanceDate": "2024-01-01T19:23:24Z",
  "credentialSchema": {
    "id": "https://www.w3.org/2022/credentials/v2/json-schema-credential-schema.json",
    "type": "JsonSchema",
    "digestSRI": "sha384-S57yQDg1MTzF56Oi9DbSQ14u7jBy0RDdx0YbeV7shwhCS88G8SCXeFq82PafhCrW"
  },
  "credentialSubject": {
    "id": "https://ptr-hostname/did:abc:ecs-trust-registry/cs/js/f4524751-8617-40de-bbe6-b2e0fef63c7a",
    "type": "JsonSchema",
    "jsonSchema": {
      "$ref": "https://ptr-hostname/did:abc:ecs-trust-registry/cs/js/f4524751-8617-40de-bbe6-b2e0fef63c7a"
    },
    "digestSRI": "sha384-ABCSGyugst67rs67rdbugsy0RDdx0YbeV7shwhCS88G8SCXeFq82PafhCeZ" 
  }
}

```

### [DT-TR-DIDDOC] Trust Registry DID Document

For each `CredentialSchema` entry a Trust Registry has created in a [[ref: PTR]], the Trust Registry MUST self-issue the corresponding DT Json Schema Credential as specified in [DT-JSON-SCHEMA-CRED].

Additionally, in MUST present the DT Json Schema Credential(s) in its DIDDocument, as well as the corresponding trust registry entry for verification. To do so, it MUST define the following entries in its DIDDocument:

- for each `CredentialSchema` entry it wants to be resolvable, a "LinkedVerifiablePresentation" service entry with a fragment that MUST start with to `#ptr-schemas`, that MUST point to a self-issued DT Json Schema Credential as specified in [DT-JSON-SCHEMA-CRED].
- a "TrustRegistry" service entry with fragment name equal to `#ptr-schemas-trust-registry`, that MUST point to the trqp-2.0 URL of this DID's trust registry in the PTR.

Example:

```json
  "service": [
    {
      "id": "did:abc:dl-trust-registry#ptr-schemas-driving-license-credential-schema-credential",
      "type": "LinkedVerifiablePresentation",
      "serviceEndpoint": ["https://dl-trust-registry/driving-license-credential-schema-presentation.json"]
    },
    {
      "id": "did:abc:dl-trust-registry#ptr-schemas-trust-registry",
      "type": "TrustRegistry",
      "serviceEndpoint": ["https://ptr-hostname/did:abc:dl-trust-registry/trqp-2.0/"]
    }
    ...
  ]
```

If the Trust Registry wishes to provide ECS trust resolution, it MUST present 3 DT Json Credential Schemas of the 3 ECSs required for trust resolution, as well as the corresponding trust registry entry for verification. To do that, it MUST define the following entries in its DIDDocument:

- a "LinkedVerifiablePresentation" service entry with fragment name equal to `#ptr-essential-schemas-service-credential-schema-credential`, that MUST point to a self-issued Service DT Json Schema Credential as specified in [SERVICE-JSON-SCHEMA-CRED] of a service json schema as specified in [ECS-SERVICE].
- a "LinkedVerifiablePresentation" service entry with fragment name equal to `#ptr-essential-schemas-org-credential-schema-credential`, that MUST point to a self-issued [[ref: json schema credential]] of a DT json schema as specified in [ECS-ORG].
- a "LinkedVerifiablePresentation" service entry with fragment name equal to `#ptr-essential-schemas-person-credential-schema-credential`, that MUST point to a self-issued [[ref: json schema credential]] of a DT json schema as specified in [ECS-PERSON].
- a "TrustRegistry" service entry with fragment name equal to `#ptr-essential-schemas-trust-registry`, that MUST point to the trqp-2.0 URL of this DID's trust registry in the PTR.

Example:

```json
  "service": [
    {
      "id": "did:abc:ecs-trust-registry#ptr-essential-schemas-service-credential-schema-credential",
      "type": "LinkedVerifiablePresentation",
      "serviceEndpoint": ["https://ecs-trust-registry/service-credential-schema-presentation.json"]
    },
    {
      "id": "did:abc:ecs-trust-registry#ptr-essential-schemas-organization-credential-schema-credential",
      "type": "LinkedVerifiablePresentation",
      "serviceEndpoint": ["https://ecs-trust-registry/org-credential-schema-presentation.json"]
    },
    {
      "id": "did:abc:ecs-trust-registry#ptr-essential-schemas-person-credential-schema-credential",
      "type": "LinkedVerifiablePresentation",
      "serviceEndpoint": ["https://ecs-trust-registry/person-credential-schema-presentation.json"]
    },
    {
      "id": "did:abc:ecs-trust-registry#ptr-essential-schemas-trust-registry",
      "type": "TrustRegistry",
      "serviceEndpoint": ["https://ptr-hostname/did:abc:ecs-trust-registry/trqp-2.0/"]
    }
    
    ...
  ]
```

### [DT-CRED] Decentralized Trust (DT) Credential

A simple diagram for a clear understanding:

```plantuml

@startuml
scale max 800 width
object "TrustRegistry (in PTR)" as tr {
  did: did:abc:ecs-trust-registry
}
object "CredentialSchema (in PTR)" as cs {
  id: f4524751-8617-40de-bbe6-b2e0fef63c7a
  json_schema: { "$id": ... "title": "ServiceCredential"}
}
object "DT Json Schema Credential" as jsc #3fbdb6 {
  id: https://ecs-trust-registry/dts-credential-schema-credential.json
  issuer: did:abc:ecs-trust-registry
  jsonSchema: https://ptr-hostname/did:abc:ecs-trust-registry/cs/js/f4524751-8617-40de-bbe6-b2e0fef63c7a
}

object "DT Credential" as dtscred #3fbdb6 {
  issuer: did:example:dts-owner
  jsonSchemaCredential: https://ecs-trust-registry/dts-credential-schema-credential.json
}

cs <-- tr : create a CredentialSchema (in PTR)
jsc <-- cs : trust registry did issue a JsonSchemaCredential based on json_schema located in CredentialSchema in the PTR
dtscred <-- jsc: DTS owner issue its DT credential based on JsonSchemaCredential issued by trust registry did

@enduml

```

A DT Credential MUST have a `credentialSchema` property:

- `id` must point to a [[ref: json schema credential]] issued by the trust registry [[ref: DID]] owner of the schema in the PTR;
- `type` MUST be `JsonSchemaCredential`.

As a matter of fact, a DT Credential MUST conform to the dereferenced [[ref: json schema]] of the `JsonSchemaCredential`.

Example DTCredential.json:

```json

{
  "@context": [
    "https://www.w3.org/ns/credentials/v2"
  ],
  "id": "did:web:user-dts.gaiaid.io",
  "type": ["VerifiableCredential", "ServiceCredential"],
  "issuer": "did:web:user-dts.gaiaid.io",
  "credentialSubject": {
     "id": "did:web:user-dts.gaiaid.io",
    ...
  },
  ...
  "credentialSchema": {
    "id": "https://ecs-trust-registry/service-credential-schema-credential.json",
    "type": "JsonSchemaCredential"
  }
}

```

### [DT-EC] DT Essential Credentials

- DT Service Essential Credential [DT-EC-SERVICE]: a [DT-CRED] linked to a CredentialSchema entry that conforms to [ECS-SERVICE].
- DT Organization Essential Credential [DT-EC-ORG]: a [DT-CRED] linked to a CredentialSchema entry that conforms to [ECS-ORG].
- DT Person Essential Credential [DT-EC-PERSON]: a [DT-CRED] linked to a CredentialSchema entry that conforms to [ECS-PERSON].

### [DTS-REQ] Requirements for a service to be a DTS

- [DTS-REQ-1] A [[ref: DTS]] MUST be identified by a [[:ref DID]]. The [[:ref DID]] of a [[ref: DTS]] MUST resolve to a [[ref: DID Document]].
- [DTS-REQ-2] A [[ref: DTS]] DID Document MUST present a DTS Service Essential Credential that conforms to [DT-EC-SERVICE].
- [DTS-REQ-3] If the issuer of the DTS Service Essential Credential of [DTS-REQ-2] is the [[ref: DID]] of this service, service DID Document MUST present a credential that conforms to [DT-EC-ORG] or (exclusive) a [DT-EC-PERSON].
- [DTS-REQ-4] If the issuer of the PTR DTS Credential of [DTS-REQ-2] is not the [[ref: DID]] of this service, issuer service MUST be a [DTS-REQ] [[ref: DTS]] that conforms to [DTS-REQ-3].

::: note
In other words, a to be a DTS, a service MUST identify itself directly by presenting an Organization or a Person Essential Credential, or the issuer of its Service Essential Credential MUST identify itself by presenting an Organization or a Person Essential Credential.
:::

- [DTS-REQ-5] The service MAY issue, present through linked verifiable presentation entries, or request presentation of any additional DTS Credential that conforms to [DT-CRED].

### [DTS-CONN-P2P] Requirements for two DTSs to establish a P2P connection

For establishing a DIDComm connection between 2 [[ref: DTS]], it is REQUIRED for both [[ref: DTS]] to be compliant with [DTS-REQ].

### [SERVICE-BROWSER] Requirements for a DTS to accept a connection from a browser

When a compliant [[ref: DTS]] accepts/establishes a DIDComm connection with a [[ref: DTS browser]], [[ref: DTS browser]] MUST be verified, else connection MUST be dropped.

::: todo
explain how to verify browser
:::

### [DTS-CI] Credential Issuance

- [DTS-CI-1] A [[ref: DTS]] CAN issue [DT-CRED] DT Credentials.
- [DTS-CI-2] A [[ref: DTS]] MUST NOT issue credentials that are not compliant with [DT-CRED].

### [DTS-PR] Presentation Request

- [DTS-PR-1] A [[ref: DTS]] CAN request presentation of [DT-CRED] DT Credentials
- [DTS-PR-2] A [[ref: DTS]] MUST NOT request presentation of credentials that are not compliant with [DT-CRED].

### [DTS-LVP] Linked Verifiable Presentations

Linked verifiable presentations of credential CAN be present in service DID Document, if present, they MUST conform to the following:

- [DTS-LVP-1] Holder of the presentation MUST be the DTS DID.
- [DTS-LVP-2] if linked verifiable presentation id fragment start with `#ptr-schemas`, presented credential and DID Document MUST conform to [DT-CRED].
- [DTS-LVP-3] if linked verifiable presentation id fragment is `#ptr-essential-schemas-service-credential`, presented credential MUST be a DT Service Essential Credential [DT-EC-SERVICE].
- [DTS-LVP-4] if linked verifiable presentation id fragment is `#ptr-essential-schemas-org-credential`, presented credential MUST be a DT Organization Essential Credential [DT-EC-ORG].
- [SERVICE-LVP-5] if linked verifiable presentation id fragment is `#ptr-essential-schemas-person-credential`, presented credential MUST be a DT Person Essential Credential [DT-EC-PERSON].

### [TR-WL] PTR and Trust Registry whitelists

Compliant [[ref: DTSs]] and [[ref: DTS browsers]] MUST maintain a list of trusted PTRs and trusted DT Essential Credential issuers, and ignore PTRs and DT ECS issuers that are not in these list when resolving trust:

- [TR-WL-PTR]: A list of prefix URLs of trusted PTRs (registry of registries).

Example:

```json

{ 
  ptrs: [ 
    { 
      "name": "ptr-mainnet",
      "baseurl": "https://ecs-trust-registry-mainnet",
      "production": true
    },
    { 
      "name": "ptr-testnet",
      "baseurl": "https://ecs-trust-registry-testnet",
      "production": false
    }
  ]
}
```

- [TR-WL-ES-TR]: A list of DIDs of trusted Trust Registries for providing essential credential schemas.

Example:

```json

{ 
  estrs: [ 
    { 
      "tr": "did:abc:ecs-trust-registry",
      "ptr": "ptr-mainnet"
    },
    { 
      "tr": "did:efg:ecs-trust-registry",
      "ptr": "ptr-testnet"
    }
  ]
}
```

### [BROWSER] DTS Browser compliance

- [BROWSER-1] A compliant [[ref: DTS browser]] MUST connect or accept connection from DTSs that complies with [DTS-REQ].
- [BROWSER-2] A compliant [[ref: DTS browser]] SHOULD NOT connect or accept connection from DTSs that does not comply with [DTS-REQ].
- [BROWSER-3] A compliant [[ref: DTS browser]] MUST dereference all DTS Credentials, DID Documents, verify DTS Json Schema Credentials, Json Schema hashes, use the Trust Registry Query Protocol v2.0,... comply with [TR-WL] to resolve trust and ensure compliance by denying unauthorized actions.

### [TR-RESOL] Verification of permission in Trust Registries

The TRQP-2.0 is used for querying trust registry.

Please refer to [MOD-TRQP-2] /entities/{entityVID}/authorization in [[ref: PTR]] specs.

Example check if issuer `did:web:service-credential-issuer` is granted issuance of credential schema `f4524751-8617-40de-bbe6-b2e0fef63c7a` owned by trust registry `did:web:service-credential-issuer` for country `fr`:

`GET /did:web:trust-registry/trqp-2.0/entities/did:web:service-credential-issuer/authorization?authorizationVID=did:web:trust-registry/cs/js/f4524751-8617-40de-bbe6-b2e0fef63c7a#ISSUER-fr`

Response:

```json
{
  "entityId": "did:web:service-credential-issuer",
  "authorizationID": "did:web:trust-registry/cs/js/f4524751-8617-40de-bbe6-b2e0fef63c7a#ISSUER-fr",
  "description": "ISSUER granted permission for fr country on credential schema f4524751-8617-40de-bbe6-b2e0fef63c7a on trust registry did:web:trust-registry",
  "authorizationUniqueString":"8611f5fc-b243-4871-8e63-d44279b57c73",
  "authorizationStatus":"current",
  "authorizationValidity": {
     "validFromDT": "2024-08-24T14:15:22Z",
     "validUntilDT": "2025-08-24T14:15:22Z",
}
```

### Example

Let's see a full example in action. Here is a DID Document of a compliant DTS:

```json
  "service": [
    {
      "id": "did:web:user-dts.gaiaid.io#ptr-essential-schemas-service-credential",
      "type": "LinkedVerifiablePresentation",
      "serviceEndpoint": ["https://user-dts.gaiaid.io/service-credential-presentation.json"]
    },
    {
      "id": "did:web:user-dts.gaiaid.io#ptr-essential-schemas-org-credential",
      "type": "LinkedVerifiablePresentation",
      "serviceEndpoint": ["https://user-dts.gaiaid.io/org-credential-presentation.json"]
    },
    {
      "id": "did:web:user-dts.gaiaid.io#ptr-schemas-trademark-credential",
      "type": "LinkedVerifiablePresentation",
      "serviceEndpoint": ["https://user-dts.gaiaid.io/trademark-credential-presentation.json"]
    }
    ...
  ]
```

Let's dereference...

service-credential-presentation.json:

```json

{
  "@context": [
    "https://www.w3.org/ns/credentials/v2"
  ],
  "holder": "did:web:user-dts.gaiaid.io",
  "type": ["VerifiablePresentation"],
  "verifiableCredential": [
    {
      "@context": [
        "https://www.w3.org/ns/credentials/v2"
      ],
      "id": "did:web:user-dts.gaiaid.io",
      "type": ["VerifiableCredential", "ServiceCredential"],
      "issuer": "did:web:user-dts.gaiaid.io",
      "credentialSubject": {
        "id": "did:web:user-dts.gaiaid.io",
        ...
      },
      ...
      "credentialSchema": {
        "id": "https://ecs-trust-registry/service-credential-schema-credential.json",
        "type": "JsonSchemaCredential"
      }
    }
  ],
  "id": "https://user-dts.gaiaid.io/service-credential-presentation.json",
  "proof": {
    "type": "Ed25519Signature2018",
    "created": "2024-02-08T17:38:46Z",
    "verificationMethod": "did:web:user-dts.gaiaid.io#_Qq0UL2Fq651Q0Fjd6TvnYE-faHiOpRlPVQcY_-tA4A",
    "proofPurpose": "assertionMethod",
    "jws": "eyJhbGciOiJFZERTQSIsImI2NCI6ZmFsc2UsImNyaXQiOlsiYjY0Il19..6_k6Dbgug-XvksZvDVi9UxUTAmQ0J76pjdrQyNaQL7eVMmP_SUPZCqso6EN3aEKFSsJrjDJoPJa9rBK99mXvDw"
  }
}

```

service-credential-schema-credential.json:

```json

{
  "@context": [
      "https://www.w3.org/ns/credentials/v2"
  ],
  "id": "https://ecs-trust-registry/service-credential-schema-credential.json",
  "type": ["VerifiableCredential", "JsonSchemaCredential"],
  "issuer": "did:abc:ecs-trust-registry",
  "issuanceDate": "2024-01-01T19:23:24Z",
  "credentialSchema": {
    "id": "https://www.w3.org/2022/credentials/v2/json-schema-credential-schema.json",
    "type": "JsonSchema",
    "digestSRI": "sha384-S57yQDg1MTzF56Oi9DbSQ14u7jBy0RDdx0YbeV7shwhCS88G8SCXeFq82PafhCrW"
  },
  "credentialSubject": {
    "id": "https://ptr-hostname/did:abc:ecs-trust-registry/cs/js/f4524751-8617-40de-bbe6-b2e0fef63c7a",
    "type": "JsonSchema",
    "jsonSchema": {
      "$ref": "https://ptr-hostname/did:abc:ecs-trust-registry/cs/js/f4524751-8617-40de-bbe6-b2e0fef63c7a"
    },
    "digestSRI": "sha384-ABCSGyugst67rs67rdbugsy0RDdx0YbeV7shwhCS88G8SCXeFq82PafhCrW" 
  }
}

```

:::note
Here for trust resolution we need to get did:abc:ecs-trust-registry DIDDocument and verify its TrustRegistry entry (see DID Doc below)
:::

org-credential-presentation.json:

```json

{
  "@context": [
    "https://www.w3.org/ns/credentials/v2"
  ],
  "holder": "did:web:user-dts.gaiaid.io",
  "type": ["VerifiablePresentation"],
  "verifiableCredential": [
    {
      "@context": [
        "https://www.w3.org/ns/credentials/v2"
      ],
      "id": "did:web:user-dts.gaiaid.io",
      "type": ["VerifiableCredential", "OrganizationCredential"],
      "issuer": "did:web:user-dts.gaiaid.io",
      "credentialSubject": {
        "id": "did:web:user-dts.gaiaid.io",
        ...
      },
      ...
      "credentialSchema": {
        "id": "https://ecs-trust-registry/org-credential-schema-credential.json",
        "type": "JsonSchemaCredential"
      }
    }
  ],
  "id": "https://user-dts.gaiaid.io/org-credential-presentation.json",
  "proof": {
    "type": "Ed25519Signature2018",
    "created": "2024-02-08T17:38:46Z",
    "verificationMethod": "did:web:user-dts.gaiaid.io#_Qq0UL2Fq651Q0Fjd6TvnYE-faHiOpRlPVQcY_-tA4A",
    "proofPurpose": "assertionMethod",
    "jws": "eyJhbGciOiJFZERTQSIsImI2NCI6ZmFsc2UsImNyaXQiOlsiYjY0Il19..6_k6Dbgug-XvksZvDVi9UxUTAmQ0J76pjdrQyNaQL7eVMmP_SUPZCqso6EN3aEKFSsJrjDJoPJa9rBK99mXvDw"
  }
}

```

org-credential-schema-credential.json:

```json

{
  "@context": [
      "https://www.w3.org/ns/credentials/v2"
  ],
  "id": "https://example.tr/credentials/OrganizationJsonSchemaCredential",
  "type": ["VerifiableCredential", "JsonSchemaCredential"],
  "issuer": "did:abc:ecs-trust-registry",
  "issuanceDate": "2024-01-01T19:23:24Z",
  "credentialSchema": {
    "id": "https://www.w3.org/2022/credentials/v2/json-schema-credential-schema.json",
    "type": "JsonSchema",
    "digestSRI": "sha384-S57yQDg1MTzF56Oi9DbSQ14u7jBy0RDdx0YbeV7shwhCS88G8SCXeFq82PafhCrW"
  },
  "credentialSubject": {
    "id": "https://ptr-hostname/did:abc:ecs-trust-registry/cs/js/79c37ba1-370f-4008-a857-a7de6649c34b",
    "type": "JsonSchema",
    "jsonSchema": {
      "$ref": "https://ptr-hostname/did:abc:ecs-trust-registry/cs/js/79c37ba1-370f-4008-a857-a7de6649c34b"
    },
    "digestSRI": "sha384-ABCSGyugst67rs67rdbugsy0RDdx0YbeV7shwhCS88G8SCXeFq82PafhCrW"  
  }
}

```

trademark-credential-presentation.json:

```json

{
  "@context": [
    "https://www.w3.org/ns/credentials/v2"
  ],
  "holder": "did:web:user-dts.gaiaid.io",
  "type": ["VerifiablePresentation"],
  "verifiableCredential": [
    {
      "@context": [
        "https://www.w3.org/ns/credentials/v2"
      ],
      "id": "did:web:user-dts.gaiaid.io",
      "type": ["VerifiableCredential", "TrademarkCredential"],
      "issuer": "did:web:trademark.abc",
      "credentialSubject": {
        "id": "did:web:user-dts.gaiaid.io",
        ...
      },
      ...
      "credentialSchema": {
        "id": "https://trademark.abc/credentials/TrademarkJsonSchemaCredential",
        "type": "JsonSchemaCredential"
      }
      "credentialSchema": {
        "id": "https://ptr-hostname/did:example:trademark-trust-registry/cs/js/44219aeb-6094-40ca-9021-fda834d01487",
        "type": "JsonSchema",
        "digestSRI": "sha384-S57yQDg1MTzF56Oi9DbSQ14u7jBy0RDdx0YbeV7shwhCS88G8SCXeFq82PafhCrW"
      }
    }
  ],
  "id": "https://user-dts.gaiaid.io/trademark-credential-presentation.json",
  "proof": {
    "type": "Ed25519Signature2018",
    "created": "2024-02-08T17:38:46Z",
    "verificationMethod": "did:web:user-dts.gaiaid.io#_Qq0UL2Fq651Q0Fjd6TvnYE-faHiOpRlPVQcY_-tA4A",
    "proofPurpose": "assertionMethod",
    "jws": "eyJhbGciOiJFZERTQSIsImI2NCI6ZmFsc2UsImNyaXQiOlsiYjY0Il19..6_k6Dbgug-XvksZvDVi9UxUTAmQ0J76pjdrQyNaQL7eVMmP_SUPZCqso6EN3aEKFSsJrjDJoPJa9rBK99mXvDw"
  }
}

```

TrademarkJsonSchemaCredential.json:

```json

{
  "@context": [
      "https://www.w3.org/ns/credentials/v2"
  ],
  "id": "https://trademark.abc/credentials/TrademarkJsonSchemaCredential",
  "type": ["VerifiableCredential", "JsonSchemaCredential"],
  "issuer": "did:example:trademark-trust-registry",
  "issuanceDate": "2024-01-01T19:23:24Z",
  "credentialSchema": {
    "id": "https://www.w3.org/2022/credentials/v2/json-schema-credential-schema.json",
    "type": "JsonSchema",
    "digestSRI": "sha384-S57yQDg1MTzF56Oi9DbSQ14u7jBy0RDdx0YbeV7shwhCS88G8SCXeFq82PafhCrW"
  },
  "credentialSubject": {
    "id": "https://example-ptr/did:example:trademark-trust-registry/cs/js/44219aeb-6094-40ca-9021-fda834d01487",
    "type": "JsonSchema",
    "jsonSchema": {
       "$ref": "https://example-ptr/did:example:trademark-trust-registry/cs/js/44219aeb-6094-40ca-9021-fda834d01487",
    }
    "digestSRI": "sha384-GHJSGyugst67rs67rdbugsy0RDdx0YbeV7shwhCS88G8SCXeFq82PafhCrW"
  }
}

```

DID Document of did:abc:ecs-trust-registry:


```json
  "service": [
    {
      "id": "did:abc:ecs-trust-registry#ptr-essential-schemas-service-credential-schema-credential",
      "type": "LinkedVerifiablePresentation",
      "serviceEndpoint": ["https://ecs-trust-registry/service-credential-schema-presentation.json"]
    },
    {
      "id": "did:abc:ecs-trust-registry#ptr-essential-schemas-organization-credential-schema-credential",
      "type": "LinkedVerifiablePresentation",
      "serviceEndpoint": ["https://ecs-trust-registry/org-credential-schema-presentation.json"]
    },
    {
      "id": "did:abc:ecs-trust-registry#ptr-essential-schemas-person-credential-schema-credential",
      "type": "LinkedVerifiablePresentation",
      "serviceEndpoint": ["https://ecs-trust-registry/person-credential-schema-presentation.json"]
    },
    {
      "id": "did:abc:ecs-trust-registry#ptr-essential-schemas-trust-registry",
      "type": "TrustRegistry",
      "serviceEndpoint": ["https://ptr-hostname/did:abc:ecs-trust-registry/trqp-2.0/"]
    }
    
    ...
  ]
```

DID Document of did:example:trademark-trust-registry:

```json
  ...
  "service": [
    {
      "id": "did:example:trademark-trust-registry#ptr-schemas-trademark-credential-schema-credential",
      "type": "LinkedVerifiablePresentation",
      "serviceEndpoint": ["https://trademark.abc/credentials/TrademarkJsonSchemaCredential"]
    },
    {
      "id": "did:example:trademark-trust-registry#ptr-schemas-trust-registry",
      "type": "TrustRegistry",
      "serviceEndpoint": ["https://ptr-hostname/did:example:trademark-trust-registry/trqp-2.0/"]
    }
    
    ...
  ]
  ...
```

### Crawlers

*This section is non normative.*

Crawlers will query the [[ref: DID Directory]] `/did-directory/list` method of a [[ref: PTR]] to get the [[ref: DIDs]] of registered [[ref:DTSs]] and resolve them to build an index by recursively resolving all linked data.

For more information, please refer to the [public-trust-registry-specs](https://github.com/2060-io/public-trust-registry-specs).

```plantuml

@startuml
scale max 800 width
object "DID Directory" as didd
object "Crawler" as crawler #3fbdb6
object "Index" as index #3fbdb6
object "DTS #1" as dts1 #7677ed
object "DTS #2" as dts2 #7677ed
object "Browser" as browser #00b0f0
object "User" as user
didd <|-- crawler : iterate over DID directory
crawler --|> dts1 : resolve DID, get linked-vps, index data
crawler --|> dts2 : resolve DID, get linked-vps, index data
browser --|> index: query index
crawler --|> index: create/update index 
user <|-- browser : show result
@enduml

```

### Browser Display of Trust Resolution

#### Credential Wallets

#### Connection Invitation

#### Presentation Request

### Internationalization

*This section is non normative.*

It is the responsibility of browsers and search engines to properly translate credential attributes, as credential schemas are always defined in a single language, that SHOULD be english.
