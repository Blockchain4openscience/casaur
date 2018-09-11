# Certificados emitidos por CASA UR

Caso de uso de emision de certificados utilizando hyperledger blockchain y siguiendo el estandar [Blockcerts](https://www.blockcerts.org/guide/standard.html)

El diseño de la red (Business Network) contien los siguientes elementos:

**Participant** </p> 
`Administrator`: emisor de los certificados, funcionario CASA UR. </p>
`ExternalUser`: usuario externos que consulta el certificado.

**Asset** </p> 
`Certificate Template`: formato generico de certificado (participacion en programa, idiomas, sanciones, etc..) </p>
`Personal Certificate`: emision de un certificado a un estudiante.

**Transaction**
`AddRoster`: emision de certificados a una lista de estudiantes.

Inicialmente el formato9 generico de certificado `Certificate Template` es creado por un funcionario de CASA UR `Administrator`, luego el certificado es emitido a un estudiante mediante la presonalizacion del certificado `Personal Certificate`  o se emite a un conmjunto de estudiantes utilizando la transaccion `AddRoster`. 

Para utilizar la red, vamos a seguir el siguiente ejemplo en el **Test** tab:

Crear un administrador `Administrator`:

```
{
  "$class": "org.degree.Administrator",
  "email": "casaur@urosario.edu.co",
  "firstName": "Juan",
  "lastName": "Admin",
  "publicKey": "CASAURadminKEYtest10092018"
}
```
AQUI VOY
Create a `Certificate Template` asset:

```
{
  "$class": "org.degree.CertificateTemplate",
  "templateId": "0001",
  "globalAdministrator": "resource:org.degree.Administrator#registry@uoflife.com",
  "typeC": "Assertion",
  "badge": {
    "$class": "composer.blockcerts.Badge",
    "id": "urn:uuid:82a4c9f2-3588-457b-80ea-da695571b8fc",
    "typen": "BadgeClass",
    "name": "Certificate of Accomplishment",
    "description": "some words in latin",
    "issuer": {
      "$class": "composer.blockcerts.Issuer",
      "id": "http://ccastroiragorri.github.io/IssuerIdTestR.json",
      "typen": "Profile",
      "name": "University of Life",
      "urln": "http://uoflife.com/",
      "email": "admin@uoflife.com",
      "school": {
        "$class": "composer.blockcerts.School",
        "id": "http://ccastroiragorri.github.io/IssuerIdTestS.json",
        "typen": "School,Extension",
        "name": "School of Social Skills",
        "urln": "http://uoflife.com/identity/groups/",
        "email": "school@uoflife.com",
        "image": "data:image/png;base64,..."
      },
      "signatureLines": {
        "$class": "composer.blockcerts.SignatureLines",
        "typen": "SignatureLine,Extension",
        "name": "John Smith",
        "image": "data:image/png;base64,...",
        "jobtitle": "Dean"
      }
    }
  },
  "context": "https://w3id.org/openbadges/v2,https://w3id.org/blockcerts/v2",
  "revoked": false
}
```

Instantiate an individual `Personal Certificate` for juan.uno@gmail.com:

```
{
  "$class": "org.degree.PersonalCertificate",
  "certId": "1000",
  "templateId": "resource:org.degree.CertificateTemplate#0001",
  "localAdministrator": "resource:org.degree.Administrator#school@uoflife.com",
  "recipient": {
    "$class": "org.degree.Recipient",
    "hashed": false,
    "email": "juan.uno@gmail.com"
  },
  "recipientProfile": {
    "$class": "org.degree.RecipientProfile",
    "typen": "RecipientProfile,Extension",
    "name": "Juan Uno",
    "publicKey": "ecdsa-koblitz-pubkey:merttWiOty56H28YxwckLarrY3DsEpvFbe"
  },
}
```
This transaction has registered generic degree base on a template `templateId:0001` to juan.uno@gmail.com.


Submit a `AddRoster` transaction to personalize many certificates at the same time:

```
{
  "$class": "org.degree.AddRoster",
  "templateId": "resource:org.degree.CertificateTemplate#0001",
  "localAdministrator": "resource:org.degree.Administrator#school@uoflife.com",
  "recipientsInfo": [{ 
    "certId": "1002", 
    "recipient": {
      "email": "juan.dos@gmail.com"
    },
    "recipientProfile": {
      "name": "Juan Dos",
      "publicKey": "ecdsa-koblitz-pubkey:mkfftSiQmc14H65YxwckLenxY3DsEpvFbe"
    }
  },
  { 
    "certId": "1003", 
    "recipient": {
      "email": "juan.tres@gmail.com"
    },
    "recipientProfile": {
      "name": "Juan Tres",
      "publicKey": "ecdsa-koblitz-pubkey:mkwgsgSiQmc14H65YxwckLenxY3DsEpvFbe"
    }
  },
  { 
    "certId": "1004", 
    "recipient": {
      "email": "juan.cuatro@gmail.com"
    },
    "recipientProfile": {
      "name": "Juan cuatro",
      "publicKey": "ecdsa-koblitz-pubkey:mkafafSiQmc14H65YxwckLenxY3DsEpvFbe"
    }
  }
  ]
}
```
This transaction has registered generic degrees base on a template `templateId:0001` to a group of students whose information is introduced as a collection of strings with the fields: id(email), name and publicKey for each student. Note that the transactions in the bna are only defined for writting onto the blockchain. Reading form the blockchain will be coded in the [frontend](https://github.com/ccastroiragorri/blockdegree-frontend) application.


