# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is an Obsidian vault de cours couvrant plusieurs domaines liés aux Java Cards :
- **Java (général)** : POO, classes, héritage, interfaces, exceptions, collections, etc.
- **Java Card** : plateforme Java Card, cycle de vie des applets, JCRE, mémoire persistante/transiente
- **Applets Java Card** : développement d'applets (install, select, process, deselect)
- **Commandes APDU** : communication avec les cartes à puce (ISO 7816)

## Niveau de l'utilisateur

L'utilisateur est **débutant en Java** — il connaît les boucles et les conditions. Les cours doivent :
- Introduire les concepts progressivement (pas de raccourcis sur les bases)
- Donner des exemples concrets et commentés
- Expliquer le vocabulaire technique (classe, objet, méthode, héritage, etc.) avant de l'utiliser
- Faire le lien entre Java général et Java Card quand c'est pertinent

## Structure du vault

- Notes en Markdown (`.md`), gérées par Obsidian
- `.obsidian/` contient la config du vault (thème : Blue Topaz) — ne pas modifier sauf demande explicite
- Utiliser le Markdown Obsidian : `[[wikilinks]]` pour les liens internes, `![[embeds]]` pour l'inclusion

## Domaines de contenu

### Java général
Classes, objets, héritage, interfaces, polymorphisme, exceptions, types primitifs vs objets, tableaux, packages, modificateurs d'accès

### Java Card
Plateforme Java Card (sous-ensemble de Java), JCRE (Java Card Runtime Environment), APDU buffer, mémoire persistante (EEPROM) vs transiente (RAM), objets partagés (Shareable Interface)

### Applets Java Card
Cycle de vie : `install()`, `select()`, `process()`, `deselect()`. Classe `javacard.framework.Applet`, gestion des AID, enregistrement de l'applet

### Commandes APDU (ISO 7816-4)
- **Command APDU** : CLA, INS, P1, P2, Lc, Data, Le
- **Response APDU** : Data + SW1-SW2
- Opérations : SELECT, READ BINARY, UPDATE BINARY, GET RESPONSE, VERIFY, AUTHENTICATE

Utiliser la notation hexadécimale (ex : `0x00A4`) et structurer les références de commandes de manière cohérente.
