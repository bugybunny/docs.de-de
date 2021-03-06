---
title: '&lt;identity&gt;'
ms.date: 03/30/2017
ms.assetid: c1d2ae56-e231-4a07-9c3f-9f13381dc0d8
ms.openlocfilehash: c77f60badd80973f0eeb36f6195b1d4b7617c386
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43509365"
---
# <a name="ltidentitygt"></a>&lt;identity&gt;
Mit dem Identitätselement kann ein Cliententwickler zur Entwurfszeit die erwartete Identität des Diensts angeben. Während des handshakevorgangs zwischen Client und Dienst die Windows Communication Foundation (WCF)-Infrastruktur stellt sicher, dass die Identität des erwarteten Diensts mit den Werten dieses Elements übereinstimmt, und daher kann authentifiziert werden kann. Weitere Informationen finden Sie unter [Dienstidentität und Authentifizierung](../../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md).  
  
 \<system.ServiceModel>  
\<Client >  
\<Endpunkt >  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<identity>  
    <certificate encodedValue="String"/>  
    <certificateReference findValue="String"   
       isChainIncluded="Boolean"  
       storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"storeName="  
       storeLocation="LocalMachine/CurrentUser"  
       X509FindType= Enumeration./>  
    <dns value="String"/>  
    <rsa value="String"/>  
    <servicePrincipalName value="String"/>  
    <usePrincipalName value="String"/>  
</identity>  
```  
  
## <a name="attributes-and-elements"></a>Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.  
  
### <a name="attributes"></a>Attribute  
 Keine  
  
### <a name="child-elements"></a>Untergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|-----------------|  
|certificate|Gibt die Einstellungen eines X.509-Zertifikats an. Dieses Element ist vom Typ <xref:System.ServiceModel.Configuration.CertificateElement>. Es enthält ein `encodedValue`-Attribut, das eine Zeichenfolge ist, die den von diesem Zertifikat codierten Wert angibt.|  
|certificateReference|Legt die Einstellungen für die X.509-Zertifikatüberprüfung fest. Dieses Element ist vom Typ <xref:System.ServiceModel.Configuration.CertificateReferenceElement>.|  
|dns|Gibt den DNS eines X.509-Zertifikats an, das zum Authentifizieren eines Diensts verwendet wird. Dieses Element enthält ein `value`-Attribut, das eine Zeichenfolge ist und die tatsächliche Identität enthält.|  
|rsa|Gibt den Wert des RSA-Felds eines für die Authentifizierung eines Diensts am Client verwendeten X.509-Zertifikats an. Dieses Element enthält ein `value`-Attribut, das eine Zeichenfolge ist und die tatsächliche Identität enthält.|  
|servicePrincipalName|Gibt eine SPN-Identität an, die dem Prinzipalnamen entspricht, der vom Client zum eindeutigen Identifizieren einer Dienstinstanz verwendet wird. Dieses Element enthält ein `value`-Attribut, das eine Zeichenfolge ist und den tatsächlichen Prinzipalnamen enthält. Dieses Element ist vom Typ <xref:System.ServiceModel.Configuration.ServicePrincipalNameElement>.|  
|userPrincipalName|Gibt eine UPN-Identität an, die dem Anmeldenamenstyp eines Benutzers in einem Netzwerk entspricht. Der Benutzerprinzipalname besteht aus den Objekt-Benutzernamen, die in Active Directory, gefolgt von verwendet das at-Zeichen (\@), und klicken Sie dann in der Regel das Domain Name System übergeordneten Domäne. Z. B. möglicherweise Jeff in der Fabrikam.com-Domänenstruktur den Benutzerprinzipalnamen [ jeff@fabrikam.com ](mailto:jeffsmith@fabrikam.com).  Dieses Element enthält ein `value`-Attribut, das eine Zeichenfolge ist und den tatsächlichen Prinzipalnamen enthält. Dieses Element ist vom Typ <xref:System.ServiceModel.Configuration.UserPrincipalNameElement>.|  
  
### <a name="parent-elements"></a>Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|-----------------|  
|[\<Benutzerdefinierte >](../../../../../docs/framework/configure-apps/file-schema/wcf/custom.md)|Gibt einen benutzerdefinierten Peerresolver für eine netPeerTcpBinding an.|  
|[\<Endpunkt >](https://msdn.microsoft.com/library/13aa23b7-2f08-4add-8dbf-a99f8127c017)|Konfiguriert unterschiedliche Endpunkttypen.|  
|[\<issuer>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuer.md)|Gibt den Sicherheitstokendienst (STS) für den Verbunddienst an.|  
|[\<issuerMetadata>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuermetadata.md)|Gibt den Metadatenendpunkt für den Sicherheitstokendienst (STS) eines Verbunddiensts an.|  
|[\<issuedTokenParameters>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuedtokenparameters.md)|Definiert Parameter für ein ausgestelltes Token in einer benutzerdefinierten Bindung.|  
|[\<localIssuer>](../../../../../docs/framework/configure-apps/file-schema/wcf/localissuer.md)|Gibt einen lokalen Sicherheitstokendienst (STS) an.|  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.ServiceModel.Configuration.IdentityElement>  
 <xref:System.ServiceModel.EndpointAddress>  
 <xref:System.ServiceModel.EndpointAddress.Identity%2A>  
 [Dienstidentität und Authentifizierung](../../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)  
 [Endpunkte: Adressen, Bindungen und Verträge](../../../../../docs/framework/wcf/feature-details/endpoints-addresses-bindings-and-contracts.md)
