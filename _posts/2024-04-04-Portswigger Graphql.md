---
layout: post
title:  "Graphql"
date:   2024-04-04 12:35:09 +0200
categories: jekyll update
permalink: /api/Graphql/
image: /assets/uploads/api.jpg
---

# Portswigger Graphql

Propriétaire: Jaouen Houllegatte

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

![Untitled](Portswigger%20Graphql%208ea2466c99e944218ec53e7786091dcc/Untitled.png)

[https://www.notion.so](https://www.notion.so)

![Untitled](Portswigger%20Graphql%208ea2466c99e944218ec53e7786091dcc/Untitled%201.png)

L’introspection est une option proposée par GraphQL permettant d’établir un schéma de la base. Cela permet de développer la plateforme plus simplement
Exemple 1 ou l’on injecte directement l’introspection dans l’onglet GraphQL de Burp

![Untitled](Portswigger%20Graphql%208ea2466c99e944218ec53e7786091dcc/Untitled%202.png)

Exemple 2 :

![Untitled](Portswigger%20Graphql%208ea2466c99e944218ec53e7786091dcc/Untitled%203.png)

Mais il existe aussi le cas où l’endpoint GraphQL est caché ainsi nous pouvons aussi encoder la requête dans l’url :

```jsx
/api?query=query+IntrospectionQuery+%7B%0A++__schema+%7B%0A++++queryType+%7B%0D%0A++++++name%0D%0A++++%7D%0D%0A++++mutationType+%7B%0D%0A++++++name%0D%0A++++%7D%0D%0A++++subscriptionType+%7B%0D%0A++++++name%0D%0A++++%7D%0D%0A++++types+%7B%0D%0A++++++...FullType%0D%0A++++%7D%0D%0A++++directives+%7B%0D%0A++++++name%0D%0A++++++description%0D%0A++++++args+%7B%0D%0A++++++++...InputValue%0D%0A++++++%7D%0D%0A++++%7D%0D%0A++%7D%0D%0A%7D%0D%0A%0D%0Afragment+FullType+on+__Type+%7B%0D%0A++kind%0D%0A++name%0D%0A++description%0D%0A++fields%28includeDeprecated%3A+true%29+%7B%0D%0A++++name%0D%0A++++description%0D%0A++++args+%7B%0D%0A++++++...InputValue%0D%0A++++%7D%0D%0A++++type+%7B%0D%0A++++++...TypeRef%0D%0A++++%7D%0D%0A++++isDeprecated%0D%0A++++deprecationReason%0D%0A++%7D%0D%0A++inputFields+%7B%0D%0A++++...InputValue%0D%0A++%7D%0D%0A++interfaces+%7B%0D%0A++++...TypeRef%0D%0A++%7D%0D%0A++enumValues%28includeDeprecated%3A+true%29+%7B%0D%0A++++name%0D%0A++++description%0D%0A++++isDeprecated%0D%0A++++deprecationReason%0D%0A++%7D%0D%0A++possibleTypes+%7B%0D%0A++++...TypeRef%0D%0A++%7D%0D%0A%7D%0D%0A%0D%0Afragment+InputValue+on+__InputValue+%7B%0D%0A++name%0D%0A++description%0D%0A++type+%7B%0D%0A++++...TypeRef%0D%0A++%7D%0D%0A++defaultValue%0D%0A%7D%0D%0A%0D%0Afragment+TypeRef+on+__Type+%7B%0D%0A++kind%0D%0A++name%0D%0A++ofType+%7B%0D%0A++++kind%0D%0A++++name%0D%0A++++ofType+%7B%0D%0A++++++kind%0D%0A++++++name%0D%0A++++++ofType+%7B%0D%0A++++++++kind%0D%0A++++++++name%0D%0A++++++%7D%0D%0A++++%7D%0D%0A++%7D%0D%0A%7D%0D%0A
```

Prenons le cas où l’introspection est désactivé.

```jsx
/api?query=query+IntrospectionQuery+%7B%0D%0A++__schema%0a+%7B%0D%0A++++queryType+%7B%0D%0A++++++name%0D%0A++++%7D%0D%0A++++mutationType+%7B%0D%0A++++++name%0D%0A++++%7D%0D%0A++++subscriptionType+%7B%0D%0A++++++name%0D%0A++++%7D%0D%0A++++types+%7B%0D%0A++++++...FullType%0D%0A++++%7D%0D%0A++++directives+%7B%0D%0A++++++name%0D%0A++++++description%0D%0A++++++args+%7B%0D%0A++++++++...InputValue%0D%0A++++++%7D%0D%0A++++%7D%0D%0A++%7D%0D%0A%7D%0D%0A%0D%0Afragment+FullType+on+__Type+%7B%0D%0A++kind%0D%0A++name%0D%0A++description%0D%0A++fields%28includeDeprecated%3A+true%29+%7B%0D%0A++++name%0D%0A++++description%0D%0A++++args+%7B%0D%0A++++++...InputValue%0D%0A++++%7D%0D%0A++++type+%7B%0D%0A++++++...TypeRef%0D%0A++++%7D%0D%0A++++isDeprecated%0D%0A++++deprecationReason%0D%0A++%7D%0D%0A++inputFields+%7B%0D%0A++++...InputValue%0D%0A++%7D%0D%0A++interfaces+%7B%0D%0A++++...TypeRef%0D%0A++%7D%0D%0A++enumValues%28includeDeprecated%3A+true%29+%7B%0D%0A++++name%0D%0A++++description%0D%0A++++isDeprecated%0D%0A++++deprecationReason%0D%0A++%7D%0D%0A++possibleTypes+%7B%0D%0A++++...TypeRef%0D%0A++%7D%0D%0A%7D%0D%0A%0D%0Afragment+InputValue+on+__InputValue+%7B%0D%0A++name%0D%0A++description%0D%0A++type+%7B%0D%0A++++...TypeRef%0D%0A++%7D%0D%0A++defaultValue%0D%0A%7D%0D%0A%0D%0Afragment+TypeRef+on+__Type+%7B%0D%0A++kind%0D%0A++name%0D%0A++ofType+%7B%0D%0A++++kind%0D%0A++++name%0D%0A++++ofType+%7B%0D%0A++++++kind%0D%0A++++++name%0D%0A++++++ofType+%7B%0D%0A++++++++kind%0D%0A++++++++name%0D%0A++++++%7D%0D%0A++++%7D%0D%0A++%7D%0D%0A%7D%0D%0A
```

![Untitled](Portswigger%20Graphql%208ea2466c99e944218ec53e7786091dcc/Untitled%204.png)

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