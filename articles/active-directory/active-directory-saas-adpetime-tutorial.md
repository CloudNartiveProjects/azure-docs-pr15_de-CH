<properties
    pageTitle="Lernprogramm: Azure Active Directory Integration ADP eTime | Microsoft Azure"
    description="So konfigurieren Sie einmaliges Anmelden zwischen Azure Active Directory und ADP eTime."
    services="active-directory"
    documentationCenter=""
    authors="jeevansd"
    manager="femila"
    editor=""/>

<tags
    ms.service="active-directory"
    ms.workload="identity"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="article"
    ms.date="10/17/2016"
    ms.author="jeedes"/>


# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a>Lernprogramm: Azure Active Directory Integration ADP eTime

Dieses Lernprogramm soll zeigen, wie Sie Azure Active Directory (Azure AD) ADP eTime integrieren.  
Azure AD ADP eTime Integration bietet Ihnen folgende Vorteile:

- Sie können in Azure AD steuern Zugriff auf ADP eTime
- Sie können die Benutzer automatisch angemeldet-ADP eTime (einmaliges Anmelden) mit ihren Azure AD-Konten auf Abrufen
- Sie können Ihre Konten zentral - klassischen Azure-Portal verwalten


Wenn Sie weitere Informationen zur Integration von SaaS Anwendung in Azure AD wissen möchten, finden Sie unter [Zugriff und single Sign-on Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Erforderliche Komponenten

Konfiguration von Azure AD-Integration mit ADP eTime benötigen Sie Folgendes:

- Ein Azure AD-Abonnement
- Eine ADP eTime Single Sign-On aktivierte Abonnements


> [AZURE.NOTE] Um Testschritte in diesem Lernprogramm empfehlen nicht wir einer.


Um die Schritte in diesem Lernprogramm zu testen, sollten Sie diese Empfehlung befolgen:

- Verwenden Sie Ihre produktionsumgebung nur dies erforderlich ist.
- Wenn Sie eine Testversion Azure AD-Umgebung haben, können Sie einem einmonatigen Testversion [hier](https://azure.microsoft.com/pricing/free-trial/)abrufen.


## <a name="scenario-description"></a>Beschreibung des Szenarios
Das Ziel dieses Lernprogramms ist Azure AD einmaliges Anmelden in einer Umgebung testen können.  
In diesem Lernprogramm beschriebenen Szenario besteht aus zwei wesentlichen Bausteine:

1. ADP-eTime aus der Galerie hinzufügen
2. Konfigurieren und Testen von Azure AD einmaliges Anmelden


## <a name="adding-adp-etime-from-the-gallery"></a>ADP-eTime aus der Galerie hinzufügen
Konfigurieren Sie die Integration der ADP eTime in Azure AD müssen Sie der Liste der verwalteten SaaS-apps ADP eTime aus der Galerie hinzufügen.

**Um ADP eTime aus der Galerie hinzuzufügen, führen Sie die folgenden Schritte:**

1. Klicken Sie im **klassischen Azure-Portal**im linken Navigationsbereich auf **Active Directory**. 

    ![Active Directory][1]

2. Wählen Sie aus der Liste **Verzeichnis** das Verzeichnis für das Verzeichnisintegration soll.

3. Ansicht Applications in der Verzeichnisansicht öffnen, klicken Sie im oberen Menü auf **Applications** .

    ![Applikationen][2]

4. Klicken Sie am unteren Rand der Seite **Hinzufügen** .

    ![Applikationen][3]

5. Klicken Sie im Dialogfeld **Was möchten Sie tun** auf **eine Anwendung aus dem Katalog hinzufügen**.

    ![Applikationen][4]

6. Geben Sie im Suchfeld **ADP eTime**.

    ![Erstellen einen Testbenutzer Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_01.png)

7. Klicken Sie im Ergebnisbereich wählen Sie **ADP eTime aus**und dann auf **vollständig** die Anwendung hinzufügen.

    ![Erstellen einen Testbenutzer Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_06.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurieren und Testen von Azure AD einmaliges Anmelden
Dieser Abschnitt soll konfigurieren und Testen Azure AD einmaliges ADP eTime basierend auf einen Testbenutzer namens "Britta Simon" angezeigt.

Azure AD muss für einmaliges Anmelden funktioniert wissen, was der Benutzer Gegenstück in ADP eTime Benutzer in Azure AD. In anderen Worten muss eine Verknüpfung Beziehung zwischen Azure AD-Benutzer und die zugehörigen Benutzer in ADP eTime hergestellt werden.  
Diese Beziehung wird eingerichtet, indem den Wert des **Benutzernamens** in Azure AD als **Benutzername** in ADP eTime.

Konfigurieren und Testen Azure AD einmaliges Anmelden mit ADP eTime müssen Sie die folgenden Bausteine durchführen:

1. **[Konfigurieren von Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - der Benutzer dieses Feature verwenden können.
2. **[Benutzer erstellen eine Azure Anzeige testen](#creating-an-azure-ad-test-user)** : Azure AD einmaliges Anmelden mit Britta Simon testen.
4. **[Erstellen einer ADP-eTime Benutzer testen](#creating-a-adpetime-test-user)** : zu Azure AD Darstellung Ihres verknüpft ist eine Entsprechung von Britta Simon ADP eTime.
5. **[Zuweisen von Azure AD Benutzer testen](#assigning-the-azure-ad-test-user)** : Britta Simon Azure AD einmaliges Anmelden verwenden aktivieren.
5. **[Testen von Single Sign-On](#testing-single-sign-on)** - überprüfen, ob die Konfiguration funktioniert.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfiguration von Azure AD einmaliges Anmelden

Ziel dieses Abschnitts ist Azure AD einmaliges Anmelden im klassischen Azure-Portal aktivieren und konfigurieren einmaliges Anmelden in der ADP eTime Anwendung.

Die ADP eTime Anwendung erwartet SAML-Assertionen in einem bestimmten Format hinzufügen benutzerdefiniertes Attribut Mappings der SAML-token Attribute Konfiguration erfordern. Der folgende Screenshot zeigt ein Beispiel dafür. Der Anspruchname werden **"PersonImmutableID"** und der Wert der wir ExtensionAttribute2 zugeordnet haben EmployeeID des Benutzers enthält. Hier die Benutzer Zuordnung vor Azure AD ADP eTime erfolgt auf EmployeeID aber Sie können dies mit einem anderen Wert auch auf Ihre Anwendung. So geben Sie Arbeit mit ADP eTime zuerst den korrekten Bezeichner eines Benutzers und Zuordnung dieser Wert mit dem **"PersonImmutableID"** .  

![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_02.png) 

Die SAML-Assertion konfigurieren zu können, müssen Sie wenden Sie sich an Ihren Support für ADP eTime und den Wert des Attributs Kennung für Ihren Mandanten anfordern. Sie benötigen diesen Wert, um den benutzerdefinierten Anspruch für die Anwendung konfigurieren.


**Konfigurieren Azure AD einmaliges Anmelden mit ADP eTime Schritte:**

1. Klicken Sie im klassischen Azure-Portal, auf der Seite Application Integration **ADP eTime** auf **Konfigurieren einmaliges Anmelden** **Konfigurieren Sie einmaliges Anmelden** Dialogfeld öffnen.

    ![Einmaliges Anmelden konfigurieren][6] 

2. Auf der Seite **Wie möchten Sie Benutzer anmelden ADP eTime** **Azure AD einmaliges Anmelden**wählen Sie und klicken Sie auf **Weiter**.

    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_03.png) 

3. Auf der **App-Einstellungen konfigurieren** , gehen Sie folgendermaßen vor:.

    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_04.png) 


    ein. Geben Sie im Feld **Antwort-URL** den URL ADP eTime Anwendung mithilfe des folgenden Musters Anmelden von Benutzern verwendet: `https://<server name>.adp.com/affwebservices/public/saml2assertionconsumer`.

    b. Klicken Sie auf **Weiter**.

4. Auf der Seite **Konfigurieren einmaliges Anmelden am ADP eTime** Schritte:

    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_05.png) 

    ein. Klicken Sie auf **Metadaten**, und speichern Sie die Datei auf Ihrem Computer.

    b. Klicken Sie auf **Weiter**.


5. Um SSO für die Anwendung konfigurierten, wenden Sie sich an Ihren Support für ADP eTime und e-Mail-Metadatendatei Anhängen herunterladen, damit sie für SSO-Integration konfiguriert werden können.

    > [AZURE.NOTE] Rufen Sie nach dem Konfigurieren der Instanz **ADP eTime** Team **RelayState** Wert werden ab. Führen Sie die nachfolgend aufgeführten Schritte aus, um ihn zu konfigurieren. Nach dieser Konfiguration können Sie die Integration testen. Also bitte beachten Sie, dass dieses wichtige Konfiguration für diese Anwendungsintegration funktioniert.

6. Zum Konfigurieren des RelayState Werts in Azure AD Schritte: 
    
    ein. [Azure-Verwaltungsportal](https://portal.azure.com) als Administrator anmelden.

    b. Klicken Sie im linken Navigationsbereich auf **Weitere Dienste**. 
    
    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_07.png)

    c. Geben Sie im Textfeld **Suchen** **Azure Active Directory**, und klicken Sie dann auf den zugehörigen Link.
    
    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_08.png)

    d. Klicken Sie auf **Anwendung**.

    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_09.png)

    e. Klicken Sie im Abschnitt **Verwalten** auf **Alle Programme**.
    
    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_10.png)

    f. Geben Sie in **das Suchtextfeld** **ADP eTime**, und klicken Sie dann auf den zugehörigen Link. 
    
    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_11.png)

    g. Klicken Sie im Abschnitt **Verwalten** auf **einmaliges Anmelden**.

    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_12.png)

    h. Wählen Sie **Erweiterte URL-Einstellungen anzeigen**.
    
    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_13.png)
    
    Ich. Geben Sie im Textfeld **Relay-Status** mit folgenden Muster:
    
    - Produktions-Umgebung:`https://fed.adp.com/saml/fedlanding.html?<id>` 
    - Staging-Umgebung:`https://fed-stag.adp.com/saml/fedlanding.html?PORTAL`

    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_14.png)

    j. Speichern.

7. Wählen Sie im klassischen Azure-Portal die Konfiguration für einzelne Zeichen Bestätigung und klicken Sie dann auf **Weiter**.

    ![Azure AD einmaliges Anmelden][10]

8. Klicken Sie auf der Seite **Bestätigung für einzelne Zeichen** auf **abgeschlossen**.  

    ![Azure AD einmaliges Anmelden][11]



### <a name="creating-an-azure-ad-test-user"></a>Erstellen einen Testbenutzer Azure AD
Dieser Abschnitt soll im klassischen Azure-Portal namens Britta Simon Testbenutzer erstellen.  
Wählen Sie in der Liste Benutzer **Britta Simon**.

![Azure AD-Benutzer erstellen][20]

**Um einen Testbenutzer in Azure AD zu erstellen, führen Sie die folgenden Schritte:**

1. Klicken Sie im **klassischen Azure-Portal**im linken Navigationsbereich auf **Active Directory**.

    ![Erstellen einen Testbenutzer Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_09.png) 

2. Wählen Sie aus der Liste **Verzeichnis** das Verzeichnis für das Verzeichnisintegration soll.

3. Klicken Sie zum Anzeigen der Benutzerliste im oberen Menü auf **Benutzer**.

    ![Erstellen einen Testbenutzer Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. Klicken Sie das Dialogfeld **Benutzer hinzufügen** der Symbolleiste an der Unterseite, **Benutzer hinzufügen**.

    ![Erstellen einen Testbenutzer Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

5. Auf der Seite **Erzählen zu diesem Benutzer** die folgenden Schritte:

    ![Erstellen einen Testbenutzer Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_05.png) 

    ein. Wählen Sie als **Typ des Benutzers** **neue Benutzer in Ihrer Organisation**.

    b. Geben Sie im Textfeld **Benutzername** **BrittaSimon**.

    c. Klicken Sie auf **Weiter**.

6.  Führen Sie auf das **Benutzerprofil** die folgenden Schritte aus:

    ![Erstellen einen Testbenutzer Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_06.png) 

    ein. Geben Sie im Textfeld **Vorname** **Britta**.  

    b. Im Feld **Nachname** Typ **Simon**.

    c. Geben Sie im Textfeld **Anzeigename** **Britta Simon**.

    d. Wählen Sie in der Liste **Rolle** **Benutzer**.

    e. Klicken Sie auf **Weiter**.

7. Klicken Sie auf der Seite **erhalten temporäres Kennwort** **Erstellen**.

    ![Erstellen einen Testbenutzer Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_07.png) 

8. Führen Sie die folgenden Schritte auf der Seite **Passwort zu erhalten** :

    ![Erstellen einen Testbenutzer Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_08.png) 

    ein. Notieren Sie den Wert für das **Neue Kennwort**.

    b. Klicken Sie auf **abgeschlossen**.   



### <a name="creating-a-adp-etime-test-user"></a>Erstellen einen Testbenutzer ADP eTime

Dieser Abschnitt soll Benutzer Britta Simon in ADP eTime erstellen. Arbeiten Sie mit ADP eTime Support-Team, die Benutzer in ADP eTime Konto hinzuzufügen. 


> [AZURE.NOTE]Benötigen Sie einen Benutzer manuell erstellen, müssen Sie den Support für ADP eTime wenden.


### <a name="assigning-the-azure-ad-test-user"></a>Zuweisen von Azure AD-Testbenutzer

Dieser Abschnitt soll Britta Simon mit Azure einmaliges Anmelden ihren Zugriff auf ADP eTime aktivieren.

![Benutzer zuweisen][200] 

**Britta Simon ADP eTime zuweisen, die folgenden Schritte:**

1. Der Azure-Verwaltungsportal Ansicht Applications in der Verzeichnisansicht öffnen, klicken Sie auf **Programme** im oberen Menü.

    ![Benutzer zuweisen][201] 

2. Wählen Sie in der Anwendungsliste **ADP eTime**.

    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_50.png) 

1. Klicken Sie im Menü oben auf **Benutzer**.

    ![Benutzer zuweisen][203] 

1. Wählen Sie in der Liste Benutzer **Britta Simon**.

2. Klicken Sie auf unten auf **zuweisen**.

    ![Benutzer zuweisen][205]



### <a name="testing-single-sign-on"></a>Testen von Single Sign-On

Dieser Abschnitt soll Azure AD einzelne Anmeldung Überprüfen der Konfiguration mithilfe der.  
Beim Klicken auf die ADP eTime Kachel in der Sie sollte automatisch zur Anwendung eTime ADP angemeldete erhalten.


## <a name="additional-resources"></a>Zusätzliche Ressourcen

* [Liste der Lernprogramme zum SaaS-Apps in Azure Active Directory integrieren](active-directory-saas-tutorial-list.md)
* [Was ist Zugriff und single Sign-on Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_205.png
