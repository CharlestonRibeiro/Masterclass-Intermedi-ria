# ARCHITECTURE

Projeto para aplicação de conceitos. Saiba mais no [README](README.md).

## Nomenclatura

Os nomes devem transmitir sua ideia central;

"Função ou parâmetro precisam de nomes que demonstrem o que eles fazem. Não se deve temer o uso de nomes extensos

```dart
// O nome da função diz exatamente o que ela faz
double calculateRectangleArea(double width, double height) {
  return width * height;
}

void main() {
  double area = calculateRectangleArea(5.0, 10.0);

  print("The area of the rectangle is: $area");
}
```

## Convenções de Nomeação:
CamelCase para nomes de classes e enums: Os nomes das classes e enums devem começar com letra maiúscula e seguir a convenção CamelCase.

```dart
class MyCustomWidget {}
enum MyEnum { valueOne, valueTwo }
```
lowerCamelCase para nomes de variáveis, constantes, métodos e funções:

```dart
var myVariable;
const myConstant;
void myFunction() {}
void myMethod() {}
```

Prefixos de sublinhado (_) para identificadores privados: Usar sublinhado no início para indicar que a variável, método ou propriedade é privado ao seu arquivo.

```dart
class _MyPrivateClass {}
var _myPrivateVariable;
void _myPrivateMethod() {}
```

## Sobre Arquivos
Um arquivo DEVE ser nomeado de acordo com a camada que representa.

```dart
// Arquivo de controller 
product_controller.dart

// Arquivo de página 
product_page.dart
```

## Sobre Variáveis

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


## Uso de comentários
Usar comentários não é uma prática ruim, desde que de fato sejam comentários relevantes.

Neste projeto, damos autonomia aos desenvolvedores para decidir quando e como utilizar comentários. Contudo, encorajamos que essa liberdade seja usada garantindo que cada comentário adicione valor real ao entendimento do código.

Ao utilizar comentários, lembre-se de que o melhor código é aquele que é suficientemente claro e autoexplicativo.

### Comentários `//TODO`

Comentários precedidos por // TODO são reconhecidos como uma prática eficiente e são amplamente utilizados. Eles servem como marcadores que sinalizam pontos de atenção, tarefas pendentes, dúvidas ou necessidades de alterações futuras no código. 

Quando aplicados de forma correta, os comentários // TODO contribuem para a manutenção e escalabilidade do projeto, assegurando que nenhum ponto importante seja negligenciado durante o desenvolvimento.


## Princípio da Menor Surpresa
O código deve ser escrito de forma que seu comportamento seja imediatamente óbvio para outros desenvolvedores. Evite surpresas no comportamento das funções e classes, tornando o código intuitivo e previsível.

```dart
class Door {
  bool isOpen = false;

  /// Alterna o estado da porta.
  /// Se estiver fechada, abre. Se estiver aberta, fecha.
  void toggle() {
    isOpen = !isOpen;
  }
}
```
A classe Door representa uma porta com uma propriedade isOpen, que indica se a porta está aberta (true) ou fechada (false).

O método toggle alterna o estado da porta. Se a porta estiver fechada (ou seja, isOpen é false), chamar toggle mudará isOpen para true, indicando que a porta está agora aberta. Se a porta estiver aberta, chamar toggle a fechará.

Este design é intuitivo e segue o Princípio da Menor Surpresa: o nome e a função do método toggle são óbvios e previsíveis, tornando o código fácil de entender e utilizar.

## Classes e interfaces devem seguir o SOLID

### 1. Responsabilidade Única (Single Responsibility Principle - SRP)
Uma classe deve ter apenas uma razão para mudar, significando que ela deve ter apenas uma responsabilidade.

```dart
// Classe focada exclusivamente em detalhes de um usuário.
class User {
  String name;
  String email;

  User(this.name, this.email);
}

// Essa classe é um bom exemplo do SRP, pois lida apenas com as propriedades do usuário, sem assumir responsabilidades adicionais como manipulação de dados ou lógica de negócio.
```

### 2. Aberto/Fechado (Open/Closed Principle)
As classes devem ser abertas para extensão, mas fechadas para modificação.

```dart
// Classe base
abstract class Shape {
  double area();
}

// Extendendo a classe, sem modificar a classe base
class Circle extends Shape {
  double radius;

  Circle(this.radius);

  @override
  double area() => 3.14 * radius * radius;
}

// O exemplo mostra como podemos estender a funcionalidade da classe Shape criando subclasses, sem necessidade de alterar a classe Shape original.
```

### 3. Substituição de Liskov (Liskov Substitution Principle - LSP)
As subclasses devem ser substituíveis por suas classes base. Isso significa que objetos de uma classe base devem ser substituíveis por objetos de suas subclasses sem afetar a corretude do programa.

```dart
// Classe base
abstract class Bird {
  void fly();
}

// Subclasse que respeita o LSP
class Sparrow extends Bird {
  @override
  void fly() {
    print("O pardal está voando.");
  }
}

// Outra subclasse que respeita o LSP
class Parrot extends Bird {
  @override
  void fly() {
    print("O papagaio está voando.");
  }
}

void makeBirdFly(Bird bird) {
  bird.fly();
}

void main() {
  Bird sparrow = Sparrow();
  Bird parrot = Parrot();

  makeBirdFly(sparrow); // Deve funcionar sem problemas
  makeBirdFly(parrot);  // Deve funcionar sem problemas
}

// Este princípio é ilustrado aqui pela capacidade de passar qualquer subclasse de Bird para a função makeBirdFly, sem alterar o comportamento esperado.
```

### 4. Segregação de Interface (Interface Segregation Principle - ISP)
Nenhuma classe deve ser forçada a depender de métodos que não utiliza.

```dart
// Interfaces específicas ao invés de uma interface genérica
abstract class Printable {
  void printContent();
}

abstract class Scannable {
  void scanContent();
}

// Classe que implementa apenas o necessário
class Printer implements Printable {
  @override
  void printContent() {
    // lógica de impressão
  }
}

// Este exemplo demonstra o ISP pela criação de interfaces específicas (Printable e Scannable), evitando a necessidade de uma classe implementar métodos que não são pertinentes ao seu propósito.
```

### 5. Inversão de Dependência (Dependency Inversion Principle - DIP)
Módulos de alto nível não devem depender de módulos de baixo nível. Ambos devem depender de abstrações.

```dart
// Dependendo de uma abstração, não de uma implementação concreta
abstract class DataRepository {
  void saveData(String data);
}

class CloudStorage implements DataRepository {
  @override
  void saveData(String data) {
    // Salva dados na nuvem
  }
}

class LocalStorage implements DataRepository {
  @override
  void saveData(String data) {
    // Salva dados localmente
  }
}

// Usando a abstração
class DataManager {
  final DataRepository repository;

  DataManager(this.repository);

  void saveData(String data) {
    repository.saveData(data);
  }
}

// O DataManager depende da abstração DataRepository, permitindo a substituição de LocalStorage por CloudStorage sem alterar o DataManager, ilustrando a inversão de dependência.
```

## Testes Unitários

Incluir testes unitários no código deve ser considerado uma prática padrão, pois eles ajudam a identificar problemas precocemente, facilitam refatorações e melhoram o código, são essenciais para garantir a qualidade e a robustez do seu código. Eles permitem que você verifique o comportamento de partes individuais do código isoladamente, garantindo que cada função ou método funcione conforme esperado.

```dart
// Ao escrever testes unitários, você deve:

// 1 - Isolar a unidade que está sendo testada.
// 2 - Preparar os dados ou configurações necessárias para o teste.
// 3 - Executar a unidade de teste e verificar se o resultado obtido corresponde ao resultado esperado.

import 'package:test/test.dart';

class Calculator {
  // Método para adicionar dois números
  double add(double a, double b) {
    return a + b;
  }
}

void main() {
  Calculator calculator;

  // Preparar o ambiente de teste antes de cada teste
  setUp(() {
    calculator = Calculator();
  });

  // Teste para o método add
  test('Calculator.add should return 4 when adding 2 and 2', () {
    var result = calculator.add(2, 2);
    expect(result, 4);
  });
}
```

```dart
    @override
  Future<AuthDto> signIn(String email, String password) async {
    try {
      final data = {'email': email, 'password': password};
      final result = await _client.create(endpoint: RouteParameters.paramAuth, data: data);
      return AuthDto.fromMap(result);
    } catch (e) {
      rethrow;
    }
  }
  // Neste segundo exemplo, se ocorrer uma exceção, em vez de tentar tratá-la especificamente, ela utiliza rethrow. Isso significa que a exceção será propagada para a camada acima que pode ter mais contexto sobre como lidar com a exceção ou notificar o usuário de forma apropriada.
```

## Camadas

- **Core:** Componentes centrais e compartilhados em toda a aplicação.
- **Data:** Lida com dados, transforma de JSON para Map ou lista.
- **Domain:** Contém as entidades e regras de negócios.
- **External:** Recursos externos, como API e banco de dados.
- **Modules:** Os módulos da aplicação, onde cada funcionalidade tem seu próprio módulo para melhor organização e manutenção.

### `core`

- **colors**: Define a paleta de cores usada em toda a aplicação.
- **errors**: Classes e funções para tratamento de erros globais.
- **images**: Contém todas as imagens e recursos visuais.
- **routes**: Gerencia as rotas e a navegação da aplicação.
- **themes**: Estilos e temas globais.
- **urls**: Endereços URLs para requisições à API.
- **widgets**: Widgets customizados reutilizáveis.

### `data`

- **dto**: Data Transfer Objects usados para transferência de dados.
- **errors**: Tratamento específico de erros relacionados a dados.
- **repositories**: Repositórios que fazem a ligação entre as fontes de dados e a lógica de negócios.
- **sources**: Diferentes fontes de dados, como API ou banco de dados.

### `domain`

- **entities**: Entidades centrais da aplicação.
- **interfaces**: Interfaces que definem contratos para outras implementações.
- **use_cases**: Casos de uso que representam ações específicas que podem ser realizadas.

### `external`

- **client**: Cliente para requisições HTTP usando o pacote Dio.
- **errors**: Erros específicos da camada externa.

### `modules`

Exemplo module/home

- **components**: Componentes visuais específicos do módulo "home".
- **home_controller.dart**: Controlador que gerencia a lógica e o estado da tela inicial.
- **home_module.dart**: Configuração e injeção de dependências do módulo.
- **home_page.dart**: A tela inicial que o usuário vê.
- **home_states.dart**: Estados possíveis para a tela inicial.

## Tratamento de Erros

Capture e Trate Exceções de Forma Específica:

Capture exceções que são esperadas durante a execução normal do programa. Trate essas exceções de forma específica e forneça feedback útil ao usuário ou ao sistema.

### Tratamento Específico por Camada
As exceções devem ser tratadas de forma específica em cada camada do código. Isso significa que cada camada deve lidar apenas com as exceções que são pertinentes à sua responsabilidade. Ao capturar exceções, forneça um tratamento adequado e forneça feedback útil ao usuário ou ao sistema. Caso a camada atual não tenha um tratamento específico para determinada exceção, utilize rethrow para permitir que a exceção seja tratada por uma camada superior.

```dart
  @override
  Future<Map<String, dynamic>> create(
      {required String endpoint, required Map<String, dynamic> data}) async {
    try {
      final response = await dio.post(endpoint, data: data);
      log(response.data.toString());
      return response.data;
    } on DioException catch (e) {
      throw DioConnectionError(e);
    } catch (e) {
      throw UnespecifiedExternalError(e);
    }
  }
  // Neste exemplo, a função create lida especificamente com DioException, uma exceção que pode ocorrer ao realizar uma requisição HTTP com o pacote Dio. Caso ocorra uma exceção que não seja DioException, a função captura essa exceção genérica e a encapsula em UnspecifiedExternalError, que é uma exceção personalizada para indicar um erro externo não especificado.
```

## Gerenciamento de Pacotes

O projeto utiliza o Flutter como framework principal e adota um conjunto específico de pacotes para garantir a consistência, qualidade e segurança do código. A inclusão de quaisquer pacotes adicionais deve ser avaliada, discutida com a equipe e devidamente documentada antes de sua integração ao projeto. Isso assegura a necessidade e relevância de cada dependência, mantendo o projeto limpo, organizado e alinhado com as melhores práticas.

### ``Bloc com Cubit``
Para o gerenciamento de estado, o projeto utiliza o padrão Bloc em conjunto com Cubit. 
Este padrão será utilizado para controlar os estados da tela...,
[Documentação do padrão](https://bloclibrary.dev/#/gettingstarted).

### ``Dio`` 
Dio é um poderoso cliente HTTP para Dart, que suporta Interceptors, Global configuration, FormData, Request Cancellation, File downloading, Timeout etc.
Para mais detalhes, consulte a documentação do Dio.
[Documentação do padrão](https://pub.dev/packages/dio).

### ``Flutter Modular``
Flutter Modular é uma injeção de dependência e controlador de rotas. Ele é inspirado em sistemas modulares que utilizam injeção de dependência e foi adaptado para o Flutter.
[Documentação do padrão](https://modular.flutterando.com.br/docs/intro/). 

### ``Flutter Secure Storage``
Flutter Secure Storage oferece uma maneira de armazenar dados de forma segura no armazenamento local do dispositivo. Os dados são criptografados no iOS e no Android, garantindo a segurança dos dados sensíveis.
[Documentação do padrão](https://pub.dev/packages/flutter_secure_storage).


## Sistema de Rotas Customizado

Para aprimorar a flexibilidade e a independência de pacotes externos, o projeto implementa um sistema de rotas customizado. Isso permite uma maior liberdade no gerenciamento de rotas e transições de tela, bem como uma fácil manutenção e atualização do sistema de navegação.

Definição de Rotas
As rotas são definidas de forma abstrata e centralizada na pasta `Routes`, na camada `CORE`, permitindo uma referência clara e consistente aos caminhos utilizados no aplicativo.

```dart
import 'modular_routes.dart';

abstract class Routes {
  // Instância que alterna o modo de roteamento
  static Routes get i => ModularRoutes();

  // Definição das rotas principais
  static String get auth => '/auth';
  static String get home => '/home';
  static String get root => '/';

  // Assinaturas de métodos para gerenciamento de navegação
  Future<T?> popAndPushNamed<T extends Object?, TO extends Object?>(...);

  Future<T?> pushNamed<T extends Object?>(...);

  Future<T?> pushNamedAndRemoveUntil<T extends Object?>(...);

  Future<T?> pushReplacementNamed<T extends Object?, TO extends Object?>(...);

  void pop<T extends Object?>([T result]);
  
  bool canPop();

  Future<bool> maybePop<T extends Object?>([T result]);

  void navigate(String path, {dynamic arguments});
}
```

### Implementação Customizada com ModularRoutes

ModularRoutes é uma implementação concreta de Routes, utilizando o pacote flutter_modular para gerenciar a navegação. Isso proporciona um ponto de extensão que pode ser substituído ou modificado conforme necessário, sem alterar o restante do aplicativo.

```dart
import 'package:flutter_modular/flutter_modular.dart';
import 'routes.dart';

class ModularRoutes implements Routes {
  
  // Implementação dos métodos de navegação utilizando flutter_modular
  @override
  bool canPop() => Modular.to.canPop();

  @override
  Future<bool> maybePop<T extends Object?>([T? result]) => Modular.to.maybePop(result);

  @override
  void navigate(String path, {Object? arguments}) => Modular.to.navigate(path, arguments: arguments);

  @override
  void pop<T extends Object?>([T? result]) => Modular.to.pop(result);

  @override
  Future<T?> popAndPushNamed<T extends Object?, TO extends Object?>(...) => Modular.to.popAndPushNamed(...);

  @override
  Future<T?> pushNamed<T extends Object?>(...) => Modular.to.pushNamed(...);

  @override
  Future<T?> pushNamedAndRemoveUntil<T extends Object?>(...) => Modular.to.pushNamedAndRemoveUntil(...);

  @override
  Future<T?> pushReplacementNamed<T extends Object?, TO extends Object?>(...) => Modular.to.pushReplacementNamed(...);
}
```