---
title: '&lt;AppContextSwitchOverrides&gt; Element'
ms.custom: updateeachrelease
ms.date: 09/19/2018
helpviewer_keywords:
- AppContextSwitchOverrides
- compatibility switches
- configuration switches
- configuration
ms.assetid: 4ce07f47-7ddb-4d91-b067-501bd8b88752
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ed2a81c4ec4f679b99f5f5a4d2a2c21270691e93
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/06/2018
ms.locfileid: "48839802"
---
# <a name="ltappcontextswitchoverridesgt-element"></a>&lt;AppContextSwitchOverrides&gt; Element
Definiert mindestens eine Option, die von der <xref:System.AppContext>-Klasse für die Bereitstellung eines Mechanismus zum Deaktivieren neuer Funktionen verwendet wird.  
  
 \<configuration>  
 \<Common Language Runtime >  
\<AppContextSwitchOverrides>  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<AppContextSwitchOverrides value="name1=value1[[;name2=value2];...]" />  
```  
  
## <a name="attributes-and-elements"></a>Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.  
  
### <a name="attributes"></a>Attribute  
  
|Attribut|Beschreibung|  
|---------------|-----------------|  
|`value`|Erforderliches Attribut.<br /><br /> Definiert einen oder mehrere Switchnamen und die zugehörigen booleschen Werte.|  
  
### <a name="value-attribute"></a>value-Attribut  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|"Name = Wert"|Der Name eines vordefinierten Switches zusammen mit seinem Wert (`true` oder `false`). Mehrere Schalter Name/Wert-Paare werden durch Semikolons getrennt (";"). Eine Liste der vordefinierten Switch-Namen, die von .NET Framework unterstützt werden finden Sie im Abschnitt "Hinweise".|  
  
### <a name="child-elements"></a>Untergeordnete Elemente  
 Keine  
  
### <a name="parent-elements"></a>Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|-----------------|  
|`configuration`|Das Stammelement in jeder von den Common Language Runtime- und .NET Framework-Anwendungen verwendeten Konfigurationsdatei.|  
|`runtime`|Enthält Informationen über Laufzeitinitialisierungsoptionen.|  
  
## <a name="remarks"></a>Hinweise  
 Ab .NET Framework 4.6, die `<AppContextSwitchOverrides>` Element in einer Konfigurationsdatei ermöglicht es dem Aufrufer, der eine API, um zu bestimmen, ob ihre app neue Funktionen nutzen oder Kompatibilität mit früheren Versionen einer Bibliothek beibehalten kann. Wenn das Verhalten einer API, die zwischen zwei Versionen einer Bibliothek geändert hat z. B. die `<AppContextSwitchOverrides>` Element ermöglicht es dem Aufrufer dieser API zum Deaktivieren der das neue Verhalten in Versionen der Bibliothek, die die neue Funktionen zu unterstützen. Für apps, die in .NET Framework-APIs Aufrufen der `<AppContextSwitchOverrides>` Element erlaubt, deren apps als eine frühere Version von .NET Framework in die neue Funktionalität zu aktivieren Ziel, wenn ihre app auf einer Version von .NET Framework ausgeführt wird, die mit, Aufrufer die Funktionalität.  
  
 Die `value` Attribut der `<AppContextSwitchOverrides>` Element besteht aus einer einzelnen Zeichenfolge, die von ein oder mehrere durch Semikolons getrennte Name-Wert-Paaren besteht.  Jeder Name identifiziert eines kompatibilitätsswitches und der entsprechende Wert ist ein boolescher Wert (`true` oder `false`), der angibt, ob der Schalter festgelegt ist. Standardmäßig ist der Switch `false`, und die Bibliotheken bieten die neue Funktionen. Sie nur die vorherige Funktionalität bieten, wenn der Schalter festgelegt ist (d. h., der Wert ist `true`). Dadurch können Bibliotheken, neues Verhalten für eine vorhandene API zu bieten, und ermöglicht Aufrufern, die auf das frühere Verhalten zu deaktivieren, die neue Funktionalität abhängig sind.  
  
 .NET Framework unterstützt die folgenden Optionen:  
  
|SwitchName|Beschreibung|Eingeführt wurden|  
|-----------------|-----------------|----------------|  
|`Switch.MS.Internal.`<br/>`DoNotApplyLayoutRoundingToMarginsAndBorderThickness`|Steuert, ob die Windows Presentation Foundation Legacy einen Algorithmus für die Steuerung des Layouts verwendet. Weitere Informationen finden Sie unter [Entschärfung: WPF-Layout](~/docs/framework/migration-guide/mitigation-wpf-layout.md).|.NET Framework 4.6|  
|`Switch.MS.Internal.`<br/>`UseSha1AsDefaultHashAlgorithmForDigitalSignatures`|Steuert, ob der Standardalgorithmus zum Signieren von paketbestandteilen verwendet werden, indem PackageDigitalSignatureManager SHA1- oder SHA-256 ist.|.NET Framework 4.7.1|
|`Switch.System.Activities.`<br/>`UseMD5CryptoServiceProviderForWFDebugger`|Bei Festlegung auf `false`, ermöglicht das Debuggen von XAML-basierten Workflow-Projekte mit Visual Studio, wenn FIPS aktiviert ist. Ohne diese einem <xref:System.NullReferenceException> in Aufrufen von Methoden in der Assembly System.Activities ausgelöst.|.NET Framework 4.7|
|`Switch.System.Activities.`<br/>`UseMD5ForWFDebugger`|Steuert, ob die Prüfsumme für eine Workflowinstanz im Debugger MD5 oder SHA1 verwendet. | .NET Framework 4.7|
|`Switch.System.Diagnostics.`<br/>`IgnorePortablePDBsInStackTraces`|Steuert, ob stapelüberwachungen abrufen, bei Verwendung portabler PDBs Quelldatei- und Zeileninformationen Quellinformationen enthalten können. `false` Um Quelldatei- und Zeileninformationen Quellinformationen sind: andernfalls `true`.|.NET Framework 4.7.2|
|`Switch.System.Drawing.`<br/>`DontSupportPngFramesInIcons`|Steuerelemente, ob die <xref:System.Drawing.Icon.ToBitmap%2A?displayProperty=nameWithType> Methode löst eine Ausnahme aus, wenn ein <xref:System.Drawing.Icon> -Objekt PNG-Bilder aufweist. Weitere Informationen finden Sie unter [Entschärfung: PNG-Bilder in Symbolobjekten](~/docs/framework/migration-guide/mitigation-png-frames-in-icon-objects.md).|.NET Framework 4.6|  
|`Switch.System.Drawing.Text.`<br/>`DoNotRemoveGdiFontsResourcesFromFontCollection`|Bestimmt, ob <xref:System.Drawing.Text.PrivateFontCollection?displayProperty=nameWithType> Objekte freigegeben werden ordnungsgemäß, beim Hinzufügen der Sammlung nach der <xref:System.Drawing.Text.PrivateFontCollection.AddFontFile(System.String)?displayProperty=nameWithType> Methode. `true` Das Legacyverhalten beibehalten; `false` aller privaten Schriftart Objekte freizugeben. |.NET Framework 4.7.2|
|`Switch.System.Drawing.Printing.`</br>`OptimizePrintPreview`|Steuerelemente, ob die Leistung der <xref:System.Windows.Forms.PrintPreviewDialog> für Netzwerkdrucker optimiert ist. Weitere Informationen finden Sie unter [Übersicht über das PrintPreviewDialog-Steuerelement](../../../winforms/controls/printpreviewdialog-control-overview-windows-forms.md).|.NET Framework 4.6|
|`Switch.System.Globalization.NoAsyncCurrentCulture`|Steuert, ob asynchrone Vorgänge nicht aus dem Kontext des aufrufenden Threads übergeben werden. Weitere Informationen finden Sie unter ["CurrentCulture" und "CurrentUICulture" flow aufgabenübergreifende](~/docs/framework/migration-guide/retargeting/4.5.2-4.6.md#currentculture-and-currentuiculture-flow-across-tasks).|.NET Framework 4.6|  
|`Switch.System.IdentityModel.`<br/>`DisableMultipleDNSEntriesInSANCertificate`|Steuerelemente, ob die <xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims%2A?displayProperty=nameWithType> -Methode versucht, den Anspruchstyp nur mit dem letzten DNS-Eintrag übereinstimmen. Weitere Informationen finden Sie unter [Entschärfung: X509CertificateClaimSet.FindClaims-Methode](~/docs/framework/migration-guide/mitigation-x509certificateclaimset-findclaims-method.md).|.NET Framework 4.6.1|  
|`Switch.System.IdentityModel.`<br/>`EnableCachedEmptyDefaultAuthorizationContext`|Steuert, ob AuthorizationContext.Empty ein änderbares Objekt zurückgeben können.|.NET Framework 4.6|  
|`Switch.System.IO.BlockLongPaths`|Steuerelemente, ob Pfade mit mehr als `MAX_PATH` (260 Zeichen) löst eine <xref:System.IO.PathTooLongException>. Weitere Informationen finden Sie unter [Unterstützung für lange Pfade](~/docs/framework/migration-guide/retargeting/4.6.1-4.6.2.md#long-path-support).|.NET Framework 4.6.2|  
|`Switch.System.IO.Compression.`<br/>`DoNotUseNativeZipLibraryForDecompression`|Steuert, ob native OS-Routinen, für die dekomprimierung durch verwendet werden die <xref:System.IO.Compression.DeflateStream> Klasse. `false` systemeigene APIs verwenden zu können; `true` verwenden die <xref:System.IO.Compression.DeflateStream> Implementierung.|.NET Framework 4.7.2|
|`Switch.System.IO.Compression.ZipFile.`<br/>`UseBackslash`|Verwendet den umgekehrten Schrägstrich ("\\") anstatt einen Schrägstrich ("/") als Pfadtrennzeichen in der <xref:System.IO.Compression.ZipArchiveEntry.FullName%2A?displayProperty=nameWithType> Eigenschaft. Weitere Informationen finden Sie unter [Entschärfung: Pfadtrennzeichen für ZipArchiveEntry.FullName](~/docs/framework/migration-guide/mitigation-ziparchiveentry-fullname-path-separator.md).|.NET Framework 4.6.1|  
|`Switch.System.IO.Ports.`<br/>`DoNotCatchSerialStreamThreadExceptions`|Steuert, ob Systemausnahmen ausgeführt, die in Hintergrundthreads, die mit erstellt ausgelöst werden <xref:System.IO.Ports.SerialPort> Streams beenden den Prozess.|.NET Framework 4.7.1| 
|`Switch.System.IO.`<br/>`UseLegacyPathHandling`|Steuert, ob legacy pfadnormalisierung verwendet wird, und die URI-Pfade, indem unterstützt werden die <xref:System.IO.Path.GetDirectoryName%2A?displayProperty=nameWithType> und <xref:System.IO.Path.GetPathRoot%2A?displayProperty=nameWithType> Methoden. Weitere Informationen finden Sie unter [Entschärfung: Pfadnormalisierung](~/docs/framework/migration-guide/mitigation-path-normalization.md) und [Entschärfung: Pfad Doppelpunkt überprüft](~/docs/framework/migration-guide/mitigation-path-colon-checks.md).|.NET Framework 4.6.2|  
|`Switch.System.`<br/>`MemberDescriptorEqualsReturnsFalseIfEquivalent`|Steuert, ob ein Test auf Gleichheit vergleicht die <xref:System.ComponentModel.MemberDescriptor.Category%2A?displayProperty=nameWithType> Eigenschaft eines Objekts mit der <xref:System.ComponentModel.MemberDescriptor.Description%2A?displayProperty=nameWithType> Eigenschaft des zweiten Objekts ist. Weitere Informationen finden Sie unter [falsche Implementierung von MemberDescriptor.Equals](~/docs/framework/migration-guide/retargeting/4.6.1-4.6.2.md#incorrect-implementation-of-memberdescriptorequals).|.NET Framework 4.6.2|  
 `Switch.System.Net.`<br/>`DontCheckCertificateEKUs`|Deaktiviert die zertifikatüberprüfung erweiterte Schlüsselverwendung (EKU)-Objekt-ID (OID). Eine EKU-Erweiterung ist eine Sammlung von OIDs, die Anwendungen kennzeichnen, die den Schlüssel verwenden.|.NET Framework 4.6|
|`Switch.System.Net.`<br/>`DontEnableSchSendAuxRecord`|Deaktiviert. TLS 1.0 Browser Exploit für SSL/TLS (BEAST)-Lösung wird die Verwendung des SCH_SEND_AUX_RECORD deaktivieren.|.NET Framework 4.6|
|`Switch.System.Net.`<br/>`DontEnableSchUseStrongCrypto`|Steuerelemente, ob die <xref:System.Net.ServicePointManager?displayProperty=nameWithType> und <xref:System.Net.Security.SslStream?displayProperty=nameWithType> Klassen können das SSL 3.0-Protokoll verwenden. Weitere Informationen finden Sie unter [Entschärfung: TLS-Protokolle](~/docs/framework/migration-guide/mitigation-tls-protocols.md).|.NET Framework 4.6|
|`Switch.System.Net.`<br/>`DontEnableSystemDefaultTlsVersions`|Deaktiviert die SystemDefault TLS-Versionen, die beim Wiederherstellen auf den Standardwert aus Tls12, Tls11, Tls.|.NET Framework 4.7|
|`Switch.System.Net.`<br/>`DontEnableTlsAlerts`|Deaktiviert die serverseitige Benachrichtigungen SslStream TLS.|.NET Framework 4.7|
|`Switch.System.Runtime.Serialization.`<br/>`DoNotUseECMAScriptV6EscapeControlCharacter` |Steuerelemente, ob die [DataContractJsonSerializer](xref:System.Runtime.Serialization.Json.DataContractJsonSerializer) serialisiert einige Steuerzeichen, die basierend auf den ECMAScript V6 und V8-Standards. Weitere Informationen finden Sie unter [Entschärfung: Serialisierung von Steuerzeichen mit dem DataContractJsonSerializer](Mitigation:%20Serialization%20of%20Control%20Characters%20with%20the%20DataContractJsonSerializer.md)| .NET Framework 4.7 |
|`Switch.System.Runtime.Serialization.`<br/>`DoNotUseTimeZoneInfo`|Steuerelemente, ob die <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> mehrere Anpassungen oder nur eine einzelne Anpassung für eine Zeitzone unterstützt. Wenn `true`, verwendet der <xref:System.TimeZoneInfo> geben, die zum Serialisieren und Deserialisieren von Datums-und Uhrzeitdaten; andernfalls wird die <xref:System.TimeZone> Typ, der mehrere Anpassungsregeln nicht unterstützt.|.NET Framework 4.6.2|
|`Switch.System.Security.ClaimsIdentity.`<br/>`SetActorAsReferenceWhenCopyingClaimsIdentity`|Steuerelemente, ob die <xref:System.Security.Claims.ClaimsIdentity.%23ctor%28System.Security.Principal.IIdentity%29?displayProperty=nameWithType> Konstruktor legt des neuen Objekts <xref:System.Security.Claims.ClaimsIdentity.Actor%2A?displayProperty=nameWithType> Eigenschaft mit dem vorhandenen Objektverweis. Weitere Informationen finden Sie unter [Entschärfung: ClaimsIdentity-Konstruktor](~/docs/framework/migration-guide/mitigation-claimsidentity-constructor.md).|.NET Framework 4.6.2|  
|`Switch.System.Security.Cryptography.`<br/>`AesCryptoServiceProvider.DontCorrectlyResetDecryptor`|Steuerelemente, ob der Versuch der Wiederverwendung bereits ein <xref:System.Security.Cryptography.AesCryptoServiceProvider> Entschlüsselungsmethode löst eine <xref:System.Security.Cryptography.CryptographicException>. Weitere Informationen finden Sie unter [die AesCryptoServiceProvider-Entschlüsselungsmethode stellt eine wiederverwendbare Transformation bereit](~/docs/framework/migration-guide/retargeting/4.6.1-4.6.2.md#aescryptoserviceprovider-decryptor-provides-a-reusable-transform).|.NET Framework 4.6.2|
|`Switch.System.Security.Cryptography.`<br/>`DoNotAddrOfCspParentWindowHandle`|Steuerelemente, ob der Wert des der [CspParameters.ParentWindowHandle](xref:System.Security.Cryptography.CspParameters.ParentWindowHandle) -Eigenschaft ist ein [IntPtr](xref:System.IntPtr) , stellt die Speicheradresse eines Fensters verarbeiten, oder gibt an, ob es ein Fensterhandle (HWND) ist. Weitere Informationen finden Sie unter [Entschärfung: CspParameters.ParentWindowHandle erwartet ein HWND](Mitigation:%20CspParameters.ParentWindowHandle%20Expects%20an%20HWND.md). |.NET Framework 4.7|   
|`Switch.System.Security.Cryptography.Pkcs.`<br/>`UseInsecureHashAlgorithms`|Bestimmt, ob der Standardwert für einige Vorgänge SignedCMS SHA1- oder SHA-256 ist. |.NET Framework 4.7.1|
|`Switch.System.Security.Cryptography.Xml.`<br/>`UseInsecureHashAlgorithms`|Bestimmt, ob der Standardwert für einige Vorgänge SignedXML SHA1- oder SHA-256 ist. |.NET Framework 4.7.1|
|`Switch.System.ServiceModel.`<br/>`AllowUnsignedToHeader`|Bestimmt, ob die `TransportWithMessageCredential` Modus können Nachrichten mit einer nicht signierten "to"-Header. Dies ist ein Opt-in-Schalter. Weitere Informationen finden Sie unter [Laufzeitänderungen in .NET Framework 4.6.1](~/docs/framework/migration-guide/runtime/4.5.2-4.6.1.md#windows-communication-foundation-wcf).|.NET Framework 4.6.1| 
|`Switch.System.ServiceModel.`<br/>`DisableAddressHeaderCollectionValidation`>|Steuerelemente, ob die <xref:System.ServiceModel.Channels.AddressHeaderCollection.%23ctor(System.Collections.Generic.IEnumerable{System.ServiceModel.Channels.AddressHeader})> Konstruktor löst eine <xref:System.ArgumentException> ist eines der Elemente `null`.|.NET Framework 4.7.1| 
|`Switch.System.ServiceModel.`<br />`DisableCngCertificates`|Bestimmt, ob der Versuch, verwenden Sie X509-Zertifikate mit ein CSG-Schlüsselspeicheranbieter eine Ausnahme auslöst. Weitere Informationen finden Sie unter [WCF-transportsicherheit unterstützt Zertifikate, die mithilfe der CNG gespeichert](~/docs/framework/migration-guide/retargeting/4.6.1-4.6.2.md#wcf-transport-security-supports-certificates-stored-using-cng).|.NET Framework 4.6.1|
|`Switch.System.ServiceModel.`<br/>`DisableExplicitConnectionCloseHeader`|Bei der Verwendung des HTTP-Transports mit einem selbst gehosteten Dienst, wenn dieser Wert auf `true` bewirkt, dass WCF ignorieren Hinzufügen einer Anwendung die `Connection: close` -Header auf die Antwortheader für eine Anforderung. Wenn dieser Wert auf `false` ermöglicht Hinzufügen der `Connection: close` Header in die Antwortheader, was dazu führt das Anforderung-Socket schließen, nachdem eine Antwort gesendet wurde.|.NET Framework 4.6|
|`Switch.System.ServiceModel.`<br/>`DisableOperationContextAsyncFlow`|Verarbeitet die Deadlocks, die entstehen, Instanzen von einem eintrittsinvarianzdienst auf einem einzelnen Thread der Ausführung zu einem Zeitpunkt zu beschränken.|.NET Framework 4.6.2|
|`Switch.System.ServiceModel.`<br/>`DisableUsingServicePointManagerSecurityProtocols`|Zusammen mit `Switch.System.Net.DontEnableSchUseStrongCrypto`, bestimmt, ob WCF-nachrichtensicherheit TLS 1.1 und TLS 1.2 verwendet.|.NET Framework 4.7 |    
|`Switch.System.ServiceModel.`<br/>`DontEnableSystemDefaultTlsVersions`|Der Wert `false` legt die Standardkonfiguration, um das Betriebssystem auf dem Protokoll zu ermöglichen. Der Wert `true` die auf das höchste verfügbare Protokoll festgelegt. (Auch auf servicing Branch von früheren Framework-Versionen verfügbar)|.NET Framework 4.7.1|
|`Switch.System.ServiceModel.`<br/>`UseSha1InMsmqEncryptionAlgorithm`|Bestimmt, ob der Algorithmus für die MSMQ-Nachrichten in WCF zum Signieren von Nachrichten SHA1- oder SHA-256.|.NET Framework 4.7.1|
|`Switch.System.ServiceModel.`<br/>`UseSha1InPipeConnectionGetHashAlgorithm`|Steuert, ob WCF ein SHA1- oder einen SHA256-Hash verwendet, um zufällige Namen für named Pipes zu generieren.|.NET Framework 4.7.1|
|`Switch.System.ServiceModel.Internals`<br/>`IncludeNullExceptionMessageInETWTrace`|Steuert, ob Auslösen einer ["NullReferenceException"](xref:System.NullReferenceException) Wenn in der Ausnahmemeldung an null ist.|.NET Framework 4.7|  
|`Switch.System.ServiceProcess.`<br/>`DontThrowExceptionsOnStart`|Steuert, ob beim Start des Diensts ausgelöste Ausnahmen an den Aufrufer der weitergegeben werden die <xref:System.ServiceProcess.ServiceBase.Run%2A?displayProperty=nameWithType> Methode.|.NET Framework 4.7.1|
|`Switch.System.Uri.`<br/>`DontEnableStrictRFC3986ReservedCharacterSets`|Bestimmt, ob bestimmte prozentcodierte Zeichen, die manchmal decodiert wurden jetzt konsistent linkscodiert sind. Wenn `true`, werden decodierte; andernfalls `false`.|.NET Framework 4.7.2|
|`Switch.System.Uri.`<br/>`DontKeepUnicodeBidiFormattingCharacters`|Bestimmt die Behandlung von bidirektionale uniccode-Zeichen in URIs an. `true` Um diese URIs zu entfernen; `false` beibehalten wird und sie Prozent-Codierung.|.NET Framework 4.7.2|
|`Switch.System.Windows.Controls.Grid.`<br/>`StarDefinitionsCanExceedAvailableSpace` |Bestimmt, ob Windows Presentation Foundation einen alten Algorithmus angewendet (`true`) oder einen neuen Algorithmus (`false`) beim Reservieren von Speicherplatz für \*-Spalten. Weitere Informationen finden Sie unter [Entschärfung: Platzzuweisung an mit Stern gekennzeichnete Spalten durch das Rastersteuerelement](Mitigation:%20Grid%20Control's%20Space%20Allocation%20to%20Star-columns.md). |.NET Framework 4.7 |
|`Switch.System.Windows.Controls.TabControl.`<br/>`SelectionPropertiesCanLagBehindSelectionChangedEvent`|Steuerelemente, die den Wert seiner Eigenschaft ausgewählten Wert gibt an, ob ein Selektor oder eine Registerkarte steuern immer aktualisiert werden, vor dem Auslösen der Auswahl geänderten Ereignis zurück.|.NET Framework 4.7.1|
|`Switch.System.Windows.Controls.Text.`<br/>`UseAdornerForTextboxSelectionRendering`|Bestimmt, ob die Auswahl nicht Adorner-Rendering für verfügbar ist. der <xref:System.Windows.Controls.TextBox> und <xref:System.Windows.Controls.PasswordBox> Steuerelemente, um zu verhindern, dass Text okkludierte (`false`), oder ob Text gerendert werden, nur in der Adorner-Ebene (`true`).|.NET Framework 4.7.2|
|`Switch.System.Windows.DoNotScaleForDpiChanges`|Bestimmt, ob für ein pro-System-DPI-Änderungen kommt (Wert `false`) oder pro-Monitor (Wert `true`).|.NET Framework 4.6.2|
|`Switch.System.Windows.Forms.`<br/>`DomainUpDown.UseLegacyScrolling`|Bestimmt, ob der Entwickler speziell behandelt muss die <xref:System.Windows.Forms.DomainUpDown.UpButton?displayProperty=nameWithType> Aktion, wenn Steuerelementtext vorhanden ist. `true` behandelt die <xref:System.Windows.Forms.DomainUpDown.UpButton> Aktion. `false` für die <xref:System.Windows.Forms.DomainUpDown.UpButton?displayProperty=nameWithType> und <xref:System.Windows.Forms.DomainUpDown.DownButton?displayProperty=nameWithType> Aktionen, die ordnungsgemäß synchronisiert werden.|.NET Framework 4.7.2|
|`Switch.System.Windows.Forms.`<br />`DontSupportReentrantFilterMessage`|"OPTS" aus dem Code, der eine benutzerdefinierte ermöglicht <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage%2A?displayProperty=nameWithType> Implementierung, die Nachrichten sicher filtern, ohne eine Ausnahme bei der <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=nameWithType> Methode wird aufgerufen. Weitere Informationen finden Sie unter [Entschärfung: Benutzerdefinierte IMessageFilter.PreFilterMessage-Implementierungen](~/docs/framework/migration-guide/mitigation-custom-imessagefilter-prefiltermessage-implementations.md).|.NET Framework 4.6.1|  
|`Switch.System.Windows.Forms.`<br/>`UseLegacyContextMenuStripSourceControlValue`|Bestimmt, ob die <xref:System.Windows.Forms.ContextMenuStrip.SourceControl?displayProperty=nameWithType> Eigenschaft gibt das Datenquellen-Steuerelement zurück, wenn der Benutzer im Menü aus einer geschachtelten öffnet <xref:System.Windows.Forms.ToolStripMenuItem> Steuerelement. `true` zurückzugebenden `null`, das Legacyverhalten; `false` zurückzugebenden des Datenquellen-Steuerelements.|.NET Framework 4.7.2|
|`Switch.System.Windows.Input.Stylus.`<br/>`EnablePointerSupport`|Bestimmt, ob ein optionales `WM_POINTER`-Basis Touch/Stift-Stapel in WPF-Anwendungen aktiviert ist. Weitere Informationen finden Sie unter [Entschärfung: zeigerbasierte Touch- und Stift-Unterstützung](../../../migration-guide/mitigation-pointer-based-touch-and-stylus-support.md)|.NET Framework 4.7|
|`Switch.System.Windows.Markup.`<br/>`DoNotUseSha256ForMarkupCompilerChecksumAlgorithm`|Bestimmt, ob der Standardhashalgorithmus, der für Prüfsummen verwendet SHA256 (`false`)- oder SHA1 (`true`).|.NET Framework 4.7.2|
|`Switch.System.Windows.Media.ImageSourceConverter.`<br/>`OverrideExceptionWithNullReferenceException`|Steuert, ob ein Legacy ["NullReferenceException"](xref:System.NullReferenceException) wird ausgelöst, anstatt die Ausnahme, die die Ursache der Ausnahme genauer gesagt gibt an (z. B. eine [DirectoryNotFoundException](xref:System.IO.DirectoryNotFoundException) oder eine [ FileNotFoundException](xref:System.IO.FileNotFoundException). Es dient zur Verwendung von Code, von denen abhängt Behandlung der ["NullReferenceException"](xref:System.NullReferenceException). | .NET Framework 4.7 |
|`Switch.UseLegacyAccessibilityFeatures`|Steuerelemente werden, ob der Zugriff auf Funktionen verfügbar ab .NET Framework 4.7.1 aktiviert oder deaktiviert. | .NET Framework 4.7.1 |
|`Switch.UseLegacyAccessibilityFeatures.2`|Gibt an, ob für die Barrierefreiheit in .NET Framework 4.7.2 verfügbar features aktiviert sind Steuerelemente (`false`) oder deaktiviert (`true`). Wenn `true`, `Switch.UseLegacyAccessibilityFeatures` zudem muss `true` Barrierefreiheitsfunktionen für die .NET Framework 4.7.1 aktivieren.|.NET Framework 4.7.2|
|`System.Xml.`<br /><br /> `IgnoreEmptyKeySequences`|Steuert, ob leere schlüsselsequenzen in zusammengesetzten Schlüsseln von XSD-schemavalidierung ignoriert werden. Weitere Informationen finden Sie unter [Entschärfung: XML-Schemaüberprüfung](~/docs/framework/migration-guide/mitigation-xml-schema-validation.md).|.NET Framework 4.6|  
  
> [!NOTE]
>  Anstatt zum Hinzufügen einer `AppContextSwitchOverrides` Element in einer Anwendungskonfigurationsdatei, Sie können auch festlegen die Switches programmgesteuert durch Aufrufen der `static` (in c#) oder `Shared` (in Visual Basic) <xref:System.AppContext.SetSwitch%2A?displayProperty=nameWithType> Methode.  
  
 Bibliotheksentwickler können auch benutzerdefinierte Schalter verwenden, um Aufrufern zum Deaktivieren der geänderten Funktionalität in höheren Versionen ihrer Bibliotheken eingeführt erlauben definieren. Weitere Informationen finden Sie in den Ausführungen zur <xref:System.AppContext>-Klasse.  
  
## <a name="switches-in-aspnet-applications"></a>Schalter in ASP.NET-Anwendungen

Sie können konfigurieren, dass eine ASP.NET-Anwendung zum Verwenden von kompatibilitätseinstellungen durch Hinzufügen einer [ \<hinzufügen >](~/docs/framework/configure-apps/file-schema/appsettings/add-element-for-appsettings.md) Element der [ \<"appSettings" >](~/docs/framework/configure-apps/file-schema/appsettings/index.md) -Abschnitt der Datei "Web.config". 

Im folgenden Beispiel wird die `<add>` Element zum Hinzufügen von zwei Einstellungen, die `<appSettings>` Abschnitt der Datei "Web.config":

```xml
<appSettings>
  <add key="AppContext.SetSwitch:Switch.System.Globalization.NoAsyncCurrentCulture" value="true" />
  <add key="AppContext.SetSwitch:Switch.System.Uri.DontEnableStrictRFC3986ReservedCharacterSets" value="true" />
</appSettings>
```

## <a name="example"></a>Beispiel

 Im folgenden Beispiel wird die `AppContextSwitchOverrides` -Elements definieren eine einzelne anwendungskompatibilitätswechsel `Switch.System.Globalization.NoAsyncCurrentCulture`, Kultur, die verhindert, dass über Threads in asynchrone Methodenaufrufe fließen.  
  
```xml  
<configuration>  
   <runtime>  
      <AppContextSwitchOverrides value="Switch.System.Globalization.NoAsyncCurrentCulture=true" />  
   </runtime>  
</configuration>  
```  
  
 Im folgenden Beispiel wird die `AppContextSwitchOverrides` -Element zum Definieren von zwei Anwendung Kompatibilitätsschalter `Switch.System.Globalization.NoAsyncCurrentCulture` und `Switch.System.IO.BlockLongPaths`. Beachten Sie, dass ein Semikolon zwei Name/Wert-Paare trennt.  
  
```xml  
<configuration>  
    <runtime>  
       <AppContextSwitchOverrides   
          value="Switch.System.Globalization.NoAsyncCurrentCulture=true;Switch.System.IO.BlockLongPaths=true" />  
    </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.AppContext?displayProperty=nameWithType>  
 [\<Common Language Runtime >-Element](runtime-element.md)  
 [\<configuration> Element](../configuration-element.md)
