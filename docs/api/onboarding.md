# API de Onboarding

!!! note ""

    __Version actual de API: 1.0__

__Swagger Sandbox__
!!! note ""

    Accedé a la documentación de swagger sandbox a través de este [__link__](https://onboarding-productor-sandbox.portfoliopersonal.com/swagger/index.html)

__Postman Collection__
!!! note ""

    Accedé a la collección de Postman a traves de este [__link__](https://www.postman.com/portfoliopersonal/workspace/associated-agents-api-ppi). Para poder usar nuestra colección de Postman deberás crear una bifurcación o "Fork".

- Realizá un fork.
- Completá estos datos para comenzar a loguearte:
    - ApiKey 
    - ApiSecret
    - AuthorizedClient 
    - ClientKey
- El AuthorizedClient y ClientKey del ambiente productivo y de sandbox (testing) van a ser proporcionados por mail.

## AUTH
### Login

Tries to log in with the given credentials. Returns a session token which is needed to use the API.

``` title="Method: POST"
/api/{v}/Auth/LoginApi
```

Parameters:

| Name        | Type                                 | Mandatory   | Description                          | Location |
| ----------  | ------------------------------------ | ----------- | ------------------------------------ | -------- |
| v       | string  | required | API Version | Path |
| AuthorizedClient       | string  | required | Authorized Client ID for the API | Headers |
| ClientKey    | string  | required | Client Key for the API | Headers |
| ApiKey    | string  | required | Api Key for the API | Headers |
| ApiSecret    | string  | required | Api Secret for the API | Headers |


``` JSON title="Response Body - 200 Success"
[
  {
    "creationDate": "2022-01-18T18:25:36.269Z",
    "expirationDate": "2022-01-18T18:25:36.269Z",
    "accessToken": "string",
    "expires": 0,
    "refreshToken": "string",
    "tokenType": "string"
  }
]
```

---


## ACCOUNTS
### OpeningFile
Creates a new opening file request

``` title="Method: POST"
/api/{v}/Account/OpeningFile
```

Parameters:

| Name        | Type                                 | Mandatory   | Description                          | Location |
| ----------  | ------------------------------------ | ----------- | ------------------------------------ | -------- |
| v       | string  | required | API Version | Path |
| AuthorizedClient       | string  | required | Authorized Client ID for the API | Headers |
| ClientKey    | string  | required | Client Key for the API | Headers |
| SELFIE    | File  | required | Selfie file (In case a special person validation is needed to open the account)
| IDENTIFICATION    | File  | required | Photo of the identification (only front page. DNI for Argentina, Passport for the rest of the world) | Body |
| IDENTIFICATION_BACK    | File  | optional | Photo of the back of the identification if needed (DNI for Argentina) | Body |
| SOURCE_FUNDS    | File  | optional | Justification to the source of the funds | Body |
| SERVICE    | File  | optional | Photo of a service to validate address (only required for pep) | Body |
| DDJJ    | File  | optional | Declaration for the anti-corruption office | Body |
| SIGNATURE    | File  | optional | Signature Registration file | Body |
| W_FORM    | File  | optional | Form w8/w9 | Body |
| UIF_FORM    | File  | optional | Financial Information Unit form | Body |
| TAX_IDENTIFICATION_FORM    | File  | optional | Tax Identification Form (Cuil registration for Argentina) | Body |
| IIBB    | File  | optional | Justification to the source of the funds (Optional) | Body |


``` JSON title="Request Body"
// Content-Type: multipart/form-data
// Type: text
// Parameter Name: File

{
	"information": {
	  "name": "string",
	  "lastname": "string",
	  "email": "string",
	  "identification": "string",
	  "gender": "string",
	  "birthdate": "1995-07-29T03:00:00Z",
	  "address": {
		"street": "string",
		"number": "string",
		"floor": "string",
		"apartment": null,
		"country": "string",
		"province": "string",
		"postalCode": "string",
		"location": "string"
	  },
	  "cell": "string",
	  "maritalStatus": "string",
	  "nationality": "string",
	  "birthCountry": "string",
	  "birthProvince": "string"
	  
	},
	"tax": {
		"country": "string",
		"condition": "string",
		"iva": "string",
		"identification": "string"
	},
	"employment": {
		"occupationType": "string",
		"autonomousType": null,
		"privateSector": true,
		"startDate": "2020-09-01T03:00:00Z",
		"activity": "string",
		"company": "string",
		"income": "string",
		"sourceFund": "string",
		"amountSourceFund": "string"
	},
	"ddjj": {
		
		"ocde": false
	},
	"InvestmentProfile": {
	  "amount": "string",
	  "instruments": [
		  "RENTA-VARIABLE", "RENTA-FIJA"
	  ],
	  "qualifiedInvestor": false
	},
"ExternalID": "5"
}
```

``` JSON title="Response Body - 200 Success"
[
  {
    "accountNumber": "string",
    "name": "string",
    "officer": {
      "name": "string",
      "eMail": "string",
      "phone": "string"
    }
  }
]
```

---

Retrieves the status of an opening file

``` title="Method: GET"
/api/{v}/Account/OpeningFile
```

Parameters:

| Name        | Type                                 | Mandatory   | Description                          | Location |
| ----------  | ------------------------------------ | ----------- | ------------------------------------ | -------- |
| v       | string  | required | API Version | Path |
| AuthorizedClient       | string  | required | Authorized Client ID for the API | Headers |
| ClientKey    | string  | required | Client Key for the API | Headers |
| openingFileID    | string  | optional | Opening file ID | Query Params |
| externalId    | string  | optional | External ID of the opening file | Query Params |


``` JSON title="Response Body - 200 Success"
  {
    "externalId": "string",
    "state": "string",
    "stateDetail": "string",
    "creationDate": "2023-10-06T14:48:23.532Z",
    "account": "string"
  }
```

---

### States
Retrieves the list of file states

``` title="Method: GET"
/api/{v}/Account/States
```

Parameters:

| Name        | Type                                 | Mandatory   | Description                          | Location |
| ----------  | ------------------------------------ | ----------- | ------------------------------------ | -------- |
| v       | string  | required | API Version | Path |
| AuthorizedClient       | string  | required | Authorized Client ID for the API | Headers |
| ClientKey    | string  | required | Client Key for the API | Headers |


``` JSON title="Response Body - 200 Success"
[
    "FINALIZADO",
    "DOCUMENTACION-FALTANTE",
    "RECHAZADO",
    "EN-PROCESO"
]
```

---

## CONFIGURATION
### Genders
Retrieves a list of available genders to use in information.

``` title="Method: GET"
/api/{v}/Configuration/Genders
```

Parameters:

| Name        | Type                                 | Mandatory   | Description                          | Location |
| ----------  | ------------------------------------ | ----------- | ------------------------------------ | -------- |
| v       | string  | required | API Version | Path |
| AuthorizedClient       | string  | required | Authorized Client ID for the API | Headers |
| ClientKey    | string  | required | Client Key for the API | Headers |

``` JSON title="Response Body - 200 Success"
[
    "MASCULINO",
    "FEMENINO"
]
```

---

### IVA
Retrieves a list of available iva conditions to use in tax.

``` title="Method: GET"
/api/{v}/Configuration/IVA
```

Parameters:

| Name        | Type                                 | Mandatory   | Description                          | Location |
| ----------  | ------------------------------------ | ----------- | ------------------------------------ | -------- |
| v       | string  | required | API Version | Path |
| AuthorizedClient       | string  | required | Authorized Client ID for the API | Headers |
| ClientKey    | string  | required | Client Key for the API | Headers |

``` JSON title="Response Body - 200 Success"
[
    "CONSUMIDOR-FINAL",
    "EXENTO",
    "RESPONSABLE-INSCRIPTO",
    "RESPONSABLE-MONOTRIBUTO"
]
```

---

### TAX Conditions
Retrieves a list of available tax conditions to use in tax.

``` title="Method: GET"
/api/{v}/Configuration/TaxConditions
```

Parameters:

| Name        | Type                                 | Mandatory   | Description                          | Location |
| ----------  | ------------------------------------ | ----------- | ------------------------------------ | -------- |
| v       | string  | required | API Version | Path |
| AuthorizedClient       | string  | required | Authorized Client ID for the API | Headers |
| ClientKey    | string  | required | Client Key for the API | Headers |

``` JSON title="Response Body - 200 Success"
[
    "EXENTO",
    "INSCRIPTO",
    "NO-INSCRIPTO"
]
```

---

### Occupation Types
Retrieves a list of occupation types to use in employment.

``` title="Method: GET"
/api/{v}/Configuration/OccupationTypes
```

Parameters:

| Name        | Type                                 | Mandatory   | Description                          | Location |
| ----------  | ------------------------------------ | ----------- | ------------------------------------ | -------- |
| v       | string  | required | API Version | Path |
| AuthorizedClient       | string  | required | Authorized Client ID for the API | Headers |
| ClientKey    | string  | required | Client Key for the API | Headers |

``` JSON title="Response Body - 200 Success"
[
    "RELACION-DE-DEPENDENCIA",
    "MONOTRIBUTISTA",
    "AUTONOMO",
    "DESOCUPADO",
    "ESTUDIANTE",
    "JUBILADO-PENSIONADO",
    "OTRO"
]
```

---

### Autonomous Types
Retrieves a list of available autonomous types to use in employment.

``` title="Method: GET"
/api/{v}/Configuration/AutonomousTypes
```

Parameters:

| Name        | Type                                 | Mandatory   | Description                          | Location |
| ----------  | ------------------------------------ | ----------- | ------------------------------------ | -------- |
| v       | string  | required | API Version | Path |
| AuthorizedClient       | string  | required | Authorized Client ID for the API | Headers |
| ClientKey    | string  | required | Client Key for the API | Headers |

``` JSON title="Response Body - 200 Success"
[
    "SOCIO",
    "INDEPENDIENTE",
    "JUBILADO-ACTIVIDAD-ESPECIAL"
]
```

---

### Marital Status
Retrieves a list of available marital status to use in information.

``` title="Method: GET"
/api/{v}/Configuration/MaritalStatus
```

Parameters:

| Name        | Type                                 | Mandatory   | Description                          | Location |
| ----------  | ------------------------------------ | ----------- | ------------------------------------ | -------- |
| v       | string  | required | API Version | Path |
| AuthorizedClient       | string  | required | Authorized Client ID for the API | Headers |
| ClientKey    | string  | required | Client Key for the API | Headers |

``` JSON title="Response Body - 200 Success"
[
    "SOLTERO",
    "CASADO",
    "DIVORCIADO",
    "VIUDO",
    "CONCUBINO"
]
```

---

### Source Funds
Retrieves a list of available source funds to use in employment.

``` title="Method: GET"
/api/{v}/Configuration/SourceFunds
```

Parameters:

| Name        | Type                                 | Mandatory   | Description                          | Location |
| ----------  | ------------------------------------ | ----------- | ------------------------------------ | -------- |
| v       | string  | required | API Version | Path |
| AuthorizedClient       | string  | required | Authorized Client ID for the API | Headers |
| ClientKey    | string  | required | Client Key for the API | Headers |

``` JSON title="Response Body - 200 Success"
[
    "RELACION-DE-DEPENDENCIA",
    "AUTONOMO",
    "VENTA-BIENES",
    "INVERSIONES",
    "HERENCIA",
    "DONACION",
    "INGRESOS-SOCIETARIOS",
    "JUBILACION"
]
```

---

### Countries
Retrieves a list of available countries to use in information and tax.

``` title="Method: GET"
/api/{v}/Configuration/Countries
```

Parameters:

| Name        | Type                                 | Mandatory   | Description                          | Location |
| ----------  | ------------------------------------ | ----------- | ------------------------------------ | -------- |
| v       | string  | required | API Version | Path |
| AuthorizedClient       | string  | required | Authorized Client ID for the API | Headers |
| ClientKey    | string  | required | Client Key for the API | Headers |

``` JSON title="Response Body - 200 Success"
[
    "ARGENTINA",
    "ALEMANIA",
    "ANGOLA",
    "ANTILLAS",
    "AUSTRALIA",
    "AUSTRIA",
    "B.V.I",
    "BAHAMAS",
    "BARBADOS",
    "BELGICA",
    "BELIZE",
    "BERMUDA",
    "BOLIVIA",
    "BRASIL",
    "CANADIENSE",
    "CAYMAN-ISLANDS",
    "CHILE",
    "CHINA",
    "COLOMBIA",
    "COSTA-RICA",
    "CUBANA",
    "CURACAO",
    "CURAZAO",
    "ECUADOR",
    "ESPAÑA",
    "ESTADOS-UNIDOS",
    "FRANCIA",
    "GRAND-CAYMAN/CAYMAN-ISLANDS",
    "GRECIA",
    "HOLANDA",
    "INGLATERRA",
    "IRLANDA",
    "ISLAS-DEL-CANAL",
    "ISLE-OF-MAN",
    "ITALIA",
    "LUXEMBURGO",
    "NICARAGUA",
    "NIUE",
    "NO-INFORMA",
    "PANAMA",
    "PARAGUAY",
    "PERU",
    "REINO-UNIDO",
    "REPUBLIC-OF-ARMENIA",
    "REPÚBLICA-DOMINICANA",
    "SINGAPUR",
    "SUDAFRICA",
    "SUIZA",
    "TAILANDIA",
    "URUGUAY",
    "VENEZUELA"
]
```

---

### Provinces
Retrieves a list of available provinces of Argentina to use in information.

``` title="Method: GET"
/api/{v}/Configuration/Provinces
```

Parameters:

| Name        | Type                                 | Mandatory   | Description                          | Location |
| ----------  | ------------------------------------ | ----------- | ------------------------------------ | -------- |
| v       | string  | required | API Version | Path |
| AuthorizedClient       | string  | required | Authorized Client ID for the API | Headers |
| ClientKey    | string  | required | Client Key for the API | Headers |

``` JSON title="Response Body - 200 Success"
[
    "MISIONES",
    "SAN-LUIS",
    "SAN-JUAN",
    "ENTRE-RÍOS",
    "SANTA-CRUZ",
    "RÍO-NEGRO",
    "CHUBUT",
    "CÓRDOBA",
    "MENDOZA",
    "LA-RIOJA",
    "CATAMARCA",
    "LA-PAMPA",
    "SANTIAGO-DEL-ESTERO",
    "CORRIENTES",
    "SANTA-FE",
    "TUCUMÁN",
    "NEUQUÉN",
    "SALTA",
    "CHACO",
    "FORMOSA",
    "JUJUY",
    "CIUDAD-AUTÓNOMA-DE-BUENOS-AIRES",
    "BUENOS-AIRES",
    "TIERRA-DEL-FUEGO,-ANTÁRTIDA-E-ISLAS-DEL-ATLÁNTICO-SUR"
]
```

---

### Instruments
Retrieves a list of available instruments to use in investmentprofile.

``` title="Method: GET"
/api/{v}/Configuration/Instruments
```

Parameters:

| Name        | Type                                 | Mandatory   | Description                          | Location |
| ----------  | ------------------------------------ | ----------- | ------------------------------------ | -------- |
| v       | string  | required | API Version | Path |
| AuthorizedClient       | string  | required | Authorized Client ID for the API | Headers |
| ClientKey    | string  | required | Client Key for the API | Headers |

``` JSON title="Response Body - 200 Success"
[
    "FCI",
    "RENTA-FIJA",
    "RENTA-VARIABLE",
    "FUTUROS",
    "ACTIVOS-EXTERIOR"
]
```

---

### Pep Types
Retrieves a list of available PEP types to use in ddjj.

``` title="Method: GET"
/api/{v}/Configuration/PepTypes
```

Parameters:

| Name        | Type                                 | Mandatory   | Description                          | Location |
| ----------  | ------------------------------------ | ----------- | ------------------------------------ | -------- |
| v       | string  | required | API Version | Path |
| AuthorizedClient       | string  | required | Authorized Client ID for the API | Headers |
| ClientKey    | string  | required | Client Key for the API | Headers |

``` JSON title="Response Body - 200 Success"
[
    "CONYUGE",
    "FAMILIAR-DIRECTO",
    "PERSONA-CERCANA"
]
```

---

### SO Types
Retrieves a list of available SO Types to use in ddjj.

``` title="Method: GET"
/api/{v}/Configuration/SOTypes
```

Parameters:

| Name        | Type                                 | Mandatory   | Description                          | Location |
| ----------  | ------------------------------------ | ----------- | ------------------------------------ | -------- |
| v       | string  | required | API Version | Path |
| AuthorizedClient       | string  | required | Authorized Client ID for the API | Headers |
| ClientKey    | string  | required | Client Key for the API | Headers |

``` JSON title="Response Body - 200 Success"
[
    "AUTORIZADO-BCRA",
    "JUEGOS-AZAR",
    "OPERATORIA-ARTE",
    "ESCRIBANO-PUBLICO",
    "DESPACHANTE-ADUANA",
    "PRODUCTOR",
    "CONTADOR",
    "CORREDOR-INMOBILIARIO",
    "COMPRAVENTA-AUTOMOVILES",
    "FIDUCIARIO"
]
```

---

### Fatca Types
Retrieves a list of available Fatca types to use in ddjj.

``` title="Method: GET"
/api/{v}/Configuration/FatcaTypes
```

Parameters:

| Name        | Type                                 | Mandatory   | Description                          | Location |
| ----------  | ------------------------------------ | ----------- | ------------------------------------ | -------- |
| v       | string  | required | API Version | Path |
| AuthorizedClient       | string  | required | Authorized Client ID for the API | Headers |
| ClientKey    | string  | required | Client Key for the API | Headers |

``` JSON title="Response Body - 200 Success"
[
    "NACIO-EEUU",
    "NACIONALIDAD-EEUU",
    "DOMICILIO",
    "GREEN-CARD",
    "RESIDENCIA-FISCAL",
    "OFICINA",
    "RESIDENCIA"
]
```