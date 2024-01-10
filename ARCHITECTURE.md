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

### Princípio da Menor Surpresa
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

Neste exemplo simplificado:

A classe Door representa uma porta com uma propriedade isOpen, que indica se a porta está aberta (true) ou fechada (false).

O método toggle alterna o estado da porta. Se a porta estiver fechada (ou seja, isOpen é false), chamar toggle mudará isOpen para true, indicando que a porta está agora aberta. Se a porta estiver aberta, chamar toggle a fechará.

Este design é intuitivo e segue o Princípio da Menor Surpresa: o nome e a função do método toggle são óbvios e previsíveis, tornando o código fácil de entender e utilizar.
```

### Uso de comentários
Usar comentários não é uma prática ruim, desde que de fato sejam comentários relevantes.

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

```
