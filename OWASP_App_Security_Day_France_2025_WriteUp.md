# OWASP App Security Day France 2025 - Write-up

**Date :** 23 septembre 2025  
**Événement :** OWASP App Security Day France 2025  
**Participant :** Tom Nicoli

## 📅 Programme et sessions

### Session 1 : Les attaques sur la supply chain.
- **Intervenant(s) :** Roni Carta alias Lupin, Co-Founder of Lupin & Holmes
- **Résumé :** 
Rony nous présente ici l'ensemble des objets de la supply chain et nous rappelle l'importance de celle-ci dans le monde du développement logiciel.
Il parle ensuite du framework SLSA pour Supply-chain Levels for Software Artifacts qui est un framework de sécurité, une liste de contrôle des normes et des contrôles visant à prévenir la falsification, à améliorer l'intégrité et à sécuriser les paquets et l'infrastructure. Il nous présente ensuite les différentes façons d'attaquer la supply chain.

1. S'en prendre directement aux sources. Cela se base sur l'idée qu'il est facile de corrompre la réputation d'un package et de lui inventer une "fausse crédibilité"
2. S'en prendre aux mainteneurs. Après un account takeover il est facile d'introduire une charge dans un package.
3. On peut utiliser une attaque "Dependency Confusion" où l'on manipule l'origine des dépendances d'un code, souvent en utilisant un comportement par défaut pour introduire une dépendance corrompue.
4. Les attaques NPX, qui utilisent l'exécution de certaines parties des packages pour créer des RCE lors de manipulations particulières.

Les gestionnaires de packages utilisent des solutions de SAST et DAST pour tenter de limiter l'introduction de code malicieux mais bien souvent ça ne suffit pas.

Il nous présente un outil, Gato-X pour attaquer les pipelines.
REX d'un cache poisoning sur des pipelines menant à une attaque supply chain

### Session 2 : Git Guardian.
- **Intervenant(s) :** Dwayne McDaniel Developer Advocate at GitGuardian
- **Résumé :** 
Dwayne nous présente rapidement GitGuardian, un outil qui scanne les repos git à la recherche de secrets exposés. Concept intéressant du honey token.

### Session 3 : Behind the scenes of creating an AI Cyber Assistant.
- **Intervenant(s) :** Adeline Villette Head of Cybersecurity Expertise and Innovation at Decathlon
- **Résumé :** 
Il y a quelques mois les équipes de Decathlon ont essayé de créer un agent permettant d'adresser les questions de sécurité en interne. L'idée vient du constat que les politiques sont souvent très bien documentées mais que les gens ont du mal à les trouver.

Je vous passe les détails techniques mais Decathlon s'est lancé un peu trop tôt dans cette tâche et a carrément fait du RAG à la main. Sans grande surprise n'ayant pas d'expérience particulière sur le sujet les équipes ont rencontré de grosses difficultés et malgré une version beta le projet n'a pas été poussé plus loin.
Le REX reste positif même s'il n'a pas eu un grand succès selon leurs dires.

### Session 4 : Living Off the Pipeline: From Supply Chain 0-Days to Predicting the next XZ-like attacks.
- **Intervenant(s) :** François Proulx VP of Security Research at BoostSecurity
- **Résumé :**

François introduit son talk en nous expliquant que les build stages sont tels que des RCEaaS.
Parmi les vulns couramment trouvées sur les pipelines on aura : 

1. les pwnd request
2. les template injections
3. via "confused deputy problem"

Garder à l'esprit que les "non ephemeral self hosted runners" sont des cibles de choix car elles permettent une assez bonne persistance et des mouvements latéraux.

Il nous présente alors "poutine" un scanner de vulns opensource permettant d'identifier du code exploitable dans nos pipelines.
Il nous fait ensuite la démonstration d'attaques sur une chaîne CI/CD. Template injection, RCE via npm start avec redéfinition de la commande start dans le fichier de dépendance, usurpation de l'identité de dependabot pour valider une PR...
Son site web LOFP nous en apprend plus sur comment sécuriser nos pipelines. (lien disponible en dessous)

### Session 5 : Remédiation automatique de vulnérabilités : que valent vraiment les LLMs ?  
- **Intervenant(s) :** Edouard Viot CTO at Symbiotic Security
- **Résumé :**

Edouard nous présente les résultats de ses recherches sur l'utilisation des LLMs dans la remédiation des vulns. Il nous apprend que les LLM sont bien meilleurs lorsqu'ils sont accompagnés. Autrement dit il faut ajouter du contexte sur la vuln et des exemples pour augmenter ses résultats, le choix du modèle est aussi important et fait varier les résultats. Un enjeu est aussi de fournir à l'IA une mémoire pour qu'elle conseille une entreprise en fonction de ses politiques de remédiation internes. Il mesure les succès avec un LLM as a Judge, qui améliore significativement les perfs. En tant que juge les LLMs se différencient aussi, parmi les LLM qu'ils ont testés, GPT 4 semble être le plus équilibré, Claude est trop optimiste ou trop perfectionniste, quant à Gemini il n'est pas un très bon juge.

Il nous rappelle qu'une bonne remédiation est plus qu'un simple patch de code et comprend un ensemble de tâches qui doivent être menées en parallèle, comme le fix, la vérification de l'impact du fix sur la logique métier, la doc etc.

### Session 6 : Des applis sans mot de passe: Passkeys en pratique ?  
- **Intervenant(s) :** Daniel Garnier-Moiroux Software Engineer, Spring
- **Résumé :**

Daniel nous présente les technos existantes qui permettent l'accès à des plateformes web sans mot de passe. Celles qui nous intéressent sont les "passkeys"
C'est une clé cryptographique conforme au standard FIDO2 / WebAuthn.
Elle repose sur un couple clé publique / clé privée :
- La clé privée reste stockée sur ton appareil (ordinateur, smartphone, clé de sécurité matérielle).
- La clé publique est transmise au service (Google, Apple, Microsoft, etc.) lors de l'enregistrement.
- Quand tu te connectes, le site envoie un défi cryptographique que seule ta clé privée peut résoudre.
- Tu confirmes ton identité via une méthode locale (empreinte digitale, Face ID, code PIN de ton appareil).

En ressource intéressante on retrouvera l'OWASP Top 10 Non-Human Identities Risks - 2025

### Session 7 : La sécurité et le vibe coding.  
- **Intervenant(s) :** ????
- **Résumé :**

Le vibe coding excelle dans la mise en place d'applications facilement exploitables. Il faut faire très attention lorsqu'on déploie des environnements hébergeant des données sensibles.

### Session 8 : Worldline's Security Champions Program: Driving DevSecOps Culture and Compliance Readiness  
- **Intervenant(s) :** Nourredine Khadri AppSec Program Leader at Worldline
- **Résumé :**

REX sur la mise en place d'un Security Champions Program chez Worldline. 
Pour assurer la pertinence du programme ils ont prévu plusieurs étapes :

- Formation
- Évaluation des vulns
- Implémentation-Évaluation2
- Offboarding + roadmap future

Pour s'assurer de l'efficacité du programme ils ont mesuré la compliance aux normes du secteur bancaire avant et après. Les auditeurs étaient avec eux au long du processus pour valider les implémentations et les rendre "pentest-ready"

Les coûts ont été optimisés en maximisant l'utilisation des ressources internes le self made (évaluation et formation) 

Par la suite ils ont mesuré l'amélioration de la posture de sécurité, le nombre d'implémentations, et la diminution des configurations faibles.

Ainsi ils ont pu améliorer la posture de sécurité de 30% de leurs assets logiciels les plus critiques.

Remarque importante : Il faut assurer un backup au "champion" pour entretenir la continuité des activités car la flamme s'éteint vite sinon. 

## 📚 Ressources et références

## 🔗 Liens utiles

- [Site officiel OWASP](https://owasp.org/)
- [OWASP France](https://owasp.org/www-chapter-france/)
- [Framework SLSA](https://slsa.dev/)
- [Gato-X](https://github.com/AdnaneKhan/gato-x)
- [LOTP](https://boostsecurityio.github.io/lotp/)
- [OWASP Top 10 Non-Human Identities Risks - 2025](https://owasp.org/www-project-non-human-identities-top-10/2025/top-10-2025/)

## 📝 Notes diverses

**Merci aux sponsors internes (Élisa, Maxime, Christophe...)**
