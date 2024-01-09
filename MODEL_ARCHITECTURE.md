# ARCHITECTURE

Coloque a descrição do projeto. Geralmente, é mais prático apontar para o README. 

Exemplo:

Projeto para aplicação de conceitos. Saiba mais no [README](README.md).

## Framework 

No Framework, descreva tudo que será usado no projeto.

## Structure 

Em Structure, descreva a estrutura das pastas. 

Observação: Isso faz parte de deixar sua **arquitetura gritante**. 

Exemplo: 

Descreva o que é necessário: **A arquitetura de pastas DEVE ser...**

    .
    └── lib/
        ├── src/
        │   └── app/
        │       ├── core/
        │       ├── data/
        │       ├── domain/
        │       ├── external/
        │       ├── modules/
        │       ├── modules.dart
        │       └── app.dart
        └── main.dart

Também é interessante descrever o módulo ou camada:

### Core

A camada **core** DEVE conter...

## Nomenclatura

Tudo que se aplica sobre **Clean Code** é relevante aqui.

### Sobre Arquivos

Um arquivo DEVE ser nomeado de acordo com a camada que representa.

```dart
// Arquivo de controller 
product_controller.dart

// Arquivo de página 
product_page.dart
```

### Sobre Variáveis

Uma variável ou propriedade deve ser declarada com um nome legível.
Não é permitido abreviações.

```dart
    
// Code smell
final num1 = 1;

// Good code
final numberOfAnything = 1;

// Code smell
final productList = [];

// Good code
final products = [];

```

### Sobre Classes e interfaces
...

## Patterns

Descreva quais **padrões de projeto** serão usados.

### Repository

Este padrão será utilizado...,
[Documentação do padrão](https://codewithandrea.com/articles/flutter-repository-pattern/).

### State Management (Bloc com Cubit)
Este padrão será utilizado para controlar os estados da tela...,
[Documentação do padrão](https://bloclibrary.dev/#/gettingstarted).

### usecase

Usado para representar a ação de um negócio.

## Packges

Descreva o motivo do uso e o que o package faz.

## State managemet

Descreva com exemplos o state manager.


## Testing

Descreva com exemplos os testes.


## OBS:

- **Sempre use o termo "DEVE" (MUST) ao descrever requisitos.**

- **Tudo que for descrito deve ter exemplos.**

- **Na parte de Packages, devemos descrever o porquê do uso e o que o package faz.**

- **No final, os desenvolvedores devem assinar o documento.**

```
Exemplo:

Desenvolvedores que concordam com a arquitetura:

- Charleston Ribeiro dos Passos.
- Eliel Cezar.
```


