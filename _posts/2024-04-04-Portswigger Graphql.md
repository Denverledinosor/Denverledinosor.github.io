---
layout: post
title:  "Graphql"
date:   2024-04-04 12:35:09 +0200
categories: jekyll update
permalink: /api/Graphql/
---

# Portswigger Graphql

GraphQL est un langage api fait pour simplifier la communication client-server. 

Cela permet au client de spécifier leformat et la donnée de la réponse permettant d’éviter une quantité de réponse inutile et des appels répété sur l’API REST.
GraphQL est souvent utilisé pour de l’authentification.

La plupart des enpoints GraphQL sont : 

- `/graphql`
- `/api`
- `/api/graphql`
- `/graphql/api`
- `/graphql/graphql`
- `/graphql/v1`

## Ressources

- Visualiser
- [http://nathanrandal.com/graphql-visualizer/](http://nathanrandal.com/graphql-visualizer/)
- [https://graphql-kit.com/graphql-voyager/](https://graphql-kit.com/graphql-voyager/)
- Tool
- [https://github.com/swisskyrepo/Grap...](https://github.com/swisskyrepo/GraphQLmap) : Repo de l’outil GraphQLmap développé par @Swissky.
- ToolBurpsuite
- Extension : InQL
- Documentation
- [https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/graphql](https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/graphql)
- [https://www.vaadata.com/blog/fr/exploitation-dun-manque-de-controle-de-droits-sur-graphql/](https://www.vaadata.com/blog/fr/exploitation-dun-manque-de-controle-de-droits-sur-graphql/)

![Untitled](/assets/uploads/Portswigger Graphql/Untitled.png)

[https://www.notion.so](https://www.notion.so)

![Untitled](/assets/uploads/Portswigger Graphql/Untitled 1.png)

L’introspection est une option proposée par GraphQL permettant d’établir un schéma de la base. Cela permet de développer la plateforme plus simplement
Exemple 1 ou l’on injecte directement l’introspection dans l’onglet GraphQL de Burp

![Untitled](/assets/uploads/Portswigger Graphql/Untitled 2.png)

Exemple 2 :

![Untitled](/assets/uploads/Portswigger Graphql/Untitled 3.png)

Mais il existe aussi le cas où l’endpoint GraphQL est caché ainsi nous pouvons aussi encoder la requête dans l’url :

```jsx
/api?query=query+IntrospectionQuery+%7B%0A++__schema+%7B%0A++++queryType+%7B%0D%0A++++++name%0D%0A++++%7D%0D%0A++++mutationType+%7B%0D%0A++++++name%0D%0A++++%7D%0D%0A++++subscriptionType+%7B%0D%0A++++++name%0D%0A++++%7D%0D%0A++++types+%7B%0D%0A++++++...FullType%0D%0A++++%7D%0D%0A++++directives+%7B%0D%0A++++++name%0D%0A++++++description%0D%0A++++++args+%7B%0D%0A++++++++...InputValue%0D%0A++++++%7D%0D%0A++++%7D%0D%0A++%7D%0D%0A%7D%0D%0A%0D%0Afragment+FullType+on+__Type+%7B%0D%0A++kind%0D%0A++name%0D%0A++description%0D%0A++fields%28includeDeprecated%3A+true%29+%7B%0D%0A++++name%0D%0A++++description%0D%0A++++args+%7B%0D%0A++++++...InputValue%0D%0A++++%7D%0D%0A++++type+%7B%0D%0A++++++...TypeRef%0D%0A++++%7D%0D%0A++++isDeprecated%0D%0A++++deprecationReason%0D%0A++%7D%0D%0A++inputFields+%7B%0D%0A++++...InputValue%0D%0A++%7D%0D%0A++interfaces+%7B%0D%0A++++...TypeRef%0D%0A++%7D%0D%0A++enumValues%28includeDeprecated%3A+true%29+%7B%0D%0A++++name%0D%0A++++description%0D%0A++++isDeprecated%0D%0A++++deprecationReason%0D%0A++%7D%0D%0A++possibleTypes+%7B%0D%0A++++...TypeRef%0D%0A++%7D%0D%0A%7D%0D%0A%0D%0Afragment+InputValue+on+__InputValue+%7B%0D%0A++name%0D%0A++description%0D%0A++type+%7B%0D%0A++++...TypeRef%0D%0A++%7D%0D%0A++defaultValue%0D%0A%7D%0D%0A%0D%0Afragment+TypeRef+on+__Type+%7B%0D%0A++kind%0D%0A++name%0D%0A++ofType+%7B%0D%0A++++kind%0D%0A++++name%0D%0A++++ofType+%7B%0D%0A++++++kind%0D%0A++++++name%0D%0A++++++ofType+%7B%0D%0A++++++++kind%0D%0A++++++++name%0D%0A++++++%7D%0D%0A++++%7D%0D%0A++%7D%0D%0A%7D%0D%0A
```

Prenons le cas où l’introspection est désactivé.

```jsx
/api?query=query+IntrospectionQuery+%7B%0D%0A++__schema%0a+%7B%0D%0A++++queryType+%7B%0D%0A++++++name%0D%0A++++%7D%0D%0A++++mutationType+%7B%0D%0A++++++name%0D%0A++++%7D%0D%0A++++subscriptionType+%7B%0D%0A++++++name%0D%0A++++%7D%0D%0A++++types+%7B%0D%0A++++++...FullType%0D%0A++++%7D%0D%0A++++directives+%7B%0D%0A++++++name%0D%0A++++++description%0D%0A++++++args+%7B%0D%0A++++++++...InputValue%0D%0A++++++%7D%0D%0A++++%7D%0D%0A++%7D%0D%0A%7D%0D%0A%0D%0Afragment+FullType+on+__Type+%7B%0D%0A++kind%0D%0A++name%0D%0A++description%0D%0A++fields%28includeDeprecated%3A+true%29+%7B%0D%0A++++name%0D%0A++++description%0D%0A++++args+%7B%0D%0A++++++...InputValue%0D%0A++++%7D%0D%0A++++type+%7B%0D%0A++++++...TypeRef%0D%0A++++%7D%0D%0A++++isDeprecated%0D%0A++++deprecationReason%0D%0A++%7D%0D%0A++inputFields+%7B%0D%0A++++...InputValue%0D%0A++%7D%0D%0A++interfaces+%7B%0D%0A++++...TypeRef%0D%0A++%7D%0D%0A++enumValues%28includeDeprecated%3A+true%29+%7B%0D%0A++++name%0D%0A++++description%0D%0A++++isDeprecated%0D%0A++++deprecationReason%0D%0A++%7D%0D%0A++possibleTypes+%7B%0D%0A++++...TypeRef%0D%0A++%7D%0D%0A%7D%0D%0A%0D%0Afragment+InputValue+on+__InputValue+%7B%0D%0A++name%0D%0A++description%0D%0A++type+%7B%0D%0A++++...TypeRef%0D%0A++%7D%0D%0A++defaultValue%0D%0A%7D%0D%0A%0D%0Afragment+TypeRef+on+__Type+%7B%0D%0A++kind%0D%0A++name%0D%0A++ofType+%7B%0D%0A++++kind%0D%0A++++name%0D%0A++++ofType+%7B%0D%0A++++++kind%0D%0A++++++name%0D%0A++++++ofType+%7B%0D%0A++++++++kind%0D%0A++++++++name%0D%0A++++++%7D%0D%0A++++%7D%0D%0A++%7D%0D%0A%7D%0D%0A
```

![Untitled](/assets/uploads/Portswigger Graphql/Untitled 4.png)

Il est encore possible d’utiliser la fonctionnalité de suggestion pour établir un schéma.

```
  #Full introspection query

query IntrospectionQuery {
    __schema {
        queryType {
            name
        }
        mutationType {
            name
        }
        subscriptionType {
            name
        }
        types {
         ...FullType
        }
        directives {
            name
            description
            args {
                ...InputValue
        }
        onOperation  #Often needs to be deleted to run query
        onFragment   #Often needs to be deleted to run query
        onField      #Often needs to be deleted to run query
        }
    }
}

fragment FullType on __Type {
    kind
    name
    description
    fields(includeDeprecated: true) {
        name
        description
        args {
            ...InputValue
        }
        type {
            ...TypeRef
        }
        isDeprecated
        deprecationReason
    }
    inputFields {
        ...InputValue
    }
    interfaces {
        ...TypeRef
    }
    enumValues(includeDeprecated: true) {
        name
        description
        isDeprecated
        deprecationReason
    }
    possibleTypes {
        ...TypeRef
    }
}

fragment InputValue on __InputValue {
    name
    description
    type {
        ...TypeRef
    }
    defaultValue
}

fragment TypeRef on __Type {
    kind
    name
    ofType {
        kind
        name
        ofType {
            kind
            name
            ofType {
                kind
                name
            }
        }
    }
}
```

```jsx
{
__schema {
queryType {
name
}, mutationType {
name
}, types {
kind, name, description, fields(includeDeprecated: true) {
name, description, args {
name, description, type {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name
}
}
}
}
}
}
}
}, defaultValue
}, type {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name
}
}
}
}
}
}
}
}, isDeprecated, deprecationReason
}, inputFields {
name, description, type {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name
}
}
}
}
}
}
}
}, defaultValue
}, interfaces {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name
}
}
}
}
}
}
}
}, enumValues(includeDeprecated: true) {
name, description, isDeprecated, deprecationReason,
}, possibleTypes {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name
}
}
}
}
}
}
}
}
}, directives {
name, description, locations, args {
name, description, type {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name, ofType {
kind, name
}
}
}
}
}
}
}
}, defaultValue
}
}
}
}
```

```
query IntrospectionQuery {
  __schema {

    queryType { name }
    mutationType { name }
    subscriptionType { name }
    types {
      ...FullType
    }
    directives {
      name
      description

      locations
      args {
        ...InputValue
      }
    }
  }
}

fragment FullType on __Type {
  kind
  name
  description

  fields(includeDeprecated: true) {
    name
    description
    args {
      ...InputValue
    }
    type {
      ...TypeRef
    }
    isDeprecated
    deprecationReason
  }
  inputFields {
    ...InputValue
  }
  interfaces {
    ...TypeRef
  }
  enumValues(includeDeprecated: true) {
    name
    description
    isDeprecated
    deprecationReason
  }
  possibleTypes {
    ...TypeRef
  }
}

fragment InputValue on __InputValue {
  name
  description
  type { ...TypeRef }
  defaultValue

}

fragment TypeRef on __Type {
  kind
  name
  ofType {
    kind
    name
    ofType {
      kind
      name
      ofType {
        kind
        name
        ofType {
          kind
          name
          ofType {
            kind
            name
            ofType {
              kind
              name
              ofType {
                kind
                name
              }
            }
          }
        }
      }
    }
  }
}

```

## La mutation

Mais d’abord comment fonctionne un champ normal. La requête est simple. Le champs name return une string définit dans l’objet “hero”

|   hero {
name
}
} |   "data": {
"hero": {
"name": "R2-D2"
}
}
} |
| --- | --- |

Ah oui et aussi il y a aussi les arguments : 

|  {
human(id: "1000") {
name
height
}
} | {
"data": {
"human": {
"name": "Luke Skywalker",
"height": 1.72
}
}
} |
| --- | --- |

| {
human(id: "1000") {
name
height(unit: FOOT)
}
} | {
"data": {
"human": {
"name": "Luke Skywalker",
"height": 5.6430448
}
}
} |
| --- | --- |

La mutation permet de faire des modifications de données“server-side”.

Alors que les champs de requête sont exécutés en parallèle, les champs de mutation s'exécutent en série, les uns après les autres.

## Prévenir les attaques GraphQL

Pour éviter de nombreuses attaques GraphQL courantes, suivez les étapes suivantes lorsque vous déployez votre API en production :

Si votre API n’est pas destinée à être utilisée par le grand public, désactivez l’introspection sur celle-ci. Cela rend plus difficile pour un attaquant d'obtenir des informations sur le fonctionnement de l'API et réduit le risque de divulgation indésirable d'informations.

Si votre API est destinée à être utilisée par le grand public, vous devrez probablement laisser l'introspection activée. Cependant, vous devez revoir le schéma de l'API pour vous assurer qu'il n'expose pas de champs involontaires au public.

Assurez-vous que les suggestions sont désactivées. Cela empêche les attaquants de pouvoir utiliser Clairvoyance ou des outils similaires pour glaner des informations sur le schéma sous-jacent.

Assurez-vous que le schéma de votre API n'expose aucun champ d'utilisateur privé, tel que des adresses e-mail ou des identifiants d'utilisateur.

Prévenir les attaques par force brute GraphQL
Il est parfois possible de contourner la limitation de débit standard lors de l'utilisation des API GraphQL. 

Pour vous défendre contre les attaques par force brute :

Limitez la profondeur des requêtes de votre API. Le terme « profondeur de requête » fait référence au “query depth” nombre de niveaux d’imbrication au sein d’une requête. Les requêtes fortement imbriquées peuvent avoir des implications significatives en termes de performances et peuvent potentiellement donner lieu à des attaques DoS si elles sont acceptées. En limitant la profondeur des requêtes acceptées par votre API, vous pouvez réduire les risques que cela se produise.

Configurez les limites de fonctionnement. Les limites d'opération vous permettent de configurer le nombre maximum de champs uniques, d'alias et de champs racine que votre API peut accepter.

Configurez le nombre maximum d'octets qu'une requête peut contenir.

Pensez à mettre en œuvre une analyse des coûts sur votre API. L'analyse des coûts est un processus par lequel une application de bibliothèque identifie le coût des ressources associé à l'exécution des requêtes au fur et à mesure de leur réception. Si une requête est trop complexe sur le plan informatique à exécuter, l’API la supprime.

Empecher les CSRF sur GraphQL

Pour vous défendre spécifiquement contre les vulnérabilités GraphQL CSRF, assurez-vous des points suivants lors de la conception de votre API :

- Votre API n'accepte que les requêtes via POST codé en JSON.
- L'API valide que le contenu fourni correspond au type de contenu fourni.
- L'API dispose d'un mécanisme de jeton CSRF sécurisé.