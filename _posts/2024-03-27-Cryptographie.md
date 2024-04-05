---
layout: post
title:  "Un peu de cryptographie"
date:   2024-03-27 11:45:09 +0200
categories: jekyll update
permalink: /cryptographie/
image: /assets/uploads/cryptographie.jpg
---

# Qu'est-ce que la cryptographie
<pre>
C'est une étude de la sécurisation des communications répondant au besoin de sécurités : 
-confidentialité
-intégrité
-authenticité 
-non répudiation
</pre>
Nous retrouvons de la cryptographie un peu partout : 
Dans les télécommunications : (mails, navigation internet, téléphonie, messagerie,)
Dans le controle d'accès : (clé de déverouillage, badge de porte ou d'immeuble, passeport, CNI même décodeur TV)
Bien-sur dans les systèmes de paiements : (cartes bancaires, cryptomonnaies)
# Principe de Kerchoffs 
La robustesse d'un système cryptographique ne doit pas reposer sur le secret de son algorithme, mais sur le secret de la clé utilisé
# Fonction de hashage
Le but d'une fonction de hashage est de transformer un message de longueur arbitraire en un message de taille fixe.
Encore une fois cette fonction de hashage ne doit pas être secrète.
On dénomine souvent la fonction H() et le message m
- Une fonction de hashage n'est pas reversible

Problème : si une liste de mots de passe courants fuite, alors leur hachés sont facilement reconnaissables c'est ce qu'on appelle une rainbow table.

Solution : Salage des mots de passe :
→ au lieu de stocker H(P), on stocke S || H(S || P) où S est un mots de n octets aléatoires (n = 16 par ex)
→ puisque S est variable, le même mot de passe courant n'aura pas le même sel S
→ pour vérifier, il suffit de comparer H(S || p) à H(S || P)

# La Cryptographie Symétrique
Pour la cryptographie symétrique notre fonction H() est en fait une fonction de xor.
Notre message chiffré C et notre clé K
C = m xor K
La clé K est souvent de la taille du message. Lorsque la clé est plus petite que le message on l'étend avec un algorithme (voir les LFSR)