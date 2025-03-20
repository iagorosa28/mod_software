# Modelagem de um sistema para uma locadora de veículos

> Status do projeto: Em andamento

> Este projeto nos foi proposto no 6º semestre na disciplina de Modelagem de Software Orientado a Objetos

> Escrevemos esse projeto juntos durante as aulas

### Tópicos

- [Apresentação](#apresentação)
- [Casos de uso](#casos-de-uso)
- [Diagrama de classes](#diagrama-de-classes)

### Dados temporários

Atores: cliente, atendente, time do pátio, operador, sistema do DETRAN

Classes: Veículo, funcionário, cliente, locação, "multas", 

## Apresentação 

## Casos de uso
### Diagrama de Casos de Uso

![DiagramaCasosDeUso1 drawio](https://github.com/user-attachments/assets/dd40e553-8912-4f22-a0a3-304fb378ef0e)

### Tabelas de Casos de Uso
| Identificador          | UC_01                                                                                                     |
| :----------------------| :---------------------------------------------------------------------------------------------------------|
| Função                 | Verificar Cadastro                                                                                        |
| Atores                 | Cliente, Atendente                                                                                      |
| Prioridade             | Essencial                                                                                                 |     
| Pré-condição           | Cliente precisa informar o código                                                                         |
| Pós-condição           | Aprovação ou rejeição do cliente                                                                          |
| Fluxo Principal        | - O cliente informa seu código <br> - O atendente verifica se o cliente já possui cadastro (FS001, FS002) |
| Fluxo Secundário FS001 | - Se o cliente não possuir cadastro, o atendente realiza o procedimento                                   |
| Fluxo Secundário FS002 | - Após confirmar o cadastro do cliente, o atendente verifica se há locações pendentes do cliente (FS003)  |
| Fluxo Secundário FS003 | - Caso o cliente tenha locações pendentes, o atendente deve recusar a locação                             |

| Identificador   | UC_02                                                                               |
| :---------------| :-----------------------------------------------------------------------------------|
| Função          | Alugar veículo                                                                      |
| Atores          | Cliente, Atendente, Time do pátio e Sistema de pagamento                            |
| Prioridade      | Essencial                                                                           |     
| Pré-condição    | Cadastro do cliente liberado                                                        |
| Pós-condição    | Aluguel concluído                                                                   |
| Fluxo Principal | - Recepção do cliente na loja <br> - O cliente escolhe a categoria e o veículo que melhor atendem às suas preferências <br> - O cliente realiza o pagamento da locação do veículo por meio de um sistema externo de pagamento <br> - O time do pátio libera o veículo para o cliente |

| Identificador          | UC_03                                                                                                           |
| :----------------------| :---------------------------------------------------------------------------------------------------------------|
| Função                 | Verificar multas                                                                                                |
| Atores                 | Detran                                                                                                          |
| Prioridade             | Essencial                                                                                                       |     
| Pré-condição           | Devolução do veículo pelo cliente concluída                                                                     |
| Pós-condição           | Conclusão final da locação                                                                                      |
| Fluxo Principal        | - O sistema consulta o Detran para verificar se há multas pendentes no veículo utilizado pelo cliente (FS004)   |
| Fluxo Secundário FS004 | - Caso existam multas pendentes relacionadas ao veículo do cliente, o sistema deve notificar e cobrar o cliente |

## Diagrama de Classes

```mermaid
classDiagram
  Pessoa <-- Cliente
  Pessoa <-- Funcionario
  Funcionario "1" -- "0..*" Cliente : Cadastra
  Funcionario "1" -- "0..*" Locacao : Libera
  Cliente "1" -- "1" Locacao : Realiza
  Cliente "1" -- "1" Veiculo : Aluga
  Cliente "1" -- "1" Historico : Tem
  Historico "1" -- "1" Locacao : Pertence
  Historico "1" -- "0..*" Multa : Registra
  Veiculo "1" -- "1" Locacao : Pertence
  Veiculo "1" -- "0..*" Multa : Leva

  class Pessoa{
  - cpf string
  - dataDeNascimento date
  - nome string
  }

  class Cliente{
  - codigo string
  - nivelCategoria int
  + cadastrar()
  + verificarCadastro()
  + atualizarNivelCategoria()
  + verificarNivelCategoria()
  }

  class Funcionario{
  - desempenho float
  - ocupacao boolean
  - tipoFuncionario string
  + atualizarDesempenho()
  + verificarDesempenho()
  }

  class Historico{
  - multasAtivas boolean
  - locacaoPendente boolean
  - sequenciaLocacao int
  + consultarHistorico()
  }

  class Locacao{
  - valorLocacao float
  - valorAdicional float
  - dataInicio date
  - dataEntrega date
  - reservaSeguranca
  + atualizarValores()
  + registrarDatas()
  }

  class Veiculo{
  - categoria string
  - modelo string
  - placa string
  + registrarVeiculo()
  + mostrarInformacoes()
  + removerVeiculo()
  }

  class Multa{
  - tipoMulta string
  - valorMulta float
  - dataMulta date
  + registrarMulta()
  }
```

### Diagrama de Sequência
![Diagrama_S1 drawio](https://github.com/user-attachments/assets/b4120673-ab19-49c8-92a5-623b6ef151da)


