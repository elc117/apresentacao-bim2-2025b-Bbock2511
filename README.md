# Análise de Código Java: Média de Notas de Alunos

Este projeto consiste em um programa Java, apresentado na última aula, que lê uma lista de estudantes e suas notas de um arquivo `.csv`, calcula a média aritmética das notas e exibe o resultado.

## Parte 1: Análise Teórica

### Pergunta 1: O que significa `private` em `private String name;` na classe `Student`?
```Java
class Student {
    private String name;
    ...
}
```

O modificador de acesso `private` implementa o **encapsulamento**. Ele garante que o atributo `name` só possa ser acessado pelo código que está dentro da própria classe `Student`. Nenhuma classe externa, como a `StudentGrades`, pode acessar este campo diretamente, o que protege o estado interno do objeto e força o uso de métodos públicos (como o construtor) para interagir com seus dados.

### Pergunta 2: Substitua `student.getGrade()` por `student.grade`. O que acontece?
```Java
double totalGrade = 0.0;
for (Student student : students) {
    totalGrade += student.grade;
}
double meanGrade = students.size() > 0 ? totalGrade / students.size() : 0.0;
```

A compilação falha com o erro **`grade has private access in Student`**. Isso ocorre porque o atributo `grade` também é `private`. A tentativa de acesso direto de uma classe externa viola a regra do encapsulamento. A única forma permitida de obter o valor da nota é através do método público `getGrade()`, que serve como uma interface segura para os dados do objeto.

### Pergunta 3: Como renomear a classe `StudentGrades` para `Main` sem erro?

```Java
public class Main {
  ...
}
```

Para renomear a classe principal sem erros de compilação, duas alterações sincronizadas são necessárias:
1.  **No código:** Alterar a declaração `public class StudentGrades` para `public class Main`.
2.  **No sistema de arquivos:** Renomear o arquivo `StudentGrades.java` para `Main.java`.
Isso satisfaz a regra do Java de que o nome do arquivo deve ser idêntico ao da classe pública que ele contém.

---

## Parte 2: Evidência Prática de Execução

### Arquivos Necessários
Crie os dois arquivos abaixo na mesma pasta:

1.  **`StudentGrades.java`**: Contendo o código-fonte Java.
2.  **`students.csv`**: Contendo os dados dos alunos.

### Passos para Compilação e Execução
1.  **Compilar:** `javac StudentGrades.java`
2.  **Executar:** `java StudentGrades`

### Evidências

#### Compilação do Programa
O GIF abaixo demonstra a execução do comando `javac` no terminal, que compila o código-fonte `.java` em bytecode `.class` sem gerar erros.

![Compilação do programa](GIF-1.gif)

#### Execução do Programa
O GIF abaixo mostra a execução do comando `java StudentGrades`, que inicia o programa. Ele lê o arquivo `students.csv`, calcula a média das notas e imprime o resultado no console.

![Execução do programa](GIF-2.gif)

---

## Parte 3: Comparativo Java vs. C (baseado no código)

### Semelhanças
1.  **Sintaxe de Laço `for` com Índice:** A versão comentada do laço `for (int i = 0; i < students.size(); i++)` é sintaticamente quase idêntica a um laço `for` em C para percorrer um array.
2.  **Tipos Primitivos:** O uso de `double` para valores de ponto flutuante e `int` para inteiros é o mesmo em ambas as linguagens.
3.  **Operadores:** Operadores aritméticos como `+=` e `/`, e operadores de comparação como `>`, são iguais.

### Diferenças
1.  **Paradigma:** Java é **Orientado a Objetos**. O código é estruturado em classes (`Student`, `StudentGrades`) que unem dados e comportamento. Em C, a abordagem seria **procedural**, usando `structs` para agrupar os dados e funções separadas para manipulá-los.
2.  **Gerenciamento de Memória:** Java usa o **Garbage Collector**. Objetos criados com `new Student(...)` têm sua memória gerenciada automaticamente. Em C, seria necessário alocar memória para cada estudante dinamicamente com `malloc` e liberá-la manualmente com `free`.
3.  **Biblioteca Padrão:** Java possui uma biblioteca padrão extremamente rica. Classes como `List`, `ArrayList`, `BufferedReader`, e `FileReader` simplificam tarefas complexas como listas dinâmicas e leitura de arquivos. A operação `line.split(",")` é um bom exemplo de método de alto nível que, em C, exigiria uma implementação manual com funções como `strtok`.
