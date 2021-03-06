<properties
    pageTitle="Lernprogramm: Azure Active Directory-Integration mit BetterWorks | Microsoft Azure"
    description="So konfigurieren Sie einmaliges Anmelden zwischen Azure Active Directory und BetterWorks."
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
    ms.date="09/29/2016"
    ms.author="jeedes"/>


# <a name="tutorial-azure-active-directory-integration-with-betterworks"></a>Lernprogramm: Azure Active Directory-Integration mit BetterWorks

Das Ziel dieses Lernprogramms ist, wie BetterWorks in Azure Active Directory (Azure AD) integriert werden.

Azure AD BetterWorks Integration bietet Ihnen folgende Vorteile:

- Sie können in Azure AD steuern, wer auf BetterWorks Zugriff
- Sie können die Benutzer automatisch angemeldet-BetterWorks (einmaliges Anmelden) mit ihren Azure AD-Konten auf Abrufen
- Sie können Ihre Konten zentral - klassischen Azure-Portal verwalten

Wenn Sie weitere Informationen zur Integration von SaaS Anwendung in Azure AD wissen möchten, finden Sie unter [Zugriff und single Sign-on Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Erforderliche Komponenten

Konfiguration von Azure AD-Integration mit BetterWorks benötigen Sie Folgendes:

- Ein Azure AD-Abonnement
- Ein BetterWorks Single Sign-On aktivierte Abonnements


> [AZURE.NOTE] Um Testschritte in diesem Lernprogramm empfehlen nicht wir einer.


Um die Schritte in diesem Lernprogramm zu testen, sollten Sie diese Empfehlung befolgen:

- Verwenden Sie Ihre produktionsumgebung nur dies erforderlich ist.
- Wenn Sie eine Testversion Azure AD-Umgebung haben, können Sie einem einmonatigen Testversion [hier](https://azure.microsoft.com/pricing/free-trial/)abrufen.


## <a name="scenario-description"></a>Beschreibung des Szenarios
Das Ziel dieses Lernprogramms ist Azure AD einmaliges Anmelden in einer Umgebung testen können.

In diesem Lernprogramm beschriebenen Szenario besteht aus zwei wesentlichen Bausteine:

1. BetterWorks aus der Galerie hinzufügen
2. Konfigurieren und Testen von Azure AD einmaliges Anmelden


## <a name="adding-betterworks-from-the-gallery"></a>BetterWorks aus der Galerie hinzufügen
Konfigurieren Sie die Integration von BetterWorks in Azure AD müssen Sie der Liste der verwalteten SaaS-apps BetterWorks aus dem Katalog hinzufügen.

**Um BetterWorks aus der Galerie hinzuzufügen, führen Sie die folgenden Schritte:**

1. Klicken Sie im **klassischen Azure-Portal**im linken Navigationsbereich auf **Active Directory**. 

    ![Active Directory][1]

2. Wählen Sie aus der Liste **Verzeichnis** das Verzeichnis für das Verzeichnisintegration soll.

3. Ansicht Applications in der Verzeichnisansicht öffnen, klicken Sie im oberen Menü auf **Applications** .
    
    ![Applikationen][2]

4. Klicken Sie am unteren Rand der Seite **Hinzufügen** .
    
    ![Applikationen][3]

5. Klicken Sie im Dialogfeld **Was möchten Sie tun** auf **eine Anwendung aus dem Katalog hinzufügen**.

    ![Applikationen][4]

6. Geben Sie im Suchfeld **BetterWorks**.

    ![Erstellen einen Testbenutzer Azure AD](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_01.png)

7. Wählen Sie im Ergebnisbereich **BetterWorks aus**und dann auf **vollständig** die Anwendung hinzufügen.

    ![Wählen die Anwendung in der Galerie](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurieren und Testen von Azure AD einmaliges Anmelden
Dieser Abschnitt soll wie Sie konfigurieren und Testen Azure AD SSO-BetterWorks basierend auf einen Testbenutzer "Britta Simon" bezeichnet.

Azure AD muss für einmaliges Anmelden funktioniert wissen, was der Benutzer Gegenstück in BetterWorks einen Benutzer in Azure AD. In anderen Worten muss eine Verknüpfung Beziehung zwischen Azure AD-Benutzer und die zugehörigen Benutzer in BetterWorks hergestellt werden.

Diese Beziehung wird eingerichtet, indem den Wert des **Benutzernamens** in Azure AD als **Benutzername** in BetterWorks.

Konfigurieren und Testen Azure AD einmaliges Anmelden mit BetterWorks müssen Sie die folgenden Bausteine durchführen:

1. **[Konfigurieren von Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - der Benutzer dieses Feature verwenden können.
2. **[Benutzer erstellen eine Azure Anzeige testen](#creating-an-azure-ad-test-user)** : Azure AD einmaliges Anmelden mit Britta Simon testen.
3. **[Erstellen einer BetterWorks testen Benutzer](#creating-a-betterworks-test-user)** - Gegenstück Britta Simon BetterWorks enthalten, die in Azure AD Darstellung Ihres verknüpft ist.
4. **[Zuweisen von Azure AD Benutzer testen](#assigning-the-azure-ad-test-user)** : Britta Simon Azure AD einmaliges Anmelden verwenden aktivieren.
5. **[Testen von Single Sign-On](#testing-single-sign-on)** - überprüfen, ob die Konfiguration funktioniert.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfiguration von Azure AD einmaliges Anmelden

Ziel dieses Abschnitts ist Azure AD einmaliges Anmelden im klassischen Azure-Portal aktivieren und konfigurieren einmaliges Anmelden in der Anwendung BetterWorks.

BetterWorks erwartet SAML-Assertionen in einem bestimmten Format. Konfigurieren Sie folgenden Angaben für diese Anwendung. Sie können die Werte dieser Attribute auf der Registerkarte "**Polysaccharid**" der Anwendung verwalten. Der folgende Screenshot zeigt ein Beispiel dafür. 

![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_06.png)

**Konfigurieren Azure AD einmaliges Anmelden mit BetterWorks die folgenden Schritte:**

1. **Klicken Sie auf im klassischen Azure-Portal, auf Integration **BetterWorks** Anwendung im Menü oben.**

    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_07.png)

2. Klicken Sie im Dialogfeld **SAML-token Attribute** für jede Zeile in der Tabelle angezeigten folgendermaßen:
    

  	| Attributname | Attributwert |
  	| --- | --- |    
  	| saml_token | bd189cf6-1701-11e6-8f90-d26992eca2a5 |

    ein. Klicken Sie auf **Hinzufügen Benutzer Attribure** Dialogfeld **Attribut hinzufügen** .

    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_12.png)
    
    b. Geben Sie im Textfeld **Attributname** Attributnamen für diese Zeile angezeigt.
    
    c. Geben Sie aus der Liste **Attributwert** Saml-token ID für diese Zeile angezeigt.
    
    d. Klicken Sie auf **vollständige**

3. Klicken Sie im Menü oben auf **Schnellstart**.

    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_11.png) 

4. Auf der Seite **Wie möchten Sie Benutzer zum Anmelden bei BetterWorks** **Azure AD einmaliges Anmelden**wählen Sie und klicken Sie auf **Weiter**.
    
    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_03.png)

5. Auf der **App-Einstellungen konfigurieren** Wenn Sie die Anwendung im **IDP initiiert Modus**konfigurieren möchten, folgendermaßen:

    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_04.png)


    ein. Geben Sie im Textfeld **Bezeichner** die URL in dem folgenden Muster:`https://app.betterworks.com/saml2/metadata/`


    b. Geben Sie im Feld **Antwort-URL** den URL in das folgende Muster:`https://app.betterworks.com/saml2/acs/`


    c. Klicken Sie auf **Weiter**

6. Wenn Sie die Anwendung im **SP initiiert Modus**konfigurieren möchten, führen Sie auf der **App-Einstellungen konfigurieren** , die die folgenden Schritte:

    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_10.png)

    ein.  Wählen Sie **Show advanced Settings (optional)**.



    b. **Anmelde-URL** -Textfeld Geben Sie die URL verwendet Ihre Benutzer anmelden, der BetterWorks-Anwendung mit dem folgenden Muster:`https://app.betterworks.com`

    b. Klicken Sie auf **Weiter**.

7. Führen Sie auf der Seite **Konfigurieren einmaliges Anmelden am BetterWorks** die folgenden Schritte aus und klicken Sie auf **Weiter**:

    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_05.png)

    ein. Klicken Sie auf **Metadaten**, und speichern Sie die Datei auf Ihrem Computer.

    b. Klicken Sie auf **Weiter**.

8. Um SSO für die Anwendung konfigurierten erhalten, wenden Sie die BetterWorks über <mailto:support@betterworks.com>. Anfügen der heruntergeladenen Metadatendatei und gemeinsam mit BetterWorks SSO auf Seite einrichten.

9. Wählen Sie im klassischen Portal die Konfiguration für einzelne Zeichen Bestätigung, und klicken Sie auf **Weiter**.
    
    ![Azure AD einmaliges Anmelden][10]

10. Klicken Sie auf der Seite **Bestätigung für einzelne Zeichen** auf **abgeschlossen**.  
    
    ![Azure AD einmaliges Anmelden][11]



### <a name="creating-an-azure-ad-test-user"></a>Erstellen einen Testbenutzer Azure AD
Dieser Abschnitt soll im klassischen Portal namens Britta Simon Testbenutzer erstellen.

![Azure AD-Benutzer erstellen][20]

**Um einen Testbenutzer in Azure AD zu erstellen, führen Sie die folgenden Schritte:**

1. Klicken Sie im **klassischen Azure-Portal**im linken Navigationsbereich auf **Active Directory**.

    ![Erstellen einen Testbenutzer Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_09.png)

2. Wählen Sie aus der Liste **Verzeichnis** das Verzeichnis für das Verzeichnisintegration soll.

3. Klicken Sie zum Anzeigen der Benutzerliste im oberen Menü auf **Benutzer**.
    
    ![Erstellen einen Testbenutzer Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_03.png)

4. Klicken Sie das Dialogfeld **Benutzer hinzufügen** der Symbolleiste an der Unterseite, **Benutzer hinzufügen**.

    ![Erstellen einen Testbenutzer Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_04.png)

5. Auf der Seite **Erzählen zu diesem Benutzer** die folgenden Schritte:

    ![Erstellen einen Testbenutzer Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_05.png)

    ein. Wählen Sie als Typ der Benutzer neuen Benutzer in der Organisation.

    b. Geben Sie im **Textfeld**von Benutzernamen **BrittaSimon**.

    c. Klicken Sie auf **Weiter**.

6.  Führen Sie auf das **Benutzerprofil** die folgenden Schritte aus:
    
    ![Erstellen einen Testbenutzer Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_06.png)

    ein. Geben Sie im Textfeld **Vorname** **Britta**.  

    b. Im Feld **Nachname** Typ **Simon**.

    c. Geben Sie im Textfeld **Anzeigename** **Britta Simon**.

    d. Wählen Sie in der Liste **Rolle** **Benutzer**.

    e. Klicken Sie auf **Weiter**.

7. Klicken Sie auf der Seite **erhalten temporäres Kennwort** **Erstellen**.
    
    ![Erstellen einen Testbenutzer Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_07.png)

8. Führen Sie die folgenden Schritte auf der Seite **Passwort zu erhalten** :
    
    ![Erstellen einen Testbenutzer Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_08.png)

    ein. Notieren Sie den Wert für das **Neue Kennwort**.

    b. Klicken Sie auf **abgeschlossen**.   



### <a name="creating-a-betterworks-test-user"></a>Erstellen einen Testbenutzer BetterWorks

In diesem Abschnitt erstellen Sie einen Benutzer namens Britta Simon in BetterWorks. 

Arbeiten Sie an das Support-Team von BetterWorks über <mailto:support@betterworks.com> in der BetterWorks-Plattform Benutzer hinzu.


### <a name="assigning-the-azure-ad-test-user"></a>Zuweisen von Azure AD-Testbenutzer

Dieser Abschnitt soll Britta Simon mit Azure einmaliges ihr Zugriff auf BetterWorks aktivieren.
    
   ![Benutzer zuweisen][200]

**Britta Simon BetterWorks zuweisen, die folgenden Schritte:**

1. Das Verwaltungsportal Ansicht Applications in der Verzeichnisansicht öffnen, klicken Sie auf **Programme** im oberen Menü.
    
    ![Benutzer zuweisen][201]

2. Wählen Sie in der Anwendungsliste **BetterWorks**.
    
    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_50.png)

1. Klicken Sie im Menü oben auf **Benutzer**.
    
    ![Benutzer zuweisen][203]

1. Wählen Sie in der Liste Benutzer **Britta Simon**.

2. Klicken Sie auf unten auf **zuweisen**.
    
    ![Benutzer zuweisen][205]



### <a name="testing-single-sign-on"></a>Testen von Single Sign-On

Dieser Abschnitt soll Azure AD einzelne Anmeldung Überprüfen der Konfiguration mithilfe der.
 
Beim Klicken auf die BetterWorks Fläche in der Sie sollte automatisch zur Anwendung BetterWorks angemeldete erhalten.


## <a name="additional-resources"></a>Zusätzliche Ressourcen

* [Liste der Lernprogramme zum SaaS-Apps in Azure Active Directory integrieren](active-directory-saas-tutorial-list.md)
* [Was ist Zugriff und single Sign-on Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_205.png
