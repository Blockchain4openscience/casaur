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

Inicialmente el formato generico de certificado `Certificate Template` es creado por un funcionario de CASA UR `Administrator`, luego el certificado es emitido a un estudiante mediante la presonalizacion del certificado `Personal Certificate`  o se emite a un conmjunto de estudiantes utilizando la transaccion `AddRoster`. 

Para utilizar la red, vamos a seguir el siguiente ejemplo en el **Test** tab:

## Creacion de participante administrador (funcionario CASA UR)

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
## Creacion de formatos de certificacion, ejemplos: participacion en programa, requisito de idioma, sancion disciplinaria.

Creacion de formato de certificado `Certificate Template` (participacion en programa: 0001):

```
{
  "$class": "org.degree.CertificateTemplate",
  "templateId": "0001", 
  "administrator": "resource:org.degree.Administrator#block4opsc@gmail.com",
  "typeC": "Assertion",
  "badge": {
    "$class": "composer.blockcerts.Badge",
    "id": "Conducta sin Antecedentes_Inactivo", 
    "typen": "BadgeClass",
    "name": "Certifica", 
    "description": "Que $name$, identificado(a) con documento de identidad No. $legalid$, estuvo vinculado(a) como estudiante del programa de $program$ durante el periodo comprendido entre $firtsdate$ y $lastdate$ y no registra antecedentes disciplinarios en su historia.",
    "criteria": "Se expide a solicitud del titular de la informacion y previa autorizacion del mismo, en Bogotá D.C. en la fecha $timestamp$.",
    "issuer": {
      "$class": "composer.blockcerts.Issuer",
      "id": "NIT. 860.007.759-3", 
      "typen": "Profile",
      "name": "Universidad del Rosario", 
      "urln": "www.urosario.edu.co",
      "email": "admin@urosario.edu.co",
      "description": "",
      "image": "https://github.com/Blockchain4openscience/diplomasExamples/blob/master/images/logoUR2.png",
      "signatureLines": {
        "$class": "composer.blockcerts.SignatureLines",
        "typen": "SignatureLine,Extension",
        "name": "John Smith", 
        "image": "https://github.com/Blockchain4openscience/diplomasExamples/blob/master/images/signature.png",
        "jobtitle": "Coordinador(a) de CASA UR"
      },
      "menid": "Personería Jurídica Res. 58 de septiembre 16 de 1895"
    }
  },
  "context": "https://w3id.org/openbadges/v2,https://w3id.org/blockcerts/v2",
  "revoked": false
}
```
Creacion de formato de certificado `Certificate Template` (requisitos de idioma: 0002):

```
{
  "$class": "org.degree.CertificateTemplate",
  "templateId": "0002", 
  "administrator": "resource:org.degree.Administrator#block4opsc@gmail.com",
  "typeC": "Assertion",
  "badge": {
    "$class": "composer.blockcerts.Badge",
    "id": "Tercera Lengua (certifica cumplimiento del requisito)", 
    "typen": "BadgeClass",
    "name": "Certifica", 
    "description": "Que $name$, identificado(a) con documento de identidad No. $legalid$, en el programa de $program$, debe cumplir el requisito academico de tercer idioma exigido por la Univeridad segun el Decreto Rectoral 1404 de 10 de febrero de 2016, para lo cual debera cumplir en cualquier momento antes de culminar el programa academcio con alguna de las siguientes opciones: Opcion 1: Aprobar 8 creditos en unos d elos siguientes idiomas ofertados por la Escuela de Ciencias Humanas: aleman, italiano, frances o portugues como requisito de grado. Estos creditos deberan inscribirse y cursarse dentro de las asignaturas ofertadas por la Universidad en estos idiopmas. Opcion 2: acreditar nivel A2 con un examen internacional reconocido por la Universidad en alguno de los siguientes idiomas: aleman, italiano, frances o portugues. En la fecha se certifica que el(a) estudiante acredita el cumplimiento del requisito de tercera lengua con la opcion $opcion$ en el idioma $idiomareq$.",
    "criteria": "Se expide a solicitud del titular de la informacion y previa autorizacion del mismo, en Bogotá D.C. en la fecha $timestamp$.",
    "issuer": {
      "$class": "composer.blockcerts.Issuer",
      "id": "NIT. 860.007.759-3", 
      "typen": "Profile",
      "name": "Universidad del Rosario", 
      "urln": "www.urosario.edu.co",
      "email": "admin@urosario.edu.co",
      "description": "",
      "image": "https://github.com/Blockchain4openscience/diplomasExamples/blob/master/images/logoUR2.png",
      "signatureLines": {
        "$class": "composer.blockcerts.SignatureLines",
        "typen": "SignatureLine,Extension",
        "name": "John Smith", 
        "image": "https://github.com/Blockchain4openscience/diplomasExamples/blob/master/images/signature.png",
        "jobtitle": "Coordinador(a) de CASA UR"
      },
      "menid": "Personería Jurídica Res. 58 de septiembre 16 de 1895"
    }
  },
  "context": "https://w3id.org/openbadges/v2,https://w3id.org/blockcerts/v2",
  "revoked": false
}
```
Creacion de formato de certificado `Certificate Template` (sancion disciplinaria: 0003):

```
{
  "$class": "org.degree.CertificateTemplate",
  "templateId": "0003", 
  "administrator": "resource:org.degree.Administrator#block4opsc@gmail.com",
  "typeC": "Assertion",
  "badge": {
    "$class": "composer.blockcerts.Badge",
    "id": "Conducta con Antecedentes_Activo", 
    "typen": "BadgeClass",
    "name": "Certifica", 
    "description": "Que $name$, identificado(a) con documento de identidad No. $legalid$, se encuentra actualmente vinculado(a) como estudiante del programa $program$,y tiene registrados los siguientes antecedentes disciplinarios en su historia: 1. Sancion disciplinaria de $sanction$ por el termino de $periods$ periodos academicos a partir de la fecha $firstdate$ por la falta disciplinaria $fault$, impuesta en la fecha $faultdate$ en el proceso disciplinario No. $processid$.",
    "criteria": "Se expide a solicitud del titular de la informacion y previa autorizacion del mismo, en Bogotá D.C. en la fecha $timestamp$.",
    "issuer": {
      "$class": "composer.blockcerts.Issuer",
      "id": "NIT. 860.007.759-3", 
      "typen": "Profile",
      "name": "Universidad del Rosario", 
      "urln": "www.urosario.edu.co",
      "email": "admin@urosario.edu.co",
      "description": "",
      "image": "https://github.com/Blockchain4openscience/diplomasExamples/blob/master/images/logoUR2.png",
      "signatureLines": {
        "$class": "composer.blockcerts.SignatureLines",
        "typen": "SignatureLine,Extension",
        "name": "John Smith", 
        "image": "https://github.com/Blockchain4openscience/diplomasExamples/blob/master/images/signature.png",
        "jobtitle": "Coordinador(a) de CASA UR"
      },
      "menid": "Personería Jurídica Res. 58 de septiembre 16 de 1895"
    }
  },
  "context": "https://w3id.org/openbadges/v2,https://w3id.org/blockcerts/v2",
  "revoked": false
}
```

## Emision de certificados a uno o varios estudiantes

Emision de certificado a un estudiante `Personal Certificate` identificado por su correo electronico for juan.uno@urosario.edu.co:

```
{
  "$class": "org.degree.PersonalCertificate",
  "certId": "1000",
  "templateId": "resource:org.degree.CertificateTemplate#0001",
  "administrator": "resource:org.degree.Administrator#casaur@urosario.edu.co",
  "recipient": {
    "$class": "org.degree.Recipient",
    "hashed": false,
    "email": "juan.uno@urosario.edu.co"
  },
  "recipientProfile": {
    "$class": "org.degree.RecipientProfile",
    "typen": "RecipientProfile,Extension",
    "name": "Juan Uno",
    "publicKey": "ecdsa-koblitz-pubkey:juan1",
    "legalid": "10123456",
    "assertions": {
      "$class": "org.degree.Assertions",
      "program": "Economia",
      "firtsdate": "2010-08-10",
      "lastdate": "2015-06-15"
    }
  },
  "hash": ""
}
```

Esta transaccion ha emitido un certificado de particiapacion en programa `templateId:0001` a juan.uno@urosario.edu.co.

Emision masiva de certificados mediante la transaccion `AddRoster` permite la personalizacion de varios certificados al mismo tiempo:

```
{
  "$class": "org.degree.AddRoster",
  "templateId": "resource:org.degree.CertificateTemplate#0001",
  "administrator": "resource:org.degree.Administrator#casaur@urosario.edu.co",
  "recipientsInfo": [{ 
    "certId": "1002", 
    "recipient": {
      "email": "juan.dos@gmail.com"
    },
    "recipientProfile": {
      "$class": "org.degree.RecipientProfile",
      "typen": "RecipientProfile,Extension",
      "name": "Juan Dos",
      "publicKey": "ecdsa-koblitz-pubkey:juan2",
      "legalid": "10789123",
      "assertions": {
      "$class": "org.degree.Assertions",
      "program": "Ciencia Politica y Gobierno",
      "firtsdate": "2011-08-10",
      "lastdate": "2016-06-15"
    }
  }},{
    "certId": "1003", 
    "recipient": {
      "email": "juan.tres@gmail.com"
    },
    "recipientProfile": {
      "$class": "org.degree.RecipientProfile",
      "typen": "RecipientProfile,Extension",
      "name": "Juan Tres",
      "publicKey": "ecdsa-koblitz-pubkey:juan3",
      "legalid": "10456689",
      "assertions": {
      "$class": "org.degree.Assertions",
      "program": "Medicina",
      "firtsdate": "2009-08-10",
      "lastdate": "2014-06-15"
    }
  },
    "certId": "1004", 
    "recipient": {
      "email": "juan.cuatro@gmail.com"
    },
    "recipientProfile": {
      "$class": "org.degree.RecipientProfile",
      "typen": "RecipientProfile,Extension",
      "name": "Juan Cuatro",
      "publicKey": "ecdsa-koblitz-pubkey:juan4",
      "legalid": "10987654",
      "assertions": {
      "$class": "org.degree.Assertions",
      "program": "Biologia",
      "firtsdate": "2004-08-10",
      "lastdate": "2018-06-15"
    }
  }}
  ]
}
```
Mediante la anterior transaccion se han emitido un conjunto de certificados de participacion de programa `templateId:0001` a un conjunto de estudiantes cuya informacion contiene los siguientes campos: id(email), nombre, publicKey, legalid(cedula), programa academico y fechas de vinculacion al programa. 
